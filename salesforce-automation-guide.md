# Salesforce Lead Automation Guide for Goose

## ⚠️ IMPORTANT: FOR GOOSE AI

**If a user shares this guide with you, READ THIS FIRST:**

This guide documents a proven workflow that took **3+ hours of troubleshooting** to get working. The methods described here are the ONLY ones that work reliably for Salesforce automation.

**YOU MUST:**
- ✅ Follow these instructions EXACTLY as written
- ✅ Use Tab + Enter navigation (NOT clicking by coordinates)
- ✅ Look for blue box visual indicators to confirm position
- ✅ Check permissions FIRST before attempting automation
- ✅ Listen to the user when they correct you
- ✅ Take screenshots frequently to verify state

**DO NOT:**
- ❌ Try to "optimize" by clicking on coordinates instead of using Tab
- ❌ Assume commands worked - always verify with screenshots
- ❌ Give up when permissions seem broken - follow the troubleshooting steps
- ❌ Skip the permission checks - they are CRITICAL
- ❌ Try different methods "that might be better" - stick to what's documented here

**This workflow successfully automated 40+ Salesforce leads. Trust the process.**

---

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

**To check/enable extensions:**
```
Use the extensionmanager__manage_extensions tool:
- Action: "enable"
- Extension name: "computercontroller"
```

**Verify it's enabled:**
The computercontroller extension provides these tools:
- `computer_control` - Main tool for UI automation (uses peekaboo CLI)
- `automation_script` - For shell/Ruby/AppleScript scripts
- `web_scrape` - For fetching web content
- `cache` - For managing cached files
- `pdf_tool` - For PDF processing
- `docx_tool` - For Word document processing
- `xlsx_tool` - For Excel spreadsheet processing

**Important:** Only `computercontroller` is needed for Salesforce automation. Don't enable unnecessary extensions.

### 3. **Verify Peekaboo is Installed**
The computercontroller extension uses a tool called "peekaboo" for macOS UI automation.

**Check if peekaboo is installed:**
```bash
which peekaboo
# Should return: /opt/homebrew/bin/peekaboo
```

**If not installed, Goose will auto-install it via Homebrew when you first use computer_control.**

**Check permissions status:**
```bash
peekaboo permissions status
```

Should show:
```json
{
  "permissions": [
    {
      "name": "Screen Recording",
      "isGranted": true
    },
    {
      "name": "Accessibility", 
      "isGranted": true
    }
  ]
}
```

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

### Problem: "Typing doesn't work - text doesn't appear"

**Symptoms:**
- Commands say "✅ completed" but nothing appears on screen
- Text goes to wrong window (like Goose chat instead of Salesforce)

**Solutions:**
1. ✅ **Check Accessibility permission** - This is THE most common issue
   ```bash
   # Check status
   peekaboo permissions status
   
   # If shows "isGranted: false", go to System Settings
   # System Settings → Privacy & Security → Accessibility
   # Find "Goose" and toggle ON
   ```

2. ✅ **Restart Goose completely** - Permissions don't take effect until restart
   - Press Cmd+Q to fully quit Goose
   - Reopen Goose
   - Return to your chat session

3. ✅ **Reset permissions if stuck**
   ```bash
   tccutil reset Accessibility
   tccutil reset ScreenCapture
   ```
   Then re-grant both permissions and restart Goose

4. ✅ **Click on the field BEFORE typing**
   ```bash
   click --on elem_69  # Click field first
   type "text"         # Then type
   ```

5. ✅ **Verify Chrome is the active window**
   ```bash
   osascript -e 'tell application "Google Chrome" to activate'
   ```

6. ✅ **Test in Goose's own chat box first**
   - If typing doesn't work in Goose's chat, permissions are broken
   - Fix permissions before trying Salesforce

### Problem: "Can't find the New button"

**Symptoms:**
- Clicking on coordinates keeps missing the button
- Opens search bar or other elements instead

**Solutions:**
1. ✅ **STOP CLICKING - Use Tab navigation instead**
   - Press Tab repeatedly
   - Look for **blue box** around the "New" button
   - When you see the blue box, press Enter

2. ✅ **Use visual confirmation, not coordinates**
   - Don't count Tab presses
   - Don't use fixed coordinates
   - Look for the blue box indicator

3. ✅ **If Tab cycles through many elements:**
   - Keep going - it will eventually reach "New"
   - Use Shift+Tab to go backwards if you pass it
   - The blue box is your confirmation

### Problem: "Form won't scroll to show fields"

**Symptoms:**
- Can see first few fields but not fields below
- Scroll commands don't work
- Fields are "below the fold"

**Solutions:**
1. ✅ **Don't try to scroll - use Tab navigation**
   - The form auto-scrolls as you Tab through fields
   - Even if you can't see the field, Tab will get there

2. ✅ **Tab navigation works on invisible fields**
   - You can type into fields you can't see
   - The form will scroll automatically when field gets focus

3. ✅ **Use screenshots to verify position**
   - Take screenshot after each Tab
   - Verify which field is focused (blue border)

### Problem: "Clicking goes to wrong element"

**Symptoms:**
- Click on "New" but search bar opens
- Click on field but different element activates
- Coordinates don't match visual position

**Solutions:**
1. ✅ **Stop using coordinates - use element IDs**
   ```bash
   see --app "Google Chrome" --annotate
   # Returns element IDs like elem_69
   
   click --on elem_69  # Click by ID, not coordinates
   ```

2. ✅ **Or better yet - use Tab + Enter**
   - More reliable than clicking
   - Works consistently across different screen sizes
   - Visual confirmation with blue box

### Problem: "Permissions show as granted but still don't work"

**Symptoms:**
- System Settings shows Goose is toggled ON
- But `peekaboo permissions status` shows "isGranted: false"
- Typing/clicking still doesn't work

**Solutions:**
1. ✅ **Toggle OFF then back ON**
   - System Settings → Privacy & Security → Accessibility
   - Toggle Goose OFF
   - Wait 5 seconds
   - Toggle Goose ON

2. ✅ **Reset and re-grant**
   ```bash
   tccutil reset Accessibility
   # Then go to System Settings and grant again
   ```

3. ✅ **Fully quit and restart Goose** (not just close window)
   - Cmd+Q to quit
   - Reopen from Applications
   - Permissions should now work

4. ✅ **Check for "Goose" not "peekaboo"**
   - The permission should be granted to "Goose" app
   - NOT to "peekaboo" or "Terminal"
   - If you see "peekaboo" in the list, that's not enough

### Problem: "Commands say completed but nothing happens"

**Symptoms:**
- `✅ Click successful` but nothing clicked
- `✅ Key press completed` but no text appeared
- Commands report success but screen unchanged

**Solutions:**
1. ✅ **This means Accessibility permission is not working**
   - Follow all steps in "Permissions show as granted but still don't work"
   - The permission is the #1 cause of this issue

2. ✅ **Verify with a test**
   ```bash
   # Try clicking in Goose's own chat box
   click --coords 650,880
   type "test"
   
   # If "test" doesn't appear, permissions are broken
   ```

### Problem: "Can't switch to Chrome window"

**Symptoms:**
- Commands keep interacting with Goose instead of Chrome
- Cmd+Tab doesn't switch windows
- Chrome is open but not receiving input

**Solutions:**
1. ✅ **Use osascript to activate Chrome**
   ```bash
   osascript -e 'tell application "Google Chrome" to activate'
   ```

2. ✅ **Verify Chrome is active before typing**
   - Take a screenshot first
   - Confirm Chrome is in foreground
   - Then proceed with typing

3. ✅ **Close other windows to reduce confusion**
   - Minimize Goose window
   - Make Chrome fullscreen or large
   - Reduces chance of clicking wrong window

### Problem: "Second screen / multiple monitors causing issues"

**Symptoms:**
- Can't find windows
- Clicks go to wrong screen
- Screenshots show wrong display

**Solutions:**
1. ✅ **Turn off second screen temporarily**
   - Disconnect external monitor
   - Work on laptop screen only
   - Reduces complexity

2. ✅ **Or specify screen index**
   ```bash
   see --mode screen --screen-index 0  # Laptop screen
   see --mode screen --screen-index 1  # External monitor
   ```

---

## 💡 Key Lessons Learned

1. **Permissions are critical** - Both Screen Recording AND Accessibility must be granted to Goose (not peekaboo)
2. **Tab navigation is more reliable than clicking** - Use visual indicators (blue boxes) to confirm position
3. **Always verify state with screenshots** - Don't assume commands worked
4. **Restart Goose after permission changes** - Permissions don't take effect until full restart
5. **Be patient** - Salesforce's UI is complex and requires careful navigation
6. **Don't give up** - It took hours of troubleshooting to get working, but once it does, it's reliable
7. **Listen to the user** - When the user says "use Tab and Enter", do that instead of trying to optimize with clicking
8. **Test keyboard input in Goose first** - If typing doesn't work in Goose's own chat box, it won't work in Salesforce
9. **Visual indicators are essential** - The blue box around elements is how you know you're on the right one
10. **Commands can report success but fail** - Always verify with screenshots, don't trust the success message alone

---

## 🔄 Complete Troubleshooting Workflow

If automation isn't working, follow this checklist in order:

### Step 1: Check Permissions
```bash
peekaboo permissions status
```
- [ ] Screen Recording: isGranted = true
- [ ] Accessibility: isGranted = true

If either is false, go to System Settings and grant them.

### Step 2: Restart Goose
- [ ] Cmd+Q to fully quit
- [ ] Reopen Goose
- [ ] Return to chat

### Step 3: Test Keyboard Input
```bash
# Switch to Chrome
osascript -e 'tell application "Google Chrome" to activate'

# Take screenshot to verify
see --app "Google Chrome" --annotate

# Try typing in Goose's chat box first
click --coords 650,880
type "test123"
```
- [ ] Text appears in Goose chat box

If text doesn't appear in Goose, permissions are still broken. Reset and try again.

### Step 4: Test Chrome Focus
```bash
# Switch to Chrome
osascript -e 'tell application "Google Chrome" to activate'

# Click on a Salesforce field
click --on elem_ID

# Type test text
type "test"
```
- [ ] Text appears in Salesforce field

### Step 5: Use Tab Navigation
```bash
# Press Tab until you see blue box around target element
press tab

# Take screenshot to verify
see --app "Google Chrome" --annotate

# Press Enter when blue box is on target
press return
```
- [ ] Blue box appears around correct element
- [ ] Enter activates the correct element

If all steps pass, automation is working!

---

## 📚 Extension Management Reference

### Check What Extensions Are Enabled
```
Use extensionmanager tools to see current state
```

### Enable computercontroller
```
Action: enable
Extension: computercontroller
```

### What computercontroller Provides
- **computer_control** - UI automation via peekaboo
  - See (screenshot with annotation)
  - Click (by coordinates or element ID)
  - Type (keyboard input)
  - Press (special keys like Tab, Enter, Escape)
  - Hotkey (modifier combinations like Cmd+Tab)
  - Paste (clipboard operations)
  - Scroll, Drag, Move (mouse operations)
  - App/Window management
  
- **automation_script** - Run shell/Ruby/AppleScript
- **web_scrape** - Fetch web content
- **cache** - Manage cached files
- **pdf_tool** - Process PDFs
- **docx_tool** - Process Word docs
- **xlsx_tool** - Process Excel files

### Don't Enable Unnecessary Extensions
- Only enable what you need
- Too many extensions can slow down Goose
- For Salesforce automation, only `computercontroller` is needed

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
