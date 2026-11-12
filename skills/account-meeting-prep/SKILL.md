---
name: account-meeting-prep
description: Prepare a brief for an upcoming meeting with a company, using r.Potential's library of Units of Potential (UoPs), its AI-hiring comparison and industry trends, plus the relationship history from a CRM connector when one is connected (for example Salesforce through ClaudeForce). Use when someone asks to prep for, get ready for, or brief them on a meeting, call, workshop or visit with an account, or asks what to bring or say to a company.
---

# Account meeting prep

Produce one brief that someone can read in five minutes before a meeting with a
company. It joins two kinds of knowledge:

- **The relationship**, from a CRM connector if one is connected: where the deal
  stands, who is in the meeting, what they asked for, what is still open.
- **The opportunity**, from the r.Potential connector: the Units of Potential
  (UoPs) that fit what those people care about, each with a modeled dollar
  range, and how the company's AI hiring compares to its peers.

The CRM says how warm the account is; r.Potential says how big the prize is and
what to bring. Either half alone is still useful: without a CRM, build the brief
from r.Potential and the user's own description of the meeting.

## Steps

1. **Pin down the meeting.** From the request, get the company, the date if
   given, and who is attending. Ask one short question only if the company is
   missing; otherwise proceed and note any gaps in the brief.

2. **Find the account in r.Potential.** Call `list_accounts`, then pick the
   account whose name matches the company. Names can differ between systems
   ("Northwind" and "NorthWind Traders", "NWT" and "Northwind Traders"): match
   on the meaning, and if two accounts could be the one, ask which. An account
   can also have sponsor copies, named like "Northwind Traders (Contoso
   copy)": a sponsor
   is a partner presenting r.Potential. Use a sponsor's copy when the user
   works for that sponsor, or when the CRM deal is that sponsor's (for example
   an opportunity to sell the sponsor's product); otherwise use the company's
   own account. Say in the brief which one you used. If there is no account
   for the company, say so and continue with the CRM half only.

3. **Read the relationship, if a CRM connector is on.** Look for the account,
   its open opportunities (stage, amount, close date, owner), the contacts who
   will attend and their titles, recent activity, notes or call logs, and open
   tasks. When the CRM is Salesforce, read `references/salesforce.md` first.
   Collect, in the customer's own words where possible, what they have asked
   for: the stated priorities, the problems they named, the things they said to
   avoid.

4. **Choose the UoPs from the whole library.** Call `list_uops` for the
   account, not only `recommend_uops`: the ranked top few rarely match a
   specific customer's asks. Pick the two or three UoPs that best fit what
   the attendees asked for and their roles (a CHRO cares about workforce, a CFO
   about cost). Call `get_uop` on each pick for its dollar range, the value
   model behind it, and the tasks it moves to agents. If nothing fits an ask,
   say so plainly and name the closest candidate as something to adapt, not as
   a match. A larger UoP that would need adapting can follow the picks as one
   short line each, labeled as needing adaptation.

5. **Add the peer view.** Call `compare_ai_hiring_to_competitors` for the
   account. Use it as a question for the meeting, not a verdict: where the
   company sits against its peers, and which roles are growing or shrinking.
   Call `get_industry_trends` only if the meeting is about the industry rather
   than this company.

6. **Write the brief** in the shape below.

## The brief

Use these sections, in this order, and leave out any that have nothing in them.

- **Where things stand.** The deal or relationship in two or three sentences:
  stage, amount, close date, owner, last real contact, open tasks. CRM only.
- **Who you're meeting and what they want.** Each attendee with their role,
  and what they have asked for or care about.
- **What r.Potential brings.** The two or three chosen UoPs. For each: the
  title, why it fits this person's ask, the dollar range with its time basis,
  which tasks move to agents and which stay with people, and any reason to be
  careful with it.
- **How they compare to peers.** The hiring comparison as one or two
  questions to ask.
- **Suggested shape for the meeting.** A short running order: what to open
  with, where to spend the time, what to agree on before leaving.
- **Check before the meeting.** Anything that looks wrong or stale: dates that
  disagree, a name spelled two ways, an attendee nobody has confirmed, a task
  or a promised deliverable past its due date, a close date before the
  meeting, a probability that looks like a placeholder.

## Rules

- **Say where each fact came from.** Mark relationship facts as coming from the
  CRM and UoPs, ranges and peer figures as coming from r.Potential.
- **Never add UoP ranges together, and never present them as pipeline or
  forecast.** Each range is modeled for its own UoP; two UoPs can cover
  overlapping work, so a sum overstates the total. A range is the customer's
  value, not the price of a deal.
- **Keep r.Potential's caveats.** Use the one confidence word r.Potential
  gives for a figure (Estimated, Modeled or Measured), as given, and do not mix
  in a second word for the same figure. Pass on any gap it reports, such as
  UoPs that carry no dollar range.
- **Do not invent.** If the CRM has no notes, or r.Potential has no library for
  the company, say so. Never fill a gap with a plausible guess, and never
  describe a UoP's tasks without having called `get_uop` for it.
- **One account at a time.** Do not mix in another company's or another
  sponsor's UoPs, even when the names look alike.
- **No contact details in the brief.** Name people and their titles, but never
  copy an email address, phone number or home address from the CRM. If one
  looks wrong, say so ("her email doesn't match her name") without repeating
  it.
- **Saving priorities is optional and needs consent.** If the customer's asks
  map onto r.Potential's fixed priorities (cost, revenue, speed, risk,
  capability, people) and the r.Potential connector offers
  `save_my_preferences`, offer to save them so its ranking reflects them next
  time. Only save after the user agrees. Free-text topics cannot be saved.

## Example

Request: "Prep me for tomorrow's workshop with Northwind Traders. I'm meeting
their CHRO and the head of supply chain."

A good brief (invented data):

> **Where things stand** (CRM). One open opportunity, "Northwind ops
> transformation", at Discovery, closing in June, owned by Alex Rivera. Last
> contact was a demo debrief six weeks ago. One open task, "Bring a workforce
> idea and a supply-chain idea to the follow-up," is two weeks overdue.
>
> **Who you're meeting and what they want.** Dana Lee, CHRO, asked for one or
> two concrete ideas her team can validate, not a menu. The head of supply chain
> raised late supplier documents as the main pain point.
>
> **What r.Potential brings.**
> - *Supplier onboarding runs itself* fits the supply-chain ask: modeled at
>   $640K–$910K a year. Collecting and checking documents moves to an agent;
>   approving exceptions stays with buyers.
> - Nothing in Northwind's library is a workforce UoP. The hiring comparison
>   below is the better workforce conversation.
>
> **How they compare to peers** (r.Potential). Northwind's AI share of hiring is
> in line with its peers. Ask Dana whether the shift toward analyst roles is
> planned.
>
> **Suggested shape for the meeting.** Open with the hiring question (10 min),
> spend most of the time on supplier onboarding with the supply-chain lead, and
> leave agreeing on one idea each to validate, with owners and a date.
>
> **Check before the meeting.** The calendar entry names a different attendee
> from the CRM contact; confirm who is coming.
