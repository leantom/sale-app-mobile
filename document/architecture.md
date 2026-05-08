# Database Design
The system uses Firestore as the primary database and is structured using a multi-tenant architecture based on stores.
## Main Collections
```txt
users/{userId}
stores/{storeId}
stores/{storeId}/branches/{branchId}
stores/{storeId}/staffs/{staffId}
stores/{storeId}/products/{productId}
stores/{storeId}/products/{productId}/variants/{variantId}
stores/{storeId}/customers/{customerId}
stores/{storeId}/suppliers/{supplierId}
stores/{storeId}/orders/{orderId}
stores/{storeId}/invoices/{invoiceId}
stores/{storeId}/returns/{returnId}
stores/{storeId}/purchaseOrders/{purchaseOrderId}
stores/{storeId}/stockTransfers/{transferId}
stores/{storeId}/stockChecks/{stockCheckId}
stores/{storeId}/stockDisposals/{disposalId}
stores/{storeId}/inventoryTransactions/{transactionId}
stores/{storeId}/cashbook/{cashTransactionId}

Core Logic

Products

Products contain basic information such as:

* Product name
* SKU
* Barcode
* Selling price
* Cost price
* Product image
* Status

Variants are used for size, color, weight, or packaging differences.

⸻

Orders

Orders are used for:

* Pending sales
* Online orders
* Draft orders
* Reservation orders

⸻

Invoices

Invoices represent completed sales transactions.

They include:

* Payment method
* Paid amount
* Debt amount
* Discount
* Final amount
* Customer information

⸻

Inventory Transactions

Inventory transactions act as the stock ledger system.

Every stock movement must generate a transaction record.

Supported transaction types:

sale
return_sale
purchase
return_purchase
transfer_in
transfer_out
stock_check_adjust
disposal

⸻

Cashbook

Cashbook records all money flow activities:

* Sales income
* Purchase expenses
* Refunds
* Debt collection
* Manual adjustments

⸻

Important Rule

All sensitive business operations must be processed through Cloud Run APIs.

The client app should not directly update:

* Stock quantity
* Invoice totals
* Inventory transactions
* Cashbook records

This helps ensure consistency and prevents invalid inventory updates.

---
````markdown
# General Architecture
The application uses a client-server architecture with Cloud Run as the backend service and Firestore as the primary database.
## Architecture Diagram
```mermaid
flowchart TD
    A[Mobile App / Web App] --> B[Firebase Auth]
    A --> C[Cloud Run API]
    C --> D[Firestore Database]
    C --> E[Cloud Storage]
    C --> F[Cloud Tasks / PubSub]
    F --> G[Cloud Run Worker]
    G --> D
    C --> H[BigQuery / Looker Studio]

Components

Mobile App / Web App

Used by store owners and staff to:

* Manage products
* Create invoices
* Handle inventory
* Manage customers
* Track reports
* Manage cashbook

⸻

Firebase Auth

Handles:

* User authentication
* Login sessions
* Role-based access control

⸻

Cloud Run API

Handles all business logic:

* Sales processing
* Invoice creation
* Inventory updates
* Purchase orders
* Returns
* Stock checks
* Cashbook transactions

Cloud Run acts as the secure backend layer between clients and Firestore.

⸻

Firestore Database

Stores operational data such as:

* Stores
* Products
* Orders
* Invoices
* Inventory transactions
* Customers
* Suppliers
* Cashbook records

⸻

Cloud Storage

Used to store exported files such as:

* Excel reports
* PDF invoices
* Sales reports
* Inventory exports
* Backup files

⸻

Cloud Tasks / PubSub

Handles asynchronous processing:

* Report generation
* Notification jobs
* Inventory recalculation
* Scheduled background tasks

⸻

Cloud Run Worker

Processes background jobs received from Cloud Tasks or PubSub.

⸻

BigQuery / Looker Studio

Optional analytics layer for:

* Dashboard reporting
* Revenue analysis
* Inventory analytics
* Business intelligence

⸻

Payment Handling

No external payment gateway is required.

The system only records internal payment methods:

cash
bank_transfer
debt
mixed