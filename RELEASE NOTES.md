
# Release Notes

Based on https://t.me/wb_api_notifications

---

## Recommended Warehouse for FBS Supplies

https://t.me/wb_api_notifications/399

**Date:** `2025-04-30`  
**Tags:** `#fbs`

Added the `recommendedWhId` field — recommended warehouse for supply for Moscow and Moscow region — to the responses of the methods:
* `GET /api/v3/supplies`
* `GET/api/v3/supplies/{suppliId}`

The recommended warehouse is defining automatically as the closest to the buyer, taking into account the parameters of all assembly orders in the supply. This allows you to deliver the items to the buyer faster. If the recommended warehouse is not defined, the value 0 will be returned in the recommendedWhId field.

If the recommended warehouse is located outside the seller's delivery area, there is no fine for delivering this supply to it. You can also choose a warehouse that is convenient for you, rather than from recommendations. In this case, it must still be in your delivery area, otherwise a fine will be charged.

---

## Changes in Product Management

https://t.me/wb_api_notifications/400

**Date:** `2025-05-04`  
**Tags:** `#items`

In the GET `/content/v2/object/charcs/{subjectId}` response added the `existNamedField` field for each characteristic. 
The field provides information on how to transfer the characteristic in requests for creating , creating with merge, and editing listings:
* `false` — in the characteristics array. For example, to specify the color for a mechanical coffee grinder, pass the characteristics ID ("id":14177449) and its value ("value":gray) in the characteristics array.
* `true` — as a separate parameter in the request. For example, to specify the item name, pass it in the title parameter.

Also, in the response of the GET `/content/v2/object/charcs/{subjectId}` method added new characteristics. 
These characteristics are transferred as separate parameters in requests for creating, creating with merge, and editing listings:

* Brand — request parameter brand
* Item title — request parameter title
* Item description — request parameter description
* Weight of the item with packaging — request parameter weightBrutto
* Width — request parameter width
* Height — request parameter height
* Length  — request parameter length

When working with product cards, pay attention to the combination of fields in the response of the GET `/content/v2/object/charcs/{subjectId}` method to check if the characteristic is required:
* `isVariable:true` and `required:true` — variable characteristic, required for creating  listings.
* `hasFilter:true` and `required:true` — key characteristic, required for creating listings for 10 subjects.

The `hasFilter` value for any characteristic may be changed. Therefore, before creating or editing of a listing, we recommend requesting an up-to-date list of characteristics.

---

## Changes in DBW and DBS Orders

https://t.me/wb_api_notifications/401

**Date:** `2025-05-05`  
**Tags:** `#dbw #dbs`

Added methods for working with lists of DBW assembly orders:
* Delete Assembly Orders Metadata — POST /api/v3/public/dbw/orders/meta/delete (https://dev.wildberries.ru/en/docs/openapi/orders-dbw#tag/DBW-Metadata/paths/~1api~1marketplace~1v3~1dbw~1orders~1meta~1delete/post)
* Add Labeling Codes Chestny ZNAK to Assembly Orders — POST /api/v3/public/dbw/orders/meta/sgtin (https://dev.wildberries.ru/en/docs/openapi/orders-dbw#tag/DBW-Metadata/paths/~1api~1marketplace~1v3~1dbw~1orders~1meta~1sgtin/post)
* Transfer Assembly Orders to Delivery — POST /api/v3/public/dbw/orders/status/deliver (https://dev.wildberries.ru/en/docs/openapi/orders-dbw#tag/DBW-Assembly-Orders/paths/~1api~1marketplace~1v3~1dbw~1orders~1status~1deliver/post)

Now, when transferring the assembly orders of DBW and DBS models to delivery, Chestny ZNAK labeling is validated for B2B orders.
Assembly orders with incorrectly specified labeling cannot be transferred to delivery. A validation error MetaValidationFail with code 409 will be returned in the errors array in the responses of the following methods:
* POST /api/v3/public/dbw/orders/status/deliver (https://dev.wildberries.ru/en/docs/openapi/orders-dbw#tag/DBW-Assembly-Orders/paths/~1api~1marketplace~1v3~1dbw~1orders~1status~1deliver/post)
* POST /api/marketplace/v3/dbs/orders/status/deliver (https://dev.wildberries.ru/en/docs/openapi/orders-dbs/#tag/DBS-Assembly-Orders/paths/~1api~1marketplace~1v3~1dbs~1orders~1status~1deliver/post)
The metaDetails array in the response will contain the labeling validation status for each assembly order. Before transferring assembly orders to delivery, check the metadata validation statuses in the responses of these methods:
* POST /api/marketplace/v3/dbw/orders/meta/details (https://dev.wildberries.ru/en/docs/openapi/orders-dbw/#tag/DBW-Metadata/paths/~1api~1marketplace~1v3~1dbw~1orders~1meta~1details/post)
* POST /api/marketplace/v3/dbs/orders/meta/details (https://dev.wildberries.ru/en/docs/openapi/orders-dbs/#tag/DBS-Metadata/paths/~1api~1marketplace~1v3~1dbs~1orders~1meta~1details/post)

On June 5, we will disable the outdated methods:
* PATCH /api/v3/dbw/orders/{orderId}/assemble (https://dev.wildberries.ru/en/docs/openapi/orders-dbw#tag/DBW-Assembly-Orders/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1assemble/patch)
* DELETE /api/v3/dbw/orders/{orderId}/meta (https://dev.wildberries.ru/en/docs/openapi/orders-dbw#tag/DBW-Metadata/paths/~1api~1v3~1dbw~1orders~1%7BorderId%7D~1meta/delete)
* PUT /api/v3/dbw/orders/{orderId}/meta/sgtin

---

## Changes in FBS Orders

https://t.me/wb_api_notifications/402

**Date:** `2025-05-06`  
**Tags:** `#fbs`

Now you can cancel assembly orders before handing them over to Wildberries.

To check whether an assembly order can be canceled, 
use the `POST /api/v3/orders/status` (https://dev.wildberries.ru/en/docs/openapi/orders-fbs/#tag/FBS-Assembly-Orders/paths/~1api~1v3~1orders~1status/post) method and the new field `isCancellable`.

---

## Changes in Seller Warehouses Inventory Methods

https://t.me/wb_api_notifications/403

**Date:** `2025-05-07`  
**Tags:** `#items`

Added an error example when using deprecated sku parameter to the inventory management (https://dev.wildberries.ru/en/openapi/work-with-products#tag/Inventory) methods responses:
* `POST /api/v3/stocks/{warehouseId}` (https://dev.wildberries.ru/en/openapi/work-with-products/#tag/Inventory/paths/~1api~1v3~1stocks~1%7BwarehouseId%7D/post)
* `PUT /api/v3/stocks/{warehouseId}` (https://dev.wildberries.ru/en/openapi/work-with-products/#tag/Inventory/paths/~1api~1v3~1stocks~1%7BwarehouseId%7D/put)
* `DELETE /api/v3/stocks/{warehouseId}` (https://dev.wildberries.ru/en/openapi/work-with-products/#tag/Inventory/paths/~1api~1v3~1stocks~1%7BwarehouseId%7D/delete)

Instead of the sku parameter in the method requests, you should pass (https://t.me/wb_api_notifications/318) the `chrtId` — item size ID. 
To get the `chrtId`, use the `POST /content/v2/get/cards/list` (https://dev.wildberries.ru/en/openapi/work-with-products/#tag/Product-Cards/paths/~1content~1v2~1get~1cards~1list/post) method.

From 1 pm Moscow time on May 20, it will be impossible to manage the inventory using sku parameter.

---

## Changes in Seller User Management Methods

https://t.me/wb_api_notifications/404

**Date:** `2025-05-12`  
**Tags:** `#general`

Expanded the list of personal account sections for which user access can be configured:
* brandsFlow — My brands (https://seller.wildberries.ru/create-brands)
* copyrightComplaints — Copyright Claims (https://seller.wildberries.ru/copyright-owner)
* pretrialClaims — Out-of-Court Claims (https://seller.wildberries.ru/pretrial-claims)
* sellersChat — Chat with Users (https://seller.wildberries.ru/chat-with-clients)

Specify the new sections in the method requests:
* Create an Invitation for a New User `POST /api/v1/invite` (https://dev.wildberries.ru/docs/openapi/api-information#tag/Seller-User-Management/paths/~1api~1v1~1invite/post)
* Update User's Access Permissions `PUT /api/v1/users/access` (https://dev.wildberries.ru/docs/openapi/api-information#tag/Seller-User-Management/paths/~1api~1v1~1users~1access/put)

You can get the updated sections list in the response of the `GET /api/v1/users` (https://dev.wildberries.ru/docs/openapi/api-information#tag/Seller-User-Management/paths/~1api~1v1~1users/get) method.

---

## Changes in Inventory Methods

https://t.me/wb_api_notifications/406

**Date:** `2025-05-13`  
**Tags:** `#items`

Please note, that on May 20, from 1 pm Moscow time we will start disabling inventory management via barcodes, the sku parameter. 
The disabling will be gradual, from 10 minutes per hour every day. 
The duration of the disabling can be changed without additional notification.

In requests for inventory management (https://dev.wildberries.ru/en/openapi/work-with-products#tag/Inventory) methods, 
you should transfer (https://dev.wildberries.ru/en/release-notes?id=522) only the `chrtId` — item size ID. 
To get the `chrtId`, use the `POST /content/v2/get/cards/list` (https://dev.wildberries.ru/en/openapi/work-with-products/#tag/Product-Cards/paths/~1content~1v2~1get~1cards~1list/post) method.

If you use the deprecated sku parameter, in the responses of inventory management methods, you will receive error 400 with the value "code":"SKUUploadDisabled", and the inventory will not be updated.

---

## Changes in Buyers Chat Methods

https://t.me/wb_api_notifications/407

**Date:** `2025-05-14`  
**Tags:** `#communication`

Due to technical reasons, we updated the format of the replySign field — the chat signature — in the method for getting 
chat lists `GET /api/v1/seller/chats` (https://dev.wildberries.ru/en/docs/openapi/user-communication#tag/Buyers-Chat/paths/~1api~1v1~1seller~1chats/get). 
To receive the replySign field in the new format, update the chat list using the `GET /api/v1/seller/chats` 
(https://dev.wildberries.ru/en/docs/openapi/user-communication#tag/Buyers-Chat/paths/~1api~1v1~1seller~1chats/get) method.

The replySign field should be specified in the request of the `POST /api/v1/seller/message` (https://dev.wildberries.ru/en/docs/openapi/user-communication#tag/Buyers-Chat/paths/~1api~1v1~1seller~1message/post) method in order to send a message to a chat.

Until June 4, you can specify replySign in the `POST /api/v1/seller/message` (https://dev.wildberries.ru/en/docs/openapi/user-communication#tag/Buyers-Chat/paths/~1api~1v1~1seller~1message/post) request in both the old and new formats.

After June 4, you will only be able to send a message to a chat using the new format of replySign. The old format will no longer be supported.


---

## Change in Request for the Getting Listings Method    

https://t.me/wb_api_notifications/408

**Date:** `2025-05-14`  
**Tags:** `#items`

The current schema of the `withPhoto` parameter values in the `POST /content/v2/get/cards/list` (https://dev.wildberries.ru/en/docs/openapi/work-with-products#tag/Product-Cards/paths/~1content~1v2~1get~1cards~1list/post) method requests:
* "withPhoto":0 or missing the parameter — only listings without photos
* "withPhoto":1 - only listings with photos
* "withPhoto":-1 - any listings, both without photos and with them

For technical reasons, starting from June 3 we will use the new scheme in requests:

* "withPhoto":0 or missing the parameter — any listings
* "withPhoto":1 - only listings with photos (no change)
* "withPhoto":-1 - only listings without photos
