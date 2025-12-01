---
title: "BRC Risk Management"
linkTitle: "BRC Risk"
weight: 10
type: docs
description: >
  Comprehensive third-party risk assessment and continuous monitoring for Business Central with real-time credit scores, risk ratings, and customizable watchlists.
---

## Overview

BRC Risk Management is a Business Central AppSource application that provides automated risk assessment and continuous monitoring of your business entities through integration with leading third-party risk data providers like TIC. It enables organizations to make informed decisions about customers, vendors, and partners by providing real-time credit scores, risk ratings, and proactive monitoring through customizable watchlists.

The app integrates seamlessly with Business Central's Customer and Vendor modules, providing risk indicators directly on cards and lists, with comprehensive business entity management and automated data fetching capabilities.

## Key Features

- **Business Entity Management**: Central repository for monitored companies with comprehensive risk data including credit scores, debt balances, and payment marks
- **Automated Risk Assessment**: Fetch credit scores and risk ratings from third-party providers with configurable update schedules (Manual, Weekly, Monthly, Annually)
- **Custom Watchlists**: Create flexible criteria-based watchlists to monitor specific risk conditions with real-time notifications
- **Seamless BC Integration**: Direct integration with Customer and Vendor cards showing visual risk indicators with customizable styling
- **Role Center**: Dedicated Risk Manager workspace with key metrics, quick actions, and overview dashboards
- **API Integration**: Robust integration with TIC and compatible risk data providers supporting company search and risk data retrieval
- **Webhook Support**: Real-time updates from external risk data providers for immediate risk level changes
- **Comprehensive Logging**: Track all API calls and changes with detailed audit trail through API Call Ledger
- **Scheduled Updates**: Automatic periodic risk data updates via Job Queue with configurable frequency
- **Extensible Architecture**: 22+ integration events for custom business logic and third-party extensions

## Business Value

### For Credit Managers
- Monitor customer payment risk with real-time credit scores
- Receive proactive alerts when customers exceed risk thresholds
- Access comprehensive payment history and collection marks

### For Procurement Teams
- Assess vendor financial stability before major purchases
- Monitor supplier risk levels for supply chain continuity
- Track debt balances and payment reliability

### For Risk Managers
- Centralized view of all business entity risk portfolios
- Customizable watchlists for proactive risk monitoring
- Comprehensive reporting and audit trail capabilities

### For Finance Teams
- Up-to-date credit information for decision making
- Automated risk level indicators on standard BC pages
- Integration with existing customer and vendor workflows

## Target Platform

- **Business Central SaaS**: Version 26.0 and later
- **Deployment**: AppSource marketplace installation
- **API Integration**: Requires TIC or compatible risk data provider account

## Getting Started

To begin using BRC Risk Management:

1. **[Install the app](setup/)** from AppSource and complete the assisted setup wizard
2. **[Configure API access](setup/configuration/)** with your risk data provider credentials
3. **[Set up risk levels](setup/configuration/)** and notification preferences  
4. **[Create watchlists](user-guide/advanced-features/#watchlists)** for proactive monitoring
5. **[Assign permissions](reference/permissions/)** to users based on their roles

## Documentation Sections

### Setup & Configuration
Complete installation and configuration guide including API setup, risk level configuration, and initial data import.

### User Guide
Step-by-step instructions for daily operations, business entity management, and advanced features like watchlists and automated monitoring.

### Integrations
Technical details on Business Central integration, API connections, webhook configuration, and third-party system compatibility.

### Reference
Comprehensive reference materials including permissions, API documentation, integration events, and troubleshooting resources.

## Support

- **Documentation**: [https://docs.brightcom.se/sv/Products/BRCRisk](https://docs.brightcom.se/sv/Products/BRCRisk)
- **Publisher**: BrightCom Solutions AB
- **Privacy Policy**: [https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk](https://docs.brightcom.se/sv/PrivacyPolicy/BRCRisk)
- **EULA**: [https://brightcom.se/EULA/](https://brightcom.se/EULA/)

---

*Version 1.0.0.0 | Business Central 26.0+ | Last Updated: December 2025*