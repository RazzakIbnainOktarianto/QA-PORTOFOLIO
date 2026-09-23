# Cart Test Cases

## Coverage Summary

| Category | Coverage |
|---|---:|
| Positive | 3 |
| Negative | 0 |
| Boundary | 0 |
| Edge Case | 0 |
| Functional | 3 |
| **Total** | **3** |

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

### Expected Result:
The product is successfully added to the shopping cart with the correct product information, quantity, price, and updated cart total.

---

## TC-CART-002 — Increase Product Quantity

**Test Type:** Functional · Positive

### Description

Verify that a user can increase the quantity of an existing product in the shopping cart.

### Precondition

User has at least one product in the shopping cart.
The product has sufficient remaining stock.
The cart is accessible.

### Parameter

| Parameter |	Value |
| --- | --- |
| Product |	Wireless Headphones |
| Current Quantity | 1 |
| Remaining Stock |	9 |
| Updated Quantity	| 2 |

### Test Steps

```
Gherkins
Given the user has an available product with quantity 1 in the shopping cart
When the user increases the product quantity to 2
Then the product quantity is updated to 2
And the cart subtotal is recalculated based on the updated quantity
And the cart total reflects the updated product quantity
```

### Expected Result:
The product quantity is successfully increased to 2, and the cart subtotal and total are recalculated correctly based on the updated quantity.

---

## TC-CART-003 — Decrease Product Quantity

**Test Type:** Functional · Positive

### Description

Verify that a user can decrease the quantity of an existing product in the shopping cart.

### Precondition

- User has at least one product in the shopping cart.
- The product quantity is greater than 1.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Current Quantity | 2 |
| Updated Quantity | 1 |

### Test Steps

```gherkin
Given the user has an available product with quantity 2 in the shopping cart
When the user decreases the product quantity to 1
Then the product quantity is updated to 1
And the cart subtotal is recalculated based on the updated quantity
And the cart total reflects the updated product quantity
```

### Expected Result

The product quantity is successfully decreased to 1, and the cart subtotal and total are recalculated correctly based on the updated quantity.

---
