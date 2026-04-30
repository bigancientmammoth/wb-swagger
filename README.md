# Wildberries OpenAPI Specifications Mirror

---

## Background

After Wildberries restricted bot access to their developer portal, any automated attempt to download API specifications started returning **HTTP 498** errors.

These specs were downloaded **manually** and published as a **static mirror** — so agents, pipelines, and tools can fetch them without hitting access walls.

---

## Usage

Fetch any spec directly from this static hosting — no authentication, no rate limits, no 498s.

```bash
# Example: download a spec
curl -O https://bigancientmammoth.github.io/wb-swagger/original/en/02-products.yaml
```

---

## Source

Original specs sourced from:
**[https://dev.wildberries.ru](https://dev.wildberries.ru)**

---

## Disclaimer

This is an **unofficial mirror**. Specs are provided as-is at the time of download and may become outdated as Wildberries updates their API. Always cross-reference with the official portal when possible.
