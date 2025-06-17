# Quantity/Area Calculator: Code Reference & Refactor Plan

## **Feature Overview**

This calculator section allows customers to enter either the total square footage (SQ. FT) or the number of boxes for a product. The calculator automatically converts between these two values based on the box size (e.g., if 1 box = 10 sq. ft., entering 10 boxes will show 100 sq. ft., and vice versa). It also displays the total price, but this will be removed when integrating with the overage calculator.

---

## **Where the Code Lives**

### **Main File**
- **`snippets/product-template.liquid`**
  - **Lines 197–488:** Contains the main HTML, CSS, and JavaScript for the calculator section.
  - **Calculator HTML:** Starts at line ~488 (`<div class="calculator_container">`).
  - **Calculator CSS:** Starts at line ~197 and is repeated in `assets/theme.css`.
  - **Calculator JavaScript:** Logic for conversion and updates is in the main product JS (see below).
  - **Conditional Rendering:** The calculator is rendered if `{% if product.tags contains 'Tile_calculator' %}`.

### **Supporting CSS**
- **`assets/theme.css`**
  - **Lines 5481+:** Styles for `.input_boxes`, `.calculator_container`, `.product_page_total`, etc.

### **Other Possibly Related Files**
- **`snippets/product_details_calculator_main.liquid`**
  - Contains similar logic for product details, not directly related to the main product page calculator.

---

## **Key Selectors & Structure**

### **Calculator Container**
- `.calculator_container` (main wrapper)
- `.calc_title` (title: "Quantity How much do I need?")
- `.calculator_wrapper` (flex container for inputs)

### **Input Boxes**
- `.input_boxes` (generic class for input wrappers)
- `#squared_size` (input for square feet)
- `#quantity_look_alike` (input for box quantity)
- `.container_titles` (labels: "SQ. FT", "Boxes")

### **Total Price (to be removed)**
- `#product_page_total` (span showing total price)
- `.product_page_total` (class for styling)

---

## **JavaScript Logic**

- **Conversion Functions:**
  - When the user changes `#squared_size`, the number of boxes is recalculated and updated in `#quantity_look_alike`.
  - When the user changes `#quantity_look_alike`, the square footage is recalculated and updated in `#squared_size`.
  - The conversion uses the box size (`box_area_clean`), which is set from product metafields.
- **Event Listeners:**
  - `#squared_size` → triggers `calculateFromSquaredSize()`
  - `#quantity_look_alike` → triggers `calculateFromQuantity()`
- **Total Price Calculation:**
  - The total price is updated in `#product_page_total` based on the number of boxes and product price.

---

## **CSS (Inlined and in theme.css)**
- **Lines 197–488 in `product-template.liquid`**
  - Styles for `.calculator_container`, `.input_boxes`, `.product_page_total`, etc.
- **Lines 5481+ in `assets/theme.css`**
  - Additional styles for `.input_boxes`, `.box_price`, `.square_price`, `.product_page_total`, etc.

---

## **How It Works (Current Flow)**

1. **Rendered for products with `Tile_calculator` tag.**
2. **User enters value in either SQ. FT or Boxes:** The other value is auto-updated.
3. **Total price is calculated and displayed.**

---

## **What Needs to Change (Refactor Plan)**

### **Goal**
- When integrating with the overage calculator, remove the total price box from this section and leave only the square foot and box quantity entry boxes.

### **Steps**
1. **Remove the total price display:** Delete or comment out the `#product_page_total` span and its label from the calculator HTML.
2. **Update CSS if needed:** Remove or adjust styles related to `.product_page_total`.
3. **Ensure conversion logic remains:** The conversion between SQ. FT and Boxes should still work as before.
4. **Test:** Ensure correct behavior for products with and without the tag, and after integration with the overage calculator.

---

## **Line References for Key Elements**

- **Calculator HTML:** `snippets/product-template.liquid` lines 488–560
- **Calculator CSS:** `snippets/product-template.liquid` lines 197–488, `assets/theme.css` lines 5481+
- **Calculator JS:** `snippets/product-template.liquid` lines 1556+ (event listeners and conversion logic)

---

## **Summary Table**

| Selector/ID/Class         | Type      | File/Line(s)                        | Description/Role                                 |
|--------------------------|-----------|-------------------------------------|--------------------------------------------------|
| `.calculator_container`   | Div       | product-template.liquid 488+        | Main calculator wrapper                          |
| `#squared_size`          | Input     | product-template.liquid 494+        | Square foot entry                                |
| `#quantity_look_alike`   | Input     | product-template.liquid 502+        | Box quantity entry                               |
| `.container_titles`      | Label     | product-template.liquid 496+, 510+  | Labels for SQ. FT and Boxes                      |
| `#product_page_total`    | Span      | product-template.liquid 518+        | Total price display (to be removed)              |
| `.product_page_total`    | Class     | theme.css 5510+                     | Styling for total price                          |

---

## **Other Notes**

- **No separate JS/CSS files** for the calculator; all logic and styles are inlined in the Liquid file or in `theme.css`.
- **Similar calculators** exist in other snippets, but this is the main product page version.

---

**This README provides a full map of the quantity/area calculator code, selectors, and logic, and outlines the plan for removing the total price box when integrating with the overage calculator.** 