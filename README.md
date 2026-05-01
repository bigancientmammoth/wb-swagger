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

## Files

| scope           | uri                                                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------|
| general         | https://bigancientmammoth.github.io/wb-swagger/original/en/01-general.yaml                                                          |
| produts         | https://bigancientmammoth.github.io/wb-swagger/original/en/02-products.yaml                                                         |
| orders-fbs      | https://bigancientmammoth.github.io/wb-swagger/original/en/03-orders-fbs.yaml                                                       |
| orders-dbw      | https://bigancientmammoth.github.io/wb-swagger/original/en/04-orders-dbw.yaml                                                       |
| orders-dbs      | https://bigancientmammoth.github.io/wb-swagger/original/en/05-orders-dbs.yaml                                                       |
| in-store-pickup | https://bigancientmammoth.github.io/wb-swagger/original/en/06-in-store-pickup.yaml                                                  |
| orders-fbw      | https://bigancientmammoth.github.io/wb-swagger/original/en/07-orders-fbw.yaml                                                       |
| promotion       | https://bigancientmammoth.github.io/wb-swagger/original/en/08-promotion.yaml                                                        |
| communications  | https://bigancientmammoth.github.io/wb-swagger/original/en/09-communications.yaml                                                   |
| tariffs         | https://bigancientmammoth.github.io/wb-swagger/original/en/10-tariffs.yaml                                                          |
| analytics       | https://bigancientmammoth.github.io/wb-swagger/original/en/11-analytics.yaml                                                        |
| reports         | https://bigancientmammoth.github.io/wb-swagger/original/en/12-reports.yaml                                                          |
| finances        | https://bigancientmammoth.github.io/wb-swagger/original/en/13-finances.yaml                                                                    |


---

## Disclaimer

This is an **unofficial mirror**. Specs are provided as-is at the time of download and may become outdated as Wildberries updates their API. Always cross-reference with the official portal when possible.
