---
title: "TidWerk: A Time Tracker Built for the Way Consultants Work"
description: "Introducing TidWerk, a streamlined time tracking application for consultants built with SvelteKit, Turso, and Drizzle."
pubDate: "2026-02-04"
---

I got tired of juggling spreadsheets and fighting clunky, over-engineered tools every time I needed to bill a client. Most time trackers are either too simple to handle complex consulting rates, or too complex for a solo developer or small team to use quickly.

That's why I built **TidWerk** (Norwegian for "time work"). It's a time tracking app designed specifically for consultants who need a fast, reliable way to manage their hours and get paid.

You can check it out live at [tidwerk.com](https://tidwerk.com).

## Why TidWerk?

As a consultant, your time is your product. But tracking that time shouldn't be a job in itself. TidWerk focuses on getting out of your way while providing the specific features that matter for billing:

- **Client-Specific Rates:** Not all hours are equal. TidWerk handles regular, overtime, and weekend rates per client, with automatic fallbacks (like 1.5x for overtime) if you haven't set a custom rate.
- **Absence Tracking:** Billing is only half the story. Tracking vacation, sick leave, and public holidays in the same interface makes monthly reporting seamless.
- **Automated Reporting:** Generate formatted HTML reports for yourself, your manager, or your clients. You can even set them to auto-send on the last weekday of the month.

## The Tech Stack

I wanted TidWerk to be fast, type-safe, and easy to deploy. The stack reflects that:

- **Framework:** SvelteKit 2 + Svelte 5 (for that sweet reactive DX)
- **Database:** Turso (SQLite at the edge)
- **ORM:** Drizzle ORM (type-safe SQL)
- **Auth:** Google & Microsoft OAuth via Arctic
- **Email:** Resend
- **Hosting:** Cloudflare Pages
- **Styling:** Tailwind CSS + shadcn-svelte

## What's Next?

TidWerk is already live and I'm using it for my own consulting work. It's been a game-changer for my end-of-month workflow, turning a two-hour spreadsheet ordeal into a two-minute report review.

If you're a consultant looking for a better way to track your work, give [tidwerk.com](https://tidwerk.com) a try. I'd love to hear what you think!
