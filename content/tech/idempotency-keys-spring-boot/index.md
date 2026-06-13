---
title: "Handling Webhooks Safely: Idempotency Keys in Spring Boot"
date: 2024-05-18
slug: idempotency-keys-spring-boot
description: "Why you need idempotency when processing webhooks, and a simple way to implement it in Spring Boot."
tags: ["spring-boot", "backend", "webhooks"]
---

When integrating with external systems like Stripe or PayPal, you typically rely on webhooks to be notified of events. However, distributed systems guarantee *at-least-once* delivery, meaning your application might receive the exact same webhook event multiple times.

If your webhook handler creates a payment record or provisions a resource, processing the same event twice can lead to severe bugs—like double-charging a customer.

This is where **idempotency** comes in. An idempotent operation is one that produces the same result regardless of how many times it is executed.

### The Idempotency Key

Most reliable providers send a unique identifier with every event, often referred to as an idempotency key or simply the `event_id`. To ensure we only process an event once, we can store this ID in our database before taking action.

Here is a simplified approach using Spring Boot and Spring Data JPA.

```java
@Service
public class WebhookHandlerService {
    
    private final ProcessedEventRepository eventRepository;
    private final PaymentService paymentService;

    @Transactional
    public void handlePaymentWebhook(WebhookEvent event) {
        // 1. Check if we've already processed this event
        if (eventRepository.existsById(event.eventId())) {
            log.info("Ignoring duplicate webhook event: {}", event.eventId());
            return;
        }

        // 2. Perform the business logic
        paymentService.fulfillOrder(event.getPayload());

        // 3. Record the event as processed
        ProcessedEvent processed = new ProcessedEvent(event.eventId(), Instant.now());
        eventRepository.save(processed);
    }
}
```

By wrapping the check and the save within a `@Transactional` boundary, we guarantee that even if our service crashes midway, we won't end up in an inconsistent state. For higher concurrency, you might want to rely on a unique constraint in the database to prevent race conditions during the initial read.

Building idempotent endpoints is a fundamental pattern in resilient backend engineering, saving you from countless operational headaches.