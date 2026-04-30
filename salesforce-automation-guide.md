# Salesforce Lead Automation Guide for Goose

## 🎯 Overview
This guide documents the complete process for automating Salesforce lead entry using Goose's computer control. This took significant troubleshooting to get working - follow these steps exactly to avoid the same issues.

---

## ✅ Prerequisites & Setup

### 1. **macOS Permissions (CRITICAL)**
Both permissions are **required** for keyboard/mouse automation to work:

#### Screen Recording Permission:
1. Go to **System Settings** → **Privacy & Security** → **Screen Recording**
2. Find **Goose** in the list (NOT peekaboo)
3. Toggle it **ON**

#### Accessibility Permission:
1. Go to **System Settings** → **Privacy & Security** → **Accessibility**
2. Find **Goose** in the list (NOT peekaboo)
3. Toggle it **ON**

#### If permissions show as granted but don't work:
```bash
# Reset the permissions
tccutil reset ScreenCapture
tccutil reset Accessibility
```
Then re-grant them and **fully restart Goose** (Cmd+Q, then reopen).

### 2. **Enable computercontroller Extension**
The `computercontroller` extension must be enabled in Goose for computer control to work.

---

## 🚫 DO NOT Do These Things

### ❌ **DO NOT try to click on Salesforce elements directly**
- Clicking by coordinates is unreliable
- Salesforce's UI is dynamic and elements move
- You'll end up clicking the wrong things constantly

### ❌ **DO NOT give up when permissions seem broken**
- Permissions often require a full Goose restart to take effect
- If it says "not granted" after toggling on, restart Goose completely
- Use `tccutil reset` if needed

### ❌ **DO NOT use Tab counts from the beginning**
- Tab navigation cycles through MANY elements
- The count changes based on page state
- Instead, use visual indicators (blue boxes) to know when you're on the right element

### ❌ **DO NOT try to scroll the Salesforce modal**
- The modal doesn't scroll properly with automation
- Fields below the visible area won't show when scrolling
- Use Tab navigation instead - the form auto-scrolls as you tab through

### ❌ **DO NOT assume typing/pasting works without testing**
- Always verify keyboard input is going to the right window
- Test with simple text first before trying complex automation
- If text doesn't appear, check window focus

---

## ✅ DO These Things

### ✅ **DO use `see --annotate` to identify elements**
```bash
see --app "Google Chrome" --annotate
```
This gives you element IDs and a visual map of clickable elements.

### ✅ **DO use Tab + Enter navigation**
- Tab through elements until you find the right one
- Look for **blue box visual indicators** around buttons
- Press Enter when the blue box is around the target button

### ✅ **DO switch to Chrome before starting**
```bash
osascript -e 'tell application "Google Chrome" to activate'
```
Or use Goose's app switching commands.

### ✅ **DO click on specific elements before typing**
```bash
click --on elem_69  # Click the element first
type "text here"     # Then type
```

### ✅ **DO take screenshots frequently to verify state**
```bash
capture_screenshot: true
```
Add this to commands to see what actually happened.

### ✅ **DO use the workflow that works**
The proven workflow for opening a new Salesforce lead:

1. Start on Salesforce Leads list page
2. Press Tab repeatedly until the **"New" button has a blue box** around it
3. Press Enter
4. Wait for the lead type selection dialog
5. US Sales is pre-selected
6. Tab to "Next" button (look for blue box)
7. Press Enter
8. Now you're on the lead form

---

## 🔧 Working Commands Reference

### Switch to Chrome:
```bash
osascript -e 'tell application "Google Chrome" to activate'
```

### Take annotated screenshot:
```bash
see --app "Google Chrome" --annotate
```

### Click on an element:
```bash
click --on elem_ID
```

### Type text (after clicking on field):
```bash
type "your text here"
```

### Press Tab:
```bash
press tab
```

### Press Enter:
```bash
press return
```

### Press Escape:
```bash
press escape
```

### Navigate backwards:
```bash
hotkey --keys shift,tab
```

---

## 📋 Salesforce Lead Entry Workflow

### Step 1: Open New Lead Dialog
```
1. Start on Leads list page
2. Press Tab until "New" button has blue box
3. Press Enter
4. Lead type dialog opens
```

### Step 2: Select Lead Type
```
1. US Sales is pre-selected
2. Tab to "Next" button (blue box indicator)
3. Press Enter
4. Lead form opens
```

### Step 3: Fill Form Fields
```
1. Use see --annotate to identify field element IDs
2. Click on field: click --on elem_ID
3. Type value: type "value"
4. Press Tab to move to next field
5. Repeat for all fields
```

### Step 4: Save Lead
```
1. Tab to "Save" button (blue box indicator)
2. Press Enter
3. Lead is created
```

---

## 🐛 Troubleshooting

### "Typing doesn't work"
- ✅ Check Accessibility permission is granted
- ✅ Restart Goose completely
- ✅ Make sure you clicked on the field first
- ✅ Verify Chrome is the active window

### "Can't find the New button"
- ✅ Use Tab navigation, not clicking
- ✅ Look for the blue box visual indicator
- ✅ Don't count tabs - use visual confirmation

### "Form won't scroll"
- ✅ Don't try to scroll - use Tab navigation
- ✅ The form auto-scrolls as you tab through fields

### "Clicking goes to wrong element"
- ✅ Stop clicking - use Tab + Enter instead
- ✅ Use see --annotate to find element IDs
- ✅ Click on specific elements by ID, not coordinates

---

## 💡 Key Lessons Learned

1. **Permissions are critical** - Both Screen Recording AND Accessibility must be granted to Goose (not peekaboo)
2. **Tab navigation is more reliable than clicking** - Use visual indicators (blue boxes) to confirm position
3. **Always verify state with screenshots** - Don't assume commands worked
4. **Restart Goose after permission changes** - Permissions don't take effect until full restart
5. **Be patient** - Salesforce's UI is complex and requires careful navigation
6. **Don't give up** - It takes time to get working, but once it does, it's reliable

---

## 🎯 Next Steps

Once you have the basic workflow working:

1. Map out all the fields you need to fill
2. Document the Tab counts or element IDs for each field
3. Create a recipe that automates the entire process
4. Test with sample data
5. Create a CSV template for bulk lead entry

---

## 📝 Notes

- This automation successfully filled 40 leads before
- The key was using Tab navigation + Enter, not clicking
- Visual indicators (blue boxes) are essential for knowing position
- Always test with one lead before doing bulk entry

---

**Created:** 2026-04-29  
**Last Updated:** 2026-04-29  
**Status:** ✅ Working - Permissions configured, navigation method proven
