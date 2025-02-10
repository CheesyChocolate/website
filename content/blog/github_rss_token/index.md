+++
title = "GitHub RSS token"
date = 2025-02-10
updated = 2025-02-10
description = "How to create and revoke a GitHub RSS token for private feeds"

[taxonomies]
tags = ["security",
        "GitHub",
        "RSS",]
+++

# Create a GitHub RSS Token

Create your GitHub RSS token by following the steps in the
[Github activity feeds API doc](https://docs.github.com/en/rest/activity/feeds?apiVersion=2022-11-28#get-feeds)
.

```
curl "https://github.com/<USER>.private.atom?token=*****************************"
```

# Revoke a GitHub RSS Token

The simplest way is to change the GitHub password. This will invalidate all the
RSS tokens. To change the password, go to the GitHub settings and click on
`Password and Authentication`. Then click on `Change password`.
