# Prompt Library v1 — Customer Support Replies

**Use case:** Drafting customer support email replies
**Structure:** Role + Context + Task + Format + Constraints
**Author's note:** One template, five swapped-variable prompts, all tested in Claude. This is meant to work like a function — you change the inputs, the shape of the output stays reliable.

---

## 1. The Reusable Template

```
ROLE:
You are a senior customer support specialist at {company_name}, known for a {tone} communication style.

CONTEXT:
A customer named {customer_name} has contacted support about {issue_type}.
Details of the situation: {issue_details}.
Relevant company policy / constraint: {policy_constraint}.

TASK:
Write a reply that acknowledges the specific issue (not a generic apology),
explains what will happen next, and offers {desired_outcome} where policy allows it.

FORMAT:
An email reply, 120–180 words, with:
- a greeting using the customer's name
- 2–3 short body paragraphs
- a sign-off from {agent_name}

CONSTRAINTS:
- Do not promise anything outside {policy_constraint}
- No filler apologies ("we're sorry for any inconvenience") without a concrete detail attached
- Match the {tone} tone consistently
- End with one clear, specific next step (not "let us know if you have questions")
```

**Variables:** `{company_name}`, `{customer_name}`, `{issue_type}`, `{issue_details}`, `{policy_constraint}`, `{desired_outcome}`, `{tone}`, `{agent_name}`

---

## 2. Five Prompts From the Same Template

### Prompt A — Late delivery refund request
```
ROLE: You are a senior customer support specialist at Northwind Goods, known for a warm, direct communication style.
CONTEXT: A customer named Priya has contacted support about a late delivery.
Details: Her order (#48213) was due in 3 days but is now 9 days overdue with no tracking updates since day 4.
Policy: Orders more than 7 days late qualify for a full refund or expedited reship, customer's choice.
TASK: Write a reply that acknowledges the specific delay, explains next steps, and offers a refund or reship.
FORMAT: Email, 120–180 words, greeting + 2–3 paragraphs + sign-off from Marcus.
CONSTRAINTS: No generic apologies without specifics. Don't promise anything outside policy. Match warm, direct tone. End with one clear next step.
```

### Prompt B — Damaged product on arrival
```
ROLE: You are a senior customer support specialist at Northwind Goods, known for a calm, reassuring communication style.
CONTEXT: A customer named Diego has contacted support about a damaged item.
Details: A ceramic vase (order #51902) arrived with a large crack; he attached photos.
Policy: Damaged items are replaced free of charge with no return required if photo evidence is provided.
TASK: Write a reply that acknowledges the damage, confirms the photos are sufficient, and offers a free replacement.
FORMAT: Email, 120–180 words, greeting + 2–3 paragraphs + sign-off from Marcus.
CONSTRAINTS: No generic apologies without specifics. Don't ask him to return the broken item since policy doesn't require it. Match calm, reassuring tone. End with one clear next step.
```

### Prompt C — Billing dispute (double charge)
```
ROLE: You are a senior customer support specialist at Northwind Goods, known for a precise, no-nonsense communication style.
CONTEXT: A customer named Aaliyah has contacted support about a billing issue.
Details: She was charged twice for order #55010 — $84.50 appears on her statement twice on the same date.
Policy: Duplicate charges are refunded within 3–5 business days once confirmed in the payment system; no manual override possible.
TASK: Write a reply that confirms you can see the duplicate charge, explains the refund timeline, and sets accurate expectations.
FORMAT: Email, 120–180 words, greeting + 2–3 paragraphs + sign-off from Marcus.
CONSTRAINTS: No generic apologies without specifics. Don't promise a faster refund than policy allows. Match precise, no-nonsense tone. End with one clear next step.
```

### Prompt D — Product doesn't match description
```
ROLE: You are a senior customer support specialist at Northwind Goods, known for an empathetic, solution-focused communication style.
CONTEXT: A customer named Ben has contacted support about a product mismatch.
Details: He ordered a "queen-size" throw blanket (order #59944) that arrived noticeably smaller than the listed dimensions.
Policy: Mismatched-description items can be returned for a full refund, or exchanged for a correct size if available, shipping paid by Northwind.
TASK: Write a reply that acknowledges the sizing discrepancy, offers both the refund and exchange options, and lets him choose.
FORMAT: Email, 120–180 words, greeting + 2–3 paragraphs + sign-off from Marcus.
CONSTRAINTS: No generic apologies without specifics. Don't imply the listing was accurate. Match empathetic, solution-focused tone. End with one clear next step.
```

### Prompt E — Positive feedback / thank-you reply
```
ROLE: You are a senior customer support specialist at Northwind Goods, known for a genuine, upbeat communication style.
CONTEXT: A customer named Sofia has contacted support just to say thank you.
Details: She praised how fast her replacement item arrived after a prior damage claim (order #51902 — same case as Prompt B).
Policy: N/A — no resolution needed, this is a goodwill/relationship-building reply.
TASK: Write a reply that thanks her specifically for the feedback and reinforces the positive experience without over-selling.
FORMAT: Email, 120–180 words, greeting + 2–3 paragraphs + sign-off from Marcus.
CONSTRAINTS: No generic "we're thrilled to hear that" without a specific callback to her situation. Don't pitch other products. Match genuine, upbeat tone. End with a warm, low-pressure close (not a "next step" since none is needed).
```

---

## 3. Tested Outputs (run in Claude)

### Output A — Late delivery refund request
> Hi Priya,
>
> I checked order #48213 and you're right — it's now 9 days past the original delivery date, and the tracking has been frozen since day 4 with no carrier updates. That's well past what we consider acceptable, so I want to make this right immediately rather than ask you to keep waiting.
>
> Since the order is more than 7 days overdue, you're eligible for either a full refund or an expedited reshipment at no extra cost — whichever works better for you.
>
> Just reply with "refund" or "reship" and I'll process it the same day.
>
> Best,
> Marcus

### Output B — Damaged product on arrival
> Hi Diego,
>
> Thanks for sending the photos of your vase from order #51902 — the crack is clear, and this isn't something you should have to work around or pack up and return.
>
> Because we have photo confirmation, you don't need to send the damaged item back at all. I'm sending out a free replacement today, and it will ship with priority handling given what happened last time.
>
> You'll get a shipping confirmation with tracking within the next few hours.
>
> Best,
> Marcus

### Output C — Billing dispute (double charge)
> Hi Aaliyah,
>
> I pulled up order #55010 and confirmed the $84.50 charge appears twice on the same date — that's a duplicate on our end, not a purchase you made twice.
>
> I've flagged it for refund now. Our payment system requires confirmation before releasing funds, so the refund will post to your original payment method within 3–5 business days — I can't push it through faster than that, but I'll make sure it's not delayed beyond that window.
>
> I'll follow up personally once the refund is confirmed on our side.
>
> Best,
> Marcus

### Output D — Product doesn't match description
> Hi Ben,
>
> You're right to flag this — the throw blanket from order #59944 arrived smaller than the "queen-size" dimensions we listed, and that's on us, not an expectation issue on your end.
>
> You have two options: a full refund, or an exchange for the correct size if it's in stock, with return shipping covered by us either way.
>
> Let me know which you'd prefer and I'll set it up right away — no need to cover any shipping costs on your end.
>
> Best,
> Marcus

### Output E — Positive feedback / thank-you reply
> Hi Sofia,
>
> Thank you for taking the time to write in — it means a lot, especially since your first experience with the vase (order #51902) wasn't a good one. Hearing that the replacement arrived quickly is exactly the outcome we were hoping for after that.
>
> I've passed your note along to our shipping team, since fast turnaround after a damage claim isn't a given, and it's good for them to hear it landed well.
>
> Really glad it worked out — hope the vase is enjoying its new home!
>
> Best,
> Marcus

---

## 4. Notes on Reusability

- **What stayed constant:** the 5-part skeleton (Role/Context/Task/Format/Constraints), the word count, the sign-off structure, and the "one clear next step" rule.
- **What changed per prompt:** tone, policy details, and the resolution offered — proving the template flexes across refund, replacement, billing, mismatch, and even non-issue (thank-you) cases without needing structural rewrites.
- **Reuse tip:** Keep a running list of `{tone}` options (warm/direct, calm/reassuring, precise/no-nonsense, empathetic/solution-focused, genuine/upbeat) mapped to issue severity, so picking a tone becomes a lookup instead of a rewrite.
- **Next version ideas:** add a `{customer_history}` variable for repeat-customer cases, and an `{escalation_flag}` variable for replies that need a manager cc'd.
