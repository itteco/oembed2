# Iframely Protocol

Iframely protocol is simple embeds content publishing and discovery method that is naturally 
interpreted into widget embed code by developers of consuming application. 

Content publisher announces what widgets are available on a web page, in which format and which sizes and what are the expected use cases. 
Content consumer selects the widgets that work for the user's environment and presents it to the user. 

Thus, the widgets are always hosted by a publisher, yet interpreted by consumer. 
This forces parties to put their best effort to collaborate on acceptable user experience for their shared audience.
See _Intro for Businesses in Section 1_.

The protocol references HTML5/CSS3 and will naturally evolve with those standards from a technical standpoint.

This document and changes to it are managed on [GitHub](https://github.com/itteco/oembed2).


# 2. Spec

## 2.1 Publishing & Discovery

Discovery is expected to happen when publisher puts <link> tag in the head of their webpage:

 <link rel="iframely player"                        // intended use case
 type="text/html"                                   // embed as iFrame
 href="//iframe.ly/bFbn"                            // with this src
 media="(min-width:100) and (min-height:100)"       // when these sizes are ok
 title="Open Web FTW!" />

## 2.2. Example of embed code
The above link on the publisher's web page would be used to generate the following embed code on consumer's site:

 <iframe src="//iframe.ly/bFbn" width="100%" height="100%"></iframe>

## 2.3 `rel`
The supported use cases shall be listed in `rel` attributes, separated by a space, in no specific order.

The initial dictionary of the use cases is listed in _Rel Types_ section:
`iframely`, `player`, `reader`, `image`, `survey`, `thumbnail`, `icon`, `logo`

However, it is fairly straightforward to expand the list. See _how to contribute_

## 2.4 `href`
The actual source of the link is address of the iFrame or script or an image, etc that needs to be added as `src` when embedding the widget.
Only `http` and `https` protocols are allowed.

`href` for links supporting both `https` and `http` transport, please, use `//` at the begining of
href attributes is preferrably via https protocol to ensure maximum distribution for publishers' content, as consumers may opt not to consider http-only embeds.
 
`href` can not be a relative path on the domain. Only absolute paths are accepted. 

## 2.5 `type`
The method that needs to be used for embedding of a widget, is given as MIME type. 
For example, `text/html` would indicate that widget needs to be embedded as `iframe`. 
Can also be `image`, `javascript`, `video` and `audio` embeds.

See the list of acceptable _MIME types_ and what HTML markup to use to embed them.

## 2.6 `media`
Iframely embeds are expected to be responsive. 

`media` attribute is for any valid [CSS3 media query](http://www.w3.org/TR/css3-mediaqueries/), indicating the sizes of the containers where embed content would fit.
See [Media Queries on W3C.org](http://www.w3.org/TR/css3-mediaqueries/)

Publishers are encouraged to use as simple media features as possible. 
Consumer apps would require extensive programming to cover all variety of queries, 
thus making complex queries a high risks of not being interpreted well and thus reducing distribution of content for publishers.

An example of simple media query is fixed `aspect-ratio`, or anything that relies on `min-` and `max-` of `height` and `width`.
 media="(aspect-ratio: 4:3)"

## 2.7 `sizes` 
`sizes` attribute can be used instead of `media` for fixed-size embeds: 
 <link rel="iframely thumbnail" sizes="800x600" type="image/png" href="//domain.com/thumbnail.png"/>

See [sizes spec on W3C](http://www.w3schools.com/tags/att_link_sizes.asp).

## 2.7 `title`
Please, note that there could potentially be a number of iframely links / widgets on the page. 
To distinguish between them, publisher must give separate titles for each of them.

For example, `logo` can have the same title on all pages on your site and be equal to your site's name.

However, if the `link` represents the same content but with different variations in use case or media sizes, 
it is expected that such multiple links would share the same `title`.


# 3. Example

Coub Example

# 4. Error Handling

# 5. Security considerations


# 6. Community

## 6.1 Partners 

Here are the companies who have helped us verify the protocol by being Iframely early adapters:
 -  
 -
 -
 -
 -
 -

## 6.2 Social Media
 - Business questions and answers are handled via [Iframely topic on Quora](http://www.quora.com/Iframely)
 - Technical Q&A - [iframely tag on StackOverflow](http://stackoverflow.com/questions/tagged/iframely)
 - News & Experiences. [#iframely](https://twitter.com/search?q=iframely&src=typd&mode=realtime) or [@iframely](https://twitter.com/iframely) on Twitter
 
## 6.2 Contributing
Please, feel free to [fork this document](https://github.com/itteco/oembed2) on GitHub or [submit an issue](https://github.com/itteco/oembed2/issues/new). 
We suggest that all new `rels` and MIME `types` first go via discussion in a ticket.

## 6.3 Open-source implementations

-  Iframely the Embeds Gateway - provides single self-hosted API endpoint to consume iframely, oEmbed, Twitter Cards and Open Graph protocols.
-  Iframely Embeds QA Whitelist - providers independent quality data for domains implementing iframely, oEmbed, Twitter Cards and Open Graph 

# 7. Authors & License

(c) 2013 [Itteco Software Corp.](http://itteco.com) Licensed under Creative Commons 3.0

Specifically, these folks from Itteco:
* [Ivan Paramonau](https://twitter.com/iparamonau) - direction, spec & analysis
* [Nazar Leush](https://github.com/nleus) - all R&D efforts

[Say hi](mailto:support@iframely.com) to us.





