---
title: "Configuration Guide"
linkTitle: "Configuration"
weight: 30
description: >
  Complete configuration guide for API setup, risk levels, notifications, and user permissions in BRC Risk Management.
---

## Configuration Overview

BRC Risk Management requires configuration of API connections, risk levels, and user access before it can fetch and display risk data. The assisted setup wizard guides you through these essential steps.

## Assisted Setup Wizard

### Starting the Wizard

1. **Access Assisted Setup**
   - Search for **"Assisted Setup"**
   - Find **"BRC Risk Setup"** in the list  
   - Click **Start** or **Set up**

2. **Wizard Steps Overview**
   - Welcome and overview
   - API Configuration
   - Risk Level Setup
   - Notification Configuration
   - User Permissions
   - Completion and testing

### Wizard Navigation

- **Next/Previous**: Navigate between steps
- **Skip**: Skip optional configuration (can be done later)
- **Test**: Test settings where applicable
- **Finish**: Complete setup and exit wizard

## API Configuration

### Provider Setup

**TIC API Configuration (Primary Provider):**
1. **API Endpoint**: Enter TIC API base URL (e.g., `https://api.ticprovider.com/v1`)
2. **API Key**: Enter your TIC API key securely stored in encrypted storage
3. **Authentication**: API key authentication in request headers
4. **Rate Limits**: Configure monthly call limits per your TIC subscription

**Alternative Provider Setup:**
- Must support compatible REST API format
- JSON response structure for risk data
- Company search capabilities
- Authentication via API key or similar

### API Settings Fields

**Risk Setup Configuration:**
- **API Base URL**: Full endpoint URL for risk data provider
- **API Key**: Encrypted storage of authentication credentials
- **Monthly API Call Limit**: Maximum calls per month per your subscription
- **Warning Threshold**: Percentage warning level (e.g., 80% of limit)
- **Connection Timeout**: Request timeout in seconds (default: 30)
- **Retry Policy**: Number of retry attempts for failed calls

### Test API Connection

**Connection Validation:**
1. Click **Test Connection** in setup wizard or Risk Setup page
2. System performs test query to verify:
   - API endpoint accessibility
   - Authentication credential validity
   - Response format compatibility
   - Network connectivity

**Test Results:**
- ✅ **Success**: Connection valid, ready for use
- ❌ **Authentication Failed**: Check API key validity
- ❌ **Endpoint Not Found**: Verify API URL accuracy
- ❌ **Network Error**: Check firewall and connectivity

## Risk Level Configuration

### Default Risk Levels

The system creates four default risk levels during setup:

| Code | Description | Style | Risk Action | Priority |
|------|-------------|--------|-------------|----------|
| CRITICAL | Critical Risk | Strong Accent | Block | 1 (Highest) |
| HIGH | High Risk | Unfavorable | Warn | 2 |
| MEDIUM | Medium Risk | Attention | Style Only | 3 |
| LOW | Low Risk | Favorable | Nothing | 4 (Lowest) |

### Customizing Risk Levels

**Available Styles:**
- **Standard**: Default BC styling, no special formatting
- **Favorable**: Green/positive styling for good risk levels
- **Attention**: Yellow/warning styling for moderate risk
- **Unfavorable**: Red/negative styling for poor risk
- **Strong Accent**: Bold red styling for critical risk

**Risk Actions:**
- **Nothing**: No action taken, data display only
- **Style Only**: Apply visual styling, no functional restrictions
- **Warn**: Show warning message when viewing entity
- **Block**: Prevent transactions or require override

### Risk Level Thresholds

Configure thresholds to automatically assign risk levels based on:

**Credit Score Ranges:**
- CRITICAL: 0-39 (Very poor credit)
- HIGH: 40-59 (Poor credit)  
- MEDIUM: 60-79 (Fair credit)
- LOW: 80-100 (Good credit)

**Debt Balance Thresholds:**
- Configure debt amount triggers for risk escalation
- Multiple currency support
- Percentage-based or absolute value thresholds

**Payment Marks:**
- Number of collection marks triggering risk levels
- Historical timeframe for mark consideration
- Severity weighting for different mark types

### Adding Custom Risk Levels

1. **Open Risk Level List**
   - Search for "Risk Levels"
   - Click **New** to create custom level

2. **Configure Risk Level**
   - **Code**: Unique identifier (10 characters max)
   - **Description**: User-friendly name
   - **Style**: Visual representation
   - **Risk Action**: Functional behavior
   - **Priority**: Evaluation order (1=highest risk)

3. **Set Threshold Criteria**
   - Define conditions triggering this risk level
   - Configure score ranges, debt limits, payment marks
   - Test threshold logic with sample data

## Notification Configuration

### Notification Types

**Available Methods:**
- **None**: No notifications sent
- **Email**: Send emails to specified recipients
- **Webhook**: HTTP POST to specified endpoint
- **Internal**: Business Central notification system

### Email Notifications

**Email Setup:**
1. Configure SMTP settings in Business Central
2. Set default sender address
3. Define recipient groups or individual addresses
4. Customize email templates for different risk scenarios

**Email Triggers:**
- Risk level changes (escalation/de-escalation)
- Watchlist criteria matches
- API errors or connection issues
- Scheduled report summaries

### Webhook Configuration

**Webhook Setup:**
- **Endpoint URL**: Target system webhook URL
- **Authentication**: Headers, tokens, or basic auth
- **Payload Format**: JSON structure for notifications
- **Retry Policy**: Failed delivery retry attempts

**Webhook Payload Example:**
```json
{
  "eventType": "RiskLevelChanged",
  "entityId": "12345",
  "companyName": "Example Company Ltd",
  "oldRiskLevel": "MEDIUM",
  "newRiskLevel": "HIGH",
  "timestamp": "2025-12-01T10:30:00Z",
  "creditScore": 45
}
```

## User Permissions Configuration

### Permission Set Assignment

**Available Permission Sets:**
- **BRC RISK - VIEW**: Read-only access to risk data
- **BRC RISK - EDIT**: Create and modify risk data
- **BRC RISK - ADMIN**: Full access including setup

### Role-Based Configuration

**Risk Manager Role:**
- Assign "BRC RISK - ADMIN" permission set
- Access to Risk Manager Role Center
- Full entity management and watchlist configuration
- Setup and configuration capabilities

**Credit Manager Role:**  
- Assign "BRC RISK - EDIT" permission set
- Entity data management
- Watchlist creation and monitoring
- Risk data fetching capabilities

**General User Role:**
- Assign "BRC RISK - VIEW" permission set  
- Read-only access to risk indicators
- Customer/Vendor card risk information
- No modification rights

### Permission Verification

**Test User Access:**
1. Assign permission sets to test users
2. Verify appropriate page access levels
3. Test functional limitations per role
4. Validate data security restrictions

## Advanced Configuration

### Job Queue Setup

**Scheduled Risk Updates:**
1. Configure Job Queue entries for automated risk data fetching
2. Set update frequencies (daily, weekly, monthly)
3. Define retry policies for failed updates
4. Monitor execution logs and results

**Background Processing:**
- Bulk entity updates
- Watchlist evaluation
- API rate limit management
- Data synchronization tasks

### Integration Events

**Available Events:**
- OnBeforeRiskDataFetch
- OnAfterRiskDataUpdated  
- OnRiskLevelChanged
- OnWatchlistCriteriaMatched
- OnApiCallCompleted

**Custom Logic Integration:**
- Subscribe to events for custom business logic
- Extend risk evaluation criteria
- Add custom notification methods
- Integrate with external systems

## Configuration Validation

### Setup Verification Checklist

After completing configuration:

- [ ] **API Connection**: Successfully tests with provider
- [ ] **Risk Levels**: Properly configured with thresholds
- [ ] **User Permissions**: Assigned per role requirements
- [ ] **Notifications**: Working email/webhook delivery
- [ ] **Job Queue**: Scheduled tasks configured
- [ ] **Test Data**: Sample entity fetch successful

### Configuration Testing

**Recommended Tests:**
1. **API Test**: Fetch risk data for known company
2. **Risk Level Test**: Verify threshold calculations
3. **Permission Test**: Confirm user access restrictions
4. **Notification Test**: Trigger test notifications
5. **Integration Test**: End-to-end workflow validation

## Configuration Maintenance

### Regular Maintenance Tasks

**Monthly:**
- Review API usage against limits
- Validate notification delivery rates
- Check job queue execution success

**Quarterly:**
- Update risk level thresholds based on business needs
- Review user permission assignments
- Validate external API connectivity

**Annually:**
- Renew API provider credentials
- Review and update notification recipients
- Archive old configuration audit logs

## Next Steps

After completing configuration:

1. **[Assign User Permissions](../reference/permissions/)** - Set up role-based access
2. **[Begin User Training](../user-guide/)** - Start with getting started guide  
3. **[Create Initial Watchlists](../user-guide/advanced-features/#watchlists)** - Set up proactive monitoring
4. **[Link Existing Data](../user-guide/daily-operations/#linking-entities)** - Connect customers and vendors

---

*Configuration typically takes 15-30 minutes. Have API credentials and business requirements ready before starting.*