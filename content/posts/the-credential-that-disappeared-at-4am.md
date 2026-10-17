---
title: "The credential that disappeared at 4am"
date: 2026-10-17
tags: ["incidents", "resilience"]
canonicalURL: "https://foreverdraft.substack.com/p/the-credential-that-disappeared-at"
summary: "A credential with 'no expiry' vanished, two apps went down, and the fix wasn't the interesting part."
---

Last week, a credential that had been created with “no expiry” quietly disappeared at 4:15 am.

Nobody on our side touched it. The owner’s account was fine. No admin changes. No security changes. It had been in production for almost a year.

A few days later, the vendor came back with their own RCA explanation:
> It may have been revoked automatically to protect your content.

No warning or notification that I had expected.

The immediate impact was a day-long partial outage across both on our web app and mobile app. Fixing it was easy enough: rotate the key, redeploy, move on.

What stuck with me was the lesson underneath it.

One part of our system kept working because it loaded its data from a cached content. Two other parts failed because they needed the credential live, in real time.

Both used the same credentials and had the same dependency but the outcomes were different.

The other surprise was that the login outage wasn’t really caused by the missing credential. It came down to one small assumption in our application flow. (error handling). A failed lookup didn’t mean what we thought it meant.

My biggest takeaway?

There is no such thing as a credential that doesn’t expire. There are only credentials whose expiry date you don’t know yet.

I’d be curious to hear if others have run into something similar. Have you ever had a dependency fail in a way nobody expected?
---

*First published on [Forever Draft](https://foreverdraft.substack.com/p/the-credential-that-disappeared-at), where the comments live.*