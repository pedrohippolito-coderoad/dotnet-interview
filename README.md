# Order Summary Coding Challenge

## Overview

The goal of this challenge is to create a simple order analytics solution using C# and .NET 10. You will work with an in-memory dataset representing customers and orders and generate a summary response containing key business metrics.

## Environment Setup

1. Navigate to: [.NET Fiddle](https://dotnetfiddle.net/?utm_source=chatgpt.com)
2. Select the **.NET 10** compiler.
3. Use the provided classes and fake database as the starting point.

---

## Provided Models

```csharp
using System.Collections.Generic;
using System;

namespace CodeRoadTest
{
    public class Customer
    {
        public int Id { get; set; }
        public string Name { get; set; } = default!;
    }

    public class Order
    {
        public int Id { get; set; }
        public int CustomerId { get; set; }
        public decimal TotalAmount { get; set; }
        public DateTime CreatedAt { get; set; }
    }

    public class OrderSummaryResponse
    {
        public int TotalOrders { get; set; }
        public decimal TotalRevenue { get; set; }
        public decimal AverageOrderValue { get; set; }
        public int TotalCustomers { get; set; }
        public string? TopCustomer { get; set; }
    }

    public static class FakeDatabase
    {
        public static List<Customer> Customers = new()
        {
            new Customer { Id = 1, Name = "Pedro" },
            new Customer { Id = 2, Name = "Ana" },
            new Customer { Id = 3, Name = "Lucas" }
        };

        public static List<Order> Orders = new()
        {
            new Order { Id = 1, CustomerId = 1, TotalAmount = 100, CreatedAt = DateTime.UtcNow.AddDays(-2) },
            new Order { Id = 2, CustomerId = 1, TotalAmount = 200, CreatedAt = DateTime.UtcNow.AddDays(-1) },
            new Order { Id = 3, CustomerId = 2, TotalAmount = 300, CreatedAt = DateTime.UtcNow },
            new Order { Id = 4, CustomerId = 3, TotalAmount = 50, CreatedAt = DateTime.UtcNow }
        };
    }
}
```

---

## Challenge Requirements

Create a method that generates an `OrderSummaryResponse` object using the data available in `FakeDatabase`.

The method must calculate the following metrics:

| Property          | Description                                  |
| ----------------- | -------------------------------------------- |
| TotalOrders       | Total number of orders                       |
| TotalRevenue      | Sum of all order amounts                     |
| AverageOrderValue | Average value of all orders                  |
| TotalCustomers    | Total number of unique customers             |
| TopCustomer       | Customer with the highest total amount spent |

### Business Rules

* `TotalOrders` should count all orders.
* `TotalRevenue` should be the sum of `TotalAmount` for all orders.
* `AverageOrderValue` should be calculated using all orders.
* `TotalCustomers` should represent the number of customers in the dataset.
* `TopCustomer` should be the customer whose combined order value is the highest.
* Use LINQ whenever appropriate.
* Handle empty collections gracefully.

---

## Expected Output

The generated `OrderSummaryResponse` should produce the following result:

```json
{
  "totalOrders": 4,
  "totalRevenue": 650,
  "averageOrderValue": 162.5,
  "totalCustomers": 3,
  "topCustomer": "Pedro"
}
```

---

## Deliverable

Provide a complete, runnable solution in .NET 10 within .NET Fiddle that generates the expected `OrderSummaryResponse` from the provided data.
