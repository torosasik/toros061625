# Inline Overage Calculator Refactor Plan

## Requirements (as clarified by user)

1. **Always Visible**
   - The overage calculator should be inline and always visible on the product page (not a pop-up/modal).

2. **Inputs**
   - Only two entry fields: SQ. FT and Boxes.
   - Customers can enter either value, and the other will update automatically.

3. **Calculation Results**
   - Results (Overage, Total, Boxes Needed, Total Price) should be displayed below the input fields and above the Add to Cart button, matching the layout in the provided screenshot.

4. **Styling**
   - The calculator and results should use the same modern, clean, indented blue/white theme as the current pop-up.
   - All logic (auto-calculation, overage options, etc.) should be the same as the pop-up.

5. **Visibility Condition**
   - The calculator should only appear for products with the tag `overage-v3`.

---

## Implementation Plan

- **Remove pop-up/modal logic** and make the calculator always visible for tagged products.
- **Move calculation results** to display below the input fields and above the Add to Cart button, as in the screenshot.
- **Apply pop-up styling** to the inline calculator and results.
- **Ensure all calculation logic matches the pop-up** (including overage options and auto-calculation).
- **Show calculator only for products with the `overage-v3` tag.**

---

## Design Decisions & Clarifications

- The calculator will not be shown as a modal or require any trigger to appear.
- The only visible fields will be SQ. FT and Boxes; total price and results will be shown below, not as a separate box.
- The UI/UX and logic will be consistent with the pop-up version, but always visible and inline.
- The calculator will not appear for products without the `overage-v3` tag.

---

**This file documents the requirements and plan for the inline overage calculator refactor, as discussed and confirmed before coding.** 

Inline Overage Calculator Refactor Steps
Remove pop-up/modal logic for the overage calculator.
Move the calculator markup to be always visible and inline for products with the overage-v3 tag.
Ensure only the SQ. FT and Boxes entry fields are shown at the top.
Display calculation results (Overage, Total, Boxes Needed, Total Price) below the inputs and above the Add to Cart button, styled like the pop-up.
Apply the same modern, clean styling as the pop-up.
Ensure all calculation logic (including overage options) matches the pop-up.
Show the calculator only for products with the overage-v3 tag.
Remove the total price box from the old quantity/area calculator if present.
Test and clean up any remaining modal-specific code or styles.