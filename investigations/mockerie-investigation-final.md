# The Mockerie.io Investigation — Final Content Document
### LinkedIn Article · LinkedIn Post · Reddit Post
### Scope: Mockerie.io only. Screely is excluded from this document entirely.

---

## Investigation Summary

**What we found:** Mockerie.io, a free mockup tool active since at least 2015 and untouched since around 2020, has a footer link labeled "Staff favorites" pointing to uk-sobs.org.uk — a domain styled to resemble Survivors of Bereavement by Suicide (SOBS), a real UK charity (charity #1098815, actual domains: uksobs.org / uksobs.com). The linked domain is not the charity — it's a fully built gambling affiliate site ("Non GamStop Casinos 2025"). We verified this directly.

**Why it matters:** VirusTotal shows uk-sobs.org.uk as 0/92 — clean, because it's neither malware nor credential phishing. But two enterprise web-categorization vendors currently misclassify it: Forcepoint ThreatSeeker labels it "service and philanthropic organizations," alphaMountain.ai labels it "Health." Only Google correctly labels it "gambling." Organizations relying on those categorization feeds for web filtering would currently let this through under a "charity" or "health" policy exception.

**Supporting technical evidence:**
- Mockerie's footer reads "© 2020"; a code comment is dated 2015 — the legitimate tool hasn't been maintained in years, consistent with a quiet, unnoticed compromise.
- uk-sobs.org.uk's console logs show a "Failed to spoof webdriver" error, indicating anti-automation detection code is present on the page (this suggests but does not confirm bot-vs-human content differences — do not claim confirmed cloaking).
- Network requests reveal non-standard WordPress plugin paths, consistent with a compromised WordPress installation as the likely mechanism.
- The favicon file is named `UK_Sobs-favicon.svg` and the meta site name is "Uk Sobs" — evidence the resemblance to the real charity's name is deliberate, not coincidental.

**What's confirmed vs. not:**
- ✅ Fully verified: the footer link, the gambling content, the charity-name mismatch, the VirusTotal score, the categorization mismatch, the console log entry, the WordPress plugin paths.
- ❌ Not confirmed, do not claim: proven cloaking (bot vs. human content differences), whether any AI assistant currently recommends Mockerie, whether the nav-menu gambling links (separate from the footer one) are visible in normal browsing.

**Sensitivity note:** This involves the name of a suicide-bereavement support charity. Keep tone factual and restrained throughout — no snark, no "gotcha" framing. Lead with the real charity's legitimate mission so no reader confuses it with the impersonating domain.

---

## 1. LinkedIn Article

---

### We Followed One Footer Link on an Old Free Tool. Here's Where It Led.

Mockerie.io has been around since at least 2015 — a simple, free tool for turning a website screenshot into a polished device mockup. It's the kind of small, single-purpose site that shows up in "best free mockup tools" roundup articles and then quietly stops getting updated once the person who built it moves on. The footer still reads "© 2020." A code comment in the page source is dated 2015. Nobody's touched the core product in years.

But someone has touched the page itself.

**What we found**

Scroll to the bottom of Mockerie.io today and there's a small section labeled "Staff favorites" — a single link, styled like a normal recommendation, pointing to a site called uk-sobs.org.uk. On an old, unmaintained tool, one out-of-place footer link is easy to miss. We followed it anyway.

**Where it led**

uk-sobs.org.uk is not what its name suggests. Survivors of Bereavement by Suicide (SOBS) is a real, registered UK charity — charity number 1098815 — supporting people bereaved by suicide. Its actual domains are `uksobs.org` and `uksobs.com`. The domain we were sent to has no connection to that charity at all. It's a fully built-out gambling affiliate site: "Non GamStop Casinos 2025," complete with betting-site logos, deposit bonus tables, and "Play Now" buttons. The favicon file is literally named `UK_Sobs-favicon.svg` — a small detail that makes it hard to believe this is coincidental naming rather than deliberate.

**Why this matters more than one bad link**

Run this domain through VirusTotal and it comes back with a community score of 0 out of 92 — no antivirus or malware engine flags it. That's not actually surprising once you understand what those engines are built for: malware signatures and phishing kits designed to steal credentials. This site isn't doing either of those things. It's a legitimately functioning, legally operating gambling business that happens to be squatting on a name built to resemble a support charity for people grieving a suicide.

Here's the part that should concern any organization relying on automated web filtering: we checked how security categorization vendors currently classify this domain. Google correctly labels it "gambling." **Forcepoint ThreatSeeker labels it "service and philanthropic organizations." AlphaMountain.ai labels it "Health."** Forcepoint's categorization feeds are used in real corporate web filtering and DLP systems. An organization with a policy that allows access to "philanthropic" or "health" sites while blocking gambling would currently let employees straight through to this one, misclassified.

We also found evidence the site is running anti-automation detection code — a console error reading "Failed to spoof webdriver" appears in its logs, alongside non-standard WordPress plugin paths that suggest the underlying mechanism here is a compromised WordPress installation, not a site built from scratch for this purpose.

**The pattern**

Put the footer link and the destination together and you get a small but complete picture of a category of risk that's easy to underestimate: an old, trusted tool with a quietly inserted link, leading to a domain built to impersonate something sympathetic and trustworthy, currently misclassified by tools organizations rely on to make access decisions. None of it trips a traditional malware scanner. All of it is verifiable by just following the link and reading what's actually there.

**What we'd want security teams to take from this**

Category-based web filtering is necessary but not sufficient — a categorization feed is only as current as its last update, and abuse like this exploits exactly that lag. Content-aware verification, that actually looks at what a page currently contains rather than trusting a label assigned months or years ago, is what catches this kind of thing before an employee clicks it.

---

## 2. LinkedIn Post

**Format:** 4-slide document/carousel recommended — slide 1: Mockerie footer screenshot, slide 2: uk-sobs.org.uk gambling page, slide 3: VirusTotal categories comparison (Google/Forcepoint/alphaMountain side by side), slide 4: takeaway + link.

> We found one out-of-place link in the footer of an old, free mockup tool.
>
> Followed it. It led to a fully built gambling site — branded to look like a UK charity that supports people bereaved by suicide.
>
> VirusTotal shows it as 0/92 — completely clean. Meanwhile, two enterprise web-categorization vendors currently label the same domain "philanthropic organizations" and "Health." Only one out of four sources we checked actually got it right.
>
> This isn't malware. It's not credential phishing. It's a category of risk that slides right past tools built to catch those two things specifically — and it's currently sitting in a corporate web filter's "safe" list somewhere.
>
> Full breakdown, screenshots, and what we think this means for category-based filtering: [link]
>
> Anyone else finding gaps like this between what a filter says and what a domain actually shows?

---

## 3. Reddit Post (r/cybersecurity or r/netsec)

> **Title:** Followed a footer link on an old free tool — ended up at a gambling site misclassified as a charity by two security vendors
>
> (Disclosure: I work in security tooling, flagging that up front — but this is a straight writeup of what we found, not a pitch.)
>
> Was poking at old, unmaintained "free tool" sites — the kind that show up in 2019-era roundup posts and never got touched again. Mockerie.io is one of them: still works, but the footer has a "Staff favorites" link that doesn't belong — points to uk-sobs.org.uk.
>
> That domain has nothing to do with any charity. It's a fully built gambling affiliate site — "Non GamStop Casinos 2025," full toplist, deposit bonuses, the works. Favicon file is literally named `UK_Sobs-favicon.svg`. There's a real UK charity called SOBS (Survivors of Bereavement by Suicide) — this domain isn't it and isn't affiliated, near as I can tell (their real domains are uksobs.org / uksobs.com).
>
> Ran it through VirusTotal — 0/92, completely clean, because it's not malware and it's not stealing credentials, so none of the malware-focused engines have a reason to flag it. But the Categories section is the interesting part: Google's got it right as "gambling," but Forcepoint ThreatSeeker has it as "service and philanthropic organizations" and alphaMountain.ai has it as "Health." Also caught a `"Failed to spoof webdriver"` line in the console logs and some non-standard wp-content plugin paths, which points to a compromised WordPress site rather than something built from scratch.
>
> Not trying to make this bigger than it is — one old tool, one bad footer link, one misclassified domain. But it's a decent, concrete example of the gap between "flagged as malware" and "actually shouldn't be trusted," and a reminder that category-based filtering is only as good as its last update. Happy to share the full VirusTotal report if anyone wants to poke holes in this.

---

## Pre-publish checklist

- [ ] Screenshot: Mockerie.io footer "Staff favorites" link, scrolled to and visible in a real browser
- [ ] Screenshot: uk-sobs.org.uk homepage (gambling content, URL bar visible)
- [ ] Screenshot: VirusTotal Categories box (Google vs. Forcepoint vs. alphaMountain)
- [ ] Screenshot: VirusTotal Console Messages showing "Failed to spoof webdriver"
- [ ] Optional: the real SOBS charity's actual site for contrast
- [ ] Confirm no claim of "confirmed cloaking" appears anywhere in final copy
- [ ] Confirm no AI-recommendation claim appears unless separately tested and screenshotted
