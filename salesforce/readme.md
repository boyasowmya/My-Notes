# <span style="color:#CD5C5C;display:block;text-align:center;">Salesforce Objects</span>

## <span style="color:#005A9C">Topics</span>
---
1. [**What is a Salesforce Object?**](#what-is-a-salesforce-object)
2. [**Creating Custom Objects**](#creating-custom-objects)
3. [**Step-by-Step Process**](#step-by-step-process)
4. [**Key Configuration Options**](#key-configuration-options)
5. [**Best Practices**](#best-practices)

---

## <span style="color:#005A9C">What is a Salesforce Object?</span>

An object in Salesforce is like a **container** or **database table** where we store all related information about people, products, or any business data.

**Think of it like:**
- A filing cabinet with organized folders
- Each object = one type of folder (Accounts, Contacts, Products)
- Records = individual files in each folder

**Examples:**
- **Account Object:** Stores company information
- **Contact Object:** Stores person details  
- **Opportunity Object:** Stores sales deals
- **Custom Object:** Your own unique data container

> **💡 Tip:** Objects are the foundation of Salesforce - everything you see and work with is stored in objects!

---

## <span style="color:#005A9C">Creating Custom Objects</span>

Custom objects let you store data that's specific to your business needs beyond the standard Salesforce objects.

**When to create custom objects:**
- Track products not covered by standard objects
- Store unique business processes
- Manage custom workflows
- Connect related data together

---

## <span style="color:#005A9C">Step-by-Step Process</span>

Here's how to create a custom object in Salesforce:

### 1. Navigate to Setup
```
Setup → Search "Object" → Object Manager
```

### 2. Create New Custom Object
```
Click "Create" → "Custom Object"
```

### 3. Fill Mandatory Fields

| Field | Description | Example |
|-------|-------------|---------|
| **Label** | Display name for users | "Product Inventory" |
| **Plural Label** | Multiple form | "Product Inventories" |
| **Object Name** | API name (auto-generated) | "Product_Inventory__c" |
| **Description** | What this object stores | "Tracks warehouse inventory items" |

### 4. Configure Settings

**Required Configurations:**
- **Record Name:** Choose format (Text or Auto-Number)
- **Data Type:** Text or Auto Number
- **Display Format:** For auto-numbers (e.g., INV-{0000})

**Example Auto-Number Setup:**
```yaml
Display Format: "PROD-{0000}"
Starting Number: 1
Result: PROD-0001, PROD-0002, etc.
```

### 5. Set Profile Permissions
```
✅ Allow Read access for specific profiles
✅ Allow Create/Edit for admin profiles  
✅ Allow Delete for admin only
```

### 6. Tab Visibility Options
- **✅ Include Tab:** Shows object in app navigation
- **❌ Don't Include Tab:** Object exists but no direct tab access
- **📱 Mobile Ready:** Available in Salesforce mobile app

### 7. Save and Deploy
```
Click "Save" → Object is created and ready to use
```

---

## <span style="color:#005A9C">Key Configuration Options</span>

### Tab Settings
| Option | When to Use | Example |
|--------|-------------|---------|
| **Default On** | Frequently used objects | Customer Orders |
| **Default Off** | Admin-only objects | System Logs |
| **Tab Hidden** | Background objects | Junction Objects |

### Security Settings
```yaml
Profiles with Access:
  - System Administrator: Full Access
  - Sales Users: Read/Create
  - Marketing Users: Read Only
  - Custom Profiles: As needed
```

---
