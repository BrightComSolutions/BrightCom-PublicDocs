---
title: "Release Notes"
linkTitle: "Release Notes" 
weight: 30
description: >
  Version history, feature additions, bug fixes, and upgrade guidance for BRC Risk Management releases.
---

## Version 1.0.0.0 - Initial Release

**Release Date:** December 2025  
**Business Central Compatibility:** 26.0+  
**Runtime Version:** 15.0

### 🎉 Initial Release Features

This is the initial release of BRC Risk Management for Microsoft Business Central, providing comprehensive third-party risk assessment and continuous monitoring capabilities.

#### Core Features

**Business Entity Management**
- Complete business entity master data with TIC Company ID integration
- Risk data storage: Credit scores (0-100), debt balance, payment marks
- Configurable update schedules: Manual, Weekly, Monthly, Annually
- Automatic next fetch date calculation based on schedule
- Customer and Vendor table extensions with linking fields

**Risk Assessment & Monitoring**
- Four default risk levels: Critical, High, Medium, Low
- Customizable risk level styling and actions (Block, Warn, Style Only, Nothing)
- Visual risk indicators on Customer/Vendor cards and lists
- Business Central standard styling options (Favorable, Attention, Unfavorable, etc.)
- Risk level threshold configuration with automatic assignment

**API Integration**
- TIC API integration for risk data fetching and company search
- Secure API key storage in Business Central encrypted storage
- Comprehensive API call logging with audit trail
- Rate limiting and usage monitoring
- Automatic retry logic for failed API calls
- Support for alternative compatible risk data providers

**Watchlist Functionality**
- Flexible criteria-based watchlists for proactive monitoring
- Multiple notification types: Email, Webhook, Internal notifications
- Automatic watchlist evaluation and match detection
- TIC watchlist registration for real-time notifications
- Custom notification recipients per watchlist

**User Interface**
- Dedicated Risk Manager Role Center with overview dashboards
- Risk Assessment Cues showing entity distribution by risk level
- Customer/Vendor FactBoxes displaying risk information
- Seamless integration with standard Business Central workflows
- Assisted Setup Wizard for initial configuration

**Background Processing**
- Job Queue integration for scheduled risk data updates
- Bulk update operations for efficient processing
- Configurable retry policies for failed operations
- Performance optimization for large entity portfolios

**Security & Compliance**
- Three-tier permission model: VIEW, EDIT, ADMIN
- Role-based access control aligned with business functions
- Comprehensive audit trail for all operations
- GDPR-compliant data handling and storage
- Encrypted credential storage and secure API communication

#### Technical Specifications

**Object Range:** 70000-70099
- Tables: Business Entity, Risk Setup, Risk Levels, Watchlists, API Logs
- Pages: Role Center, Setup, Entity Management, Watchlist Management
- Codeunits: API Client, Watchlist Manager, Job Queue Helper
- Extensions: Customer/Vendor table and page extensions

**Namespace Organization:**
- `BrightCom.Risk.Entity` - Business entity management
- `BrightCom.Risk.Setup` - Configuration and setup
- `BrightCom.Risk.API` - External API integration  
- `BrightCom.Risk.Logging` - Audit trail and logging
- `BrightCom.Risk.Watchlist` - Proactive monitoring
- `BrightCom.Risk.Webhook` - Webhook integration

**Integration Events:** 22+ published events for extensibility
- Risk data fetch lifecycle events
- Risk level change notifications
- Watchlist match triggers
- API call completion events
- Entity linking workflow events

### 🔧 Installation & Setup

**Prerequisites:**
- Business Central SaaS version 26.0 or later
- Valid TIC account or compatible risk data provider
- Outbound HTTPS network access for API calls
- Appropriate user permissions for installation

**Installation Process:**
1. Install from Microsoft AppSource
2. Run Assisted Setup Wizard
3. Configure API provider credentials
4. Set up risk levels and thresholds
5. Assign user permissions
6. Create initial watchlists

### 📋 Supported Scenarios

**Risk Assessment:**
- Manual risk data fetching for individual entities
- Scheduled automatic updates via Job Queue
- Bulk operations for portfolio-wide updates
- Real-time risk level change notifications

**Customer Management:**
- Credit assessment before sales quotes
- Payment risk evaluation for credit decisions
- Automated monitoring of key customer accounts
- Integration with sales and credit workflows

**Vendor Management:**
- Supplier financial stability assessment
- Procurement risk evaluation
- Payment terms adjustment based on risk
- Supply chain continuity monitoring

**Portfolio Monitoring:**
- Comprehensive risk portfolio dashboards
- Trend analysis and reporting
- Proactive alerts for risk threshold breaches
- Executive reporting and analytics

### 🧪 Testing & Quality Assurance

**Test Coverage:** Comprehensive test suite included
- Unit tests for all critical business logic
- Integration tests for API connectivity
- UI tests for page functionality
- Performance tests for bulk operations

**Quality Standards:**
- AL language best practices implementation
- Business Central extension guidelines compliance
- Security review and penetration testing
- Performance optimization and scalability testing

### 📚 Documentation

**Complete Documentation Package:**
- Installation and setup guides
- User guides for all roles and permission levels
- API integration documentation
- Troubleshooting and FAQ resources
- Technical reference materials

**Training Resources:**
- Role-based user guides
- Administrative setup documentation
- Best practices and optimization guides
- Integration event catalog for developers

### 🔄 Future Roadmap

**Planned Enhancements:**
- Additional risk data provider integrations
- Enhanced reporting and analytics capabilities
- Mobile access optimization
- Advanced AI-driven risk scoring
- Integration with Power BI for advanced analytics

### 📞 Support

**Support Channels:**
- Microsoft AppSource support
- BrightCom Solutions technical support
- Comprehensive online documentation
- Community forums and knowledge base

**Documentation Links:**
- Online Help: [https://docs.brightcom.se/sv/Products/BRCRisk](https://docs.brightcom.se/sv/Products/BRCRisk)
- Privacy Policy: [https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk](https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk)
- EULA: [https://brightcom.se/EULA/](https://brightcom.se/EULA/)

---

## Upgrade Guidelines

### From Pre-Release to 1.0.0.0

This is the initial production release. No upgrade path required.

### Future Version Upgrades

Future version upgrade instructions will be provided in subsequent releases.

**Recommended Upgrade Process:**
1. Review release notes for breaking changes
2. Test upgrade in non-production environment
3. Schedule maintenance window for production upgrade
4. Backup environment before upgrade
5. Follow specific upgrade instructions per version

### Data Migration

**Initial Installation:** No data migration required
**Future Versions:** Migration guides will be provided for significant schema changes

---

## Known Issues & Limitations

### Version 1.0.0.0 Known Issues

**Minor Issues:**
- None reported at initial release

### Current Limitations

**Platform Limitations:**
- Business Central SaaS only (On-Premise support planned for future versions)
- Single risk data provider per environment
- API rate limits determined by provider subscription

**Functional Limitations:**
- Maximum 20 active watchlists per environment
- Bulk operations limited to 100 entities per batch
- API call history retained for 12 months maximum

### Workarounds

**For Large Portfolios:**
- Use multiple smaller bulk operations instead of single large batches
- Implement staggered update schedules to optimize API usage
- Archive older entities that no longer require monitoring

**For Advanced Analytics:**
- Export risk data to Power BI for advanced reporting
- Use integration events for custom analytics implementations
- Leverage Application Insights for performance monitoring

---

*For technical support or upgrade assistance, contact BrightCom Solutions or your Business Central partner.*