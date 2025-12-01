---
title: "Daily Operations"
linkTitle: "Daily Operations"
weight: 20
type: docs
description: >
  Common tasks and workflows for daily BRC Risk Management operations including risk data fetching, entity management, and monitoring.
---

## Daily Operations Overview

This guide covers the most common tasks you'll perform when using BRC Risk Management on a day-to-day basis. Whether you're a credit manager, risk analyst, or general user, these workflows will help you efficiently manage risk assessment data.

## Common Daily Tasks

### Checking Customer Risk Before Sales

**When:** Before preparing quotes, processing orders, or setting payment terms
**Who:** Sales representatives, credit managers, customer service

**Steps:**
1. Open the **Customer Card** for the specific customer
2. Look at the **Risk FactBox** on the right side of the page
3. Review key indicators:
   - **Risk Level**: Current risk category (Critical, High, Medium, Low)
   - **Credit Score**: Numerical score from 0-100
   - **Debt Balance**: Outstanding debt amount
   - **Payment Marks**: Number of collection marks
   - **Last Updated**: When risk data was last fetched

4. **If data is outdated** (more than your update schedule):
   - Click **Actions** → **Fetch Risk Data**
   - Wait for the update to complete
   - Review updated risk information

5. **If customer has no risk data linked**:
   - Click **Actions** → **Link to Business Entity**
   - Search for the company using name or VAT number
   - Select the correct company from search results
   - Confirm the linking

### Monitoring High-Risk Entities

**When:** Daily risk review, morning checks, before major decisions
**Who:** Risk managers, credit managers

**Steps:**
1. Open **Risk Manager Role Center**
2. Review **Risk Assessment Cues** for portfolio overview:
   - Count of Critical and High-risk entities
   - Recent risk level changes
   - Entities requiring attention

3. **For detailed review:**
   - Click **Business Entities** to open the list
   - **Filter by Risk Level** → Select "CRITICAL" and "HIGH"
   - Review entities with recent changes or high balances

4. **Take action on high-risk entities:**
   - Open individual **Business Entity Cards**
   - Review recent changes in risk level
   - Check connected customers/vendors
   - Consider adding to watchlists for closer monitoring

### Updating Risk Data for Key Accounts

**When:** Before important business decisions, weekly/monthly reviews
**Who:** Credit managers, risk analysts

**Bulk Update Process:**
1. Open **Business Entity List**
2. **Select multiple entities** using Ctrl+Click
3. Use bulk actions to:
   - **Fetch Risk Data** for selected entities
   - **Add to Watchlist** for monitoring
   - **Update Schedule** for automatic refreshes

**Individual Update Process:**
1. Open **Business Entity Card**
2. Click **Actions** → **Fetch Risk Data**
3. Review the updated information
4. Check for risk level changes
5. Update **Next Fetch Date** if needed

### Linking Customers and Vendors to Risk Data {#linking-entities}

**When:** Setting up new customers/vendors, discovering unlinked entities
**Who:** Data entry staff, credit managers

**For New Customers/Vendors:**
1. Create the customer/vendor record as normal
2. On the **Customer/Vendor Card**, look for the **Risk FactBox**
3. If no risk data is shown:
   - Click **Actions** → **Link to Business Entity**
   - **Search Process:**
     - Enter company name (primary search)
     - If no results, try VAT registration number
     - If still no results, try company registration number
   - **Select correct match** from search results
   - **Confirm linking** to create the connection

**For Existing Unlinked Records:**
1. **Find unlinked records:**
   - Filter Customer/Vendor lists where **BRC TIC Company ID** is blank
   - Or run reports to identify unlinked records

2. **Link in bulk:**
   - Select multiple unlinked records
   - Use batch linking actions
   - Review and confirm each link

### Watchlist Management

**Creating Watchlists:**
1. Open **Risk Watchlists** page
2. Click **New** to create a watchlist
3. **Configure criteria:**
   - **Name and Description**: Clear purpose statement
   - **Risk Level Triggers**: Which risk levels to monitor
   - **Credit Score Thresholds**: Minimum/maximum scores
   - **Debt Balance Limits**: Amount thresholds
   - **Payment Mark Limits**: Collection mark thresholds

4. **Set notifications:**
   - **Notification Type**: Email, Webhook, or Internal
   - **Recipients**: Email addresses or webhook URLs
   - **Frequency**: Immediate or scheduled

**Monitoring Watchlists:** {#watchlists}
1. **Check watchlist matches:**
   - Open **Risk Watchlists** page
   - Review **Last Check Date/Time** for each watchlist
   - Open individual watchlists to see current matches

2. **Review notifications:**
   - Check email for watchlist alerts
   - Review internal notifications in Business Central
   - Monitor webhook endpoints for real-time updates

3. **Take action on matches:**
   - Contact customers/vendors that match criteria
   - Adjust credit limits or payment terms
   - Create follow-up tasks or reminders

## Weekly Tasks

### Portfolio Risk Review

**Every Monday Morning:**
1. **Open Risk Manager Role Center**
2. **Review weekly metrics:**
   - Total entities by risk level
   - New high-risk entities
   - Risk level changes from previous week

3. **Generate reports:**
   - High-risk customer report
   - Vendor risk assessment summary
   - API usage summary

4. **Plan week's activities:**
   - Prioritize high-risk account reviews
   - Schedule customer/vendor communications
   - Plan risk data updates for key accounts

### Bulk Risk Data Updates

**Scheduled Weekly Updates:**
1. **Identify entities for update:**
   - Filter by **Next Fetch Date** = today or overdue
   - Focus on high-value or high-risk entities

2. **Perform bulk updates:**
   - Select entities for update
   - Execute **Fetch Risk Data** action
   - Monitor for API errors or failures

3. **Review results:**
   - Check for risk level changes
   - Identify new high-risk entities
   - Update watchlist criteria if needed

## Monthly Tasks

### API Usage Review

**Monitor API Consumption:**
1. **Check API usage:**
   - Review current month's API call count
   - Compare against monthly limits
   - Identify peak usage periods

2. **Optimize usage:**
   - Adjust update schedules for low-priority entities
   - Review and remove obsolete business entities
   - Optimize bulk update scheduling

### System Maintenance

**Data Cleanup:**
1. **Archive old data:**
   - Review API call logs older than 12 months
   - Archive inactive business entities
   - Clean up old notification logs

2. **Review configurations:**
   - Validate risk level thresholds
   - Update watchlist criteria
   - Review user permissions and access

## Troubleshooting Common Issues

### Risk Data Not Updating

**Symptoms:** Old data, fetch actions fail
**Solutions:**
1. Check API credentials in Risk Setup
2. Verify network connectivity
3. Check API rate limits
4. Review error logs in API Call Ledger

### Linking Problems

**Symptoms:** Cannot find company in search, linking fails
**Solutions:**
1. Verify company name spelling
2. Try alternative search criteria (VAT, registration number)
3. Check if company exists in risk provider database
4. Manual entity creation if necessary

### Watchlist Not Triggering

**Symptoms:** No notifications despite criteria being met
**Solutions:**
1. Check watchlist is enabled
2. Verify notification configuration
3. Test email/webhook endpoints
4. Review watchlist evaluation logs

## Performance Tips

### Efficient Workflows

**Batch Operations:**
- Use bulk actions for multiple entities
- Schedule updates during off-peak hours
- Group similar tasks together

**Smart Filtering:**
- Use saved filters for common views
- Set up role-based default filters
- Use quick actions for frequent tasks

**Monitoring Optimization:**
- Set appropriate update schedules
- Focus monitoring on high-risk/high-value entities
- Use watchlists instead of manual monitoring

---

*For advanced features and power user capabilities, see [Advanced Features](advanced-features/). For basic orientation, start with [Getting Started](getting-started/).*