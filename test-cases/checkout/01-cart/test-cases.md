# Cart Test Cases

## Coverage Summary

| Category | Coverage |
|---|---:|
| Positive | 5 |
| Negative | 2 |
| Boundary | 2 |
| Edge Case | 0 |
| Functional | 9 |
| **Total** | **9** |

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

```gherkin
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

```gherkin
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

## TC-CART-004 — Remove Product from Cart

**Test Type:** Functional · Positive

### Description

Verify that a user can successfully remove a product from the shopping cart.

### Precondition

- User has at least one product in the shopping cart.
- The cart contains the product selected for removal.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Current Quantity | 1 |
| Cart Item Count | 1 |

### Test Steps

```gherkin
Given the user has a product in the shopping cart
When the user clicks the "Remove" button for the product
Then the product is removed from the shopping cart
And the removed product is no longer displayed in the cart
And the cart subtotal is recalculated
And the cart total is updated accordingly
```

### Expected Result

The selected product is successfully removed from the shopping cart, and the cart subtotal and total are recalculated correctly based on the remaining cart items.

---

## TC-CART-005 — Display Empty Cart State

**Test Type:** Functional · Positive

### Description

Verify that the cart displays the correct empty state when all products have been removed.

### Precondition

- User has at least one product in the shopping cart.
- The cart contains only one product.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Current Quantity | 1 |
| Expected Cart Items | 0 |
| Expected Cart Total | $0.00 |

### Test Steps

```gherkin
Given the user has one product in the shopping cart
When the user removes the product from the cart
Then the cart displays the empty state
And no product items are displayed in the cart
And the cart total is updated to $0.00
And the user is shown an option to continue shopping
```

### Expected Result

The cart successfully displays the empty state with no remaining products, the cart total is $0.00, and the user can continue shopping.

---

## TC-CART-006 — Prevent Adding Out-of-Stock Product

**Test Type:** Functional · Negative

### Description

Verify that a user cannot add an out-of-stock product to the shopping cart.

### Precondition

- User is on the product listing or product detail page.
- The selected product is currently out of stock.
- The product cannot be purchased.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Available Stock | 0 |
| Requested Quantity | 1 |

### Test Steps

```gherkin
Given the user is viewing a product that is out of stock
When the user attempts to add the product to the shopping cart
Then the product is not added to the shopping cart
And an appropriate out-of-stock message is displayed
And the cart contents remain unchanged
```

### Expected Result

The out-of-stock product cannot be added to the shopping cart, an appropriate message is displayed, and the existing cart contents remain unchanged.

---

## TC-CART-007 — Prevent Invalid Product Quantity

**Test Type:** Functional · Negative

### Description

Verify that the user cannot set an invalid quantity for a product in the shopping cart.

### Precondition

- User has an available product in the shopping cart.
- The product has sufficient stock.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Current Quantity | 1 |
| Invalid Quantity | 0, -1 |

### Test Steps

```gherkin
Given the user has an available product with quantity 1 in the shopping cart
When the user attempts to set the product quantity to an invalid value such as 0 or -1
Then the product quantity is not updated to the invalid value
And the cart displays an appropriate validation message or maintains the minimum allowed quantity
And the cart total remains correctly calculated
```

### Expected Result

The system prevents the user from setting an invalid product quantity and maintains a valid cart state with the correct cart total.

---
## TC-CART-008 — Validate Maximum Product Quantity

**Test Type:** Boundary · Negative

### Description

Verify that the system prevents the user from exceeding the maximum allowed purchase quantity for a product.

### Precondition

- User has an available product in the shopping cart.
- The product has sufficient stock.
- The maximum purchase quantity for the product is 10 units.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Maximum Allowed Quantity | 10 |
| Current Quantity | 10 |
| Attempted Quantity | 11 |

### Test Steps

```gherkin
Given the user has a product in the shopping cart with quantity 10
When the user attempts to increase the quantity to 11
Then the product quantity is not increased beyond the maximum allowed quantity of 10
And an appropriate maximum quantity validation message is displayed
And the cart total remains correctly calculated based on quantity 10
```

### Expected Result

The system prevents the product quantity from exceeding the maximum allowed quantity of 10 units, displays an appropriate validation message, and maintains the correct cart total.

---

## TC-CART-009 — Validate Minimum Product Quantity

**Test Type:** Boundary · Negative

### Description

Verify that the system prevents the product quantity from being set below the minimum allowed quantity.

### Precondition

- User has an available product in the shopping cart.
- The product quantity is currently 1.
- The cart is accessible.
- The minimum allowed product quantity is 1.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Minimum Allowed Quantity | 1 |
| Current Quantity | 1 |
| Attempted Quantity | 0 |

### Test Steps

```gherkin
Given the user has a product in the shopping cart with quantity 1
When the user attempts to decrease the quantity to 0
Then the product quantity is not reduced below the minimum allowed quantity
And the system prevents the cart from containing an invalid quantity
And the cart total remains correctly calculated
```

### Expected Result

The system prevents the product quantity from being reduced below 1 and maintains a valid cart state with the correct cart total.

---
