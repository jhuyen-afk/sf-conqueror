# Salesforce Lead Source Field Guide

**Last Updated**: 2025-01-29

This document provides complete information about the **Lead Source** field, including all available options and how to select "Sales Sourced" for lead creation.

---

## 📍 Field Location

**Section**: Routing Information (Section 8 of the form)

**Position**: After the Social Media section, before System Information

**Field Type**: Dropdown (same behavior as Industry field)

---

## 🎯 Required Selection

**For US Sales leads, you MUST select**: **"Sales Sourced"**

This is a **REQUIRED field** for creating leads in the automation workflow.

---

## 📋 Complete Lead Source Options

When you open the Lead Source dropdown, you'll see these 11 options (plus "--None--"):

1. **--None--** (default, not valid for saving)
2. **Esense**
3. **Business Partner**
4. **Externally Sourced**
5. **Field Created**
6. **Internally Sourced**
7. **Lead Partner**
8. **Marketing Sourced**
9. **Sales Sourced** ← **SELECT THIS ONE**
10. **Solutions Partners**
11. **Unified Funnel**

**Total**: 11 lead source options (plus "--None--" default)

---

## ⚙️ How to Fill the Lead Source Field

**CRITICAL**: The Lead Source field works exactly like the Industry field!

### Steps:

#### Step 1: Navigate to Lead Source Dropdown
**Tab until you reach the Lead Source field. You'll know you're there when:**
- You see **"View all dependencies"** link with blue border/underline
- This means you've gone **ONE field too far**
- Press **Shift+Tab ONCE** to go back
- Now the Lead Source dropdown (showing "--None--") will have the blue border ✅

**Alternative**: If you land directly on the Lead Source dropdown with blue border, skip Shift+Tab

#### Step 2: Open the Dropdown
- Press **Enter** to open the dropdown
- You'll see all 11 lead source options listed

#### Step 3: Navigate to "Sales Sourced"
- Use **Down Arrow** (↓) to scroll through the options
- Count: From "--None--" to "Sales Sourced" = **8 down arrows**
- Use **Up Arrow** (↑) to go backwards if you overshoot
- The highlighted option will have a blue background

#### Step 4: Select "Sales Sourced"
- Press **Enter** to select the highlighted option
- The dropdown closes and "Sales Sourced" appears in the field ✅

---

## 🎨 Visual Cues

- **Blue border** = Field is focused (ready for interaction)
- **Blue background** = Option is highlighted in dropdown
- **Checkmark** = Currently selected value
- **"View all dependencies" link** = You've gone one field too far, press Shift+Tab

---

## 🤖 Automation Commands

### Example Command Sequence:

```bash
# Navigate to Lead Source field (Tab until "View all dependencies" is focused)
osascript -e 'tell application "System Events" to key code 48'  # Tab
# (repeat until "View all dependencies" link has blue border)

# Go back one field to Lead Source dropdown
osascript -e 'tell application "System Events" to key code 48 using shift down'  # Shift+Tab

# Open dropdown
osascript -e 'tell application "System Events" to key code 36'  # Enter

# Navigate to "Sales Sourced" (8 down arrows from "--None--")
for i in {1..8}; do
  osascript -e 'tell application "System Events" to key code 125'  # Down Arrow
  sleep 0.1
done

# Select "Sales Sourced"
osascript -e 'tell application "System Events" to key code 36'  # Enter
```

---

## 🔄 Field Dependencies

**Note**: The Lead Source field has a dependency relationship with **Source Detail**:
- Source Detail is the field to the right of Lead Source
- Source Detail options may change based on selected Lead Source
- Source Detail is NOT required to save the lead

---

## ✅ Validation

Before you can save the lead:
- **Lead Source** must not be "--None--"
- **Must select a valid option** (e.g., "Sales Sourced")
- If left as "--None--", the lead may fail to save or trigger validation errors

---

## 📊 Summary

**Field Name**: Lead Source  
**Location**: Routing Information section  
**Type**: Dropdown  
**Required**: Yes (for automation workflow)  
**Target Value**: "Sales Sourced"  
**Total Options**: 11 (plus "--None--" default)  
**Navigation**: Same as Industry field (Shift+Tab from "View all dependencies")  

---

## 🔗 Related Fields

**In the same Routing Information section:**
- Lead Source (this field)
- Source Detail (dependent dropdown, optional)
- Managed Book Model Name (text field, optional)
- Email Opt Out (checkbox, optional)
- TOSV (checkbox, optional)
- Do Not Contact (checkbox, optional)
- Sync to Marketo (checkbox, optional)
- Referrer (text field, optional)

---

## 📚 Related Documents

- **salesforce-required-fields.md** - Complete list of required fields (now includes Lead Source)
- **salesforce-field-mapping.md** - All 97 fields mapped across 9 sections
- **salesforce-automation-guide.md** - Setup and workflow guide
- **salesforce-data-rules.md** - Business rules for handling missing data

---

**End of Lead Source Guide**
