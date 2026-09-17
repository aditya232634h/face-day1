# MongoDB Aggregation Project – `aggex`

## Overview

This task covers MongoDB aggregation using the `aggex` collection, which
was intended to contain 5,000 randomly generated e-commerce documents.

**Important:** Because the documents were generated randomly, the exact
numerical outputs cannot be known without running the commands against
the actual MongoDB database. The outputs below are example formats.

## 1. Count Total Documents

### Input

``` javascript
db.aggex.countDocuments()
```

### Expected output

``` text
5000
```

If the script was executed more than once, the count may be greater than
5,000.

## 2. Count Products by Category

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            totalProducts: { $sum: 1 }
        }
    }
])
```

### Example output

``` javascript
{ _id: "Books", totalProducts: 850 }
{ _id: "Electronics", totalProducts: 920 }
{ _id: "Clothing", totalProducts: 790 }
```

These values are illustrative only.

## 3. Count Products by Brand

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$brand",
            totalProducts: { $sum: 1 }
        }
    }
])
```

### Example output

``` javascript
{ _id: "Apple", totalProducts: 720 }
{ _id: "Samsung", totalProducts: 690 }
{ _id: "Dell", totalProducts: 710 }
```

## 4. Average Price by Category

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            averagePrice: { $avg: "$price" }
        }
    }
])
```

### Example output

``` javascript
{ _id: "Books", averagePrice: 47250.35 }
{ _id: "Electronics", averagePrice: 51890.72 }
```

## 5. Maximum Price in Each Category

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            maximumPrice: { $max: "$price" }
        }
    }
])
```

### Example output

``` javascript
{ _id: "Books", maximumPrice: 95499 }
{ _id: "Electronics", maximumPrice: 95320 }
```

## 6. Minimum Price in Each Category

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            minimumPrice: { $min: "$price" }
        }
    }
])
```

### Example output

``` javascript
{ _id: "Books", minimumPrice: 520 }
{ _id: "Electronics", minimumPrice: 610 }
```

## 7. Total Revenue by Category

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            totalRevenue: { $sum: "$revenue" }
        }
    }
])
```

### Example output

``` javascript
{ _id: "Books", totalRevenue: 18500000 }
{ _id: "Electronics", totalRevenue: 21450000 }
```

## 8. Sort Categories by Total Revenue

### Input

``` javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            totalRevenue: { $sum: "$revenue" }
        }
    },
    {
        $sort: {
            totalRevenue: -1
        }
    }
])
```

### Example output

``` javascript
{ _id: "Electronics", totalRevenue: 21450000 }
{ _id: "Books", totalRevenue: 18500000 }
```

`-1` means descending order. `1` means ascending order.

## 9. Find Products with Price Greater Than ₹50,000

### Input

``` javascript
db.aggex.aggregate([
    {
        $match: {
            price: { $gt: 50000 }
        }
    }
])
```

### Example output

``` javascript
{
    productId: "PROD00020",
    productName: "Apple Fiction 20",
    price: 94234,
    discountedPrice: 48059,
    category: "Books"
}
```

The command can return many matching documents.

## 10. Count Products with Price Greater Than ₹50,000

### Input

``` javascript
db.aggex.aggregate([
    {
        $match: {
            price: { $gt: 50000 }
        }
    },
    {
        $count: "expensiveProducts"
    }
])
```

### Example output

``` javascript
{ expensiveProducts: 2634 }
```

The number `2634` is only an example and is not a verified database
result.

## 11. Example Document Structure

The generated e-commerce documents contain fields such as:

``` javascript
{
    productId: "PROD00020",
    productName: "Apple Fiction 20",
    category: "Books",
    subCategory: "Fiction",
    brand: "Apple",
    price: 94234,
    discountPercentage: 49,
    discountedPrice: 48059,
    quantity: 2,
    revenue: 96118,
    rating: 3.2,
    reviewCount: 4211,
    stock: 54,
    inStock: true,
    seller: {
        name: "MegaStore",
        sellerRating: 2.3
    },
    customer: {
        customerId: "CUS0765",
        city: "Bangalore",
        state: "West Bengal",
        age: 45
    },
    payment: {
        method: "Net Banking",
        transactionId: "TXN1rcn9848dp"
    },
    orderStatus: "Cancelled",
    orderDate: ISODate("2024-03-28T18:02:00.123Z"),
    tags: ["popular", "budget"],
    specifications: {
        warranty: "2 years",
        color: "Silver",
        weight: 2.62
    },
    isFeatured: true,
    createdAt: ISODate("2026-09-16T04:33:03.804Z")
}
```

## 12. Verification Commands

### Count documents

``` javascript
db.aggex.countDocuments()
```

### Display one document

``` javascript
db.aggex.findOne()
```

### Display three documents

``` javascript
db.aggex.find().limit(3)
```

### Show available categories

``` javascript
db.aggex.distinct("category")
```

### Show available brands

``` javascript
db.aggex.distinct("brand")
```

## 13. Operators Used

| Operator | Purpose                              |
|----------|--------------------------------------|
| `$match` | Filters documents                    |
| `$group` | Groups documents                     |
| `$sum`   | Adds values or counts documents      |
| `$avg`   | Calculates an average                |
| `$max`   | Finds the maximum value              |
| `$min`   | Finds the minimum value              |
| `$sort`  | Sorts results                        |
| `$count` | Counts documents reaching that stage |

## 14. Final Summary

- **Collection:** `aggex`
- **Intended dataset size:** 5,000 documents
- **Main topic:** MongoDB Aggregation Pipeline
- **Concepts practiced:** counting, grouping, filtering, calculating
  averages, finding minimum and maximum values, calculating revenue,
  sorting, and counting filtered results.

To replace the example outputs with real outputs, run each command in
MongoDB Atlas and copy the returned values into this file.


---

# 15. Additional MongoDB Aggregation Practice

The following ten additional aggregation exercises expand the project and make the total number of aggregation exercises at least twenty.

## 15.1 Count Products That Are In Stock

### Input

```javascript
db.aggex.aggregate([
    {
        $match: {
            inStock: true
        }
    },
    {
        $count: "inStockProducts"
    }
])
```

### Example output

```javascript
{ inStockProducts: 4200 }
```

The output number is an example only.

---

## 15.2 Count Products That Are Out of Stock

### Input

```javascript
db.aggex.aggregate([
    {
        $match: {
            inStock: false
        }
    },
    {
        $count: "outOfStockProducts"
    }
])
```

### Example output

```javascript
{ outOfStockProducts: 800 }
```

---

## 15.3 Find the Average Rating by Brand

### Input

```javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$brand",
            averageRating: { $avg: "$rating" }
        }
    },
    {
        $sort: {
            averageRating: -1
        }
    }
])
```

### Example output

```javascript
{ _id: "Samsung", averageRating: 4.12 }
{ _id: "Apple", averageRating: 3.98 }
{ _id: "Dell", averageRating: 3.76 }
```

---

## 15.4 Find the Total Quantity Sold by Category

### Input

```javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            totalQuantity: { $sum: "$quantity" }
        }
    },
    {
        $sort: {
            totalQuantity: -1
        }
    }
])
```

### Example output

```javascript
{ _id: "Electronics", totalQuantity: 2650 }
{ _id: "Books", totalQuantity: 2410 }
{ _id: "Clothing", totalQuantity: 2305 }
```

---

## 15.5 Find the Highest-Rated Products

### Input

```javascript
db.aggex.aggregate([
    {
        $sort: {
            rating: -1
        }
    },
    {
        $limit: 10
    },
    {
        $project: {
            _id: 0,
            productId: 1,
            productName: 1,
            brand: 1,
            rating: 1
        }
    }
])
```

### Example output

```javascript
{
    productId: "PROD01234",
    productName: "Premium Product",
    brand: "Samsung",
    rating: 5
}
```

This returns up to ten products with the highest ratings.

---

## 15.6 Find the Ten Most Expensive Products

### Input

```javascript
db.aggex.aggregate([
    {
        $sort: {
            price: -1
        }
    },
    {
        $limit: 10
    },
    {
        $project: {
            _id: 0,
            productId: 1,
            productName: 1,
            price: 1,
            discountedPrice: 1
        }
    }
])
```

### Example output

```javascript
{
    productId: "PROD04567",
    productName: "Premium Laptop",
    price: 95499,
    discountedPrice: 72100
}
```

---

## 15.7 Calculate Average Discount by Category

### Input

```javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$category",
            averageDiscount: { $avg: "$discountPercentage" }
        }
    },
    {
        $sort: {
            averageDiscount: -1
        }
    }
])
```

### Example output

```javascript
{ _id: "Electronics", averageDiscount: 28.45 }
{ _id: "Books", averageDiscount: 25.87 }
{ _id: "Clothing", averageDiscount: 24.92 }
```

---

## 15.8 Count Orders by Order Status

### Input

```javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$orderStatus",
            totalOrders: { $sum: 1 }
        }
    },
    {
        $sort: {
            totalOrders: -1
        }
    }
])
```

### Example output

```javascript
{ _id: "Delivered", totalOrders: 1350 }
{ _id: "Pending", totalOrders: 920 }
{ _id: "Cancelled", totalOrders: 780 }
```

---

## 15.9 Calculate Total Revenue by Payment Method

### Input

```javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$payment.method",
            totalRevenue: { $sum: "$revenue" }
        }
    },
    {
        $sort: {
            totalRevenue: -1
        }
    }
])
```

### Example output

```javascript
{ _id: "UPI", totalRevenue: 25600000 }
{ _id: "Credit Card", totalRevenue: 22400000 }
{ _id: "Net Banking", totalRevenue: 19800000 }
```

---

## 15.10 Find the Average Customer Age by State

### Input

```javascript
db.aggex.aggregate([
    {
        $group: {
            _id: "$customer.state",
            averageCustomerAge: { $avg: "$customer.age" }
        }
    },
    {
        $sort: {
            averageCustomerAge: 1
        }
    }
])
```

### Example output

```javascript
{ _id: "Rajasthan", averageCustomerAge: 29.84 }
{ _id: "Maharashtra", averageCustomerAge: 31.26 }
{ _id: "West Bengal", averageCustomerAge: 32.15 }
```

---

## 16. Additional Operators Introduced

| Operator | Purpose |
|---|---|
| `$limit` | Limits the number of documents returned |
| `$project` | Selects or hides fields in the output |
| `$sort` | Sorts documents in ascending or descending order |
| `$match` | Filters documents before further processing |

## 17. Updated Project Summary

- **Collection:** `aggex`
- **Intended dataset size:** 5,000 documents
- **Original aggregation exercises:** 10
- **Additional aggregation exercises:** 10
- **Total aggregation exercises:** 20
- **Main topic:** MongoDB Aggregation Pipeline

**Reminder:** All numerical outputs in this document are examples. Run the commands in MongoDB Atlas to obtain the actual results from your randomly generated data.
