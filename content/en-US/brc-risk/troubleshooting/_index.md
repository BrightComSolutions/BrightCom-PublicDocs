---
title: "Troubleshooting"
linkTitle: "Troubleshooting"
weight: 60
type: docs
description: >
  Common issues, solutions, and troubleshooting guidance for BRC Risk Management.
---

## Troubleshooting Overview

This section provides solutions to common issues you might encounter while using BRC Risk Management. Issues are organized by functional area with step-by-step resolution guidance.

## API and Connectivity Issues

### API Connection Failures

**Symptoms:**
- "Connection failed" errors when fetching risk data
- Timeout errors during company search
- API credentials rejected

**Resolution Steps:**

1. **Verify API Credentials:**
   - Open **Risk Setup** page
   - Test the API connection using **Test Connection** action
   - If test fails, verify:
     - API key is correctly entered
     - API endpoint URL is accurate
     - No extra spaces or characters in credentials

2. **Check Network Connectivity:**
   - Verify outbound HTTPS access from Business Central environment
   - Test connectivity to risk provider endpoints
   - Check firewall settings and proxy configuration

3. **Validate API Limits:**
   - Review monthly API call consumption
   - Check if rate limits have been exceeded
   - Verify subscription status with risk provider

**Common Solutions:**
- **Invalid API Key**: Contact risk provider for new credentials
- **Network Blocked**: Work with IT to allow outbound HTTPS to provider endpoints
- **Rate Limit Hit**: Wait for limit reset or upgrade API subscription

### Slow API Response Times

**Symptoms:**
- Risk data fetching takes longer than expected
- Timeout errors during bulk operations
- User interface becomes unresponsive during updates

**Optimization Steps:**

1. **Batch Size Optimization:**
   - Reduce bulk operation batch sizes
   - Use smaller groups for concurrent updates
   - Schedule updates during off-peak hours

2. **Network Optimization:**
   - Check Business Central environment location vs. API provider
   - Optimize network routing if possible
   - Monitor for peak usage times

3. **System Resource Check:**
   - Monitor Business Central environment performance
   - Check for other intensive operations running concurrently
   - Consider dedicated time slots for risk data updates

## Data and Linking Issues

### Company Search Returns No Results

**Symptoms:**
- Cannot find company when searching by name
- No matches for valid VAT or registration numbers
- Search works for some companies but not others

**Search Strategy:**

1. **Try Alternative Search Methods:**
   ```
   Search Order:
   1. Exact company legal name
   2. Company name without legal suffixes (Ltd, Inc, etc.)
   3. VAT registration number
   4. Company registration number
   5. Partial name matches
   ```

2. **Name Variations to Try:**
   - Remove punctuation and special characters
   - Try abbreviated versions
   - Check for different legal name formats
   - Use holding company or parent company names

3. **Verify Company Exists:**
   - Confirm company is registered with risk data provider
   - Check if company operates in supported countries/regions
   - Verify company is still active (not dissolved)

### Entity Linking Problems

**Symptoms:**
- Cannot link customer/vendor to business entity
- "Entity already linked" errors
- Linked entity shows wrong company information

**Resolution Process:**

1. **Check Existing Links:**
   - Search for existing Business Entity with same TIC Company ID
   - Verify if entity is already linked to different customer/vendor
   - Review entity linking history

2. **Resolve Link Conflicts:**
   - **Duplicate Links**: Remove incorrect links and re-establish proper connections
   - **Wrong Entity**: Unlink and search for correct company
   - **Multiple Matches**: Choose most accurate match based on company details

3. **Manual Entity Creation:**
   - If company not found in provider database
   - Create Business Entity manually with available information
   - Set up manual update schedule or monitoring

### Missing or Incorrect Risk Data

**Symptoms:**
- Risk fields show blank or zero values
- Credit scores seem inconsistent
- Risk level doesn't match expected value

**Data Validation Steps:**

1. **Check Data Freshness:**
   - Review **Last Fetch DateTime** on Business Entity
   - Verify update schedule is appropriate
   - Force manual update to get latest data

2. **Validate Source Data:**
   - Compare with risk provider's direct interface
   - Check if provider has updated their data model
   - Verify field mappings are correct

3. **Review Risk Level Calculation:**
   - Check risk level thresholds in Risk Level setup
   - Verify automatic risk level assignment logic
   - Test manual risk level assignment

## User Access and Permission Issues

### Cannot Access Risk Pages

**Symptoms:**
- "You do not have permission" errors
- Risk pages not visible in navigation
- Missing actions on Customer/Vendor cards

**Permission Troubleshooting:**

1. **Verify Permission Set Assignment:**
   ```
   User Role → Required Permission Set
   General User → BRC RISK - VIEW
   Credit Manager → BRC RISK - EDIT
   Risk Administrator → BRC RISK - ADMIN
   ```

2. **Check Permission Set Details:**
   - Ensure permission set is assigned to correct company
   - Verify no expiration dates on permissions
   - Check for conflicting permission sets

3. **Test Permission Levels:**
   - Log in as test user with known working permissions
   - Compare permission assignments
   - Escalate to Business Central administrator if needed

### Risk Data Not Visible on Customer/Vendor Cards

**Symptoms:**
- Risk FactBox not displayed
- Risk actions missing from Customer/Vendor pages
- Risk level styling not applied

**Page Configuration Check:**

1. **Verify Page Personalization:**
   - Check if FactBox is hidden in user personalization
   - Reset page personalization to default
   - Verify page extensions are properly loaded

2. **Check Data Linking:**
   - Confirm customer/vendor is linked to Business Entity
   - Verify BRC TIC Company ID field is populated
   - Test with known working customer/vendor record

## Watchlist and Notification Issues

### Watchlist Not Triggering Notifications

**Symptoms:**
- Entities meet criteria but no notifications sent
- Email notifications not received
- Webhook calls not being made

**Notification Troubleshooting:**

1. **Verify Watchlist Configuration:**
   - Check watchlist is **Enabled**
   - Review criteria settings for accuracy
   - Test criteria against known matching entities

2. **Check Notification Settings:**
   - **Email**: Verify SMTP configuration in Business Central
   - **Webhook**: Test webhook endpoint accessibility
   - **Recipients**: Confirm email addresses or URLs are correct

3. **Review Watchlist Evaluation:**
   - Check **Last Check DateTime** is updating
   - Verify Job Queue entry for watchlist evaluation is running
   - Review evaluation logs for errors

### Watchlist Matching Too Many Entities

**Symptoms:**
- Watchlist generates excessive notifications
- Criteria too broad, matching unintended entities
- Performance impact from large match sets

**Criteria Refinement:**

1. **Narrow Criteria:**
   - Add additional AND conditions
   - Tighten thresholds (credit score ranges, debt limits)
   - Add entity filters (customer vs. vendor, active only)

2. **Implement Tiered Monitoring:**
   - Create separate watchlists for different risk levels
   - Use different notification frequencies
   - Set up escalation paths for critical vs. warning conditions

## Performance and System Issues

### Slow System Performance

**Symptoms:**
- Pages load slowly
- Risk data fetching takes excessive time
- Background jobs not completing

**Performance Analysis:**

1. **Identify Bottlenecks:**
   - Monitor API response times
   - Check database query performance
   - Review Job Queue execution times

2. **Optimization Actions:**
   - **Database**: Optimize filters and indexes
   - **API**: Implement caching and batch operations
   - **UI**: Use pagination for large data sets

3. **Resource Management:**
   - Schedule intensive operations during off-peak hours
   - Limit concurrent API calls
   - Archive old data to improve performance

### Job Queue Failures

**Symptoms:**
- Scheduled updates not running
- Job Queue entries show error status
- Background processing inconsistent

**Job Queue Troubleshooting:**

1. **Check Job Queue Configuration:**
   - Verify Job Queue is properly configured
   - Check user permissions for Job Queue execution
   - Review recurring job settings

2. **Analyze Error Messages:**
   - Review error logs in Job Queue Entry
   - Check for permission or connectivity issues
   - Verify object dependencies are available

3. **Restart and Monitor:**
   - Restart failed jobs manually
   - Monitor execution for recurring issues
   - Adjust scheduling if resource conflicts exist

## Error Messages and Solutions

### Common Error Messages

| Error Message | Cause | Solution |
|---------------|-------|----------|
| "API key invalid" | Incorrect or expired API credentials | Update API key in Risk Setup |
| "Rate limit exceeded" | Too many API calls in time period | Wait for reset or upgrade subscription |
| "Company not found" | Search criteria don't match any companies | Try alternative search terms |
| "Entity already linked" | Business Entity linked to different record | Check existing links and resolve conflicts |
| "Permission denied" | User lacks required permissions | Assign appropriate BRC RISK permission set |
| "Connection timeout" | Network or performance issue | Check connectivity and retry |
| "Invalid risk level" | Risk level code not found | Verify Risk Level setup configuration |

## Getting Additional Help

### Diagnostic Information to Gather

When contacting support, provide:

1. **System Information:**
   - Business Central version and environment type
   - BRC Risk Management app version
   - User permission sets assigned

2. **Error Details:**
   - Exact error message text
   - Steps to reproduce the issue
   - Affected users or entities

3. **Configuration Information:**
   - Risk provider and API endpoint
   - Relevant setup configuration (without sensitive data)
   - Recent changes to system or configuration

### Support Resources

**Internal Resources:**
- Business Central administrator
- IT support team
- Risk management process owner

**External Resources:**
- BrightCom Solutions support
- Microsoft Business Central support
- Risk data provider support

**Documentation:**
- [User Guide](../user-guide/) for operational questions
- [Reference Documentation](../reference/) for technical details
- [Setup Guide](../setup/) for configuration issues

---

*For additional support, contact your Business Central administrator or BrightCom Solutions technical support.*