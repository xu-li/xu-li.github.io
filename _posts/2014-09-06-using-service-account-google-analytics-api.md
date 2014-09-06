---
layout: post
title: Using service account for google analytics api
category: code
tags: google analytics api, google service account
---

One of my clients came to me yesterday. He asked if I could use service account in the code I wrote 4 months ago.

It's a simple php class wrapping on top of [google-api-php-client](https://github.com/google/google-api-php-client), with some *clever* APIs like visualizing funnels.

As far as I could remember, I tried to use service account before, but no luck. This time, he also sent me the solution, [a link to stackoverflow](http://stackoverflow.com/questions/9863509/service-applications-and-google-analytics-api-v3-server-to-server-oauth2-authen).

And I tried, it works!

How could I not be able to find this at that time? I googled, stackoverflowed, and searched google groups. 

I should be more insistent next time, I think.
