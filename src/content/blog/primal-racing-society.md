---
title: "PRS: Building a Website for a Car Community"
description: "How I built a website for Primal Racing Society, a Norwegian car community I started in 2023, organizing driveouts, trackdays, and Cars & Coffee meetups."
pubDate: "2026-02-07"
---

I started Primal Racing Society back in 2023 because I wanted an excuse to drive good roads with good people. Turns out a lot of other car nerds in Norway wanted the same thing. We started organizing driveouts, trackdays, and Cars & Coffee meetups, and the community just kept growing. Our last driveout pulled 215 RSVPs. Not bad for a group that started with a few guys and a Facebook page.

The problem was that "a Facebook page" was literally all we had. Event info buried in comment threads, photos scattered across stories, no central place to point people to. So I did what any reasonable person with a car addiction and a code editor would do. I built us a website.

Check it out at [primalracingsociety.com](https://primalracingsociety.com).

## What It Does

It's a single-page site. No login, no CMS, no overthinking it. Just the essentials:

- **Hero:** A full-screen background video from our Fornebu-to-Tjøme driveout. On mobile it swaps to a static image so it doesn't murder your data plan.
- **About:** Three cards breaking down what we actually do (driveouts, trackdays, Cars & Coffee), with some nice scroll animations.
- **Events:** A timeline showing what's coming up and what already happened. Badges for status, locations, dates. Easy to keep updated.
- **Media:** Our YouTube recap embedded front and center, plus a live Instagram feed that scrolls on its own via the Behold API.
- **Join CTA:** Links to Instagram, YouTube, and the Facebook group. No membership fees, no forms. Just show up with something you like driving.

## The Tech Stack

- **Framework:** Next.js 16 with the App Router
- **Styling:** Tailwind CSS 4
- **Animations:** Motion (Framer Motion) for scroll-triggered reveals
- **Icons:** Lucide React
- **Instagram Feed:** Behold API
- **Hosting:** Vercel

## The Vibe

I wanted the site to feel like motorsport, not like a corporate landing page. So it's all black backgrounds, bold uppercase Oswald headings, and a red-orange accent that hits hard. Every section animates in as you scroll, and the hero plays a muted driveout video on desktop. It honestly looks cooler than it had any right to.

The whole thing is seven React components composed in a single `page.tsx`. No routing, no state management, no backend. Just a fast page that makes people want to come to the next meet.

If you're into cars and you're in Norway, come hang out. [primalracingsociety.com](https://primalracingsociety.com)
