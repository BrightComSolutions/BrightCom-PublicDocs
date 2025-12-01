---
title: "Prerequisites"
linkTitle: "Prerequisites" 
weight: 10
type: docs
description: >
  System requirements, license needs, and external dependencies for BRC Risk Management.
---

## System Requirements

### Business Central Environment
- **Platform**: Microsoft Dynamics 365 Business Central SaaS
- **Version**: 26.0 or later (required)
- **Runtime**: Version 15.0 support
- **Target**: Cloud deployment only

### Network Requirements
- **Outbound HTTPS Access**: Required for API calls to risk data providers
- **Ports**: Standard HTTPS (443) access
- **Firewall**: Allow outbound connections to risk provider endpoints
- **SSL/TLS**: TLS 1.2 or later for secure API communication

## Business Central Licenses

### Required Licenses
- **Business Central License**: Valid subscription with user access
- **User Permissions**: Appropriate role-based permissions for functionality access

### User Role Requirements
- **Risk Managers**: Full access to all risk assessment features
- **Credit Managers**: Entity management and risk data access
- **General Users**: Read-only access to risk indicators
- **Administrators**: Setup and configuration capabilities

See [Permissions Reference](../reference/permissions/) for detailed permission requirements.

## External Dependencies

### Risk Data Provider Account

**TIC (Recommended Provider)**
- Active subscription with TIC credit risk services
- API access credentials (API key and endpoint)
- Service agreement for data usage rights

**Alternative Providers**
- Must support compatible REST API structure
- JSON response format with required data fields
- Authentication via API key or similar mechanism

### Required API Capabilities
- **Company Search**: Search by name, VAT number, or registration number
- **Risk Data Retrieval**: Credit scores, debt balance, payment marks
- **Bulk Operations**: Support for multiple company queries
- **Webhook Support**: Real-time notifications (optional but recommended)

## Data Requirements

### Business Central Data
- **Customer Records**: Active customers for risk assessment
- **Vendor Records**: Suppliers requiring monitoring
- **Company Information**: VAT numbers and registration details for accurate matching

### Master Data Quality
- **Company Names**: Accurate legal company names for search matching
- **VAT Numbers**: Valid VAT registration numbers where applicable
- **Addresses**: Complete address information for verification
- **Contact Information**: Email addresses for notifications

## Technical Prerequisites

### Object ID Ranges
- **Object IDs**: 70000-70099 (reserved by app)
- **No Conflicts**: Ensure no existing objects in this range
- **Namespace Support**: Uses BrightCom.Risk.* namespaces

### Integration Points
- **Customer Table**: Extensions for TIC Company ID linkage
- **Vendor Table**: Extensions for TIC Company ID linkage  
- **Job Queue**: Background processing support
- **Application Insights**: Telemetry data collection

### Performance Considerations
- **API Rate Limits**: Respect provider API call limitations
- **Background Processing**: Job queue capacity for scheduled updates
- **Storage**: Adequate database space for risk data and audit logs

## Security Requirements

### Data Protection
- **API Key Storage**: Secure storage in Business Central encrypted storage
- **Data Encryption**: In-transit and at-rest encryption
- **Access Logging**: Comprehensive audit trail for all operations
- **Permission Management**: Role-based access control

### Privacy Compliance
- **GDPR Compliance**: Data protection regulation adherence
- **Data Retention**: Configurable data retention policies
- **Consent Management**: Appropriate consent for third-party data usage
- **Privacy Policy**: Review [privacy statement](https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk)

## Installation Prerequisites

### User Permissions for Installation
- **SUPER Permission Set**: Required for initial extension installation
- **Extension Management**: Access to install from AppSource
- **System Administration**: Rights to configure assisted setup

### Environment Readiness
- **Development/Test**: Recommended to test in non-production environment first
- **Backup**: Current environment backup before installation
- **Maintenance Window**: Planned installation window for production environments

## Pre-Installation Checklist

Before beginning installation:

- [ ] **Business Central version 26.0+** confirmed
- [ ] **Risk data provider account** active with API credentials
- [ ] **User permissions** verified for installation
- [ ] **Network access** confirmed for outbound HTTPS
- [ ] **Master data quality** reviewed for customers/vendors
- [ ] **Privacy compliance** requirements understood
- [ ] **Installation window** scheduled
- [ ] **Test environment** available for validation

## Validation Steps

After meeting prerequisites:

1. **Test API Connection**: Verify ability to reach provider endpoints
2. **Validate Credentials**: Confirm API key works with test queries
3. **Review Data**: Ensure customer/vendor data is ready for linking
4. **Check Permissions**: Verify user access levels are appropriate

## Next Steps

Once prerequisites are met:
- **[Proceed to Installation](installation/)** 
- **[Review Configuration Requirements](configuration/)**
- **[Prepare User Training Materials](../user-guide/)**

---

*Estimated prerequisite verification time: 30-60 minutes*