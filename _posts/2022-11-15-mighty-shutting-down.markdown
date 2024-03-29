---
layout: post
title: "Mighty Retrospective"
date: 2022-11-15T14:09:00-07:00
---

This past Sunday, we announced that [Mighty](https://web.archive.org/web/20220903024816/https://www.mightyapp.com/) is shutting down. I’ve been working on it since its infancy -- before we pivoted to even making a browser at all. I want to spend some time talking about why we built Mighty in the first place, and why we weren’t able to ultimately achieve those goals. This is essentially a case study on a topic I’ve been intimately close to over the past 3.5 years.

## What were we trying to build, and why?

Mighty’s short term goal was to make people more productive with their browser. Our longer term goal was to build [a new type of computer](https://blog.mightyapp.com/mightys-secret-plan-to-invent-the-future-of-computing/), but for this post I’ll be discussing our shorter term goals. The core goal was to make a faster web browser. By faster, I mean the time difference between a user taking some action and that action happening, like loading a webpage, clicking on a link, closing a tab, etc. The first users of Mighty were those that explicitly found Chrome slow. Figma, Google Drive, hundreds of tabs, slow internal tools, competing non-browser apps, and old laptops were common examples of this. Later on, we started to find people that simply were curious to try out Mighty, and to their surprise they ended up finding it was faster.

Mighty also had many other benefits besides raw speed, which I’ll discuss later, but we ultimately found that the biggest fraction of users that were passionate about Mighty were mainly compelled by its speed.

You might be surprised that people would be willing to spend $35/month when the competing products were free, but the answer is simple: people value their time, and are willing to spend money to be more efficient. As long as we can save people some substantial time, many people would be willing to pay. The question was: could we?

## How do you make a cloud browser faster than a normal one?

Since Chrome is already hyper-optimized in many of the performance critical areas, our approach was to use the unique aspects of a browser running on a server to make Chrome faster. The most basic idea: give the browser better hardware (CPU, RAM, GPU) to run on.

- CPU: We gave users a 16 core machine just for their browser, but it turns out that the web is largely limited by single core performance (think JS, layout, html parsing, etc). On top of that, Apple’s new M1 chip turns out to have phenomenal single core performance. It’s faster than almost any server CPU money can buy. So fast, in fact, that we went on a quest figuring out how to get desktop Intel i9 processors running in a datacenter. Overclocked and all. And that was simply to beat the M1’s performance by a small margin.
- RAM: Mighty allowed users to open hundreds of tabs without being worried that their RAM would be consumed. But my sense is this was not a killer feature. The benefit simply isn’t massive: the alternative is to close tabs and “clean things up”. Many people probably do this anyway because it’s visually hard to have hundreds of tabs open, so users end up closing tabs even with infinite RAM. This is evident in the data: when we gave users 32gb of RAM, 90+% of them didn’t go beyond 16. We did have the opportunity to provide users with a whole new interface of tab management -- one in which tabs never have to be closed and hundreds of tabs are visually manageable. Maybe this would have been a smash hit, it’s hard to be sure.
- GPU: This is impactful on certain web apps like Google Earth, visualization tools, or even fancy animations like github.com’s old home page. But the fraction of websites impacted by this turns out not to be huge (yet).

Besides these direct hardware benefits, we could also use the extra hardware in other creative ways:

- Pre-loading websites in the URL bar before a user presses enter.
- Saving recently used websites as background tabs, so that they load instantly.
- Making a local CDN
- Increasing cache sizes wherever is beneficial

## The other benefits of Mighty

There were a few awesome features that Mighty provided other than speed.

- Longer battery life
- Quieter fan
- Google Drive search, tab search, and other helpful shortcuts
- Zoom reminders
- Assurance that their tabs will be saved when Mighty is closed, and that they won’t need to reload when Mighty is opened back up
- Auto-updating experience -- we restart the browser for users when they’re not using it

We also toyed around with the idea of AI integration. Though we didn’t deeply explore this, you could in theory resize images in a right click menu, summarizing articles, fill out forms better, or even have Mighty click around on the web for you to complete a task.

Some of these features could be put on a local browser, and I think they’re great ideas. I hope someone steals them. You might even be able to make a viable business by doing this, as some are trying to do (Brave, [Arc](https://thebrowser.company/)). It’d just need to be cheaper because the value it gives is not as significant as a faster browser, which is possible because the unit costs are near-zero for a local browser.

## Why did users churn?

Many users didn’t continue paying for the product for a variety of reasons. Some of the top ones were networking stutters, stability issues, and missing features (like webcam support). We also ironically struggled with a sluggishness issue. There were some specific cases where if you pushed Mighty hard enough, it would end up performing worse than Chrome for some reason that we’re still not entirely sure of.

## Why did we shut down?

While Suhail was the one to make this decision and has the full context on the decision, as I see it the benefits of Mighty just weren’t substantial enough to handle the drawbacks, and thus churn was unlikely to be quickly brought down to reasonable levels. In addition, Suhail had been trying out building [a new product](https://playgroundai.com/) that was showing to be a reasonable alternative bet.

I don’t think we necessarily needed Mighty to be 10x faster than an M1. Even if it was the *same performance*, which it largely was, this would be a substantial boon to all the Windows users that don’t have access to such a processor. Through some quick tests, it seemed reasonable to expect Mighty to be at least 2x faster for most Windows users. But we would have needed to make significant progress on the other issues with Mighty.

The thing was, building Mighty ended up being incredibly challenging. I’ll pick audio as an example of something that we built. Since the browser is running in the cloud, we had to stream audio down to the client. But it’s really important that the audio is smooth and contiguous. Any lost audio will be immediately noticeable, whereas dropping a video frame is not as bothersome. We went through many versions of this over several moments, with many brilliant “a-ha!” moments. By the end of this work, it was pretty excellent, but still had a few unfinished bugs. This sort of significant effort for run-of-the-mill features was quite common. File downloads, scrolling, VPN, ip geolocation, battery usage, YubiKey support, and smooth videos are just a few examples. And building a feature-compatible browser was only one of the several tough challenges we faced.

It’s a hard call, especially given the immense effort we’ve put into it, but I think it’s the right one.

## Thank You

I want to thank all our users. Without you, we would have been entirely blind. Your feedback helped us make the product better week after week, and kept me motivated throughout the journey. You’re the reason this even had a chance of succeeding. And of course, I have immense gratitude to my team that I had the privilege of working with. I learned a ton from you all and had so much fun getting to know you.

## Addendum

Hopefully I’ll have the opportunity to document some of the technical details of Mighty. One of the coolest examples I’ve seen of a company closing was from Makani power. They released their entire avionics, flight controls and simulation [code repositories](https://github.com/google/makani), [flight logs](https://console.cloud.google.com/marketplace/product/bigquery-public-datasets/makani-logs), [technical videos](https://www.youtube.com/playlist?list=PL7og_3Jqea4VRCZmMNK4LDH64sYgkLZzv), a 1200 page technical report, and a [full length documentary](https://www.youtube.com/watch?v=qd_hEja6bzE). I don’t plan to do anything that detailed, but something in that direction could be cool.
