## Application Overview
This Zoho Creator app manages customer orders from sales intake through inventory, fulfillment, shipping, payment tracking, and operational reporting. It now includes an executive-dark Admin Dashboard with HTML snippets for internal oversight.

## Forms
| Form Name | Purpose | Key Lookups |
|---|---|---|
| customers | Customer/contact and billing master data | — |
| customer_priorities | Customer priority history | customers |
| items | Product/item catalog | — |
| inventory | Stock levels and reorder tracking | items, transfer_orders |
| transfer_orders | Warehouse transfer records | — |
| sales_orders | Imported/source sales order records | — |
| orders | Main order header and lifecycle | customers, sales_orders |
| order_items | Products and quantities on orders | orders, items |
| payment_records | Order payment tracking | orders |
| shipping_addresses | Order delivery addresses | orders |
| order_adjustments | Discounts/manual adjustments | orders |
| order_status_logs | Status history entries | orders |
| fulfillment_schedules | Shipment planning and carrier assignment | orders, carriers |
| carriers | Carrier/contact master data | — |

## Reports
| Report Name | Type | Source Form |
|---|---|---|
| customers_Report | list | customers |
| customer_priorities_Report | list | customer_priorities |
| customer_priorities_by_priority_level | board | customer_priorities |
| items_Report | list | items |
| inventory_Report | list | inventory |
| transfer_orders_Report | list | transfer_orders |
| sales_orders_Report | list | sales_orders |
| orders_Report | list | orders |
| orders_by_status | board | orders |
| order_items_Report | list | order_items |
| payment_records_Report | list | payment_records |
| payment_records_by_payment_method | board | payment_records |
| shipping_addresses_Report | list | shipping_addresses |
| order_adjustments_Report | list | order_adjustments |
| order_adjustments_by_adjustment_type | board | order_adjustments |
| order_status_logs_Report | list | order_status_logs |
| order_status_logs_by_status | board | order_status_logs |
| fulfillment_schedules_Report | list | fulfillment_schedules |
| fulfillment_schedules_by_status | board | fulfillment_schedules |
| carriers_Report | list | carriers |

## Pages
| Page Name | Purpose | Key Components |
|---|---|---|
| DashBoard | Existing operational dashboard | KPI panels, charts, embedded orders report |
| Admin_Dashboard | New executive admin command center | HTML hero, KPI cards, status grids, activity tables, quick links |

## Design Decisions
- Added Admin_Dashboard as a new page instead of replacing the existing dashboard.
- Built the dashboard primarily with `.dshtml` snippets for flexible executive-dark styling.
- Added the page to web navigation beside the existing Dashboard.
- Granted explicit access to custom internal profiles while excluding portal-facing profiles.