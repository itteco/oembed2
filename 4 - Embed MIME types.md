# Generate Responsive Embed Code for Each MIME Type

## iFrame embeds

- text/html
- application/x-shockwave-flash

Embed code:

	<iframe src="link.href" frameborder="0" />

To prevent showing scrollers some iframes can send their internal size to parent window. This event occurs dynamically after iframe content loaded and work using `window.postMessage` method.

Here is step by step scenario:

1. Parent window sends event to child iframe (see https://github.com/itteco/iframely/blob/master/static/js/iframely.js: $.iframely.registerIframesIn):

	iframeElement.contentWindow.postMessage({method: "register", windowId: uid}, '*');

2. Child iframe receives event and stores `windowId` (see https://github.com/itteco/iframely/blob/master/static/js/iframely-utils.js):

	window.addEventListener('message', function(e) {
		if (e.data.method == "register") {
            windowId = e.data.windowId;
        }
	});

3. When child iframe knows its size it sends back it to parent window:

	window.parent.postMessage({method: "resize", windowId: uid, height: height}, '*');

4. Parent window receives new iframe size and makes proper element manipulations.

## Script embeds

MIME types:

 - text/javascript
 - application/javascript

Embed code:

 	<script type="link.type" src="link.href"></script>

Rendering scenarios:

1. By default: exactly after script tag.

2. In specific container only if it exists:

	<div iframely-container-for="link.href"></div>

Script should work with both static and dynamic embedding.

After script finished render event on widget's parent element `iframely.loaded` should occur.

## Image embeds

MIME types:

 - image/*

Embed code:

 	<img src="link.href" title="link.title" alt="link.title" width="link.media.width" height="link.media.height" />

## Media embeds

MIME types:

 - video/mp4
 - video/webm
 - video/ogg

Embed code:

 	<video
 		controls
 		poster="thumbnail.href">
 			Your browser does not support HTML5 video.
			<source
				src="link.href"
				type="link.type" />
 	</video>

`thumbnail.href` - link to same aspect-ratio thumbnail if available.

# Wrapping `iframe` and `video` tags to use `aspect-ratio`, `min-width` and `max-width` media query attributes

Wrapper implementation could be found at https://github.com/itteco/iframely/blob/master/static/js/iframely.js

Lets assume our `iframe` or `video` tag called `element`. Specific attributes like `src` or `frameborder` will be skipped as obvious.

`media` - is `link.media` attribute.

## Fixed `width` and `height` case

	<!-- Just element itself with size. -->
    <element style="width: media.width;
    				height: media.height;" />

## Responsive size with `aspect-ratio` case.

	<!-- Responsive container. -->
	<div style="left: 0;
				width: 100%;
				height: 0;
				position: relative;
				padding-top: 100*media['aspect-ratio']%">

		<!-- Element with 100% size. -->
		<element style="top: 0;
						left: 0;
						width: 100%;
						height: 100%;
						position: absolute;" />
	</div>

## `max-width` and `min-width` cases.

To limit container size from previous responsive case it must be wrapped with simple `<div>`:

	<!-- Size constraint container. -->
	<div style="min-width: media['min-width'];
				max-width: media['max-width'];">

				<!-- Responsive container here. -->
	</div>

Using 'max-height' or 'min-height' not supported by this method.