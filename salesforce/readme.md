# <span style="color:#CD5C5C;display:block;text-align:center;">Salesforce Objects</span>

## <span style="color:#005A9C">Topics</span>
---
1. [**Understanding Salesforce Objects**](#understanding-salesforce-objects)
   - [What is a Salesforce Object?](#what-is-a-salesforce-object)
   - [Types of Objects](#types-of-objects)
2. [**Creating Custom Objects**](#creating-custom-objects)
   - [Step-by-Step Process](#step-by-step-process)
   - [Configuration Options](#configuration-options)
   - [Security and Permissions](#security-and-permissions)
3. [**Best Practices**](#best-practices)
   - [Naming Conventions](#naming-conventions)
   - [Performance Considerations](#performance-considerations)

---

## <span style="color:#005A9C">Understanding Salesforce Objects</span>

### What is a Salesforce Object?

An object in Salesforce is like a **container** or **database table** where we store all related information about people, products, or any business data.

**Think of it like:**
- A filing cabinet with organized folders
- Each object = one type of folder (Accounts, Contacts, Products)
- Records = individual files in each folder

> **💡 Tip:** Objects are the foundation of Salesforce - everything you see and work with is stored in objects!

### Types of Objects

**Standard Objects (Built-in):**
- **Account Object:** Stores company information
- **Contact Object:** Stores person details  
- **Opportunity Object:** Stores sales deals
- **Lead Object:** Stores potential customers

**Custom Objects (Your Creation):**
- Your own unique data containers
- Built for specific business needs
- End with "__c" (e.g., Product_Inventory__c)

---

## <span style="color:#005A9C">Creating Custom Objects</span>

Custom objects let you store data that's specific to your business needs beyond the standard Salesforce objects.

**When to create custom objects:**
- Track products not covered by standard objects
- Store unique business processes
- Manage custom workflows
- Connect related data together

### Step-by-Step Process

Here's how to create a custom object in Salesforce:

#### 1. Navigate to Setup
```
Setup → Search "Object" → Object Manager
```

#### 2. Create New Custom Object
```
Click "Create" → "Custom Object"
```

#### 3. Fill Mandatory Fields

| Field | Description | Example |
|-------|-------------|---------|
| **Label** | Display name for users | "Product Inventory" |
| **Plural Label** | Multiple form | "Product Inventories" |
| **Object Name** | API name (auto-generated) | "Product_Inventory__c" |
| **Description** | What this object stores | "Tracks warehouse inventory items" |

### Configuration Options

#### Record Name Settings
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

#### Tab Visibility Options
- **✅ Include Tab:** Shows object in app navigation
- **❌ Don't Include Tab:** Object exists but no direct tab access
- **📱 Mobile Ready:** Available in Salesforce mobile app

**Tab Settings:**
| Option | When to Use | Example |
|--------|-------------|---------|
| **Default On** | Frequently used objects | Customer Orders |
| **Default Off** | Admin-only objects | System Logs |
| **Tab Hidden** | Background objects | Junction Objects |

### Security and Permissions

#### Profile Permissions
```
✅ Allow Read access for specific profiles
✅ Allow Create/Edit for admin profiles  
✅ Allow Delete for admin only
```

#### Security Settings Example
```yaml
Profiles with Access:
  - System Administrator: Full Access
  - Sales Users: Read/Create
  - Marketing Users: Read Only
  - Custom Profiles: As needed
```

#### Final Step
```
Click "Save" → Object is created and ready to use
```

---

## <span style="color:#005A9C">Navigation Types</span>

### Console Navigation vs Standard Navigation

| Navigation Type | Description | Use Case |
|-----------------|-------------|----------|
| **Console Navigation** | Opens records in different tabs for easy viewing | Multi-tasking, comparing records |
| **Standard Navigation** | Opens all records in the same single tab | Simple navigation, less complex workflows |

### Application Creation Process

**Steps to Create Lightning App:**
```
Setup → App Manager → New Lightning App → Create New App → Create Skill Horizon
```

---

## <span style="color:#005A9C">Field Types & Data Management</span>

### Field Data Types Overview

**Core Field Types:**
- **Picklist:** Single-selection dropdown values
- **Global Picklist:** Reusable picklist across multiple objects
- **Multi-Select Picklist:** Multiple-selection dropdown values  
- **Formula Fields:** Calculated fields based on other field values

### Advanced Field Configurations

#### Dependent Picklist Setup
```yaml
Navigation: Object → Field Relationships → Dependent Field → Create New
Configuration:
  - Controller Field: Parent picklist that controls values
  - Dependent Field: Child picklist with filtered values
```

**Example Use Case:**
- Controller: Country (USA, Canada, UK)
- Dependent: State/Province (filtered by country selection)

---

## <span style="color:#005A9C">Relationship Fields</span>

Both Lookup and Master-Detail relationships follow **one-to-many** patterns but have key differences:

### Lookup Relationship

**Characteristics:**
- ✅ **Independent:** Child records exist independently
- ✅ **Flexible:** Parent deletion doesn't affect child records
- ✅ **Creation:** Lookup field created on child object
- ❌ **No Rollup Summary:** Cannot create rollup summary fields

**Use Case Example:**
```yaml
Scenario: Contact → Account relationship
Result: If Account is deleted, Contact remains in system
```

### Master-Detail Relationship

**Characteristics:**
- 🔗 **Dependent:** Strong parent-child dependency
- ⚠️ **Cascading Delete:** Parent deletion removes all child records
- 📊 **Rollup Summary:** Supports aggregation from child to parent
- 🎯 **One-to-Many:** Follows strict hierarchical structure
- ⚙️ **Creation:** Master-Detail field created on child object

#### Rollup Summary Features
**Available Operations:**
- **COUNT:** Number of child records
- **SUM:** Total of numeric values
- **MIN:** Minimum value from child records  
- **MAX:** Maximum value from child records

#### Implementation Notes
> **⚠️ Important:** Cannot directly create Master-Detail on existing records

**Migration Process:**
```yaml
Step 1: Create Lookup relationship first
Step 2: Populate all mandatory fields in existing records
Step 3: Convert Lookup to Master-Detail relationship
```

### Many-to-Many Relationship

**Concept Overview:**
Many-to-many relationships connect records where each record in one object can relate to multiple records in another object, and vice versa.

#### Implementation via Junction Object

**Key Characteristics:**
- 🔗 **Junction Object:** Bridge object that creates the many-to-many connection
- 📊 **Schema Builder:** Visual tool for viewing relationship graphically
- ⚙️ **Creation:** Junction object contains two Master-Detail relationships
- 🎯 **Location:** Junction object created as separate entity, not on child objects

#### Practical Example: Student-Course Enrollment

**Scenario Setup:**
```yaml
Business Need:
  - One student can enroll in many courses
  - One course can have many students enrolled
  
Solution Structure:
  - Student Object (Master)
  - Course Object (Master)  
  - Enrollment Object (Junction)
```

**Relationship Structure:**
| Object | Relationship Type | Connected To | Purpose |
|---------|------------------|--------------|----------|
| **Student** | Master | → Enrollment | Controls student enrollments |
| **Course** | Master | → Enrollment | Controls course registrations |
| **Enrollment** | Junction | ↔ Student + Course | Bridge connecting both objects |

#### Schema Builder Navigation
```
Setup → Schema Builder → Visual relationship mapping
Benefit: Graphical representation of all object relationships
```

**Junction Object Benefits:**
- ✅ **Flexibility:** Supports complex many-to-many scenarios
- ✅ **Data Integrity:** Maintains referential integrity through Master-Detail
- ✅ **Additional Fields:** Can store relationship-specific data (enrollment date, grade, etc.)
- ✅ **Rollup Summaries:** Supports aggregation on both parent objects

---

## <span style="color:#005A9C">Learning Progress Log</span>

### December 18, 2025
**Topics Covered:**
- Field data types fundamentals
- Picklist variations and implementations
- Formula field basics

### December 22, 2025  
**Topics Covered:**
- Advanced formula field techniques
- Dependent picklist configuration
- List view management
- Relationship field deep-dive

### December 24, 2025
**Topics Covered:**
- Many-to-many relationship concepts
- Junction object implementation
- Schema Builder for visual relationship mapping
- Student-Course enrollment example
- Junction object creation best practices

---