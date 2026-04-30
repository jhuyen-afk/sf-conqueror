# Salesforce Lead Entry - Data Handling Rules

**Last Updated**: 2025-01-29

This document defines the **BUSINESS RULES** for handling missing or incomplete data when filling out Salesforce leads from a CSV template.

---

## 🎯 Core Principle

**Reps may not have all information on hand.** Use these fallback rules to complete leads even with incomplete data.

---

## 📋 Field-by-Field Data Rules

### 1. First Name
**Rule**: If First Name is empty in the template:
- **Use Company Name instead**
- Example: If Company = "Acme Corp" and First Name is empty → Fill First Name with "Acme Corp"

**Why**: Salesforce requires a name in the contact fields. Using the company name ensures the lead can be saved.

```
Template: First Name = "" (empty)
Template: Company = "Acme Corp"
Action: Fill First Name with "Acme Corp"
```

---

### 2. Last Name
**Rule**: If Last Name is empty in the template:
- **Use "Team" as the last name**
- Example: First Name = "Acme Corp", Last Name = empty → Fill Last Name with "Team"

**Why**: Creates a generic contact name like "Acme Corp Team" when individual contact info is unavailable.

```
Template: Last Name = "" (empty)
Action: Fill Last Name with "Team"
Result: Full name becomes "[Company Name] Team" or "Team"
```

---

### 3. Email
**Rule**: If Email is empty in the template:
- **Skip filling out the Email field**
- Leave it blank
- Do NOT use a placeholder or fake email

**Why**: Better to have no email than incorrect/fake data. Sales reps can add it later.

```
Template: Email = "" (empty)
Action: Skip the Email field (leave blank)
```

---

### 4. Revenue Range
**Rule**: If Revenue Range is empty or "None" in the template:
- **Skip filling out the Revenue Range field**
- Leave it as "--None--" (default)

**Why**: Revenue Range is optional. Reps may not have this financial information during initial lead capture.

```
Template: Revenue Range = "" (empty) OR "None"
Action: Skip the Revenue Range field (leave as "--None--")
```

---

### 5. Expected Annual GPV (Gross Payment Volume)
**Rule**: If Expected Annual GPV is empty in the template:
- **Skip filling out the Expected Annual GPV field**
- Leave it blank

**Why**: GPV is a projection that reps may not have during initial outreach. Can be added later.

```
Template: Expected Annual GPV = "" (empty)
Action: Skip the Expected Annual GPV field (leave blank)
```

---

## 📊 Complete Data Handling Matrix

| Field | If Empty in Template | Action | Example |
|-------|---------------------|--------|---------|
| **First Name** | Empty | Use Company Name | Company="Acme" → First Name="Acme" |
| **Last Name** | Empty | Use "Team" | Last Name="Team" |
| **Email** | Empty | Skip (leave blank) | Email field remains empty |
| **Revenue Range** | Empty or "None" | Skip (leave as "--None--") | Dropdown stays at "--None--" |
| **Expected Annual GPV** | Empty | Skip (leave blank) | GPV field remains empty |
| **Company** | Empty | ❌ ERROR - Cannot proceed | Company is REQUIRED |
| **Phone** | Empty | ❌ ERROR - Cannot proceed | Phone is REQUIRED |
| **Street** | Empty | ❌ ERROR - Cannot proceed | Street is REQUIRED |
| **City** | Empty | ❌ ERROR - Cannot proceed | City is REQUIRED |
| **State/Province** | Empty | ❌ ERROR - Cannot proceed | State is REQUIRED |
| **Zip/Postal Code** | Empty | ❌ ERROR - Cannot proceed | Zip is REQUIRED |
| **Country** | Empty | ❌ ERROR - Cannot proceed | Country is REQUIRED |
| **Industry** | Empty or "None" | ❌ ERROR - Cannot proceed | Industry is REQUIRED |

---

## ✅ Required vs Optional Fields

### REQUIRED (Cannot be empty):
1. ~~First Name~~ - Can use Company Name as fallback
2. ~~Last Name~~ - Can use "Team" as fallback
3. **Company** - MUST have value
4. **Phone** - MUST have value
5. **Street** - MUST have value
6. **City** - MUST have value
7. **State/Province** - MUST have value
8. **Zip/Postal Code** - MUST have value
9. **Country** - MUST have value
10. **Industry** - MUST have value (cannot be "--None--")

### OPTIONAL (Can skip if empty):
- Email
- Revenue Range
- Expected Annual GPV
- All other fields

---

## 🤖 Automation Logic

### Pseudocode for Goose AI:

```python
# Read CSV row
row = read_csv_row()

# Handle First Name
if row['First Name'] is empty:
    first_name = row['Company']  # Use company name
else:
    first_name = row['First Name']

# Handle Last Name
if row['Last Name'] is empty:
    last_name = "Team"  # Use "Team"
else:
    last_name = row['Last Name']

# Handle Email
if row['Email'] is empty:
    skip_email_field()  # Leave blank
else:
    email = row['Email']

# Handle Revenue Range
if row['Revenue Range'] is empty or row['Revenue Range'] == "None":
    skip_revenue_range_field()  # Leave as "--None--"
else:
    revenue_range = row['Revenue Range']

# Handle Expected Annual GPV
if row['Expected Annual GPV'] is empty:
    skip_gpv_field()  # Leave blank
else:
    gpv = row['Expected Annual GPV']

# Validate REQUIRED fields
if row['Company'] is empty:
    raise Error("Company is required")
if row['Phone'] is empty:
    raise Error("Phone is required")
if row['Industry'] is empty or row['Industry'] == "None":
    raise Error("Industry is required")
# ... (validate all required fields)

# Fill out the form
fill_field("First Name", first_name)
fill_field("Last Name", last_name)
if email:
    fill_field("Email", email)
# ... (continue with other fields)
```

---

## 📝 CSV Template Format

### Example CSV with Missing Data:

```csv
First Name,Last Name,Company,Phone,Email,Street,City,State/Province,Zip/Postal Code,Country,Industry,Revenue Range,Expected Annual GPV
,,"Acme Corp",555-1234,,123 Main St,San Francisco,CA,94102,USA,Food and Drink,,
John,Doe,Beta LLC,555-5678,john@beta.com,456 Oak Ave,Austin,TX,78701,USA,Health,1M-5M,2500000
,,"Gamma Inc",555-9999,,789 Pine Rd,Seattle,WA,98101,USA,Beauty,None,
```

### How Goose Should Fill:

**Row 1 (Acme Corp):**
- First Name: "Acme Corp" (used Company name)
- Last Name: "Team" (used fallback)
- Email: Skip (leave blank)
- Revenue Range: Skip (leave as "--None--")
- Expected Annual GPV: Skip (leave blank)

**Row 2 (Beta LLC):**
- First Name: "John" (provided)
- Last Name: "Doe" (provided)
- Email: "john@beta.com" (provided)
- Revenue Range: "1M-5M" (provided)
- Expected Annual GPV: "2500000" (provided)

**Row 3 (Gamma Inc):**
- First Name: "Gamma Inc" (used Company name)
- Last Name: "Team" (used fallback)
- Email: Skip (leave blank)
- Revenue Range: Skip (says "None")
- Expected Annual GPV: Skip (leave blank)

---

## 🚨 Error Handling

### If REQUIRED fields are missing:
1. **Log the error** with row number and missing field
2. **Skip that row** and continue to next lead
3. **Report at the end** which rows failed and why

### Example Error Log:
```
Row 5: ERROR - Missing required field 'Company'
Row 12: ERROR - Missing required field 'Phone'
Row 18: ERROR - Missing required field 'Industry'

Summary:
- Total rows: 50
- Successful: 47
- Failed: 3
```

---

## 💡 Best Practices

1. **Validate CSV before starting** - Check for required fields
2. **Use fallback rules consistently** - Always use "Team" for missing last name
3. **Don't invent data** - If Email is missing, leave it blank (don't use placeholder@example.com)
4. **Log everything** - Track which fallback rules were used for each lead
5. **Report to user** - Show summary of how many leads used fallbacks

---

## 🔄 Future Enhancements

Consider adding:
- **Phone number validation** - Check format before filling
- **Email validation** - Verify email format if provided
- **Industry mapping** - Map common industry names to Salesforce verticals
- **Duplicate detection** - Check if company already exists before creating lead
- **Batch reporting** - Generate summary report after bulk upload

---

## 📚 Related Documents

- **salesforce-required-fields.md** - Complete list of required fields
- **salesforce-field-mapping.md** - All 97 fields mapped
- **salesforce-automation-guide.md** - Setup and workflow guide
- **future-improvements.md** - Known challenges and roadmap

---

**End of Data Handling Rules**
