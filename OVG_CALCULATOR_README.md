# Overage Calculator Pop-up: Code Reference & Refactor Plan

## **Feature Overview**

The "Overage Calculator" is a UI component for certain products (tagged with `overage-popup-v3`) that helps customers calculate the total quantity of product to order, including extra for waste, cuts, and repairs. It currently appears as a modal pop-up, triggered by the Add to Cart button, and includes options for overage percentage, manual input, and displays calculation results.

---

## **Where the Code Lives**

### **Main File**
- **`snippets/product-template.liquid`**
  - **Lines 600–1800+**: Contains the main HTML, CSS, and JavaScript for the calculator and pop-up.
  - **Pop-up HTML:** Starts at line ~1259 (`<div id="ovg-popup">`).
  - **Pop-up CSS:** Starts at line ~820 and is repeated for mobile at ~1157.
  - **Pop-up JavaScript:** Starts at line ~1450 and continues through ~2299.
  - **Conditional Rendering:** The pop-up is only rendered if `{% if product.tags contains "overage-popup-v3" %}`.

### **Supporting CSS**
- **`assets/theme.css`**
  - **Lines 5509, 5528:** Styles for `#overage` (legacy calculator, not the pop-up).
  - **Pop-up styles are inlined in `product-template.liquid`** (see above).

### **Other Possibly Related Files**
- **`snippets/product_details_calculator_popup.liquid`**
  - Contains a different calculator for product details, not directly related to the overage pop-up, but uses similar logic for area/quantity calculation.

---

## **Key Selectors & Structure**

### **Pop-up Container**
- `#ovg-popup` (modal overlay, currently `display: none` unless open)
- `#ovg-popup-content` (main content box)
- `#ovg-popup-close` (close button, top right)

### **Header**
- `.ovg-header` (blue header bar)
- `.heading` (title: "Overage Calculator")
- `.section-intro` (subtitle: "Add overage for cuts, waste, breaks, and repairs")

### **Input Section**
- `.ovg-input-section`
  - `#ovg-calculator-footage` (input for square feet)
  - `.input-label` ("Square Feet")

### **Overage Selection**
- `.ovg-overage-section`
  - `#ovg-overage`
    - `#ovg-overage-selectors` (radio buttons for 10%, 15%, manual, no overage)
      - `input[name="properties[OVERAGE]"]`
      - `#ovg-manualInputRadio` (manual input radio)
      - `#ovg-manual-input-wrapper` (manual % input, shown if manual selected)
  - `.ovg-info-section` (info text for each overage option)

### **Results Section**
- `.ovg-results`
  - `.ovg-results-title` ("Calculation Results")
  - `.ovg-result-row` (each result: Overage, Total, Boxes Needed, Total Price)
    - `#ovg-overage-display`
    - `#ovg-total-display`
    - `#ovg-boxes-display`
    - `#ovg-price-display`

### **Add to Cart**
- `#ovg-addToquanitity` (button: "Add To Cart")

---

## **JavaScript Logic**

- **Auto-calculation:** Listens for changes in overage selection, manual input, and square footage to auto-calculate results.
- **Calculation Function:** `calculateOverage()` (lines ~1800+)
  - Reads input values, computes overage, total, boxes, and price.
  - Updates both hidden and visible result fields.
- **Event Listeners:**
  - Open/close pop-up on button click or outside click.
  - Add to Cart triggers calculation and closes the pop-up.
- **Pop-up Control:** Adds/removes `.ovg-popup-open` class to show/hide modal.

---

## **CSS (Inlined in Liquid)**
- **Lines 820–1148, 1157–1252 in `product-template.liquid`**
  - Styles for modal, header, input, overage selectors, results, and responsiveness.
- **Legacy/Other Styles:** `#overage` in `assets/theme.css` (lines 5509, 5528) is for a different calculator.

---

## **How It Works (Current Flow)**

1. **Rendered for products with `overage-popup-v3` tag.**
2. **User clicks Add to Cart:** Pop-up appears (`#ovg-popup`).
3. **User enters square footage, selects overage:** Results auto-calculate.
4. **User clicks "Add To Cart" in pop-up:** Quantity is set, pop-up closes, and product is added to cart.

---

## **What Needs to Change (Refactor Plan)**

### **Goal**
- Make the calculator always visible (inline/indented), not a pop-up, for products with the tag.

### **Steps**
1. **Remove modal overlay logic:** Eliminate `#ovg-popup`, `.ovg-popup-open`, and related show/hide JS.
2. **Move calculator markup:** Place the calculator directly in the product page layout, always visible.
3. **Update Add to Cart logic:** The main Add to Cart button should use the calculator's result directly.
4. **Refactor CSS:** Remove modal-specific styles, ensure the calculator looks good inline.
5. **Test:** Ensure correct behavior for products with and without the tag.

---

## **Line References for Key Elements**

- **Pop-up HTML:** `snippets/product-template.liquid` lines 1259–1450
- **Pop-up CSS:** `snippets/product-template.liquid` lines 820–1148, 1157–1252
- **Pop-up JS:** `snippets/product-template.liquid` lines 1450–2299
- **Legacy calculator:** `assets/theme.css` lines 5509, 5528 (`#overage`)

---

## **Summary Table**

| Selector/ID/Class                | Type      | File/Line(s)                        | Description/Role                                 |
|----------------------------------|-----------|-------------------------------------|--------------------------------------------------|
| `#ovg-popup`                     | Div/Modal | product-template.liquid 1259+       | Pop-up container (to be removed)                 |
| `.ovg-header`                    | Div       | product-template.liquid 1267+       | Header section                                   |
| `.ovg-input-section`             | Div       | product-template.liquid 1277+       | Input for square feet                            |
| `#ovg-overage-selectors`         | Div       | product-template.liquid 1295+       | Overage % radio buttons                          |
| `.ovg-manual-input-wrapper`      | Div       | product-template.liquid 1332+       | Manual % input                                   |
| `.ovg-results`                   | Div       | product-template.liquid 1348+       | Results display                                  |
| `#ovg-addToquanitity`            | Button    | product-template.liquid 1453+       | Add to Cart button in pop-up                     |
| `calculateOverage()`             | Function  | product-template.liquid 1801+       | Main calculation logic                           |
| `#overage`                       | Div/ID    | theme.css 5509, 5528                | Legacy calculator (not the pop-up)               |

---

## **Other Notes**

- **No separate JS/CSS files** for the pop-up; all logic and styles are inlined in the Liquid file.
- **Legacy calculators** exist in the codebase (e.g., `#overage`), but are not the same as the pop-up.
- **`snippets/product_details_calculator_popup.liquid`** is a different calculator, not directly related.

---

**This README provides a full map of the overage calculator pop-up code, selectors, and logic, and outlines the plan for converting it to an always-visible inline component.** 