# Cart Test Cases

## Coverage Summary

### Test Outcome

| Category | Coverage |
|---|---:|
| Positive | 11 |
| Negative | 6 |
| **Total Test Cases** | **11** |

### Testing Approach

| Category | Coverage |
|---|---:|
| Functional | 17 |
| Boundary | 2 |
| Edge Case | 3 |
| Business Rule | 3 |

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

## TC-CART-010 — Validate Cart Subtotal Calculation

**Test Type:** Functional · Positive

### Description

Verify that the cart subtotal is calculated correctly based on the product price and selected quantity.

### Precondition

- User has products in the shopping cart.
- Product prices are correctly configured.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---:|
| Product A | Wireless Headphones |
| Product A Unit Price | $50.00 |
| Product A Quantity | 2 |
| Product B | USB-C Cable |
| Product B Unit Price | $10.00 |
| Product B Quantity | 1 |
| Expected Subtotal | $110.00 |

### Test Steps

```gherkin
Given the user has multiple products with known prices and quantities in the shopping cart
When the user views the cart subtotal
Then the subtotal is calculated by multiplying each product price by its quantity
And the subtotal includes all products in the cart
And the displayed subtotal is $110.00
```

### Expected Result

The cart subtotal is calculated correctly as:

`($50.00 × 2) + ($10.00 × 1) = $110.00`

The displayed cart subtotal is **$110.00**.

---

## TC-CART-011 — Validate Cart Total Calculation

**Test Type:** Functional · Positive

### Description

Verify that the cart total is calculated correctly based on the subtotal, applicable tax, and service fee.

### Precondition

- User has products in the shopping cart.
- Product prices are correctly configured.
- The applicable tax rate is configured as 10%.
- The applicable service fee is configured as $5.00.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---:|
| Product Subtotal | $110.00 |
| Tax Rate | 10% |
| Tax Amount | $11.00 |
| Service Fee | $5.00 |
| Expected Cart Total | $126.00 |

### Test Steps

```gherkin
Given the user's cart has a subtotal of $110.00
When the user views the cart total
Then the tax is calculated as 10% of the subtotal
And the service fee of $5.00 is added to the subtotal and tax
And the displayed cart total is $126.00
```

### Expected Result

The cart total is calculated correctly as:

`$110.00 + $11.00 + $5.00 = $126.00`

The displayed cart total is **$126.00**.

---
## TC-CART-012 — Preserve Cart Data After Page Refresh

**Test Type:** Edge Case · Positive

### Description

Verify that the user's cart data remains unchanged after refreshing the cart page.

### Precondition

- User has at least one available product in the shopping cart.
- The product quantity and cart total are correctly displayed.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Quantity | 2 |
| Product Unit Price | $50.00 |
| Expected Subtotal | $100.00 |

### Test Steps

```gherkin
Given the user has a product with quantity 2 in the shopping cart
When the user refreshes the cart page
Then the product remains in the shopping cart with quantity 2
And the product price remains unchanged
And the cart subtotal remains $100.00
And the cart total remains correctly calculated
```

### Expected Result

The cart data remains unchanged after the page refresh, including the product, quantity, price, subtotal, and total.

---

## TC-CART-013 — Calculate Subtotal for Multiple Products

**Test Type:** Functional · Positive

### Description

Verify that the cart subtotal is calculated correctly when multiple products with different quantities are added to the shopping cart.

### Precondition

- User has access to the shopping cart.
- Multiple products are available for purchase.
- Product prices are correctly configured.

### Parameter

| Parameter | Value |
|---|---:|
| Product A | Wireless Headphones |
| Product A Unit Price | $50.00 |
| Product A Quantity | 2 |
| Product B | USB-C Cable |
| Product B Unit Price | $10.00 |
| Product B Quantity | 3 |
| Expected Subtotal | $130.00 |

### Test Steps

```gherkin
Given the user has multiple products with different quantities in the shopping cart
When the user views the cart subtotal
Then each product subtotal is calculated based on its unit price and quantity
And all product subtotals are combined into the cart subtotal
And the displayed cart subtotal is $130.00
```

### Expected Result

The cart subtotal is calculated correctly as:

`($50.00 × 2) + ($10.00 × 3) = $130.00`

The displayed cart subtotal is **$130.00**.

---

## TC-CART-014 — Preserve Cart After Browser Navigation

**Test Type:** Edge Case · Positive

### Description

Verify that the user's cart data remains unchanged after navigating to another page and returning to the cart.

### Precondition

- User has at least one available product in the shopping cart.
- The product quantity and cart total are correctly displayed.
- The user can navigate between pages within the application.

### Parameter

| Parameter | Value |
|---|---|
| Product | Wireless Headphones |
| Quantity | 2 |
| Product Unit Price | $50.00 |
| Expected Subtotal | $100.00 |

### Test Steps

```gherkin
Given the user has a product with quantity 2 in the shopping cart
When the user navigates to another page and then returns to the shopping cart
Then the product remains in the shopping cart with quantity 2
And the product price remains unchanged
And the cart subtotal remains $100.00
And the cart total remains correctly calculated
```

### Expected Result

The cart data remains unchanged after browser navigation, including the product, quantity, price, subtotal, and total.

---

## TC-CART-015 — Prevent Quantity from Exceeding Available Stock

**Test Type:** Business Rule · Negative

### Description

Verify that the system prevents the user from increasing the product quantity beyond the available stock.

### Precondition

- User has an available product in the shopping cart.
- The product has limited available stock.
- The maximum purchase quantity is higher than the available stock.
- The cart is accessible.

### Parameter

| Parameter | Value |
|---|---:|
| Product | Wireless Headphones |
| Available Stock | 3 |
| Maximum Purchase Quantity | 10 |
| Current Quantity | 3 |
| Attempted Quantity | 4 |

### Test Steps

```gherkin
Given the user has a product with quantity 3 in the shopping cart and only 3 units are available
When the user attempts to increase the product quantity to 4
Then the product quantity is not increased beyond the available stock
And an appropriate stock availability message is displayed
And the product quantity remains 3
And the cart total remains correctly calculated based on quantity 3
```

### Expected Result

The system prevents the user from purchasing more units than the available stock. The product quantity remains at 3, an appropriate stock availability message is displayed, and the cart total remains correctly calculated.

---

## TC-CART-016 — Handle Stock Reduction After Product Is Added to Cart

**Test Type:** Edge Case · Business Rule · Negative

### Description

Verify that the system correctly handles a product quantity in the cart when the available stock is reduced after the product has already been added to the cart.

### Precondition

- User has an available product in the shopping cart.
- The product quantity in the cart is higher than the subsequently available stock.
- The system supports real-time or refreshed stock validation before checkout.

### Parameter

| Parameter | Value |
|---|---:|
| Product | Wireless Headphones |
| Initial Cart Quantity | 5 |
| Initial Available Stock | 5 |
| Updated Available Stock | 3 |
| Expected Maximum Quantity | 3 |

### Test Steps

```gherkin
Given the user has 5 units of Wireless Headphones in the shopping cart
When the available stock is reduced from 5 units to 3 units before the user proceeds to checkout
Then the system detects that the cart quantity exceeds the available stock
And the user is informed that only 3 units are currently available
And the user cannot proceed with an invalid quantity of 5
And the cart quantity is adjusted or the user is required to update the quantity to 3
```

### Expected Result

The system detects the stock reduction and prevents the user from proceeding with a quantity that exceeds the current available stock. The user is clearly informed of the available quantity and can update the cart to a valid quantity.

---

## TC-CART-017 — Handle Adding the Same Product Multiple Times

**Test Type:** Business Rule · Functional · Positive

### Description

Verify that adding the same product to the shopping cart multiple times combines the quantity into a single cart item instead of creating duplicate cart items.

### Precondition

- User has access to the product listing or product detail page.
- The product is available for purchase.
- The product has sufficient stock.
- The shopping cart is initially empty.

### Parameter

| Parameter | Value |
|---|---:|
| Product | Wireless Headphones |
| First Quantity | 1 |
| Second Quantity | 2 |
| Expected Combined Quantity | 3 |

### Test Steps

```gherkin
Given the user adds 1 unit of Wireless Headphones to the shopping cart
When the user adds 2 additional units of the same product
Then the shopping cart contains a single Wireless Headphones item
And the product quantity is updated to 3
And no duplicate cart item is created for the same product
And the cart subtotal is recalculated based on the combined quantity
```

### Expected Result

The system combines the quantities of the same product into a single cart item. The cart displays Wireless Headphones with a quantity of 3, without creating a duplicate cart item, and the subtotal is recalculated correctly.

---
