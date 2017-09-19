# Iframely Protocol for Responsive Embeds

[http://iframely.com/oembed2](http://iframely.com/oembed2)

Iframely protocol is simple publishing and discovery method for responsive embeds of web content. 

This is how it works:

- Content Publisher puts available widget as `<link>` tag in the `<head>` section of (X)HTML document. Publisher indicates MIME type of a hosted resource, sizing options and what are the expected use cases. 
- Consumer selects the widgets that work for user's environment and app circumstances and presents it to the user. 

__Sample:__

    <link rel="iframely player"                          // list of functional use cases
          type="text/html"                               // guides to embed as iFrame
          href="//iframe.ly/bFbn"                        // with this src
          media="(min-width:100) and (min-height:100)"   // when these sizes are ok
          title="Open Web FTW!" />



Iframely protocol does not compete with specs of [oEmbed](http://oembed.com), [Open Graph](http://ogp.me) or [Twitter Cards](http://https://dev.twitter.com/docs/cards), but rather supplements them, as it only focuses on User Experience and not on semantic data. 


The protocol references HTML5/CSS3 and will naturally evolve with those standards from a technical standpoint.


 
## Contributing

Please, feel free to [fork this document](https://github.com/itteco/oembed2) on GitHub or [submit an issue](https://github.com/itteco/oembed2/issues/new). 
We suggest that all new `rels` and MIME `types` first go via discussion in a ticket.



## Useful links

- [Iframely Embeds API](https://iframely.com) - cloud API that consumes embeds in that format.
- [Iframely on GitHub](https://github.com/itteco/iframely) - provides self-hosted parsers and API endpoint to consume Iframely protocol, oEmbed, Twitter Cards and Open Graph protocols.
- [Iframely Debug Tool](http://iframely.com/debug) - to check how other apps see your site.



## Acknowledgements 

The ideas for Iframely protocol were influenced by these publications since we started in Febuary 2012:

- [How To Save The Internet](http://www.businessinsider.com/how-to-save-the-internet-2009-11) by [John Borthwick](https://twitter.com/Borthwick) / 2009
- ["Responsive embeds"](http://amobil.se/2011/11/responsive-embeds/) by [Anders M. Andersen](https://twitter.com/andmag) / 2011
- [Creating Intrinsic Ratios for Video](http://alistapart.com/article/creating-intrinsic-ratios-for-video) by [Thierry Koblentz](https://twitter.com/thierrykoblentz) / 2009
- [oEmbed](http://oembed.com) spec / 2008
- [Open Graph](http://ogp.me) by Facebook and RDFa approach in general / 2011
- [Twitter Cards](https://dev.twitter.com/docs/cards/types/player-card) spec / 2012
- [EmbedLink](https://sites.google.com/site/embedlink/home) proposal by Brian Mearns was in line with what we were working on.



## Authors & License

(c) 2013 - 2017 [Itteco Software Corp.](http://itteco.com) 

Specifically, these folks from Itteco:

- [Ivan Paramonau](https://twitter.com/iparamonau) - spec & analysis
- [Nazar Leush](https://github.com/nleus) - R&D
- Anatoly Ivanov - PoC version of Iframely parsers

<a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-sa/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Iframely Protocol</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://iframely.com/oembed2" property="cc:attributionName" rel="cc:attributionURL">Itteco Software Corp.</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/3.0/deed.en_US">Creative Commons Attribution-ShareAlike 3.0 Unported License</a>.