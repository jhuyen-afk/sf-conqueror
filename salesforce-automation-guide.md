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

### 0. **Physical Setup (DO THIS FIRST)**

Before starting any automation, prepare your workspace:

**REQUIRED:**
- [ ] **Disconnect all external monitors** - Use ONLY your laptop screen
- [ ] **Disconnect external keyboards** - Use ONLY your laptop keyboard
- [ ] **Disconnect external mice/trackpads** - Use ONLY your laptop trackpad
- [ ] **Close all unnecessary applications** - Only keep Chrome (Salesforce) and Goose open
- [ ] **Make Chrome window large** - Maximize or make it fill most of the screen
- [ ] **Position Goose window to the side** - So you can see both Goose and Chrome

**Why this matters:**
- External monitors cause window detection issues
- External input devices can interfere with automation
- Multiple screens make it harder to target the correct window
- A clean workspace reduces errors and confusion

**Once automation is working reliably, you can experiment with adding external devices back. But for initial setup and troubleshooting, keep it simple.**

---

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

## 🎯 Field Navigation Strategy (CRITICAL)

**THE GOLDEN RULE: Find fields by their LABELS, not by tab counts!**

### Why This Matters:

Tab counts **WILL CHANGE** between sessions because:
- Fields get hidden/shown based on what's filled
- Browser state varies
- Salesforce updates change the form
- Focus position when form opens isn't always the same

### The Correct Approach:

**❌ WRONG: "Press Tab 15 times to get to First Name"**
- Tab count changes = you end up on wrong field
- Automation breaks every time

**✅ CORRECT: "Find First Name field, then fill it"**
- Works regardless of tab count
- Reliable across sessions
- Self-correcting

### How to Navigate to a Specific Field:

```
STRATEGY: Tab + Screenshot + Verify + Repeat until found

1. Take screenshot to see current field
2. Check field label - is this the field we want?
   - YES → Type the value, move to next field
   - NO → Press Tab, take another screenshot, repeat

3. Keep tabbing until you see the target field label
4. Visual confirmation: blue border around the field
5. Type the value
6. Move to next field in your list
```

### Example: Finding "First Name" Field

```bash
# Start: Form just opened, we're somewhere in the form

# Step 1: Where are we?
osascript -e 'tell application "Google Chrome" to activate'
# Take screenshot - see we're on "Merchant Token" field

# Step 2: Not First Name yet, keep tabbing
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot - see we're on "Current Situation" field

# Step 3: Still not First Name, keep tabbing
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot - see we're on "Need/Pain/Interest" field

# Keep repeating until...

# Step N: Found it!
# Take screenshot - see "First Name" label with blue border
osascript -e 'tell application "System Events" to keystroke "John"'
# Success! Now move to next field (Last Name)
```

### Field Order for Automation:

**Fill fields in this order** (matches form layout top-to-bottom):

1. **First Name** - Tab until you see "First Name" label
2. **Last Name** - Tab once from First Name (they're adjacent)
3. **Company** - Tab until you see "Company" label (required field)
4. **Email** - Tab until you see "Email" label
5. **Phone** - Tab until you see "Phone" label
6. **Industry** - Tab until you see "Industry" label (required field)
7. (Continue for other fields as needed)

### Visual Indicators to Look For:

- **Field label text** - "First Name", "Last Name", "Company", etc.
- **Blue border** - Shows which field is currently focused
- **Red border** - Shows required field that's empty
- **Section headers** - "Contact Information", "Business Information", etc.

### The Tab-and-Verify Loop:

```
REPEAT until target field found:
  1. Take screenshot
  2. Read field label
  3. Is this the target field?
     YES → Type value, move to next target
     NO  → Press Tab, go to step 1
```

### Why This Works:

✅ **Resilient** - Doesn't break when tab counts change  
✅ **Self-correcting** - Finds the field no matter where you start  
✅ **Visual confirmation** - Always know where you are  
✅ **No clicking** - Uses reliable Tab navigation  
✅ **Repeatable** - Works the same way every time  

### Important Notes:

- **Don't count tabs from the beginning** - Start wherever you are, find the field
- **Take screenshots frequently** - Visual confirmation is key
- **Read field labels** - That's how you know you're in the right place
- **Be patient** - It might take 5-10 tabs to find a field, that's OK
- **Trust the process** - This method is proven to work
- **NO CLICKING** - Tab navigation only, clicking doesn't work

---


---

## 🔍 Real-World Example: Finding the First Name Field

**This is a REAL example from an actual automation session showing how to find the First Name field.**

### The Challenge:
- Form was open but focus was somewhere unknown
- Tab count was unreliable (could be anywhere from Tab 10 to Tab 50+)
- Needed to find and fill the First Name field

### The Solution: Tab-and-Verify Loop

#### Step 1: Activate Chrome
```bash
osascript -e 'tell application "Google Chrome" to activate'
```
**Result**: Chrome window came to front

---

#### Step 2: Take Screenshot to See Current Position
```bash
# Take screenshot to see where we are
```
**What I Saw**: Form was visible, but couldn't tell which field had focus

---

#### Step 3: Start Tabbing Forward
```bash
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot
```
**What I Saw**: "Recent Items" link at bottom had blue underline - I was outside the form

---

#### Step 4: Continue Tabbing to Get Into Form
```bash
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot
```
**What I Saw**: URL bar had blue border - still in browser chrome, not form yet

---

#### Step 5: Keep Tabbing
```bash
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot
```
**What I Saw**: "View profile" button appeared - still in header area

---

#### Step 6: More Tabbing
```bash
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot
```
**What I Saw**: Form scrolled to top, showing Regulator Details section - now in form!

---

#### Step 7: Continue Tabbing Through Form
```bash
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot
```
**What I Saw**: Contact Information section visible! Could see First Name, Middle Name, Last Name fields

---

#### Step 8: Keep Tabbing
```bash
osascript -e 'tell application "System Events" to key code 48'
# Take screenshot
```
**What I Saw**: "DS Best Time to Call" dropdown had blue border - I went past First Name!

---

#### Step 9: Go Backwards with Shift+Tab
```bash
osascript -e 'tell application "System Events" to key code 48 using shift down'
# Take screenshot
```
**What I Saw**: **Middle Name field had blue border** - getting closer!

---

#### Step 10: One More Shift+Tab
```bash
osascript -e 'tell application "System Events" to key code 48 using shift down'
# Take screenshot
```
**What I Saw**: 🎉 **FIRST NAME FIELD HAS BLUE BORDER!** Found it!

---

### Step 11: Type the Value
```bash
osascript -e 'tell application "System Events" to keystroke "John"'
```
**Result**: "John" appeared in the First Name field ✅

---

### Key Lessons from This Real Example:

1. **Tab count was irrelevant** - It took ~10+ tabs to find First Name, but exact count doesn't matter
2. **Visual confirmation is critical** - Blue border told me when I found the field
3. **Shift+Tab is your friend** - When you overshoot, go backwards
4. **Be patient** - It took 10+ screenshots to find the field, that's normal
5. **The form scrolls automatically** - As you tab, Salesforce scrolls to show focused field
6. **No clicking needed** - Pure keyboard navigation worked perfectly

### Why This Works Every Time:

✅ **Doesn't rely on tab counts** - Works regardless of starting position  
✅ **Self-correcting** - If you overshoot, Shift+Tab backwards  
✅ **Visual confirmation** - Blue border proves you're in the right place  
✅ **Reliable** - No clicking that might miss the target  
✅ **Repeatable** - Same process works every session  

### The Pattern to Follow:

```
1. Activate Chrome
2. Take screenshot
3. LOOP:
   - Is this First Name field? (check for blue border + "First Name" label)
   - YES → Type value, done!
   - NO → Press Tab (or Shift+Tab if you went past it)
   - Take screenshot
   - Repeat LOOP
```

### Time Investment:
- **First time finding field**: ~2-3 minutes (10+ screenshots)
- **Subsequent times**: ~30 seconds (you know the general area)
- **Worth it?** YES! Reliable automation that works every time

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

**CRITICAL**: Two scenarios can happen when saving:

#### Scenario A: Successful Save (No Duplicates)
```
1. Tab forward until "Save" button has blue box indicator
2. Press Enter
3. Lead is created successfully
4. Form closes and returns to Leads list
```

#### Scenario B: Duplicate Detection Popup ⚠️

**If a duplicate lead exists, a POPUP will appear and PREVENT you from saving.**

**What Happens:**
- Modal dialog appears over the form
- Message: "Potential Duplicate Detected" or similar
- Shows existing lead(s) that match (by Company name, Phone, etc.)
- Buttons available: "Cancel", "Save Anyway", or "Merge"

**How to Handle:**
1. **Take screenshot** to see the duplicate popup
2. **Read the message** to understand what matched
3. **Navigate with Tab** to the appropriate button:
   - **Cancel** - Abort save, close popup, return to form (RECOMMENDED)
   - **Save Anyway** - Create duplicate lead despite warning
   - **Merge** - Merge with existing lead (if available)
4. **Press Enter** to select your choice

**Recommended Action:**
- Press Tab until "Cancel" button has blue border
- Press Enter to cancel
- Notify user: "Duplicate detected for [Company Name]. Lead not created."
- Log the duplicate in your report

**Visual Cues:**
- Popup appears as overlay on top of form
- Popup has its own Tab navigation (separate from form)
- Blue border indicates focused button in popup
- Background form is dimmed/disabled

---


## 📊 Field Mapping Reference

**CRITICAL: A complete field mapping document (`salesforce-field-mapping.md`) has been created that maps all 97 fields in the US Sales lead form.**

### Why This Matters:

The field mapping was created through a **one-time discovery process** where every field in the form was systematically documented. This means:

✅ **Future automation is FAST** - No need to explore the form again  
✅ **Field recognition over tab counting** - Know fields by their labels, not position  
✅ **Complete documentation** - All 9 sections and 97 fields mapped  
✅ **Required fields identified** - Know exactly what must be filled  

### Using the Field Mapping:

When filling out leads, refer to `salesforce-field-mapping.md` to:
1. **Identify which fields exist** in each section
2. **Recognize fields by their labels** (not tab counts)
3. **Know which fields are required** vs optional
4. **Understand field types** (text, dropdown, checkbox, etc.)

### The 9 Form Sections:

1. **Regulator Details** - Merchant Token
2. **Opportunity Description** - Current Situation, Business Type, Timeline, etc.
3. **Contact Information** - Name, Company (required), Phone, Email, Address
4. **Business Information** - Industry (required), Revenue, POS, Processor
5. **Lead Status** - Lead Status, Drip Date, Rating
6. **Next Steps** - Next Steps text, Next Step Date
7. **Social Media** - Facebook, Twitter, Instagram, LinkedIn, etc.
8. **Routing Information** - Lead Source, Source Detail, Email Opt Out
9. **System Information** - Lead Type (defaults to "Sales")

### Required Fields (Minimum to Save):

1. **Last Name** (Contact Information)
2. **Company** (Contact Information)
3. **Industry** (Business Information)
4. **Lead Currency** (Business Information) - defaults to USD
5. **Lead Status** (Lead Status) - defaults to Open
6. **Lead Type** (System Information) - defaults to Sales

### Field Recognition Tips:

**Don't count tabs!** Instead, recognize fields by:
- **Section headers** - Bold, larger text (e.g., "Contact Information")
- **Field labels** - Text above or beside input fields
- **Required indicators** - Red asterisk (*) and red borders when empty
- **Visual cues** - Blue border = focused, Red border = required & empty
- **Field types** - Dropdowns show arrows, text areas are taller, checkboxes are squares

### Why Tab Counts Change:

Tab order can vary based on:
- Which fields are visible/hidden
- Field dependencies (e.g., Sub-Industry depends on Industry)
- What's already filled in
- Browser state and focus

**The solution**: Recognize fields by their labels and visual appearance, not by counting tabs from the start.

### Time Savings:

- **Initial mapping**: 30+ minutes (one-time discovery)
- **Future lead entry**: 2-3 minutes per lead (using the mapping)

**The mapping document makes all future automation fast and reliable.**

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
