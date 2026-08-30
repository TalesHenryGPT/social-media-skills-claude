---
name: wikipedia-entry
description: >
  Turn any list of rules, tells, mistakes or definitions into a graphic that looks
  like a real Wikipedia article. Use when the user says "wikipedia style", "make it
  look like an encyclopedia entry", "signs of", "anatomy of", "glossary", or has a
  long list that a normal card grid cannot hold. Best for 20 to 40 short rules.
  Produces a 1080x1350 PNG for LinkedIn or Instagram.
---

# Wikipedia Entry

## CRITICAL: Auto-start on load

Go straight to Step 1. Do not summarise. Do not explain the format. Start.

## Why this format works

A borrowed world does the persuading before a word is read. Everyone knows what a
Wikipedia page looks like, so the layout arrives pre-trusted and the reader spends
their attention on your content instead of decoding your design.

It also holds far more than a card grid. Twenty-nine numbered rules, an infobox, a
sidebar and a sources block fit on one portrait canvas and still read at feed size.
A card layout tops out around twelve.

The catch, and it is the whole job: **it only works if it is accurate.** A fake
Wikipedia page with the wrong sidebar links or a made-up infobox reads as a
template. Get the chrome right and it reads as an artefact.

## Step 1 — Get the list

Ask for one thing only: the rules, in a numbered list, shortest first.

Each rule is **one line, one sentence, under about 70 characters.** If a rule needs
two lines the entry starts to look like a blog post and the illusion breaks.

Twenty to forty rules is the range. Under fifteen, the page looks empty and a card
layout is better. Over forty, the type drops below readable.

If the user hands you a paragraph, cut it into single-line rules yourself and show
them the list before you build anything.

## Step 2 — Group into four to six sections

Wikipedia articles have numbered sections and so does this. Four to six, each with
five to nine rules under it.

Name them the way an encyclopedia would: a plain noun phrase, no verbs, no wit.
`Colour and type`, `Things to delete`, `Layout`, `Treatment`, `Sources`.

The last section is always **Sources**, and it is what makes the whole thing land.

## Step 3 — The Sources block is the proof

Real Wikipedia articles carry citations. Yours carries **direct quotes with dates.**

Pull six real quotes from wherever the rules came from: your own feedback, client
notes, code review comments, support tickets, your Slack. Each one gets a date.

```
1. "I never ever used the loop arrow. I hate seeing that." (18/06/2026)
2. "I don't like the power ending you've added here." (25/08/2026)
```

This is the part nobody can copy. A stranger can rebuild your layout in an hour.
They cannot produce six dated quotes from inside your own work.

**Rule: never invent a quote.** If you have fewer than six real ones, ship four.
An article with four real citations beats one with six invented ones, and the
difference is visible to anyone who reads carefully.

## Step 4 — Build the chrome

Four parts, and each has to be right or the illusion breaks.

**Left sidebar, about 220px.** The globe mark at the top, then the wordmark, then
the real Wikipedia navigation in its real order: Main page, Contents, Featured
content, Current events, Random article. Then an `Interaction` group, then a
`Tools` group. Slip ONE of your own links into the nav — that is the joke, and one
is funnier than three.

**Article tabs across the top.** Article / Talk on the left. Read / View source /
View history on the right, with a search box. All in Wikipedia blue `#3366CC`.

**The infobox, floated right, about 390px.** Grey header bar with the title, then a
drawn specimen of the thing you are describing, then a caption, then a
`Classification` table: Also known as, Type, Documented by, Instances, Sample size,
First observed, Treatment, See also.

Draw the specimen in CSS. Do not generate it. It is the one picture on the page and
a generated one will not match the rest.

**Serif for headings, sans for body.** Wikipedia uses a serif for the article title
and section headings and a sans for body text. Getting this backwards is the single
fastest way to make it look fake.

## Step 5 — The type scale

```
Article title      38px serif
Section heading    23px serif, thin rule underneath
Body and rules     16px sans, line-height 1.35
Infobox            12px sans
Sources            11px sans, italic, two columns
```

Set the canvas to 1080x1350 and render at 2x for a 2160x2700 PNG.

Everything left-aligned. Wikipedia has no centred text and neither does this.

## Step 6 — Fit it

The last rule must clear the footer. Measure it, do not eyeball it.

If it overflows, the fix is in this order:
1. Cut a rule. There is always one that repeats another.
2. Tighten line-height by 0.02.
3. Drop the body by 0.4px.

Never go below 15px on the body. Below that nobody reads it at feed size, and the
whole point of the format is that it holds a lot of readable text.

## The starting HTML

```html
<div id="canvas">
  <aside class="side">
    <svg class="globe" viewBox="0 0 100 100">...</svg>
    <div class="wordmark">WIKIPEDIA</div>
    <div class="tagline">The Free Encyclopedia</div>
    <nav>
      <a>Main page</a><a>Contents</a><a>Featured content</a>
      <a>Current events</a><a>Random article</a>
      <a class="mine">Your own link</a>
    </nav>
    <h3>Interaction</h3>
    <nav><a>Help</a><a>About</a><a>Community portal</a><a>Recent changes</a></nav>
    <h3>Tools</h3>
    <nav><a>What links here</a><a>Related changes</a><a>Permanent link</a></nav>
  </aside>

  <main>
    <div class="tabs">
      <span class="on">Article</span><a>Talk</a>
      <div class="right"><span>Read</span><a>View source</a><a>View history</a></div>
    </div>

    <aside class="infobox">
      <div class="ib-head">Your title</div>
      <div class="specimen"><!-- CSS-drawn example --></div>
      <div class="ib-cap">What the specimen shows.</div>
      <div class="ib-head">Classification</div>
      <table>
        <tr><th>Also known as</th><td>...</td></tr>
        <tr><th>Type</th><td>...</td></tr>
        <tr><th>Instances</th><td>29 recorded</td></tr>
      </table>
    </aside>

    <h1>Your title</h1>
    <div class="sub">From <em>Your Name</em>, the free encyclopedia</div>
    <p class="lead"><b>Your title</b> is a set of ... Every instance below appeared
       in my own work first, was rejected, and became a rule.</p>

    <h2>1&nbsp;&nbsp;Section name</h2>
    <ol><li>Rule.</li><li>Rule.</li></ol>

    <h2>6&nbsp;&nbsp;Sources</h2>
    <ol class="refs"><li>&ldquo;Quote.&rdquo; <span>(date)</span></li></ol>
  </main>

  <footer>Last edited by <a>Your Name</a> · 29 rules, 66 builds</footer>
</div>
```

Colours: link blue `#3366CC`, rules and borders `#A2A9B1`, infobox header `#EAECF0`,
body ink `#202122`. Those are Wikipedia's real values. Use them.

## Before you show it

- [ ] Every quote in Sources is real and carries a date
- [ ] The sidebar nav matches the real Wikipedia order
- [ ] Serif on the title and headings, sans on the body
- [ ] Every rule fits on one line
- [ ] The last rule clears the footer
- [ ] Nothing is centred
- [ ] The specimen is drawn, not generated

## What breaks it

**Rules that wrap to two lines.** The page stops reading as a reference and starts
reading as an article someone wrote.

**Invented citations.** The one thing that cannot be faked is the thing worth
having. Ship fewer real ones.

**A generated infobox image.** It will not match the CSS around it and it is the
first thing a reader's eye lands on.

**Too much of your own branding.** One nav link and the footer. The format does the
work; your logo on top of it fights the borrowed world you just built.
