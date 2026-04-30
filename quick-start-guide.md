# 🚀 QUICK START GUIDE - Salesforce Lead Automation

**Use this guide to fill out leads quickly. Follow each step exactly.**

---

## 📋 PRE-FLIGHT CHECKLIST

Before starting, verify:
- [ ] Laptop only (no external monitors/keyboards/mice)
- [ ] Chrome is the only window open
- [ ] Do Not Disturb mode ON
- [ ] Computer plugged in
- [ ] Screen Recording + Accessibility permissions granted to Goose
- [ ] Have CSV with lead data ready

---

## 🎯 LEAD DATA REQUIRED (10 fields minimum)

For each lead, you need:
1. First Name (or use Company name if empty)
2. Last Name (or use "Team" if empty)
3. Company
4. Phone
5. Street
6. City
7. State/Province
8. Zip/Postal Code
9. Country
10. Industry (select from: Beauty, Casual Use, Channel, Charities/Education/Membership, Fitness, Food and Drink, Health, Home and Repair, IT and Services, Leisure and Entertainment)

**Optional:** Email (fill if available, skip if not)

---

## 🚀 WORKFLOW - STEP BY STEP

### **STEP 1: Open the Form**
```bash
1. Open new tab in Chrome (Cmd+T)
2. Paste URL: https://squareinc.lightning.force.com/lightning/o/Lead/new?recordTypeId=012E0000000VckzIAC
3. Press Enter
4. Wait 2 seconds for form to load
```

**SUCCESS CRITERIA:** You see "New Lead: US Sales" title at top

---

### **STEP 2: Zoom Out to See Everything**
```bash
1. Press Cmd+Minus 20 times (hold Cmd, tap Minus 20x)
2. Press Cmd+Home to scroll to top
3. Take ONE screenshot to see entire form
```

**SUCCESS CRITERIA:** You can see multiple sections at once (Regulator Details, Opportunity Description, Contact Information)

---

### **STEP 3: Navigate to First Name Field**

**From top of form:**
```bash
1. Press Tab repeatedly until you see "Contact Information" section
2. Keep tabbing until "First Name" field has BLUE BORDER
3. Count approximately 25-35 tabs from start
```

**SUCCESS CRITERIA:** 
- Blue border around "First Name" input field
- You can see the label "First Name" above the field

**VISUAL CHECK:** Take screenshot to confirm before typing

---

### **STEP 4: Fill Contact Information Fields**

**Once at First Name field:**

```bash
1. Type First Name value (or Company name if empty)
2. Press Tab once → should land on "Middle Name" (skip it)
3. Press Tab once → should land on "Last Name" (BLUE BORDER)
4. Type Last Name value (or "Team" if empty)
5. Press Tab once → should land on "Suffix" (skip it)
6. Press Tab 2-3 times → should land on "Company" (BLUE BORDER, required field with red border)
7. Type Company name
8. Press Tab 1-2 times → should land on "Phone" (BLUE BORDER)
9. Type Phone number
```

**SUCCESS CRITERIA:** 
- Each field shows the typed value
- Blue border moves to next field after each Tab
- Required fields (Last Name, Company) lose their red error borders

**VISUAL CHECK:** Take screenshot after filling all 4 fields to verify

---

### **STEP 5: Fill Address Fields**

**Continue from Phone field:**

```bash
1. Press Tab 5-8 times → should land on "Street" field (BLUE BORDER)
   (You'll pass: Mobile, Website, Email, DS Best Time to Call, Address Search)
2. Type Street address
3. Press Tab once → should land on "City" (BLUE BORDER)
4. Type City
5. Press Tab once → should land on "State/Province" (BLUE BORDER)
6. Type State (e.g., "NY")
7. Press Tab once → should land on "Zip/Postal Code" (BLUE BORDER)
8. Type Zip code
9. Press Tab once → should land on "Country" (BLUE BORDER)
10. Type Country (e.g., "United States")
```

**SUCCESS CRITERIA:**
- All address fields filled correctly
- Blue border moves sequentially through fields
- No fields skipped

**VISUAL CHECK:** Take screenshot after filling all 5 address fields

---

### **STEP 6: Fill Industry Dropdown**

**Continue from Country field:**

```bash
1. Press Tab 8-12 times → should land on "Industry" dropdown (BLUE BORDER, shows "--None--")
2. Press Enter to open dropdown
3. Press Down Arrow to navigate through options:
   - Beauty
   - Casual Use
   - Channel
   - Charities, Education and Membership
   - Fitness
   - Food and Drink
   - Health
   - Home and Repair
   - Information Technology and Services
   - Leisure and Entertainment
4. When correct industry is highlighted (blue background), press Enter to select
5. Dropdown closes, selected value appears
```

**DEFAULT INDUSTRY:** If not specified, use "Beauty"

**SUCCESS CRITERIA:**
- Dropdown opens when you press Enter
- Selected industry appears in the field (not "--None--")
- Dropdown closes after selection

**VISUAL CHECK:** Take screenshot to confirm industry is selected

---

### **STEP 7: Navigate to Save Button**

**Two methods:**

**Method A - Tab to bottom:**
```bash
1. Press Tab repeatedly until you reach bottom navigation tabs
2. You'll see "Recent Items" with light blue/gray background (focused)
3. Press Shift+Tab 4 times to reach "Save" button
4. "Save" button should have BLUE BORDER
```

**Method B - Direct:**
```bash
1. Scroll down to see Save button
2. Tab until "Save" button has BLUE BORDER
```

**SUCCESS CRITERIA:**
- "Save" button has blue border around it
- No validation errors visible on form
- All required fields filled (no red borders)

**VISUAL CHECK:** Take screenshot to confirm Save button is focused

---

### **STEP 8: Save the Lead**

```bash
1. Verify Save button has blue border
2. Press Enter
3. Wait 2-3 seconds
```

**SUCCESS CRITERIA - Two possibilities:**

**A) Success:**
- Form closes
- Returns to Leads list OR
- Shows success message

**B) Duplicate Detected:**
- Popup appears: "Potential Duplicate Detected"
- Shows matching lead(s)
- Options: Cancel, Save Anyway, Merge

**If duplicate detected:**
```bash
1. Press Escape to close popup
2. Log: "DUPLICATE - Company: [name]"
3. Close tab (Cmd+W)
4. Move to next lead
```

**VISUAL CHECK:** Take screenshot of result (success or duplicate popup)

---

### **STEP 9: Clean Up**

```bash
1. If form closed successfully: Close tab (Cmd+W)
2. If still on form: Press Escape, then Cmd+W
3. Clear cache periodically: Run `cache clear` every 10 leads
```

---

## 📊 PROGRESS TRACKING

**For each lead, log:**
- ✅ SUCCESS - Lead created for [Company Name]
- ⚠️ DUPLICATE - [Company Name] already exists
- ❌ FAILED - [Company Name] - [Error reason]

**Example log:**
```
Lead 1: ✅ SUCCESS - ID Jewelry
Lead 2: ⚠️ DUPLICATE - Acme Corp
Lead 3: ✅ SUCCESS - Best Bakery
Lead 4: ❌ FAILED - Missing phone number
```

---

## 🚨 TROUBLESHOOTING

### **Problem: Can't find First Name field**
**Solution:**
- Take screenshot to see current position
- Look for "Contact Information" section header
- Tab forward until you see it
- First Name is the first field in that section

### **Problem: Typed in wrong field**
**Solution:**
- Press Cmd+Z to undo
- Or: Select all text (Cmd+A), Delete
- Take screenshot to see which field has blue border
- Shift+Tab back or Tab forward to correct field

### **Problem: Industry dropdown won't open**
**Solution:**
- Make sure field has blue border
- Press Enter (not Space)
- If still doesn't open, Tab away and back, try again

### **Problem: Can't find Save button**
**Solution:**
- Scroll to bottom of form
- Look for "Recent Items" tab with light blue background
- Shift+Tab 4 times from there
- Or: Tab forward from last field until Save button has blue border

### **Problem: Form closed accidentally**
**Solution:**
- Open new tab (Cmd+T)
- Paste URL again
- Start over (data was not saved)

### **Problem: Duplicate popup appeared**
**Solution:**
- Press Escape to cancel
- Log the duplicate
- Close tab (Cmd+W)
- Move to next lead
- Do NOT click "Save Anyway" unless instructed

---

## ⏱️ TIME EXPECTATIONS

**First lead:** 5-10 minutes (learning the workflow)
**Second lead:** 3-5 minutes (getting comfortable)
**Third+ leads:** 2-3 minutes each (confident execution)

**For 40 leads:** ~2-3 hours total

---

## 🎯 SUCCESS METRICS

**Good execution:**
- 90%+ success rate (36+ out of 40 leads created)
- <5% duplicates
- <5% errors
- Average 3-4 minutes per lead

---

## 📝 BEFORE STARTING EACH SESSION

1. Read this guide completely
2. Read `dos-donts.md` checklist
3. Read `failures-successes.md` to learn from past mistakes
4. Have lead data ready in CSV or list format
5. Set up environment (laptop only, Chrome only, Do Not Disturb)

---

## 🔗 RELATED DOCUMENTS

- `dos-donts.md` - Complete behavioral rules and mistakes to avoid
- `failures-successes.md` - Learning log of what worked and what didn't
- `meta-rules.md` - How to use and update the checklists
- `salesforce-automation-guide.md` - Detailed technical guide
- `salesforce-field-mapping.md` - All 97 fields documented
- `salesforce-required-fields.md` - Minimum fields needed
- `salesforce-data-rules.md` - How to handle missing data

---

## 💡 KEY REMINDERS

1. **ALWAYS verify with blue border before typing**
2. **Take screenshots at key checkpoints**
3. **Don't rush - accuracy over speed**
4. **Log all results (success/duplicate/failed)**
5. **Clear cache every 10 leads**
6. **Close tabs after each lead**
7. **If stuck, take screenshot and analyze**
8. **Never click - Tab and Enter only**
9. **Zoom out to see everything at once**
10. **Read the checklists before starting**

---

**Last Updated:** 2026-04-30
**Version:** 1.0
