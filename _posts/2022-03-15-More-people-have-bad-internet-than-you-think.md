---
layout: single
title: "More people have bad internet than you think"
date: 2022-03-15 01:00:00 +100
last_modified_at:
categories:
tags: internet rage fury old-man-yells-at-cloud reliability 
---

*tl;dr: the word 'average' in statistical contexts doesn't mean what most people seem to think it means*

I'm writing this from an airbnb in a foreign country that I've travelled to for work. 

I had a problem reaching the airbnb - I thought my prepaid SIM would give me coverage here, turns out it does, but the roaming charges are so egregious that I burned through my limit in like five minutes, it took me about half an hour to find a public wifi that I could connect to so that I could coordinate with my host.

Now that I'm in the airbnb it's not so bad, I can use the apartment's wifi. The wifi doesn't work terribly well in my room, mind you; I was listening to a Twitter Space on my phone while doing some computer things on my laptop. The phone and laptop can only connect to the wifi in the far corner of the room, so I'm huddled in the corner with my devices. Turns out there's not enough internet for both the Space and a file download at the same time, so I exited the Space and now my 30mb download actually starts. It'll take a while to finish, about ten minutes[^1], but it starts.

Would you like to guess which country I'm in? Would you have guessed I'm in Switzerland? I'm in Switzerland. I'm not in the sticks either, I'm in Zürich.

Before I flew out here I was in an airbnb in London. The wifi wasn't as bad there, but it was still irregular. The airbnb was in a high density council estate where dozens and dozens of overlapping wifi routers interfere with each other constantly. There simply weren't enough channels to go around.

Before London I was in Berlin, where wifi is nonexistent in public spaces and mobile internet doesn't work inside their buildings which are built like faraday cages.

Before Berlin, I lived in Melbourne, and if you know Australians you'll know how fond they are of complaining about their terrible internet services.

Amidst and between these locations I've used a variety of public wifi points and phone hotspots, they've all been variously bad.

Why am I telling you this? I'm telling you this because engineers need to realise how bad the internet is for many, many people. These are not poor countries I've described. I'm talking about major cities in wealthy countries, and the internet there is _patchy_.

I'd hazard a guess that I'm unlike most technology workers in that I get my mobile internet from cheap prepaid SIM cards and I have a tendency to hang out around people who aren't technology people, and I visit places whose proprietors aren't good at/concerned with optimising the placement of their wifi APs. You might say this is a choice on my part, and you're correct! But that's not the point.

The point is that enormous numbers of real people have inconsistent internet access - even in wealthy countries -  and if you're engineering for them, you need to take this into account.

I'll end this rant with some things to keep in mind:
- What's the median internet speed of your users/visitors? To mangle the George Carlin joke, half of them are worse off than that.

- Presumably your webpage/app/service loads/performs acceptably well for the median user, what's the experience for the 40th percentile? 25th? 10th? **Do you know what the 10th percentile of internet quality for your userbase is?**

- Would you be comfortable standing up in front of your management/hierarchs and telling them that your service only serves 90% of customers, by design? **If not, then even the 10th percentile is above your benchmark**.

- Following on from the last point, if your service was designed for the median user, then you're potentially excluding **50% of your users**

- Internet quality is not a random distribution, it has a long, crappy tail. This means that if your service is designed for the _mean_ user, then you're potentially designing for **less than 50% of your users**

- Internet services are used by people, not routers. Keep in mind that final hop over (usually) wifi and how fraught that can be.

- The examples I gave above relate to major cities in wealthy, developed countries. Does your service also have users in less developed countries? In regional towns? Remote areas?

For what it's worth I don't think the answer is to go back to plain html webpages, nor do I myself know the 10th percentile-of-internet-quality among users of any service I've worked on. I do feel strongly about bloat however, and I feel like we should all push back against it whenever we have the opportunity. I think the above points provide a good way to frame discussions about it.

If you're ever in a meeting where someone frames a discussion about internet bandwidth/latency/reliability in terms of "the average user", consider the above.

[^1]: After writing this rant I tabbed over to check the download. It had failed.