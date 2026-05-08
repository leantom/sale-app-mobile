# Database Table Meanings

## Core Tables

| Table | Meaning |
|---|---|
| `USERS` | Stores user account information. A user can be a store owner, manager, cashier, or staff member. |
| `STORES` | Represents one business/store. This is the main tenant entity of the system. |
| `STORE_MEMBERS` | Connects users to stores and defines their role inside each store. |
| `BRANCHES` | Represents physical store branches or locations. |
| `CATEGORIES` | Groups products into categories such as drinks, food, fashion, electronics, etc. |

---

# Product & Inventory Tables

| Table | Meaning |
|---|---|
| `PRODUCTS` | Stores general product information such as name, SKU, barcode, image, unit, and description. |
| `PRODUCT_VARIANTS` | Stores product options such as size, color, weight, or packaging. Example: Size M, Size L, 500ml, 1kg. |
| `INVENTORY_STOCKS` | Stores the current stock quantity of each product variant in each branch. |
| `INVENTORY_TRANSACTIONS` | Acts as the stock movement ledger. Every sale, return, purchase, transfer, adjustment, or disposal creates one transaction record. |

---

# Customer & Supplier Tables

| Table | Meaning |
|---|---|
| `CUSTOMERS` | Stores customer information such as name, phone, address, and notes. |
| `SUPPLIERS` | Stores supplier/vendor information for purchasing stock. |

---

# Sales Tables

| Table | Meaning |
|---|---|
| `ORDERS` | Stores draft or pending sales before they become invoices. Useful for reservations, online orders, or unfinished carts. |
| `ORDER_ITEMS` | Stores the list of products inside an order. |
| `INVOICES` | Stores completed sales records. An invoice is created when a sale is confirmed. No payment gateway is involved. |
| `INVOICE_ITEMS` | Stores the list of products sold in an invoice. |

---

# Return Tables

| Table | Meaning |
|---|---|
| `RETURNS` | Stores sales return records linked to an invoice. |
| `RETURN_ITEMS` | Stores products returned by the customer. Returning items can increase stock again. |

---

# Purchasing Tables

| Table | Meaning |
|---|---|
| `PURCHASE_ORDERS` | Stores stock purchase records from suppliers. |
| `PURCHASE_ORDER_ITEMS` | Stores products included in each purchase order. When confirmed, stock increases. |

---

# Stock Operation Tables

| Table | Meaning |
|---|---|
| `STOCK_TRANSFERS` | Stores stock transfer records between branches. |
| `STOCK_TRANSFER_ITEMS` | Stores products transferred from one branch to another. |
| `STOCK_CHECKS` | Stores stock checking sessions. Used when staff compare system stock with real physical stock. |
| `STOCK_CHECK_ITEMS` | Stores each checked product and the difference between system stock and actual stock. |
| `STOCK_DISPOSALS` | Stores damaged, expired, lost, or discarded stock records. |
| `STOCK_DISPOSAL_ITEMS` | Stores products removed from inventory due to disposal. |

---

# Export Table

| Table | Meaning |
|---|---|
| `EXPORT_FILES` | Stores exported file records such as Excel reports, PDF invoices, inventory reports, or backup files. |

---

# Most Important MVP Tables

```txt
USERS
STORES
STORE_MEMBERS
BRANCHES
PRODUCTS
PRODUCT_VARIANTS
INVENTORY_STOCKS
INVENTORY_TRANSACTIONS
INVOICES
INVOICE_ITEMS
EXPORT_FILES
```