---
title: "PRS: Building a Website for a Car Community"
description: "How I built a website for Primal Racing Society — a Norwegian car community I started in 2023, organizing driveouts, trackdays, and Cars & Coffee meetups."
pubDate: "2026-02-07"
---

I started Primal Racing Society back in 2023 as a way to bring car enthusiasts together here in Norway. We organize driveouts through some of the country's best roads, trackdays, and casual Cars & Coffee meetups. The community has been growing fast — our last driveout had 215 RSVPs — but everything was scattered across Facebook posts and Instagram stories. We needed a proper home on the web.

So I built one. The goal was simple: something bold, fast, and unmistakably car culture. No blog, no CMS, no user accounts — just a clean single-page site that tells people who we are and how to join.

You can see it live at [primalracingsociety.com](https://primalracingsociety.com).

## What It Does

The site is a single-page experience built around a few key sections:

- **Hero:** Full-screen YouTube background video from our Fornebu-to-Tjøme driveout, with a mobile fallback image. Sets the tone immediately.
- **About:** Three cards covering what PRS does — driveouts, trackdays, and Cars & Coffee — each with scroll-triggered animations.
- **Events:** A timeline of upcoming and past events with dates, locations, and status badges. Easy to update as the season progresses.
- **Media:** An embedded YouTube video and a live Instagram feed pulled from the Behold API, displayed as an auto-scrolling marquee.
- **Join CTA:** Links to Instagram, YouTube, and our Facebook group. No membership fees, no sign-up forms — just follow and show up.

## The Tech Stack

- **Framework:** Next.js 16 with the App Router
- **Styling:** Tailwind CSS 4
- **Animations:** Motion (Framer Motion) for scroll-triggered reveals and staggered transitions
- **Icons:** Lucide React
- **Instagram Feed:** Behold API
- **Hosting:** Vercel

## The Vibe

The design leans hard into the motorsport aesthetic — black background, bold uppercase Oswald headings, and a red-orange accent color. Every section uses `whileInView` animations so the page feels alive as you scroll. On desktop, the hero autoplays a muted driveout video behind the logo. On mobile, it falls back to a static thumbnail to save bandwidth.

The whole thing is a single `page.tsx` composing seven components. No routing complexity, no state management — just a fast, visual landing page that gets people excited and points them to the right socials.

If you're into cars and happen to be in Norway, check out [Primal Racing Society](https://primalracingsociety.com) and join the pack.
