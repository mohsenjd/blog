---
title: "Hello, world"
date: 2026-05-17
slug: hello-world
description: "A brief introduction and what to expect from this blog."
tags: ["meta"]
draft: true
---

A first post — what to expect, what I'm interested in writing about, and the general shape of things here.

This is a draft. Edit it or delete it before publishing.

## A code block, to verify highlighting

```java
@Service
public class IdempotentWebhookHandler {
    private final WebhookEventRepository repository;

    public WebhookResult handle(WebhookEvent event) {
        return repository.findById(event.id())
            .map(existing -> WebhookResult.alreadyProcessed(existing))
            .orElseGet(() -> processNew(event));
    }
}
```

A trailing paragraph so the post has more than one block of content.