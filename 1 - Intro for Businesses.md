# Iframely intro for Businesses

## The Cause

The purpose of Iframely protocol is to help open web take the next step by making it possible 
for the web content to follow user from website to website. 

A person sees and likes content on one site, which publishes that content as embed widgets.  
A person shares its canonical URL on the other site. That site presents embeds, so that 
community can consume main content quickly and easily, without going to the actual URL. 

The protocol makes the experience more smooth and engaging for all users 
and it introduces a new web particle, namely content widget. 
As consequence, it facilitates wide range of social apps and platforms to become 
a new web browser for the content-only frames.

Ultimately, it is a grass-roots take on any current or future major 
player's monopoly on social apps, as content will be easily consumed on whatever platform 
or devices the users opted to communicate on.

Inspired by [John Borthwick's article on Open Web](http://www.businessinsider.com/how-to-save-the-internet-2009-11). 


## The Business Case

There are three main business models around content at the moment. 

First monetizes the timeline of a user (e.g. ads on a news site, or promoted statuses on Facebook or Twitter).
Second monetizes the content itself (e.g. in-video ads by YouTube, or in-article ads on a blog, 
or even sponsored search results by Google).

The third is supplementary services, helping the first two monetization options. For example 
real-time analytics for better the content aggregation or editing and hosting tools for the media itself.

As content and consumer platforms get more distinct separation in their business models, 
it is worth to introduce a "good citizen" policy and business etiquette.

Consumer and publisher should work together towards a common goal
of serving the best user experience possible for their shared audience 
and not against each other in order to solicit a customer.

Never should it be acceptable to undermine user experience instead of providing value.

Iframely protocol's focus on specifying embeds use cases will help publisher and consumer 
to find a balance between viral distribution versus acquiring and retaining customers.

[Read the full spec](http://iframely.com/oembed2)


## The oEmbed/2

The protocol's roots are in oEmbed v1, published in 2008. 

The working title for the new protocol was "oEmbed/2" (read as "oEmbed two" or "half oEmbed"), 
as it keeps simplicity of embeds discovery, while reducing the complexity of implementation by half. 

The protocol leaves semantic data out of scope, as other semantic protocols such as 
Open Graph (and RDFa approach in general) cover it and have clearly gone mainstream.

`iframely` is the official name of the released protocol, a noun and an adverb hinting the way 
how embeds are being transferred from one web page to another (e.g. "via iFrame").

The protocol's primarily focus is on user experience and technical aspects of publishing 
and consuming widgets on the web in current realities (HTML5, CSS3, HTTP1.1).

[Read the full spec](http://iframely.com/oembed2)


## QA & Whitelist

During [Itteco](http://itteco.com)'s research and development effort with existing embeds and semantic protocols, 
we got a clear indication that the lack of centralized Quality Assurance for embeds is what is 
holding its progress. 

There are technical/security considerations that can be resolved algorithmically, but it really 
requires a human eye to see if the user experience of the embeds can be relied on. 

As such, all oEmbed consumer implementations were choosing (very) small portion of publishers into their internal whitelists, 
leaving the long tail of less popular providers struggling to get distribution. 

Facebook and Twitter have their own whitelists for the embeds they consume, but this information isn't public.

Itteco therefore launches [Whitelist DB](http://iframely.com/qa), as the first independently run embeds QA service. 
We cover iframely, oEmbed v1, Twitter Cards and Open Graph protocols in our test runs. 

[Get Whitelist File](http://iframely.com/qa/buy) or [Submit Your Domain](http://iframely.com/qa/request). 