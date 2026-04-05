# Event Design

Guidelines for designing custom events that produce useful analytics. Apply these when recommending events to track, reviewing existing instrumentation, or implementing `track()` calls.

## Core Principle

Track decisions, milestones, and outcomes — not every UI interaction. Every event should help answer a product, growth, support, or reliability question.

## Naming

Use `snake_case` past-tense or verb-oriented names:

```ts
track("signup_completed");
track("checkout_started");
track("feature_used");
track("report_exported");
```

Avoid camelCase, generic names, or implementation-coupled names:

```ts
// Bad
track("signupCompleted");
track("ButtonClick");
track("clicked_button_123");
```

Prefer one event with properties over many near-duplicate events:

```ts
// Good
track("feature_used", { feature: "export", format: "csv" });

// Bad
track("csv_export_clicked");
track("xlsx_export_clicked");
```

## Property Design

Properties should help segment the event. Keep them low-cardinality.

Good properties: `plan`, `source`, `feature`, `variant`, `step`, `method`, `status`, `currency`, `revenue`, `page_type`, `environment`.

```ts
track("signup_completed", {
  method: "google",
  plan: "pro",
  source: "landing_page",
});
```

### Low Cardinality

A property is useful when it takes a bounded set of values:

```ts
// Good — filterable
plan: "free" | "pro" | "enterprise"
method: "email" | "google" | "github"
status: "success" | "error"

// Bad — millions of unique values
path: "/products/9a84f457-7f19-4bc7-a5e9-6c8c9dc4a521?coupon=SPRING25"
```

If a high-cardinality value is needed for debugging, restrict it to narrow error/backend events.

## What Not To Track

- PII: emails, full names, phone numbers, addresses, payment details, tokens
- Every generic button click with no business meaning
- Events that duplicate auto-captured page views
- Mouse hovers, scroll events, keystrokes
- Large JSON blobs, full stack traces, or request payloads on broad events

Prefer coarse summaries:

```ts
// Good
track("search_performed", { results_count: 18, category: "templates" });

// Bad — contains user-provided text
track("search_performed", { query: "john smith payroll complaint" });
```

## Starter Taxonomies

### SaaS Product

```
signup_started → signup_completed → trial_started → project_created
invite_sent → feature_used → checkout_started → purchase_completed
```

### Content / Marketing Site

```
newsletter_signup, demo_requested, cta_clicked, contact_submitted, pricing_viewed
```

### API / Backend Product

```
api_key_created, request_succeeded, request_failed, webhook_processed, integration_connected
```

### Backend Events (Node.js)

Track server-side when the server is the source of truth:

```ts
await client.track({
  name: "webhook_processed",
  properties: { provider: "stripe", status: "success", event_type: "invoice.paid" },
});

await client.track({
  name: "job_failed",
  properties: { job: "nightly_export", stage: "upload", error_type: "timeout" },
});
```

## Declarative Tracking (`trackAttributes`)

Use `data-track` attributes for a few important CTAs and entry points, not as a blanket substitute for event design. Requires `trackAttributes: true`.

```html
<button data-track="cta_clicked" data-location="hero">Get Started</button>
```

## Review Checklist

Before adding an event, verify:

1. It answers a real business or product question
2. The name is stable `snake_case` describing an action/outcome
3. Properties are low-cardinality enough to filter and segment
4. No PII or secrets in properties
5. It does not duplicate an auto-captured event
6. A smaller taxonomy could not answer the same question
