# Iframely Protocol for Responsive Embeds

Iframely protocol is simple embeds content publishing and discovery method that is naturally interpreted into responsive widget embed code by developers of consuming application.

Content publisher announces what widgets are available on a web page, in which format and which sizes and what are the expected use cases. Content consumer selects the widgets that work for the user's environment and presents it to the user.

Thus, the widgets are always hosted by a publisher, yet interpreted by consumer. This forces parties to put their best effort to collaborate on acceptable user experience for their shared audience. See [Business Intro](http://iframely.com/oembed2/intro).

Iframely protocol does not compete with specs of [oEmbed](http://oembed.com), [Open Graph](http://opg.me) or [Twitter Cards](http://https://dev.twitter.com/docs/cards), but rather supplements them, as it only focuses on User Experience and not on semantic data. 

__This is how it works:__

- Content Publisher puts available widgets as `<link>` tag in the `<head>` section of (X)HTML document. Publisher indicates MIME type of a hosted resource, sizing options and what are the expected use cases. 
- Consumer selects the widgets that work for the user's environment and app circumstances and presents it to the user. 

The protocol references HTML5/CSS3 and will naturally evolve with those standards from a technical standpoint.

This document and changes to it are managed on [GitHub](https://github.com/itteco/oembed2).



## Publish and Discover Embeds - via `<link>` tag

Automatic discovery starts when publisher puts a number of `<link>` tags in the `head` of their webpage:

    <link rel="iframely player"                          // list of functional use cases
          type="text/html"                               // guides to embed as iFrame
          href="//iframe.ly/bFbn"                        // with this src
          media="(min-width:100) and (min-height:100)"   // when these sizes are ok
          title="Open Web FTW!" />

Publisher may specify a number of links, either for various user experience options of the same content, or links for multiple pieces of content on the same page. 

Consumer (perhaps with user's explicit choice) selects what link to use, given the other viewers' environment (e.g. device, screen resolutions, etc) and functional context (e.g. "media library", "Feed reader", etc). 

Consumer app transofrms `<link>` information into embed code, based on MIME `type`, `media` queries and `href` source.
The link above will be transformed into `iframe` embed code:

    <iframe src="//iframe.ly/bFbn" width="100%" height="100%"></iframe>



## Quick Example - Coub Viral Videos

Quick example. Publisher, for example [Coub](http://coub.com) adds the following `player` link to the head of [web page](http://coub.com/view/2pc24rpb):

    <link rel="iframely player" href="https://coub.com/embed/2pc24rpb" type="text/html" 
     title="PARADISE BEACH"  media="(aspect-ratio: 1280:720)"/>


Consumer, for example [Realtidbits](http://realtidbits.com/), detects the link, sees that it requires iFrame responsive embed with aspect-ratio of  1280/720. 

Consumer generates the following embed code for it (see [Creating Intrinsic Ratios for Video](http://alistapart.com/article/creating-intrinsic-ratios-for-video) by Thierry Koblentz):

	<div style="left: 0px; width: 100%; height: 0px; position: relative; padding-bottom: 56%;">
		<iframe src="http://coub.com/embed/2pc24rpb" 
		frameborder="0" style="top: 0px; left: 0px; width: 100%; height: 100%; position: absolute;">
		</iframe>
	</div>


Voilà! User sees (try re-sizing your browser's window):
<div style="left: 0px; width: 100%; height: 0px; position: relative; padding-bottom: 56%;">
<iframe src="http://coub.com/embed/2pc24rpb" frameborder="0" style="top: 0px; left: 0px; width: 100%; height: 100%; position: absolute;"></iframe>
</div>
<p></p>


## Specify Use Case - in `rel` attribute

The supported use cases of a published widget should be listed in `rel` attribute, separated by a space, in no specific order.

The initial dictionary of the use cases is listed in [Rel Types](http://iframely.com/oembed2/rels) section and includes:

- `iframely` 
- `player` 
- `reader`
- `image`
- `survey`
- `thumbnail`
- `icon`
- `logo`

However, it is fairly straightforward to expand the list. See [how to contribute](http://iframely.com/oembed2/references).



## Host & Source the Widget - via `href` attribute

`href` is the actual source of the link is address of the iFrame or script or an image, etc that needs to be added as `src` when embedding the widget.

- Only sources with `http` and `https` protocols are allowed.
- If `href` for link supports both `https` and `http` transport, use opening `//` in source value.
- `href` can not be a relative path on a domain. Only absolute paths are accepted. 

HTTPS protocol is preferred to ensure maximum distribution for publishers' content, as consumers may opt not to consider HTTP-only embeds.



## Choose Embed Method - as MIME `type`

The method that needs to be used for embedding of a widget, is given as MIME type. 

For example, `text/html` indicates that widget needs to be embedded as `<iframe>`. 

Can also be:

- `javascript`
- `image`
- `video` and `audio` embeds.

See the list of acceptable [MIME types](http://iframely.com/oembed2/types) and which HTML markup and best practices to use to embed them.



## Select Size Options - via `media` query

Iframely embeds are expected to be fluid. Widgets should load responsively, and also react to resize event triggers of a browser or app.

`media` attribute is for any valid [CSS3 media query](http://www.w3.org/TR/css3-mediaqueries/), indicating the sizes of the containers where embed content would fit.

See [Media Queries on W3C.org](http://www.w3.org/TR/css3-mediaqueries/)

Publishers are encouraged to use as simple media features as possible. Consumer apps would require extensive programming to cover all variety of queries, thus making complex queries a high risks of not being interpreted well and thus reducing distribution of content for publishers.

An example of a simple media query is fixed `aspect-ratio`, or anything that relies on `min-` and `max-` of `height` and `width`:

    media="(aspect-ratio: 4:3)"



## For Non-Responsive - use `sizes`

`sizes` attribute can be used instead of `media` for fixed-size embeds: 

    <link rel="iframely thumbnail" sizes="800x600" type="image/png" href="//domain.com/thumbnail.png"/>

See [sizes spec on W3C](http://www.w3schools.com/tags/att_link_sizes.asp). Please, note that value `any` of `sizes` attribute is only allowed for `image` MIME type.



## For Multiple Embeds On The Page - itemize with `title`

Both Publisher and Consumer should assume that there could potentially be a number of Iframely links/widgets on a page. 

To distinguish between them, publisher must give separate titles for each one.

For example, `logo` can have the same title on all pages on your site and be equal to your "Site Name".

However, if the `link` represents the same content but with different variations in use case or media sizes, 
it is expected that such multiple links would share the same `title`.

If `tittle` attribute is omitted, the title should be taken from Open Graph `og:title` value or the value of  `<title>...</title>` HTML tag on the web page.