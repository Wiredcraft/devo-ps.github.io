---
collection: blog
title: Announcing dopy with Digital Ocean API v2 support
tags:
  - dopy

author: vincent
hn:
date: 2014-10-11

template: post.html
---

A few month back Digital Ocean announced the beta support of [its API v2](https://www.digitalocean.com/company/blog/api-v2-enters-public-beta/).

Not many tools or library [supports it](https://www.digitalocean.com/community/questions/what-libraries-and-wrappers-are-there-for-digitalocean-s-apiv2), but thanks to [Igor A. Borisov](https://github.com/fizban79) pull request, [dopy](https://github.com/devo-ps/dopy) now supports version 2 of the API!

![Good news everyone!](/images/posts/good-news-everyone.jpg)

You can proceed to the install via regular `pip install dopy`. The new version of dopy (v0.3.0) is compatible with former implementations and if you still uses Digital Ocean API v1 no changes are required.

Looking forward to future integration of the V2 in other similar libraries, like [libcloud](https://libcloud.apache.org), or projects that rely on dopy like Ansible and its digital ocean support.

In the mean time I updated a personal project to perform simple cleanup of your test instances, and autoremove droplets older than x hours. Have a look at [digitalocean_cleaner](https://github.com/zbal/digitalocean_cleaner) - nothing fancy, just a conveniency tool to avoid forgetting your test droplets and stop being charged.

Now preparing the support for V2 in [devo.ps](http://devo.ps), most likely released in the near future. Stay tuned!