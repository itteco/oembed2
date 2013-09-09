# Iframely Protocol for Responsive Embeds

Iframely protocol is simple publishing and discovery method for responsive embeds of web content. 

- Content widgets are always hosted and controled by Publisher. 
- Consumer app interprets and presents embeds to User, giving the experience circumstances. 
- This clear separation of responsibilities balances Publisher and Consumer objectives. It forces them to work together to provide best user experience to their shared audience. See [Business Intro](http://iframely.com/oembed2/intro)

Iframely protocol does not compete with specs of [oEmbed](http://oembed.com), [Open Graph](http://opg.me) or [Twitter Cards](http://https://dev.twitter.com/docs/cards), but rather supplements them, as it only focuses on User Experience and not on semantic data. 

This is how it works:
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


The user sees:
<div style="left: 0px; width: 100%; height: 0px; position: relative; padding-bottom: 56%;">
<iframe src="http://coub.com/embed/2pc24rpb" frameborder="0" style="top: 0px; left: 0px; width: 100%; height: 100%; position: absolute;"></iframe>
</div>


## `rel`
The supported use cases of published widget shall be listed in `rel` attributes, separated by a space, in no specific order.

The initial dictionary of the use cases is listed in _Rel Types_ section:
`iframely`, `player`, `reader`, `image`, `survey`, `thumbnail`, `icon`, `logo`

However, it is fairly straightforward to expand the list. See _how to contribute_

## `href`
The actual source of the link is address of the iFrame or script or an image, etc that needs to be added as `src` when embedding the widget.
Only `http` and `https` protocols are allowed.

`href` for links supporting both `https` and `http` transport, please, use `//` at the begining of
href attributes is preferrably via https protocol to ensure maximum distribution for publishers' content, as consumers may opt not to consider http-only embeds.
 
`href` can not be a relative path on the domain. Only absolute paths are accepted. 

## `type`
The method that needs to be used for embedding of a widget, is given as MIME type. 
For example, `text/html` would indicate that widget needs to be embedded as `iframe`. 
Can also be `image`, `javascript`, `video` and `audio` embeds.

See the list of acceptable _MIME types_ and what HTML markup to use to embed them.

## `media`
Iframely embeds are expected to be responsive. 

`media` attribute is for any valid [CSS3 media query](http://www.w3.org/TR/css3-mediaqueries/), indicating the sizes of the containers where embed content would fit.
See [Media Queries on W3C.org](http://www.w3.org/TR/css3-mediaqueries/)

Publishers are encouraged to use as simple media features as possible. 
Consumer apps would require extensive programming to cover all variety of queries, 
thus making complex queries a high risks of not being interpreted well and thus reducing distribution of content for publishers.

An example of simple media query is fixed `aspect-ratio`, or anything that relies on `min-` and `max-` of `height` and `width`.
    media="(aspect-ratio: 4:3)"

## `sizes` 
`sizes` attribute can be used instead of `media` for fixed-size embeds: 
    <link rel="iframely thumbnail" sizes="800x600" type="image/png" href="//domain.com/thumbnail.png"/>

See [sizes spec on W3C](http://www.w3schools.com/tags/att_link_sizes.asp).

## `title`
Please, note that there could potentially be a number of iframely links / widgets on the page. 
To distinguish between them, publisher must give separate titles for each of them.

For example, `logo` can have the same title on all pages on your site and be equal to your site's name.

However, if the `link` represents the same content but with different variations in use case or media sizes, 
it is expected that such multiple links would share the same `title`.

If `tittle` attribute is omitted, the title should be considered to value in `<title>...</title>` HTML tag of the web page.


# Example

Coub Example


# Community

## Partners 

Here are the companies who have helped us verify the protocol by being Iframely early adapters:
 -  
 -
 -
 -
 -
 -

## Social Media
 - Business questions and answers are handled via [Iframely topic on Quora](http://www.quora.com/Iframely)
 - Technical Q&A - [iframely tag on StackOverflow](http://stackoverflow.com/questions/tagged/iframely)
 - News & Experiences. [#iframely](https://twitter.com/search?q=iframely&src=typd&mode=realtime) or [@iframely](https://twitter.com/iframely) on Twitter
 
## Contributing

Please, feel free to [fork this document](https://github.com/itteco/oembed2) on GitHub or [submit an issue](https://github.com/itteco/oembed2/issues/new). 
We suggest that all new `rels` and MIME `types` first go via discussion in a ticket.

## Useful links
 -  [Iframely the Embeds Gateway](http://iframely.com/gateway) - provides single self-hosted API endpoint to consume iframely, oEmbed, Twitter Cards and Open Graph protocols.
 -  [Iframely Embeds QA Whitelist](http://iframely.com/qa) - providers independent quality data for domains implementing iframely, oEmbed, Twitter Cards and Open Graph 
 -  [Iframely Debug Tool](http://iframely.com/debug) - debugs 4 embeds protocols

# Authors & License

(c) 2013 [Itteco Software Corp.](http://itteco.com) Licensed under Creative Commons 3.0

Specifically, these folks from Itteco:
* [Ivan Paramonau](https://twitter.com/iparamonau) - direction, spec & analysis
* [Nazar Leush](https://github.com/nleus) - all R&D efforts

[Say hi](mailto:support@iframely.com) to us.





