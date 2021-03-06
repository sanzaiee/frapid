# inventory.transaction_view view

| Schema | [inventory](../../schemas/inventory.md) |
| ------ | ----------------------------------------------- |
| Materialized View Name | transaction_view |
| Owner | frapid_db_user |
| Tablespace | DEFAULT |
| Description |  |

**Source:**

```plpgsql
 CREATE OR REPLACE VIEW inventory.transaction_view
 AS
 SELECT checkouts.checkout_id,
    checkouts.value_date,
    checkouts.transaction_master_id,
    checkouts.transaction_book,
    checkouts.office_id,
    checkout_details.store_id,
    checkout_details.transaction_type,
    checkout_details.item_id,
    checkout_details.price,
    checkout_details.discount,
    checkout_details.cost_of_goods_sold,
    checkout_details.tax,
    checkouts.shipper_id,
    checkout_details.shipping_charge,
    checkout_details.unit_id,
    checkout_details.quantity
   FROM inventory.checkouts
     JOIN inventory.checkout_details ON checkouts.checkout_id = checkout_details.checkout_id
     JOIN finance.transaction_master ON checkouts.transaction_master_id = transaction_master.transaction_master_id
  WHERE NOT checkouts.cancelled AND NOT checkouts.deleted AND transaction_master.verification_status_id > 0;
```


### Related Contents
* [Schema List](../../schemas.md)
* [View List](../../views.md)
* [Materialized View List](../../materialized-views.md)
* [Table of Contents](../../README.md)

