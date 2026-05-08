erDiagram
    USERS {
        string userId PK
        string fullName
        string email
        string phone
        string avatarUrl
        string status
        timestamp createdAt
        timestamp updatedAt
    }

    STORES {
        string storeId PK
        string ownerId FK
        string name
        string logoUrl
        string businessType
        string status
        timestamp createdAt
        timestamp updatedAt
    }

    STORE_MEMBERS {
        string memberId PK
        string storeId FK
        string userId FK
        string role
        string status
        timestamp joinedAt
    }

    BRANCHES {
        string branchId PK
        string storeId FK
        string name
        string address
        string phone
        boolean isMain
        string status
        timestamp createdAt
    }

    CATEGORIES {
        string categoryId PK
        string storeId FK
        string name
        string parentId
        number sortOrder
        string status
    }

    PRODUCTS {
        string productId PK
        string storeId FK
        string categoryId FK
        string name
        string sku
        string barcode
        string unit
        string imageUrl
        string description
        string status
        timestamp createdAt
        timestamp updatedAt
    }

    PRODUCT_VARIANTS {
        string variantId PK
        string storeId FK
        string productId FK
        string name
        string sku
        string barcode
        number salePrice
        number costPrice
        string status
        timestamp createdAt
    }

    INVENTORY_STOCKS {
        string stockId PK
        string storeId FK
        string branchId FK
        string productId FK
        string variantId FK
        number currentStock
        number lowStockThreshold
        timestamp updatedAt
    }

    CUSTOMERS {
        string customerId PK
        string storeId FK
        string fullName
        string phone
        string email
        string address
        string note
        string status
        timestamp createdAt
    }

    SUPPLIERS {
        string supplierId PK
        string storeId FK
        string name
        string phone
        string email
        string address
        string note
        string status
        timestamp createdAt
    }

    ORDERS {
        string orderId PK
        string storeId FK
        string branchId FK
        string customerId FK
        string orderCode
        string status
        number totalAmount
        number discountAmount
        number finalAmount
        string createdBy FK
        timestamp createdAt
    }

    ORDER_ITEMS {
        string itemId PK
        string orderId FK
        string productId FK
        string variantId FK
        string productName
        string variantName
        number quantity
        number unitPrice
        number discountAmount
        number totalAmount
    }

    INVOICES {
        string invoiceId PK
        string storeId FK
        string branchId FK
        string customerId FK
        string orderId FK
        string invoiceCode
        string status
        number totalAmount
        number discountAmount
        number finalAmount
        string createdBy FK
        timestamp createdAt
    }

    INVOICE_ITEMS {
        string itemId PK
        string invoiceId FK
        string productId FK
        string variantId FK
        string productName
        string variantName
        number quantity
        number unitPrice
        number discountAmount
        number totalAmount
    }

    RETURNS {
        string returnId PK
        string storeId FK
        string branchId FK
        string invoiceId FK
        string returnCode
        string reason
        string status
        number totalAmount
        string createdBy FK
        timestamp createdAt
    }

    RETURN_ITEMS {
        string itemId PK
        string returnId FK
        string productId FK
        string variantId FK
        number quantity
        number unitPrice
        number totalAmount
    }

    PURCHASE_ORDERS {
        string purchaseOrderId PK
        string storeId FK
        string branchId FK
        string supplierId FK
        string purchaseCode
        string status
        number totalAmount
        string createdBy FK
        timestamp createdAt
    }

    PURCHASE_ORDER_ITEMS {
        string itemId PK
        string purchaseOrderId FK
        string productId FK
        string variantId FK
        number quantity
        number costPrice
        number totalAmount
    }

    STOCK_TRANSFERS {
        string transferId PK
        string storeId FK
        string fromBranchId FK
        string toBranchId FK
        string transferCode
        string status
        string createdBy FK
        timestamp createdAt
    }

    STOCK_TRANSFER_ITEMS {
        string itemId PK
        string transferId FK
        string productId FK
        string variantId FK
        number quantity
    }

    STOCK_CHECKS {
        string stockCheckId PK
        string storeId FK
        string branchId FK
        string checkCode
        string status
        string createdBy FK
        timestamp createdAt
    }

    STOCK_CHECK_ITEMS {
        string itemId PK
        string stockCheckId FK
        string productId FK
        string variantId FK
        number systemStock
        number actualStock
        number difference
    }

    STOCK_DISPOSALS {
        string disposalId PK
        string storeId FK
        string branchId FK
        string disposalCode
        string reason
        string status
        string createdBy FK
        timestamp createdAt
    }

    STOCK_DISPOSAL_ITEMS {
        string itemId PK
        string disposalId FK
        string productId FK
        string variantId FK
        number quantity
        string reason
    }

    INVENTORY_TRANSACTIONS {
        string transactionId PK
        string storeId FK
        string branchId FK
        string productId FK
        string variantId FK
        string type
        string refType
        string refId
        number quantity
        number beforeStock
        number afterStock
        string createdBy FK
        timestamp createdAt
    }

    EXPORT_FILES {
        string exportFileId PK
        string storeId FK
        string fileName
        string fileType
        string fileUrl
        string module
        string status
        string createdBy FK
        timestamp createdAt
    }

    USERS ||--o{ STORES : owns
    USERS ||--o{ STORE_MEMBERS : joins
    STORES ||--o{ STORE_MEMBERS : has
    STORES ||--o{ BRANCHES : has
    STORES ||--o{ CATEGORIES : has
    STORES ||--o{ PRODUCTS : has
    PRODUCTS ||--o{ PRODUCT_VARIANTS : has
    BRANCHES ||--o{ INVENTORY_STOCKS : stores
    PRODUCT_VARIANTS ||--o{ INVENTORY_STOCKS : tracked_by
    STORES ||--o{ CUSTOMERS : has
    STORES ||--o{ SUPPLIERS : has
    STORES ||--o{ ORDERS : has
    ORDERS ||--o{ ORDER_ITEMS : contains
    STORES ||--o{ INVOICES : has
    INVOICES ||--o{ INVOICE_ITEMS : contains
    INVOICES ||--o{ RETURNS : may_have
    RETURNS ||--o{ RETURN_ITEMS : contains
    SUPPLIERS ||--o{ PURCHASE_ORDERS : supplies
    PURCHASE_ORDERS ||--o{ PURCHASE_ORDER_ITEMS : contains
    STOCK_TRANSFERS ||--o{ STOCK_TRANSFER_ITEMS : contains
    STOCK_CHECKS ||--o{ STOCK_CHECK_ITEMS : contains
    STOCK_DISPOSALS ||--o{ STOCK_DISPOSAL_ITEMS : contains
    STORES ||--o{ INVENTORY_TRANSACTIONS : logs
    STORES ||--o{ EXPORT_FILES : generates