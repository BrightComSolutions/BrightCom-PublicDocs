---
title: "Reference"
linkTitle: "Reference"
weight: 50
description: >
  Comprehensive reference materials including permissions, API documentation, integration events, and technical specifications.
---

## Reference Documentation

This section provides comprehensive technical reference materials for BRC Risk Management including detailed permission specifications, API documentation, integration event catalog, and system requirements.

## Documentation Sections

### [Permissions](permissions/)
Complete permission set documentation including role-based access control, security model, and user assignment guidelines.

### [API Reference](api-reference/)
Technical API documentation for integration developers including endpoints, request/response formats, authentication, and error handling.

### [Release Notes](release-notes/)
Version history, feature additions, bug fixes, and upgrade guidance for each release.

## Quick Reference

### Version Information
- **Current Version**: 1.0.0.0
- **Business Central**: 26.0+ (SaaS only)
- **Runtime**: 15.0
- **Publisher**: BrightCom Solutions AB
- **Object Range**: 70000-70099

### Core Objects

**Primary Tables:**
- **Business Entity** (70000): Master risk data storage
- **Risk Level** (70003): Risk categorization and styling
- **Risk Setup** (70004): System configuration
- **Risk Watch List** (70005): Proactive monitoring configuration
- **API Call Ledger** (70010): Integration audit trail

**Key Pages:**
- **Risk Manager Role Center** (70050): Main workspace
- **Risk Setup Card** (70020): Configuration interface  
- **Business Entity List/Card** (70030/70031): Entity management
- **Risk Watchlists** (70040): Monitoring management

**Table Extensions:**
- **Customer** (70000): Adds BRCTICCompanyId linking field
- **Vendor** (70001): Adds BRCTICCompanyId linking field

### Permission Sets

**BRC RISK - VIEW**: Read-only access to risk data
**BRC RISK - EDIT**: Operational risk data management  
**BRC RISK - ADMIN**: Full access including setup and configuration

### Namespaces

All objects use structured namespaces for proper organization:
- `BrightCom.Risk.Entity` - Business entity management
- `BrightCom.Risk.Setup` - Configuration and setup
- `BrightCom.Risk.API` - External API integration
- `BrightCom.Risk.Logging` - Audit trail and logging
- `BrightCom.Risk.Watchlist` - Proactive monitoring
- `BrightCom.Risk.Webhook` - Webhook integration

## Integration Events

BRC Risk Management publishes 22+ integration events for extensibility:

### Core Events
- `OnBeforeRiskDataFetch`: Before API call for risk data
- `OnAfterRiskDataUpdated`: After successful risk data update
- `OnRiskLevelChanged`: When entity risk level changes
- `OnWatchlistCriteriaMatched`: When entity matches watchlist criteria

### API Events  
- `OnApiCallCompleted`: After any API call completion
- `OnApiCallFailed`: When API calls fail with errors
- `OnApiRateLimitReached`: When approaching or hitting rate limits

### Entity Events
- `OnBeforeEntityLink`: Before linking customer/vendor to entity
- `OnAfterEntityLinked`: After successful entity linking
- `OnEntitySearchCompleted`: After company search operations

## Support Information

### Documentation Resources
- **Online Help**: [https://docs.brightcom.se/sv/Products/BRCRisk](https://docs.brightcom.se/sv/Products/BRCRisk)
- **Privacy Policy**: [https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk](https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk)
- **EULA**: [https://brightcom.se/EULA/](https://brightcom.se/EULA/)

### Publisher Information
- **Publisher**: BrightCom Solutions AB
- **Website**: [https://brightcom.se/](https://brightcom.se/)
- **Support**: Available through standard Business Central support channels

### Technical Support
- **AppSource Support**: Microsoft AppSource support channels
- **Implementation Support**: Available from BrightCom Solutions
- **Integration Support**: Technical assistance for API and custom development

## System Requirements

### Minimum Requirements
- **Business Central**: SaaS version 26.0 or later
- **Runtime**: AL Runtime 15.0 support
- **Network**: Outbound HTTPS access for API calls
- **Storage**: Adequate database space for risk data and audit logs

### Recommended Requirements  
- **API Provider**: Active TIC account with appropriate API limits
- **Monitoring**: Application Insights for telemetry (recommended)
- **Backup**: Regular backup schedule including BRC Risk data
- **Training**: User training on risk assessment concepts and workflows

## Compliance and Certifications

### Security Standards
- **Data Encryption**: In-transit and at-rest encryption
- **Access Control**: Role-based permission model
- **Audit Trail**: Comprehensive logging of all operations
- **API Security**: Secure authentication and communication

### Privacy Compliance
- **GDPR**: General Data Protection Regulation compliance
- **Data Retention**: Configurable retention policies
- **Consent Management**: Clear consent for third-party data usage
- **Data Export**: Support for data portability requirements

## Performance Specifications

### API Performance
- **Response Time**: Typical API response under 2 seconds
- **Rate Limits**: Configurable limits per provider subscription
- **Concurrent Calls**: Support for multiple simultaneous requests
- **Error Handling**: Automatic retry and circuit breaker patterns

### Database Performance
- **Entity Capacity**: No practical limit on business entities
- **Search Performance**: Optimized indexing for quick entity lookup
- **Report Generation**: Efficient query optimization for reporting
- **Archive Management**: Automated cleanup of historical data

---

*For detailed technical information, refer to the specific reference sections or contact BrightCom Solutions support for implementation assistance.*