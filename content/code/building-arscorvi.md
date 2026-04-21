+++
date = '2026-04-21T16:54:24+01:00'
draft = false
title = 'Building arscorvi.github.io'
+++

I like making websites.

I've always liked making websites. I wouldn't necessarily consider myself a designer, developer, or coder — these are all words that I would use to describe someone who does this with much more frequency and demonstrable ability than I do — but I do enjoy making private little corners of the internet for my things. When it comes to languages, HTML and CSS are the ones that I am most familiar with for as long as I can remember; I used my rudimentary understanding of these languages as far back as the age of 14-years-old to design various little blurbs and rulesets for the games that I played and hosted, and that knowledge never really went away.

Not that I have much experience, beyond those small little projects, with the bigger picture that is web design and hosting. For years, the extent of my knowledge was applied almost exclusively to profiles for the various characters that I play across different types of media, with each community having its own spin on things. The Final Fantasy XIV role-playing community, for example, has a preference for using Carrd, a (mostly) free-to-use website designer. Templates? Check. A user-friendly interface? Check. Hosting, too? It has everything that the community wants.

And it had everything I wanted, too, for a time. But my tendency to become rather determined to have the end results of my creative processes to look *exactly* the way that I imagine them, it fell short in certain areas. Certain features — such as embedding code, removing watermarks, and the like — are locked behind a yearly subscription service. I found myself wrestling with the interface more and more in order to get things looking the way that I wanted. But I was still happy with the end results, even if they weren't really what I had in mind.

Then I found Hugo. A static website builder was much more my style; I had no need for dynamic elements, I could freely design and edit things to be just the way that I wanted them, because Hugo gives you total control, and it scratched an itch that I had forgotten was there. But it had been *years* since I exercised my web design and coding muscles, and I didn't know what I was doing.

It was a headache. I felt out of my depth. I read document after document, followed tutorials, browsed support forums, and made a veritable Frankenstein's monster of HTML, CSS, and Hugo shortcodes. Old coding habits crept back in. My attempts at problem solving were the equivalent of throwing the baby out with the bath water; I jumped to conclusions that made little to no sense whatsoever without showing any signs of slowing down, taking a sip of coffee, and reviewing the problem from a less frustrated perspective. The one and only example I am willing to share is this:

My main CSS body tag has the max-width property set to 40em; this keeps everything neatly organised at a size that I like. Unfortunately, my character profiles (and most of my entries in general) can run a little long, so I wanted to have the ability to make separate, 40em width columns. I did this by using a shortcode — a pre-determined template to embed/insert various elements, chiefly HTML — and... Broke the website. The columns were there, yes, but they were all haphazardly stuffed within the pre-determined max width. My solution was to set the max-width property for the p tag rather than the body: 

```css
body {
    background: var(--background-color);
    color: var(--foreground-color);
    font-family: monospace;
}

p {
    max-width: 40em;
}
```

This gave me the desired results, yes, but it broke everything else, too. Lists and horizontal rules were spilling out to absurd lengths and it was, frankly, *ugly*. I panicked. I tried changing the properties in the CSS that were responsible for the columns with the !important flag:

```css
.md-columns {
    display: flex;
    flex-wrap: wrap;
    margin-left: -1rem;

}

.md-columns > div {
    flex: 1 1;
    margin: 0rem 0;
    width: 100% !important;
    min-width: 40em !important;
    padding: 0 1rem;

}

.md-columns .markdown-inner {
    margin-top: 0;
    margin-bottom: 0;

}
```

But this did nothing. Of course it did nothing! I didn't know what I was *doing*! Frustrated and tired, my immediate solution to this problem was to simply have the pages that required columns to load their own CSS file. I spent half an hour trying to remember how to do this, quickly realised that I had forgotten entirely, and then spent a further hour reading on how to make it happen. I asked friends for help.

And then I realised, after much trial and error, that I was overthinking things. I could just amend the shortcode's HTML template to the following to get the desired results:

```html
<body style="max-width: 100%;">
<div class="md-columns">
{{ range split .Inner "<--->" }}
{{ printf "<div class=\"markdown-inner\">" | htmlUnescape | safeHTML }}
<div style="max-width: 40em;">
{{ . | safeHTML }}
</div>
{{ printf "</div>" | htmlUnescape | safeHTML }}
{{ end }}
</body>
</div>
```

In classic web design fashion, however, this ruined something else: mobile view. I can't remember how I fixed that, but I did. And then it was simply a matter of polishing up the website's page structure, tidying up files, and settling on a colour scheme, something minimal and pleasing.

All in all, it took me a couple of months from start to finish to get this website designed, built, and deployed, but it only took so long because of a rather lengthy break in the middle wherein I forgot that I wanted to have a website to begin with and, upon returning to the project, was left wondering what on earth I was thinking only a few months ago and decided to start from scratch.

I guess it only took a few days, then.

I'm not done, either. By the time I make another post in this section about this site, it will probably look remarkably different. But that's one of the things that I enjoy the most about web design as a whole — the frequent iterations, the constant tweaking, and the endless cycle of making, breaking, fixing, and making again and again.

