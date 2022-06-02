---
layout: post
title:  "Removing IP restrictions from Cloudflare API Tokens"
date:   2022-06-02 21:23:11 +0000
categories: jekyll update
---
[Cloudflare API Tokens][cloudflare-api-tokens] offer IP address conditions, which can be used to restrict the locations that a particular API token can be used from. These are able to be _set_ within the UI, however if you need to _remove_ the condition entirely, this cannot be done from the UI as you cannot remove the "is in"/"is not in" filter.

The only way this can be done is via the API with a tool like cURL, and some other tools such as `jq`...

So first, set up your environment by making sure you have a valid Cloudflare credential with the right permissions. I got lazy and used the API **Key** (which is different from an API **token**) and crafted my cURL commands accordingly:

```sh
g-a-c@shell:~> read -s CF_KEY
# paste in the key and press Enter
```

This means that I need to pass some specific HTTP headers with my request (`X-Auth-Key` and `X-Auth-Email`) instead of the generic `Authorization` header. So first I need to get a list of current API Tokens on my account. This returns JSON data so `jq` can be used to prettify the output and get only the ID and name of each token:

```sh
g-a-c@shell:~> curl -sX GET "https://api.cloudflare.com/client/v4/user/tokens" -H "X-Auth-Key: ${CF_TOKEN}" -H "X-Auth-Email: cloudflare@example.com" | \
  jq -r '.result[] | {"id": .id, "name": .name}'
```

This will return a JSON document with a `results` key, containing an array of current API Tokens. From this, you'll know the ID of the API Token you want to change; this ID is used in the next set of calls.

The next thing to do is to retrieve that single key in isolation so that we can grab its _current_ state and use `jq` to manipulate it before updating the key in place. This will remove the contents of the `condition` key in the JSON document, but retain the key itself as empty. Then the resulting JSON document is `PUT`ed back to Cloudflare to replace the original JSON document describing the API token. I've split this onto multiple lines for human readability on this page, not necessarily the correct format for pasting into your shell...

```sh
g-a-c@shell:~> curl -X GET "https://api.cloudflare.com/client/v4/user/tokens/<ID>" -H "X-Auth-Key: ${CF_TOKEN}" -H "X-Auth-Email: cloudflare@example.com" | \
  jq '.result | del(.condition."request.ip")' | \
  curl -X PUT "https://api.cloudflare.com/client/v4/user/tokens/<ID>" -H "X-Auth-Key: ${CF_TOKEN}" -H "X-Auth-Email: cloudflare@example.com" -H "Content-Type: application/json" --data-binary @- | \
  jq
```

[cloudflare-api-tokens]: https://dash.cloudflare.com/profile/api-tokens
