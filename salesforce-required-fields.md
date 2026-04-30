# Salesforce US Sales Lead - Required Fields Guide

**Last Updated**: 2025-01-29

This document lists the **MINIMUM REQUIRED FIELDS** to successfully create a Salesforce US Sales lead, along with the complete Industry/Vertical options.

---

## 📋 Required Fields to Create a Lead

To successfully save a new lead, you MUST fill out these fields:

### 1. Contact Information Section
- **First Name** (text field)
- **Last Name** (text field) - REQUIRED (red border if empty)

### 2. Company Information Section  
- **Company** (text field) - REQUIRED (red border if empty)

### 3. Contact Details Section
- **Phone** (text field)
- **Email** (text field) - if available

### 4. Address Section
- **Street** (text area)
- **City** (text field)
- **State/Province** (text field)
- **Zip/Postal Code** (text field)
- **Country** (text field)

### 5. Business Information Section
- **Industry** (dropdown) - REQUIRED (red border if empty)
  - Must select one of the 11 available verticals (see list below)

---

## 🏢 Complete Industry/Vertical List

When you reach the **Industry** field, press **Enter** to open the dropdown, then use **Up/Down arrows** to navigate and select from these options:

1. **--None--** (default, not valid for saving)
2. **Beauty**
3. **Casual Use**
4. **Channel**
5. **Charities, Education and Membership**
6. **Fitness**
7. **Food and Drink**
8. **Health**
9. **Home and Repair**
10. **Information Technology and Services**
11. **Leisure and Entertainment**

**Total**: 11 industry verticals (plus "--None--" option)

---

## 🎯 Field Fill Order (Recommended)

Follow this order to efficiently fill the form using Tab navigation:

1. **First Name** → Tab
2. **Last Name** → Tab (continue tabbing through other fields)
3. **Company** → Tab
4. **Phone** → Tab
5. **Email** → Tab (continue tabbing)
6. **Street** → Tab
7. **City** → Tab
8. **State/Province** → Tab
9. **Zip/Postal Code** → Tab
10. **Country** → Tab
11. **Industry** → Press Enter → Use Down Arrow to select vertical → Press Enter

---

## ⚙️ How to Fill the Industry Field

**CRITICAL**: The Industry field is a dropdown, not a text field!

### Steps:
1. **Tab to Industry field** until you see the dropdown with blue border (showing "--None--")
2. **Press Enter** to open the dropdown
3. **Use Down Arrow** (↓) to scroll through the 11 verticals
4. **Use Up Arrow** (↑) to go backwards if you overshoot
5. **Press Enter** to select the highlighted vertical
6. The dropdown closes and the selected industry appears in the field

### Visual Cues:
- **Blue border** = Field is focused
- **Red border** = Required field is empty
- **Blue highlight** = Option is selected in dropdown
- **Checkmark** = Currently selected value

---

## 🚫 Common Mistakes

1. **Don't click the "View all dependencies" link** - This opens a modal dialog instead of the dropdown
2. **Don't try to type in the Industry field** - It's a dropdown, not a text field
3. **Don't count tabs** - Tab counts change! Use visual confirmation (blue borders) instead
4. **Don't forget to press Enter twice** - Once to open dropdown, once to select the option

---

## ✅ Validation Rules

Before you can save the lead:
- **Last Name** must not be empty
- **Company** must not be empty
- **Industry** must not be "--None--" (must select a vertical)
- All other fields are optional but recommended

---

## 📝 Automation Strategy

### For Goose AI:
1. **Read this document** to know which fields are required
2. **Use Tab-and-Verify loop** to find each field by label (not by counting)
3. **Fill fields in the recommended order** (First Name → Last Name → Company → etc.)
4. **For Industry dropdown**:
   - Tab until Industry field has blue border
   - Press Enter to open
   - Press Down Arrow multiple times to find the target vertical
   - Press Enter to select
5. **Visual confirmation** - Take screenshot after each field to verify position
6. **No clicking** - Use Tab, Enter, and Arrow keys only

### Example Command Sequence:
```bash
# Navigate to First Name
osascript -e 'tell application "System Events" to key code 48'  # Tab
# (repeat until First Name has blue border)

# Type value
osascript -e 'tell application "System Events" to keystroke "John"'

# Navigate to Industry dropdown
osascript -e 'tell application "System Events" to key code 48'  # Tab
# (repeat until Industry dropdown has blue border)

# Open dropdown
osascript -e 'tell application "System Events" to key code 36'  # Enter

# Navigate to desired vertical (e.g., "Food and Drink")
osascript -e 'tell application "System Events" to key code 125'  # Down Arrow
# (repeat until "Food and Drink" is highlighted)

# Select vertical
osascript -e 'tell application "System Events" to key code 36'  # Enter
```

---

## 🔄 Field Dependencies

**Note**: The Industry field has a dependency relationship with Sub-Industry. When you select an Industry:
- The Sub-Industry dropdown becomes available
- Sub-Industry options change based on selected Industry
- Sub-Industry is NOT required to save the lead

---

## 💾 Saving the Lead

After filling all required fields:
1. **Tab to the Save button** (at bottom of form)
2. **Press Enter** to save
3. OR use keyboard shortcut: **Cmd+S** (if supported)

**Alternative**: 
- **Save & New** button - Saves current lead and opens a new blank form
- **Cancel** button - Discards changes and closes form

---

## 📊 Summary

**Minimum Required Fields**: 11 fields
- First Name
- Last Name  
- Company
- Phone
- Email (if available)
- Street
- City
- State/Province
- Zip/Postal Code
- Country
- Industry (select from 11 verticals)

**Industry Verticals**: 11 options
- Beauty, Casual Use, Channel, Charities/Education/Membership, Fitness, Food and Drink, Health, Home and Repair, IT and Services, Leisure and Entertainment

**Key Strategy**: Tab-and-Verify loop with visual confirmation (blue borders)

**Time Estimate**: 2-3 minutes per lead once you know the workflow

---

**End of Required Fields Guide**
