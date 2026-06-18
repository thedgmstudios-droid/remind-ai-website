# Remind AI — App Description & Feature Overview

## What It Is

Remind AI is a minimalist iOS reminder app that lets you create reminders by simply talking or typing in plain language — "Call Mom on Sunday at 7pm", "Water the plants every weekend", "Pay rent Friday." The AI parses your natural language and turns it into a scheduled reminder with notifications, no forms to fill out.

What sets it apart from built-in reminder apps is a lightweight personal CRM layer built right in: you can link reminders to specific people in your life, and attach private notes to each person — the kind of small details that make you a better friend, partner, or colleague. Big companies pay thousands for CRMs to remember every detail about their customers. Remind AI gives you one for the people in your life.

The app is iOS-only, paid from day one, and built for low-friction daily use — the kind of tool you reach for without thinking.

---

## Core Features

### Natural Language Reminder Creation
Two ways to create a reminder — chat or manual form. The Chat tab accepts free-text or voice input and passes it through an AI parser (Claude Haiku) that extracts the reminder title, date/time, recurrence, and linked person. The parser strips command phrasing so the reminder title is always the *thing to do*, never the command: "Call Mom", not "Set a reminder to call Mom." For users who prefer structure, a manual Add Reminder sheet lets them set every field by hand.

### Voice Input
The mic button in the Chat composer starts on-device speech-to-text (framed to the user as AI, since the experience is identical). The transcript feeds live into the input field while recording so the user can review it before sending. Voice and text share the same AI parse pipeline and the same usage limits.

### Recurring Reminders
Six recurrence options — daily, weekly, biweekly, monthly, yearly, and custom (any number of days). Recurring reminders behave differently from one-off reminders throughout the app: they never go to "Overdue" (a daily vitamin reminder being 2 hours late isn't missed — it's just today's instance still pending), they surface in a dedicated "Recurring · Today" section, they show a circular-arrow badge instead of a checkbox, and they advance to their next occurrence rather than completing.

### Smart Notification Escalation
One-off reminders trigger a 3-stage notification chain: at the scheduled time, then +1 day, then +3 days. This ensures nothing falls through the cracks without being annoying for recurring items. Recurring reminders use a single-fire notification at their scheduled time, since they'll surface again automatically. Notification actions let users mark done or skip directly from the lock screen.

### Reminders List with Intelligent Sections
The home tab groups reminders into time-based sections in a fixed priority order: Overdue → Recurring · Today → Today → Tomorrow → This Week → Later → Completed Today. Completed Today auto-clears at midnight so the list never accumulates stale history. Each section has a distinct visual treatment — overdue in red, recurring today in accent blue, all others in muted grey.

### Lightweight Personal CRM (People Tab)
Add people manually or import them in bulk from iPhone Contacts (names only, no phone numbers or email addresses stored). Each person gets a dedicated detail screen showing all reminders linked to them and their private notes. The People tab is alphabetically sorted and supports swipe-to-delete. You can @-mention a person in the chat composer for quick linking ("Remind me to pick up flowers for @Sarah").

### Private Notes per Person
Each person can have unlimited plain-text notes (or up to 10 on the Personal Memory plan). Notes are timestamped, stored privately in iCloud, and never leave the device to any backend. Use them for anything: what you talked about last time, her favorite restaurant, his new dog's name, context before a difficult conversation. Notes are fully editable via tap or long-press context menu.

### Offline Resilience
The Chat tab requires an internet connection (it's gated by a network monitor) and shows a clear offline state with a manual-add fallback button. Manual reminder creation via the form sheet stays fully offline-capable so users are never completely blocked.

### Active Reminder Limit Enforcement
A hard-coded limit guard checks the user's tier cap before any reminder creation — whether via the FAB, the Chat tab, or the Person Detail CTA. Blocked requests show a static message and never hit the AI backend, so users at their limit cost zero AI tokens. The guard runs client-side before parsing.

---

## Onboarding

A 14-screen Cal-AI-style funnel designed to build emotional investment before the paywall. Key screens:

- **What slips through the cracks?** — multi-select of forget categories (birthdays, follow-ups, tasks, medications, etc.)
- **Try the AI** — a passive typewriter animation showing natural-language inputs being parsed into reminders in real time, including recurring examples with badge pills. No real API calls, no input affordance.
- **Or just talk to it** — a passive voice animation with a pulsing mic, waveform, and a transcript that fills word by word before resolving into a parsed reminder.
- **Your People** — a preview of the CRM tab with sample contacts and their upcoming reminders, including recurring-badge examples.
- **Private Notes** — a focused preview of the notes surface with timestamped note bubbles and the iCloud privacy footer.
- **Your personal CRM** — the plan screen. Positions the app as the CRM that big companies pay thousands for, now for your personal life. Three capability cards: effortless AI reminders, iPhone Contacts integration, private notes per person.
- **Paywall** — 7-day free trial, two tiers, yearly billing as default.

---

## Pricing

Two tiers, no free plan. 7-day free trial on both.

| Plan | Monthly | Yearly | Active Reminders | Notes/Person |
|---|---|---|---|---|
| Personal Memory | $3.99 | $29.99 | 50 | 10 |
| Ultra Memory ⭐ | $12.99 | $99.99 | 400 | Unlimited |

Both plans include full access to Chat, Reminders, People, and Person Detail with private notes. The ladder is volume and notes-per-person, not feature gating. Ultra Memory is the pre-selected popular default. Gross margin is verified at ≥85% on both tiers on the yearly cadence (Personal Memory 94.3%, Ultra Memory 86.4%).

---

## Technical Stack

- **Platform:** iOS 17+, SwiftUI
- **Persistence:** SwiftData + CloudKit (private database, stored on user's iCloud quota at $0 infrastructure cost)
- **AI parsing:** Claude Haiku 4.5 via a Cloudflare Worker proxy with App Attest + JWT security and KV-based per-device rate limiting
- **Voice:** On-device speech recognition via AVFoundation / Speech framework
- **Distribution:** App Store, TikTok-first marketing
