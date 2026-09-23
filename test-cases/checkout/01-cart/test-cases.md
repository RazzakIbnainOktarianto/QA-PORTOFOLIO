# Cart Test Cases

## Coverage Summary

| Category | Coverage |
|---|---:|
| Positive | 1 |
| Negative | 0 |
| Boundary | 0 |
| Edge Case | 0 |
| Functional | 1 |
| **Total** | **1** |

---

## TC-CART-001 — Add Product to Cart

**Test Type:** Functional · Positive

### Description

Verify that a user can successfully add an available product to the shopping cart.

### Precondition

- User is on the product listing or product detail page.
- The selected product is available for purchase.
- The product has sufficient stock.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Available Stock | 10 |
| Quantity | 1 |

### Test Steps

```
gherkin
Given the user is viewing an available product with sufficient stock
When the user clicks the "Add to Cart" button
Then the product is added to the shopping cart with quantity 1
And the cart displays the correct product name, price, and quantity
And the cart total is updated according to the added product
```

Expected Result:
The product is successfully added to the shopping cart with the correct product information, quantity, price, and updated cart total.

---
