# FINAL PLAN: Inline Overage & Quantity Calculator

## **Project Goal**

The objective is to refactor the product page to include an always-visible, inline calculator for products tagged with `"overage-v3"`. This new component will combine the features of the existing overage pop-up and the quantity/area calculator, with a UI that matches the user-provided screenshot.

---

## **Key Requirements**

1.  **Visibility & Trigger:**
    *   The calculator will only appear for products with the tag `"overage-v3"`.
    *   It will be always visible and inline (not a pop-up).

2.  **UI & Layout (as per screenshot):**
    *   The top part of the calculator will contain two input fields: **SQ. FT** and **Boxes**. The user can enter a value in either field, and the other will update automatically.
    *   The "Total Price" box from the original quantity calculator will be removed.
    *   Below the input fields, the **"Overage Amount"** section from the pop-up (10%, 15%, Manual, etc.) will be displayed.
    *   The **"Calculation Results"** (Overage, Total, Boxes Needed, Total Price) will be displayed below the overage options, but just above the "Add to Cart" button.

3.  **Styling & Logic:**
    *   The styling will match the modern, clean, indented look of the pop-up calculator.
    *   All calculation logic from the overage pop-up will be preserved and integrated with the SQ. FT/Boxes inputs.

---

## **Implementation Plan**

1.  **Refactor HTML in `snippets/product-template.liquid`:**
    *   Create a new inline calculator section that appears only for products with the `"overage-v3"` tag.
    *   Move and combine elements from the existing overage pop-up and quantity calculator.
    *   Remove the pop-up/modal HTML.

2.  **Adjust CSS (inlined in `product-template.liquid` and `assets/theme.css`):**
    *   Remove pop-up-specific styles (e.g., `position: fixed`, `display: none`).
    *   Apply the pop-up's theme to the new inline component to achieve the desired look.

3.  **Update JavaScript in `snippets/product-template.liquid`:**
    *   Remove all pop-up trigger and display logic (e.g., `.ovg-popup-open`, click handlers for showing/hiding).
    *   Integrate the `calculateFromSquaredSize()` and `calculateFromQuantity()` functions with the `calculateOverage()` function to ensure all calculations are linked.
    *   Ensure the main "Add to Cart" button correctly uses the final quantity calculated by this new integrated component.

---

## **File & Code Summary**

### **Files to Modify**
- **`snippets/product-template.liquid`:** For HTML, CSS, and JS changes.
- **`assets/theme.css`:** For any necessary global CSS adjustments.

### **Key Selectors & Functions**
- **From Overage Calculator:**
  - `#ovg-popup`, `#ovg-overage-selectors`, `.ovg-results`, `calculateOverage()`
- **From Quantity Calculator:**
  - `.calculator_container`, `#squared_size`, `#quantity_look_alike`, `calculateFromSquaredSize()`, `calculateFromQuantity()`

---

**This file documents the final, consolidated requirements and plan for the inline overage & quantity calculator, as discussed and confirmed before coding.** 