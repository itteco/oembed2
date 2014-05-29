# Iframely Protocol for Responsive Embeds

[http://iframely.com/oembed2](http://iframely.com/oembed2)

Iframely protocol is simple publishing and discovery method for responsive embeds of web content. 

This is how it works:

- Content Publisher puts available widgets as `<link>` tag in the `<head>` section of (X)HTML document. Publisher indicates MIME type of a hosted resource, sizing options and what are the expected use cases. 
- Consumer selects the widgets that work for the user's environment and app circumstances and presents it to the user. 

__Sample:__

    <link rel="iframely player"                          // list of functional use cases
          type="text/html"                               // guides to embed as iFrame
          href="//iframe.ly/bFbn"                        // with this src
          media="(min-width:100) and (min-height:100)"   // when these sizes are ok
          title="Open Web FTW!" />



Iframely protocol does not compete with specs of [oEmbed](http://oembed.com), [Open Graph](http://ogp.me) or [Twitter Cards](http://https://dev.twitter.com/docs/cards), but rather supplements them, as it only focuses on User Experience and not on semantic data. 


The protocol references HTML5/CSS3 and will naturally evolve with those standards from a technical standpoint.



## Social Media

- Business questions and answers are handled via [Iframely topic on Quora](http://www.quora.com/Iframely)
- Technical Q&A - [iframely tag on StackOverflow](http://stackoverflow.com/questions/tagged/iframely)
- News & Experiences. [#iframely](https://twitter.com/search?q=iframely&src=typd&mode=realtime) or [@iframely](https://twitter.com/iframely) on Twitter


 
## Contributing

Please, feel free to [fork this document](https://github.com/itteco/oembed2) on GitHub or [submit an issue](https://github.com/itteco/oembed2/issues/new). 
We suggest that all new `rels` and MIME `types` first go via discussion in a ticket.



## Useful links

- [Iframely the Embeds Gateway](http://iframely.com/gateway) - provides single self-hosted API endpoint to consume Iframely protocol, oEmbed, Twitter Cards and Open Graph protocols.
- [Iframely Embeds QA Whitelist](http://iframely.com/qa) - independent quality data for domains implementing Iframely protocol, oEmbed, Twitter Cards and Open Graph.
- [Iframely Debug Tool](http://iframely.com/debug) - debugs 4 embeds protocols. Also a [Chrome extension](https://chrome.google.com/webstore/detail/iframely-semantic-url-deb/lhemgegopokbfknihjcefbaamgoojfjf).
- [iframe.ly](http://iframe.ly) - the demo app. As both consumer and publisher.



## Acknowledgements 

The ideas for Iframely protocol were influenced by these publications since we started in Febuary 2012:

- [How To Save The Internet](http://www.businessinsider.com/how-to-save-the-internet-2009-11) by [John Borthwick](https://twitter.com/Borthwick) / 2009
- ["Responsive embeds"](http://amobil.se/2011/11/responsive-embeds/) by [Anders M. Andersen](https://twitter.com/andmag) / 2011
- [Creating Intrinsic Ratios for Video](http://alistapart.com/article/creating-intrinsic-ratios-for-video) by [Thierry Koblentz](https://twitter.com/thierrykoblentz) / 2009
- [oEmbed](http://oembed.com) spec / 2008
- [Open Graph](http://ogp.me) by Facebook and RDFa approach in general / 2011
- [Twitter Cards](https://dev.twitter.com/docs/cards/types/player-card) spec / 2012
- [EmbedLink](https://sites.google.com/site/embedlink/home) proposal by Brian Mearns was in line with what we were working on, though we don't agree that oEmbed is considered harmful, but rather a question of proper [whitelist](http://iframely.com/qa) / 2013


The following folks and companies helped with feedback and validation of the concepts:

- [Nowork FM](http://nowork.fm) - [Itteco](http://itteco.com)'s simple intranet, we opted to build to immerse ourselves in all requirements of embeds Consumer
- Anatoly Ivanov built the 3rd reincarnation of [Iframely Open-Source Gateway](http://github.com/itteco/iframely) (we ended up releasing the 4rth incarnation of it)
- [Mathias Panzenböck](https://github.com/panzi) and his [CrowdRanking](http://crowdranking.com/) was the first publisher under Iframely protocol (even ahead of [us ourselves](http://iframe.ly))
- [Jon Cianciullo](https://twitter.com/jonnyjon/) helped validate some ideas.
- [Taras Kuba](https://twitter.com/taraskuba) is our brilliant designer, who added a lot of the design trends vision for future web,
- Ideas, similar to [Why Cards are the Future of the Web](http://insideintercom.io/why-cards-are-the-future-of-the-web/) by [Paul Adams](https://twitter.com/padday)
- [Coub](http://coub.com), [SocialMention](http://socialmention.com), [realtidbits](http://realtidbits.com), [SlimSurveys](http://slimsurveys.com) helped the ball rolling by being our early adapters.




## Authors & License

(c) 2013 [Itteco Software Corp.](http://itteco.com) 

Specifically, these folks from Itteco:

- [Ivan Paramonau](https://twitter.com/iparamonau) - direction, spec & analysis
- [Nazar Leush](https://github.com/nleus) - all R&D efforts

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Iframely Protocol</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://iframely.com/oembed2" property="cc:attributionName" rel="cc:attributionURL">Itteco Software Corp.</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.