---
title: "Permissions Reference" 
linkTitle: "Permissions"
weight: 10
type: docs
description: >
  Complete permission set documentation including role-based access control, security model, and user assignment guidelines.
---

## Permissions Overview

BRC Risk Management implements a least-privilege security model with three permission sets providing granular access control based on user roles and responsibilities.

### Security Principles

- **Least Privilege**: Users receive only the permissions they need for their role
- **Role-Based Access**: Permissions align with business functions and job responsibilities
- **Extensible**: Permission sets can be combined with other Business Central permissions
- **Auditable**: All data access and modifications are logged for security auditing

### Permission Set Hierarchy

```
BRC RISK - ADMIN
    ├── All BRC RISK - EDIT permissions
    └── Setup and configuration rights

BRC RISK - EDIT  
    ├── All BRC RISK - VIEW permissions
    └── Create/modify operational data

BRC RISK - VIEW
    └── Read-only access to risk data
```

## Permission Sets Detail

### BRC RISK - VIEW (Read-Only Access)

**Purpose:** Read-only access to risk data for general users and executives who need risk visibility without data modification capabilities.

**Target Users:**
- General staff needing risk visibility
- Executives reviewing risk reports  
- Customer service representatives
- Sales staff checking customer risk before quotes
- Finance staff reviewing vendor risk levels

**Permissions Granted:**

| Object Type | Object Name | Read | Insert | Modify | Delete |
|-------------|-------------|------|--------|--------|--------|
| **Tables** |
| Table | Business Entity | ✅ | ❌ | ❌ | ❌ |
| Table | Risk Level | ✅ | ❌ | ❌ | ❌ |
| Table | Risk Watch List | ✅ | ❌ | ❌ | ❌ |
| Table | Risk Watch List Line | ✅ | ❌ | ❌ | ❌ |
| Table | API Call Ledger | ✅* | ❌ | ❌ | ❌ |
| Table | Risk Setup | ✅** | ❌ | ❌ | ❌ |
| **Pages** |
| Page | Business Entity List | ✅ | ❌ | ❌ | ❌ |
| Page | Business Entity Card | ✅ | ❌ | ❌ | ❌ |
| Page | Risk Watchlists | ✅ | ❌ | ❌ | ❌ |
| Page | Risk Manager Role Center | ✅ | - | - | - |
| Page | Customer Card (Risk FactBox) | ✅ | - | - | - |
| Page | Vendor Card (Risk FactBox) | ✅ | - | - | - |

*API Call Ledger shows sanitized data with API keys masked  
**Risk Setup read-only for display purposes, no sensitive data access

**Functional Capabilities:**
- ✅ View business entities and their risk levels
- ✅ See risk indicators on Customer/Vendor cards and lists
- ✅ View watchlists and their current matches
- ✅ Review API call history (with sensitive data masked)
- ✅ Access Risk Manager Role Center in view-only mode
- ✅ Generate and view risk-related reports
- ❌ Cannot create or edit entities
- ❌ Cannot fetch new risk data from API
- ❌ Cannot modify watchlists or criteria
- ❌ Cannot access configuration or setup pages

**Use Case Examples:**
- Sales representative checking customer credit score before preparing quote
- Executive reviewing high-risk customer portfolio in monthly reports
- Customer service agent understanding risk context during support calls
- Finance manager reviewing vendor risk levels for payment terms decisions

### BRC RISK - EDIT (Standard Operational Access)

**Purpose:** Full operational access for users who actively manage risk data and monitoring processes.

**Target Users:**
- Risk analysts and credit managers
- Operations managers handling customer/vendor relationships
- Accounts receivable/payable staff
- Treasury staff managing financial exposure

**Permissions Granted:**

*Includes all BRC RISK - VIEW permissions, plus:*

| Object Type | Object Name | Read | Insert | Modify | Delete |
|-------------|-------------|------|--------|--------|--------|
| **Tables** |
| Table | Business Entity | ✅ | ✅ | ✅ | ✅ |
| Table | Risk Watch List | ✅ | ✅ | ✅ | ✅ |
| Table | Risk Watch List Line | ✅ | ✅ | ✅ | ✅ |
| **Actions & Codeunits** |
| Action | Fetch Risk Data | Execute | - | - | - |
| Action | Link to Entity | Execute | - | - | - |
| Action | Add to Watchlist | Execute | - | - | - |
| Codeunit | Risk Data Fetcher | Execute | - | - | - |
| Codeunit | Entity Linking Manager | Execute | - | - | - |
| Codeunit | Watchlist Manager | Execute | - | - | - |

**Additional Functional Capabilities:**
- ✅ Create and edit business entities manually
- ✅ Trigger risk data fetches from API
- ✅ Link customers and vendors to business entities
- ✅ Create and manage watchlists with custom criteria
- ✅ Add entities to existing watchlists
- ✅ Evaluate watchlists manually for immediate results
- ✅ Modify entity update schedules and preferences
- ❌ Cannot modify risk level definitions or thresholds
- ❌ Cannot access API configuration or credentials
- ❌ Cannot change system-wide setup parameters
- ❌ Cannot manage Job Queue entries for automation

**Use Case Examples:**
- Credit analyst creating new business entity for large customer
- Risk manager setting up watchlist to monitor entities with debt over €100k
- AR manager fetching updated credit scores for overdue accounts
- Operations manager linking newly created vendor to risk monitoring

### BRC RISK - ADMIN (Full Administrative Access)

**Purpose:** Complete administrative access for system configuration, setup, and maintenance.

**Target Users:**
- Risk management administrators
- Business Central application administrators
- IT administrators responsible for system configuration
- Implementation consultants during setup

**Permissions Granted:**

*Includes all BRC RISK - EDIT permissions, plus:*

| Object Type | Object Name | Read | Insert | Modify | Delete |
|-------------|-------------|------|--------|--------|--------|
| **Tables** |
| Table | Risk Setup | ✅ | ✅ | ✅ | ❌* |
| Table | Risk Level | ✅ | ✅ | ✅ | ✅ |
| Table | Risk Level Threshold | ✅ | ✅ | ✅ | ✅ |
| Table | API Call Ledger | ✅ | ❌ | ❌ | ✅** |
| **Pages & Setup** |
| Page | Risk Setup Card | ✅ | - | ✅ | - |
| Page | Risk Level List/Card | ✅ | ✅ | ✅ | ✅ |
| Page | Assisted Setup | Execute | - | - | - |
| **Codeunits & Administration** |
| Codeunit | API Client | Execute | - | - | - |
| Codeunit | Job Queue Helper | Execute | - | - | - |
| Codeunit | Risk Setup Management | Execute | - | - | - |
| Codeunit | System Diagnostics | Execute | - | - | - |

*Risk Setup record cannot be deleted (system integrity)  
**API Call Ledger cleanup for maintenance purposes

**Administrative Capabilities:**
- ✅ Configure API provider settings and credentials
- ✅ Create and modify risk level definitions and styling
- ✅ Set up automatic risk level thresholds and calculations
- ✅ Run assisted setup wizard for initial configuration
- ✅ Test API connectivity and troubleshoot integration issues
- ✅ Configure Job Queue entries for scheduled operations
- ✅ Delete old API call ledger entries for maintenance
- ✅ View complete API logs including sensitive data (when appropriate)
- ✅ Configure notification settings and webhook endpoints
- ✅ Manage telemetry and Application Insights integration
- ✅ Export/import configuration for environment setup

**Use Case Examples:**
- Administrator performing initial system setup after installation
- IT administrator configuring TIC API integration with credentials
- Risk admin creating custom risk levels for industry-specific requirements
- Admin setting up automated nightly risk data updates via Job Queue
- Administrator troubleshooting API connectivity issues

## Role-Based Assignment Guidelines

### Assignment Recommendations

| User Role | Recommended Permission Set | Rationale |
|-----------|---------------------------|-----------|
| **Business Users** |
| Executive/C-Level | BRC RISK - VIEW | Strategic oversight, no operational needs |
| Sales Representative | BRC RISK - VIEW | Check customer risk before quotes |
| Customer Service Rep | BRC RISK - VIEW | Understand customer context |
| Finance Manager | BRC RISK - VIEW or EDIT* | Analysis needs, may require data updates |
| **Operational Users** |
| Credit Analyst | BRC RISK - EDIT | Active risk data management |
| Risk Manager | BRC RISK - EDIT or ADMIN* | Depends on setup responsibilities |
| AR/AP Manager | BRC RISK - EDIT | Monitor payment risk, fetch updates |
| Treasury Staff | BRC RISK - EDIT | Manage financial exposure |
| **System Users** |
| Application Admin | BRC RISK - ADMIN | System configuration and maintenance |
| IT Administrator | BRC RISK - ADMIN | Technical setup and troubleshooting |
| Implementation Consultant | BRC RISK - ADMIN | Initial setup and configuration |

*Role may require higher permission set depending on organization structure

### Permission Assignment Process

#### Via Business Central User Interface

1. **Access User Management**
   - Search for **"Users"** in Business Central
   - Open the **Users** page

2. **Select User**
   - Find the specific user in the list
   - Click on the user to open the User Card

3. **Assign Permission Set**
   - Navigate to **User Permission Sets** section
   - Click **New** to add permission set
   - Select appropriate **BRC RISK** permission set
   - Set **Company** scope (leave blank for all companies)
   - Click **OK** to confirm

4. **Verify Assignment**
   - Confirm permission set appears in user's list
   - Test user access to ensure proper functionality

#### Via PowerShell (Bulk Assignment)

```powershell
# Example: Assign BRC RISK - VIEW to multiple sales users
$Users = @("sales1@company.com", "sales2@company.com", "sales3@company.com")
foreach ($User in $Users) {
    Add-NAVUserPermissionSet -ServerInstance BC240 -UserName $User -PermissionSetId "BRC RISK - VIEW"
}
```

### Permission Validation

#### Testing User Access

**For VIEW Users:**
- [ ] Can open Business Entity List (read-only)
- [ ] Can see risk indicators on Customer/Vendor cards
- [ ] Cannot access Risk Setup pages
- [ ] Cannot execute "Fetch Risk Data" actions

**For EDIT Users:**  
- [ ] Can create and modify Business Entities
- [ ] Can execute "Fetch Risk Data" from Customer/Vendor cards
- [ ] Can create and manage Watchlists
- [ ] Cannot access Risk Setup configuration

**For ADMIN Users:**
- [ ] Can access Risk Setup page and modify settings
- [ ] Can create/modify Risk Levels
- [ ] Can run Assisted Setup wizard
- [ ] Can view complete API logs and diagnostics

### Security Considerations

#### Sensitive Data Access

**API Credentials:**
- Only ADMIN users can view/modify API keys and endpoints
- API Call Ledger masks sensitive data for VIEW/EDIT users
- Audit trail tracks all configuration changes

**Customer/Vendor Data:**
- Risk data access follows standard BC Customer/Vendor permissions
- Users must have appropriate BC permissions for linked records
- Risk data supplements but doesn't override BC security

#### Compliance Requirements

**Data Protection:**
- Permission sets respect GDPR data access requirements
- Audit trail logs all data access and modifications
- Personal data access follows standard BC compliance framework

**Financial Regulations:**
- Risk data access aligns with financial compliance needs
- Segregation of duties maintained between operational and administrative users
- Audit capabilities support regulatory reporting requirements

### Troubleshooting Permissions

#### Common Issues

**User Cannot See Risk Data:**
1. Verify BRC RISK permission set is assigned
2. Check underlying Customer/Vendor table permissions
3. Confirm user has company access where data exists
4. Validate risk data exists for the entities being viewed

**User Cannot Fetch Risk Data:**
1. Confirm user has BRC RISK - EDIT or ADMIN permission set
2. Verify API configuration is complete (ADMIN task)
3. Check Job Queue permissions for background processing
4. Validate network connectivity and API credentials

**Setup Pages Not Accessible:**
1. Verify user has BRC RISK - ADMIN permission set
2. Check for conflicting permission sets that might restrict access
3. Confirm user session hasn't timed out
4. Validate Business Central version compatibility

#### Permission Conflicts

**Overlapping Permission Sets:**
- BRC RISK permission sets can be combined with standard BC sets
- Higher permission levels (ADMIN) automatically include lower levels
- Custom permission sets should not conflict with BRC RISK objects

**Object-Level Conflicts:**
- Ensure no custom permission sets restrict access to BRC objects (70000-70099)
- Validate table extension permissions don't conflict with base Customer/Vendor access
- Check for company-specific permission restrictions

---

*For implementation questions or permission assignment assistance, refer to the [Support](../#support) section or contact your Business Central administrator.*