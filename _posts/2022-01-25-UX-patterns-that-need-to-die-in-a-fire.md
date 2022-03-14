---
layout: single
title: "UX patterns that need to die in a fire please"
date: 2022-03-14 01:00:00 +100
last_modified_at:
categories:
tags: rants ux rage fury old-man-yells-at-cloud
---

I sometimes run into UX behaviour that makes me openly wonder whether or not the people who designed it actually use computers at all.

I'll update this post with examples as I encounter them. This list will be very extremely biased towards my personal preferences.

## 1. You click on something and it moves

This breaks my mental flow and I'm sure it breaks yours too.

![F]({{ "assets/images/2022-01-25-UX-patterns-that-need-to-die-in-a-fire/safari_address_move.gif" | absolute_url}})

The thing I want to work with has moved. I clicked on it because I wanted to control it, and now it's somewhere else! Bad! Little frustrations and frictions like this make an interface irritating to work with. 

## 2. You're reading a news article and when you scroll up a useless bar appears on top of what you were reading

This crime is very common on mobile, but I've seen it on web as well. Many (most?) people do not read linearly. They read back and forth through an article, mostly reading forwards but tracking back every now and again to find where concept, person, organisation, (etc.) was first mentioned or to clarify some fact that was introduced previously.

If, as you read down, you scroll such that your eye level is around the top of the screen then as soon as you scroll up to see what the previous line or paragraph was, the line you want is covered up by an awful "navigation bar" or some garbage that is of no use to anyone, ever[^1].

The most egregious example of this I've seen is on KnowYourMeme. Check out this monstrosity. Here's by browser looking at a page about a meme, I'm reading the history but I want to re-read the last paragraph. Time to scroll up! Let's see what happens.

![F]({{ "/assets/images/2022-01-25-UX-patterns-that-need-to-die-in-a-fire/kym_bad.gif" | absolute_url}})

The text I wanted to read is covered up by a bar of useless trash. The assumption appears to be that I scrolled up because I _wanted_ to summon the bigger bar, that the slimline convenience bar they provided me while I was scrolling down was not _big_ enough and I wanted more bar. I never want more bar.

In the event that your users legitimately _do_ want more bar, there's a behaviour that does this better. The Daily Beast has the best implementation of this pattern that I've seen so far. I actually appreciate how slick this is! Observe that the above text rolls down for a few lines before the Big Bar appears, and even then it rolls down elegantly, instead of heaving its bulk down onto the text I wanted to read.

![F]({{ "/assets/images/2022-01-25-UX-patterns-that-need-to-die-in-a-fire/tdb_good.gif" | absolute_url}})

Better still are the navbars which don't expand until you reach the very top of the page, buuut...

## 3. Navigation bars in general, actually

Here is the easiest and most commonly used workflow for finding a thing on the internet:
1. open a new tab
2. type a search term for the thing
3. click on the link that appears in the search results

This workflow even applies if you're already reading a page on the website where your thing is hosted. Navigation bars are actually useless. I know there's some rusted-on belief that you "should" have them for inarticulable reasons of properness, but if you must have a vestigial navbar, please make it as unobtrusive as possible.[^2] I strongly suspect that the optimal navbar consists of a the title/logo of the article/website (for when you inevitably come back to a half-read tab and need to remember what it is and why you had it open) and maybe login button or something.

## 4. `mailto` links belong in the bin. I never want email addresses to be interactive

I do my email in gmail, both my personal mail and my professional email. Every single time I've clicked on a `mailto:` link it's beeen a mistake because I intended to right click it. Every single itme. 
The desired email workflow is this: 
1. right click the email address in the thing I'm looking at
2. copy
3. paste into my gmail tab
4. write the email and send

I do not ever want a mailto link to open Apple Mail or Outlook or Outlook Express. I never ever want them to open in whatever terrible mail client ships with my phone, and if I make the mistake of left-clicking intead of right-clicking (or short tapping instead of long tapping, or if I don't double-touch the trackpad properly, or whatever) then I really don't want to be punished for that by having my system's mail client steal focus and churn through its initialisation process before I can terminate it.

This is even worse when you're looking at some company's website on mobile and their email address is hidden behind an opaque 'contact us' link, and you're merely a badly executed long-tap away from being sent to Apple Mail. It's bad.

## 5. Any shortcut/gesture that maps to the 'back' button on a browser will only ever be activated by mistake

The number of times I have deliberately activated a 'back' gesture is like two or three times, total. The number of times I've accidentally activated one is much, much higher. 

The number of times I've accidentally activated one in the middle of filling out an online form or some online government workflow is too infuriating to think about. Gestures suck[^3]. Gestures that do irreversible things that break workflows are just unacceptable. 

[^1]: Ever.
[^2]: Please also use your telemetry scripts to find out what percentage of your visitors actually use the damned thing. If it's more than the low single digits, I owe you a coke
[^3]: the exception-that-proves-the-rule is the 'switch desktop' gestures on mac laptops. They're the one gesture that isn't a pain to use in my experience. They require a bigger commitment - three fingers makes them hard to activate by accident - and the gesture is entirely reversible - you can just swipe back! Nothing is changed, removed, deleted, or terminated! Good gesture