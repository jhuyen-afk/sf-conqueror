# Salesforce Automation Fail-Safes

**Last Updated**: 2025-01-29

This document contains critical fail-safe procedures to prevent automation failures.

---

## 🛡️ Fail-Safe #1: Window Focus Verification

**Problem**: Automation could type into wrong window if Chrome loses focus.

**Solution**: Always verify Chrome is active before sending keystrokes.

### Implementation:

```bash
# Before EVERY action, run this:
osascript -e 'tell application "Google Chrome" to activate'
sleep 0.5  # Wait for window to activate
```

### When to Use:
- Before typing into any field
- Before pressing Tab
- Before pressing Enter
- After taking a screenshot
- After any wait period

### Visual Confirmation:
- Take screenshot after activating Chrome
- Verify you see the Salesforce form
- Check for blue borders on focused fields

---

## 🛡️ Fail-Safe #2: Screenshot After Every Critical Action

**Problem**: Can't see errors or validation issues without visual confirmation.

**Solution**: Take screenshot after every important action.

### When to Screenshot:
1. After activating Chrome
2. After pressing Tab (to see which field is focused)
3. After typing a value (to confirm it appeared)
4. After opening a dropdown (to see options)
5. After selecting from dropdown (to confirm selection)
6. After pressing Save (to see success or error messages)

### What to Look For:
- ✅ Blue border = field is focused correctly
- ✅ Text appears in field after typing
- ✅ Dropdown shows selected value
- ❌ Red error messages at top of form
- ❌ Validation errors on fields
- ❌ "Complete this field" messages

---

## 🛡️ Fail-Safe #3: Wait Periods Between Actions

**Problem**: Salesforce UI needs time to respond to actions.

**Solution**: Add strategic wait periods.

### Wait Times:

```bash
# After activating Chrome
sleep 0.5

# After pressing Tab
sleep 0.3

# After typing text
sleep 0.2

# After opening dropdown
sleep 0.5  # Dropdown needs time to populate

# After selecting from dropdown
sleep 0.5  # Selection needs time to register

# After pressing Save
sleep 2.0  # Page needs time to save and redirect
```

### Adjustable Based On:
- Network speed (slower network = longer waits)
- Salesforce performance (peak hours = longer waits)
- Computer speed (older computer = longer waits)

---

## 🛡️ Fail-Safe #4: Field Recognition Verification

**Problem**: Tab count changes, might land on wrong field.

**Solution**: Always verify field label before typing.

### Process:
1. Press Tab
2. Take screenshot
3. **READ the field label** in the screenshot
4. Verify it matches the target field (e.g., "First Name")
5. If wrong field → Tab again and repeat
6. If correct field → Type the value

### Field Identification:
- Look for **field label text** above or beside the input
- Look for **blue border** around the input field
- Look for **placeholder text** inside the field
- Check **section header** to confirm you're in right section

### Example:
```
Target: First Name
Screenshot shows: "Middle Name" with blue border
Action: Tab again (wrong field)

Screenshot shows: "First Name" with blue border  
Action: Type value (correct field!) ✅
```

---

## 🛡️ Fail-Safe #5: Dropdown Selection Verification

**Problem**: Dropdown might not register selection.

**Solution**: Verify selection after closing dropdown.

### Process:
1. Open dropdown (Press Enter)
2. Take screenshot (see options)
3. Navigate with arrows
4. Take screenshot (see highlighted option)
5. Press Enter to select
6. **Take screenshot** (verify dropdown closed)
7. **Check dropdown now shows selected value** (not "--None--")

### Verification:
- Dropdown should be **closed**
- Selected value should be **visible** in the field
- Example: "Sales Sourced" appears instead of "--None--"

### If Selection Failed:
- Dropdown still shows "--None--"
- **Retry**: Open dropdown again and reselect
- **Max retries**: 3 attempts
- **If still fails**: Log error and skip this lead

---


## 🛡️ Fail-Safe #6: Save Button Verification

**Problem**: Might not reach Save button, or button might be disabled.

**Solution**: Verify Save button is visible and enabled before clicking.

### Process:
1. Tab until you see Save button in screenshot
2. Verify button text says "Save" (not "Cancel" or "Save & New")
3. Check button is **not grayed out** (enabled state)
4. Verify no validation errors visible on form
5. Press Enter on Save button
6. **Wait 2 seconds**
7. Take screenshot to verify result

### Success Indicators:
- Form closes
- Returns to Leads list page
- Or: Success message appears

### Failure Indicators:
- Red error message at top
- Red borders around fields
- Form still open

---

## 🛡️ Fail-Safe #7: Duplicate Detection Handling

**Problem**: Duplicate popup blocks save.

**Solution**: Press Escape to cancel, log duplicate, move to next lead.

---

## 🛡️ Fail-Safe #8: Data Validation Before Filling

**Problem**: Invalid data format causes save errors.

**Solution**: Validate phone (10+ digits), email (@domain), zip (5 digits) before typing.

---

## 🛡️ Fail-Safe #9: Session Timeout Detection

**Problem**: Salesforce session expires during automation.

**Solution**: Check for login page in screenshots, stop if detected.

---

## 🛡️ Fail-Safe #10: Progress Tracking & Logging

**Problem**: If crash, don't know which leads succeeded.

**Solution**: Log every lead with status (SUCCESS/DUPLICATE/FAILED).

---

## 🛡️ Fail-Safe #11: Batch Processing

**Problem**: Long sessions increase error risk.

**Solution**: Process 10 leads at a time with 2-minute breaks between batches.

---

## 🛡️ Fail-Safe #12: Emergency Stop

**Problem**: Need to stop if something goes wrong.

**Solution**: User can press Escape or close Chrome to stop gracefully.

---

## 📋 Pre-Flight Checklist

Before starting automation:

### Environment:
- [ ] Laptop only (no external monitors)
- [ ] Chrome is only window open
- [ ] Salesforce logged in, on Leads list
- [ ] Do Not Disturb mode ON
- [ ] Computer plugged in

### Permissions:
- [ ] Screen Recording granted to Goose
- [ ] Accessibility granted to Goose
- [ ] Goose restarted
- [ ] Test screenshot works

### Data:
- [ ] CSV validated (phone, email, zip formats)
- [ ] Industry values match Salesforce options
- [ ] Lead Source = "Sales Sourced"

### Testing:
- [ ] Created 1 test lead successfully
- [ ] Tested duplicate detection

---

## ✅ Success Criteria

Lead is successful when:
1. ✅ All 12 required fields filled
2. ✅ Save pressed, no errors
3. ✅ Form closed, returned to Leads list
4. ✅ New lead visible in list

---

**End of Fail-Safes Document**
