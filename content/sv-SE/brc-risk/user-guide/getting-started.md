---
title: "Getting Started"
linkTitle: "Getting Started"
weight: 10
description: >
  First-time user orientation for BRC Risk Management including basic concepts, navigation, and initial tasks.
---

## Welcome to BRC Risk Management

BRC Risk Management helps you monitor and assess the financial risk of your business partners through automated integration with third-party risk data providers. This guide will help you understand the key concepts and get started with basic operations.

## Key Concepts

### Business Entities
**Business Entities** are the core records that store risk assessment data for companies. Each entity represents a company that you monitor, linked to your Business Central customers and vendors.

**Key Information Stored:**
- **TIC Company ID**: Unique identifier from the risk data provider
- **Company Details**: Name, registration number, address information
- **Risk Data**: Credit score (0-100), debt balance, payment marks
- **Risk Level**: Calculated risk category (Critical, High, Medium, Low)
- **Update Schedule**: How frequently risk data is refreshed

### Risk Levels
**Risk Levels** define how risk assessment data is categorized and displayed throughout Business Central.

**Default Risk Levels:**
- **CRITICAL** (Red): Immediate attention required, potential transaction blocking
- **HIGH** (Orange): Significant risk, warning messages displayed  
- **MEDIUM** (Yellow): Moderate risk, attention-style indicators
- **LOW** (Green): Low risk, favorable-style indicators

### Watchlists
**Watchlists** provide proactive monitoring by automatically checking entities against specific criteria and sending notifications when conditions are met.

**Example Watchlist Criteria:**
- Credit score drops below 50
- Debt balance exceeds €50,000
- Payment marks increase by more than 2
- Risk level changes to High or Critical

## User Interface Overview

### Risk Manager Role Center

The **Risk Manager Role Center** provides a centralized workspace for risk management activities:

**Headlines Section:**
- **Risk Assessment Cues**: Overview of entity counts by risk level
- **Recent Alerts**: Latest risk level changes and watchlist matches
- **API Usage**: Current month's API call consumption

**Quick Actions:**
- **Business Entities**: Access entity list and management
- **Watchlists**: Create and manage proactive monitoring
- **Risk Setup**: Configuration and administration
- **API Logs**: Review integration history and errors

### Customer and Vendor Integration

Risk information is seamlessly integrated into standard Business Central pages:

**Customer/Vendor Lists:**
- **Risk Indicators**: Color-coded styling based on risk level
- **Quick Access**: Risk level visible in list columns
- **Filtering**: Filter by risk level or linked status

**Customer/Vendor Cards:**
- **Risk FactBox**: Detailed risk information on the right side
- **Risk Actions**: "Fetch Risk Data" and "Add to Watchlist" buttons
- **Visual Indicators**: Color styling on company name and number

### Business Entity Management

**Business Entity List:**
- **Complete Portfolio**: All monitored entities in one view
- **Risk Overview**: Risk level, credit score, and last update columns
- **Bulk Actions**: Multi-select operations for efficiency
- **Advanced Filtering**: Filter by risk criteria, update status, etc.

**Business Entity Card:**
- **Complete Risk Profile**: All available risk data fields
- **Update History**: Track when data was last fetched
- **Linked Records**: See connected customers and vendors
- **Manual Actions**: Fetch data, schedule updates, add to watchlists

## Your First Tasks

### 1. Explore the Risk Manager Role Center

1. **Access the Role Center**
   - Use the role selector to switch to "Risk Manager"
   - Alternatively, search for "Risk Manager" in the navigation

2. **Review the Overview**
   - Check the Risk Assessment Cues for current portfolio status
   - Note any existing entities and their risk distribution
   - Review recent activity in headlines section

3. **Familiarize with Navigation**
   - Click through each main action to see available pages
   - Explore the menu structure and available reports
   - Bookmark frequently used pages

### 2. Understand Existing Data

If your organization has been using BRC Risk Management:

1. **Review Business Entities**
   - Open the Business Entity List
   - Sort by Risk Level to see highest-risk entities first
   - Note update frequencies and last fetch dates

2. **Check Customer/Vendor Links**
   - Open a Customer Card
   - Look for the Risk FactBox on the right side
   - Click "Fetch Risk Data" to see the data fetching process

3. **Examine API Usage**
   - Check current month's API call consumption
   - Review rate limits and remaining calls
   - Understand your organization's usage patterns

### 3. Learn Basic Navigation

**Search Functionality:**
- Use **Tell Me** (Alt+Q) to search for "Risk" related features
- Quick access to Business Entities, Risk Setup, and Watchlists
- Search customer/vendor names to jump to their cards

**Page Navigation:**
- **Business Entity List** → **Business Entity Card** (drill-down)
- **Customer List** → **Customer Card** → Risk FactBox
- **Risk Manager Role Center** → Quick action navigation

**Filtering and Sorting:**
- Filter Business Entities by Risk Level
- Sort by Credit Score or Last Update Date
- Use quick filters for efficient data review

## Common First-Time User Scenarios

### Scenario 1: Checking Customer Risk Before a Large Sale

**Steps:**
1. Open the **Customer Card** for the specific customer
2. Look at the **Risk FactBox** on the right side
3. Review the **Credit Score** and **Risk Level**
4. If data is old, click **Fetch Risk Data** to update
5. Consider the risk factors in your sales decision

**What to Look For:**
- Credit Score below 60 (consider higher risk)
- Recent Risk Level changes (trend analysis)
- Payment Marks above 3 (collection history concerns)
- Last update date (ensure data freshness)

### Scenario 2: Setting Up Monitoring for Key Customers

**Steps:**
1. Identify your most important customers for monitoring
2. Open each **Customer Card**
3. Click **Add to Watchlist** to set up monitoring
4. Configure notification preferences
5. Set appropriate risk thresholds for alerts

**Monitoring Recommendations:**
- Large customers: Monitor for any risk level changes
- Credit-sensitive accounts: Alert on score drops below 70
- Regular suppliers: Watch for payment mark increases
- International partners: Monitor for country risk changes

### Scenario 3: Understanding Your Risk Portfolio

**Steps:**
1. Open the **Business Entity List**
2. Use the **Risk Level** column to understand distribution
3. Filter to show only **High** and **Critical** risk entities
4. Review update schedules to ensure data freshness
5. Consider creating watchlists for systematic monitoring

**Analysis Points:**
- Percentage of portfolio in each risk category
- Entities with outdated risk data
- Customers/vendors not yet linked to risk data
- Trends in risk level changes over time

## Getting Help

### Built-in Help
- **ToolTips**: Hover over fields for explanations
- **Page Help**: Click the ? icon for page-specific guidance
- **Field Lookup**: Use dropdown lists to see available options

### Documentation Resources
- **[Daily Operations](daily-operations/)**: Common task procedures
- **[Advanced Features](advanced-features/)**: Power user capabilities
- **[Troubleshooting](../troubleshooting/)**: Issue resolution
- **[FAQ](../troubleshooting/faq/)**: Frequently asked questions

### Support Contacts
- **Internal IT**: Your organization's Business Central administrators
- **BrightCom Solutions**: Publisher support for technical issues
- **Risk Provider**: API and data-related questions

## Next Steps

### For Basic Users
1. **[Daily Operations](daily-operations/)** - Learn common tasks
2. **Practice Navigation** - Explore customer/vendor risk indicators  
3. **Understand Reports** - Review available risk reports
4. **Ask Questions** - Connect with your risk manager or IT support

### For Risk Managers
1. **[Advanced Features](advanced-features/)** - Master watchlists and automation
2. **Setup Review** - Ensure optimal configuration
3. **User Training** - Prepare materials for team training
4. **Process Integration** - Align with existing business processes

### For Administrators
1. **[Reference Documentation](../reference/)** - Technical specifications
2. **Permission Management** - Configure role-based access
3. **Integration Planning** - Connect with other business systems
4. **Performance Monitoring** - Optimize system usage

---

*Take time to explore the interface and understand your organization's current risk data before moving to advanced features.*