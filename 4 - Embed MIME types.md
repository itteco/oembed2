# How to Generate Embed Code for Each MIME Type

This document describes how to generate embed code for specific MIME Types under [Iframely Protocol](http://iframely.com/oembed2).



## iFrame Embeds

When embed is published with MIME type 'text/html', it should be wrapped into the embed code of an iFrame:

	<iframe src="link.href" />

For security purposes, we also suggest to wrap into iFrame the embeds published as `application/x-shockwave-flash`.

Consumers may opt to specify additional attributes such as for example `frameborder="0"`, `allowFullScreen`, etc. See details on specific cases of responsive media queries in the next sections.


### Fixed width and height

The simples case of is when media query of a published embed gives `width` and `height` values explicitly:

	<!-- Just iframe itself with proper size -->
    <iframe src="..."  
            style="width: {MEDIA.WIDTH};
                   height: {MEDIA.HEIGHT};" />



### Responsive iFrames with fixed `aspect-ratio`

The approach to when the media query contains only the fixed `aspect-ratio` value is fairly straightforward as well. 
The full description of the trick can be found [in this blog post](http://alistapart.com/article/creating-intrinsic-ratios-for-video):

	<!-- Responsive container. Revese the aspect-ratio here-->
	<div style="left: 0;
				width: 100%;
				height: 0;
				position: relative;
				padding-top: 100 * {ASPECT-RATIO}%">

		<!-- iframe with 100% size. -->
		<iframe style="top: 0;
						left: 0;
						width: 100%;
						height: 100%;
						position: absolute;" />
	</div>



### Limit `max-width` and `min-width`

To limit the size of a responsive container, it can simply be wrapped with additional `<div>`:

	<!-- Container that limits the size -->
	<div style="min-width: {MIN-WIDTH}};
				max-width: {MAX-WIDTH}};">

				<!-- Responsive Embeds Container here. -->
	</div>

This method does not support 'max-height' or 'min-height' however. See next section.



### Prevent Vertical Scrollbars on `height` - constrained embeds

Some iFrames  do not have fixed height due to dynamic nature of the content. In such cases. it is required that Publisher and Consumer co-operate to prevent scrollbars to ruin the experience of a user.

The approach is based on event messaging between the embedded iframe (publisher) and the parent window (consumer app). To prevent showing scrollers, iframe escalates its actual internal size to a parent window. This event occurs dynamically after iframe content loaded and works using `window.postMessage` method.

Here is step by step event flow:

1. Parent window embeds iframe and tells it its `ID` via message containing `windowId`:

		iframeElement.contentWindow.postMessage({method: "register", windowId: {ID} }, '*');

2. Child iframe listens for the event and keeps `windowId` value as its caller id:

		window.addEventListener('message', function(e) {
			if (e.data.method == "register") {
	            windowId = e.data.windowId;
	        }
		});

3. When child iframe is done loading the content and knows its exact size, it sends up it to the parent window:

		window.parent.postMessage({method: "resize", windowId: {ID}, height: {HEIGHT} }, '*');

4. Parent window receives new iframe size and adjusts the sizes of iframe container.


The following name convention constitues the spec: 

- `windowId` and `height` for the parameters
- `register` and `resize` for the events.


Publishers who have the content of such nature are encouraged to provide JavaScript embeds instead of iframe ones. This way, the above flow can be covered by the same party.



For performance purposes, Publishers are encouraged to implement ["Dynamic Async iFrame"](http://www.aaronpeters.nl/blog/iframe-loading-techniques-performance) approach.




## Media Embeds

Generated embed code for MIME types `video/mp4`, `video/webm` and `video/ogg` is:

 	<video
 		controls
 		poster="{THUMBNAIL.HREF}}">
 			Your browser does not support HTML5 video.
			<source
				src="{LINK.HREF}"
				type="{LINK.TYPE}}" />
 	</video>

Where `{THUMBNAIL.HREF}` - link to thumbnail image with the same aspect-ratio if it is available.

The sizing tricks are the same for iFrame embeds above.

The `audio/*` types, the embed code is generated using HTML5 `<audio>` 



## Image Embeds

For all image MIME types (`image/*`), embed code is simply an image:

 	<img src="{LINK.HREF}" 
 	     title="{LINK.TITLE}" alt="{LINK.TITLE}" 
 	     width="{LINK.MEDIA.WIDTH}" height="LINK.MEDIA.HEIGHT" />



## JavaScript Embeds

Embed code for MIME type `application/javascript` will look like:

 	<script type="application/javascript" src="link.href"></script>


Please, note that `text/javascript` MIME type is obsolete now.

The rendering of the embed widget should occur right after `<script>` tag. It would mean using `document.write` inside the javascript. This approach only works when the HTML code is generated on the server-side, and so the embedded javascript loads with the entire page.


It is not friendly for consumers who generate the page contents dynamically on the client-side. 
To make javascript embeds work for apps that render on the client side, a different solution needs to take place.

Publish the embed link with `id` tag included:

    <link rel="..." href="..."
           id = "{YOUR SERVER PREFIX: ID}"
	       type="application/javascript" />

The Consumer adds an empty `<div>` with given `id` field, then adds the javascript, which finds the div by id and renders inside it:

    <div id="{YOUR SERVER PREFIX: ID}"></div>





## Extra considerations: Security, Cache and Error Codes


### Publishers should not be selective with origins

Security is top concern. However, publishers should not discriminate the origins: either allow all or deny all. 

When Publisher providers a JavaScript embed, that requires a call to the Publisher's API, this API method should be made public with [CORS headers](http://www.w3.org/TR/cors/) set to allow XMLHttpRequest from all origins:

	Access-Control-Allow-Origin: *

Please, note, that Publisher still may and should secure sensitive API methods, that are not required to publicly display the embed widgets. If none of the API calls can be made public, it is advised to use `iframe` embeds instead. 

Same policy goes for `X-FRAME-OPTIONS`. This header should be omitted on the hosted embed resources.


### Cache

Consumers should follow the caching instructions of the origin server, when they retrieve the list of embed `links` and other semantics of the original webpage. Publishers should include standard HTTP1.1 caching mechanisms, such as 'Cache-Control', 'Expires' or 'Last-Modified' headers or just rely on 'ETag' value.

### HTTP Status Codes 

It is Publisher's responsibility to handle and present user-friendly error messages. 

For example, when resource is not available any longer (error 404) or can not be served for user in a specific geographic location, Publisher of a player can show an image instead with the text message clearly stating the reason. For images, it can be a boilerplate image with the error text.

Never should a publisher return HTTP error code on the hosted embed resouce with the empty response body. 

The HTTP errors on widget href location should be identical to the ones user would see if she goes to the original URL on publisher's site. This would help consumer app detect errors (for example `onError` event handler ) and re-fetch the original information from a host's canonical address.


<a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Iframely Protocol</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://iframely.com/" property="cc:attributionName" rel="cc:attributionURL">Itteco</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/3.0/deed.en_US">Creative Commons Attribution 3.0 License</a>.
