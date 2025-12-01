---
title: "Installation Steps"
linkTitle: "Installation"
weight: 20
type: docs
description: >
  Detailed AppSource installation procedures and verification steps for BRC Risk Management.
---

## Installation Overview

BRC Risk Management installs as a standard Business Central extension through Microsoft AppSource. The installation process includes app deployment, table creation, and initial data setup.

## Step-by-Step Installation

### 1. Access AppSource

**Via Business Central:**
1. Open your Business Central environment
2. Search for **"Extension Management"**
3. Click **Extension Management** to open the page
4. Select **Extension Marketplace** or **Browse Extensions**

**Via Web Browser:**
1. Navigate to [Microsoft AppSource](https://appsource.microsoft.com/)
2. Search for **"BRC Risk Management"** 
3. Select **Dynamics 365 Business Central** as the product

### 2. Locate BRC Risk Management

**Search Criteria:**
- **App Name**: "BRC Risk Management" or "BrightCom Risk"
- **Publisher**: BrightCom Solutions AB
- **Category**: Risk Management / Financial Management
- **Version**: 1.0.0.0 or later

**Verification Points:**
- ✅ Publisher name matches exactly: "BrightCom Solutions AB"  
- ✅ App description mentions risk assessment and TIC integration
- ✅ Compatible with Business Central 26.0+
- ✅ Reviews and ratings from verified customers

### 3. Install the Extension

**From AppSource Website:**
1. Click **Get it now** or **Free Trial** button
2. Sign in with your Microsoft account (Business Central admin)
3. Select your Business Central environment from dropdown
4. Click **Install** to confirm
5. Review app permissions and data access requirements
6. Click **Accept** to proceed with installation

**From Business Central Extension Management:**
1. Click **Install** on the app listing
2. Review installation requirements and permissions
3. Click **Accept** to confirm installation
4. Monitor installation progress

### 4. Monitor Installation Progress

**Installation Steps:**
1. **Download** - App package downloaded to environment (30-60 seconds)
2. **Deploy** - Extension deployed to Business Central (1-2 minutes)
3. **Install** - Database objects created and configured (2-3 minutes)
4. **Initialize** - Initial data and setup records created (30 seconds)

**Progress Indicators:**
- Extension Management shows installation status
- Email notification sent upon completion
- Extension appears in installed extensions list

## Installation Verification

### 1. Extension Management Check

1. Open **Extension Management**
2. Verify **BRC Risk Management** appears in the list
3. Check installation details:
   - **Status**: Installed
   - **Version**: 1.0.0.0
   - **Publisher**: BrightCom Solutions AB
   - **Runtime Version**: 15.0

### 2. Navigation Verification

Confirm the following navigation items are available:

**Search Navigation:**
- Search for "Risk" shows Risk-related pages
- Search for "Business Entity" shows entity management
- Search for "Risk Setup" shows configuration page

**Menu Navigation:**
- Role Explorer shows "Risk Manager" role center
- Departments → Financial Management → Risk Management

### 3. Page Accessibility

**Test Page Access:**
1. **Risk Setup** page opens without errors
2. **Business Entity List** page displays (empty initially)
3. **Risk Manager Role Center** loads with default layout
4. **Customer Card** shows Risk-related FactBox
5. **Vendor Card** shows Risk-related FactBox

### 4. Permission Verification

**Test User Access:**
1. Assign "BRC RISK - VIEW" permission set to test user
2. Verify user can access Risk-related pages in read-only mode
3. Test "BRC RISK - EDIT" permission for operational users
4. Confirm "BRC RISK - ADMIN" works for setup and configuration

### 5. Database Objects Check

The installation creates the following primary objects:

**Tables Created:**
- Business Entity (70000)
- Risk Setup (70004) 
- Risk Watch List (70005)
- API Call Ledger (70010)
- Risk Level (70015)

**Pages Created:**
- Risk Setup Card (70020)
- Business Entity List/Card (70030/70031)
- Risk Manager Role Center (70050)
- Customer/Vendor extensions with TIC Company ID fields

**Extensions Applied:**
- Customer table extension (70000) - adds BRCTICCompanyId field
- Vendor table extension (70001) - adds BRCTICCompanyId field
- Customer Card/List page extensions with risk indicators
- Vendor Card/List page extensions with risk indicators

## Post-Installation Tasks

### 1. Run Assisted Setup

**Mandatory Step:**
1. Search for **"Assisted Setup"** 
2. Find **"BRC Risk Setup"** in the list
3. Click **Start** or **Set up**
4. Follow the guided configuration wizard

### 2. Initial Configuration

**Required Configuration:**
- API provider credentials and endpoint
- Risk level definitions and styling
- User permission assignments
- Notification preferences

**See:** [Configuration Guide](configuration/) for detailed setup instructions

### 3. User Training Preparation

**Prepare Resources:**
- [User Guide documentation](../user-guide/)
- Permission set assignments per role
- Training environment setup
- Test data for demonstrations

## Troubleshooting Installation

### Common Installation Issues

**Extension Not Found:**
- Verify Business Central version is 26.0+
- Check AppSource region availability
- Confirm user has extension management permissions

**Installation Fails:**
- Check environment has sufficient resources
- Verify no conflicting extensions using object IDs 70000-70099
- Review error messages in Extension Management log

**Permission Errors:**
- Confirm user has SUPER permission set for installation
- Check company database access rights
- Verify extension installation permissions in admin center

**Incomplete Installation:**
- Refresh Extension Management page
- Check for partial installation state
- Contact support if tables/pages are missing

### Support Resources

**If Installation Issues Persist:**
- [Troubleshooting Guide](../troubleshooting/)
- [FAQ Section](../troubleshooting/faq/)
- BrightCom Solutions support channels
- Microsoft Business Central support

## Next Steps

After successful installation:

1. **[Complete Configuration](configuration/)** - Set up API access and preferences
2. **[Assign User Permissions](../reference/permissions/)** - Configure role-based access
3. **[Begin User Training](../user-guide/)** - Start with getting started guide
4. **[Set up Monitoring](../user-guide/advanced-features/#watchlists)** - Create watchlists

---

*Total installation time: 5-10 minutes. Configuration and setup: 15-30 minutes additional.*