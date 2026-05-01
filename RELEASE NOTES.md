
# Release Notes

Based on https://t.me/wb_api_notifications

---

## Recommended Warehouse for FBS Supplies

**Date:** `2025-04-30`  
**Tags:** `#fbs`

Added the `recommendedWhId` field — recommended warehouse for supply for Moscow and Moscow region — to the responses of the methods:
* `GET /api/v3/supplies`
* `GET/api/v3/supplies/{suppliId}`

The recommended warehouse is defining automatically as the closest to the buyer, taking into account the parameters of all assembly orders in the supply. This allows you to deliver the items to the buyer faster. If the recommended warehouse is not defined, the value 0 will be returned in the recommendedWhId field.

If the recommended warehouse is located outside the seller's delivery area, there is no fine for delivering this supply to it. You can also choose a warehouse that is convenient for you, rather than from recommendations. In this case, it must still be in your delivery area, otherwise a fine will be charged.
