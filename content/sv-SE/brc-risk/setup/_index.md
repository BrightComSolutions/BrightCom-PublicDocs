---
title: "Setup & Installation"
linkTitle: "Setup"
weight: 20
description: >
  Complete setup guide for BRC Risk Management including installation, API configuration, and initial data setup.
---

## Overview

BRC Risk Management requires initial configuration to connect with your risk data provider and set up monitoring preferences. This section guides you through the complete setup process.

## Prerequisites

### Business Central Requirements
- **Version**: Microsoft Dynamics 365 Business Central SaaS 26.0 or later
- **License**: Valid Business Central license with appropriate user permissions
- **Network Access**: Outbound HTTPS access for API calls to risk data provider

### Risk Data Provider Requirements
- **TIC Account**: Active subscription with TIC or compatible risk data provider
- **API Credentials**: Valid API key and endpoint information
- **API Documentation**: Access to provider's API documentation for reference

### User Permissions
- **Installation**: SUPER permission set required for initial installation
- **Configuration**: SUPER or System Administrator permissions for setup
- **Usage**: See [Permissions Reference](../reference/permissions/) for role-based access

## Installation Process

### 1. AppSource Installation

1. **Access Extension Management**
   - Open Business Central
   - Search for "Extension Management"
   - Click **Extension Marketplace**

2. **Find BRC Risk Management**
   - Search for "BRC Risk Management" or "BrightCom Risk"
   - Verify publisher: **BrightCom Solutions AB**
   - Check compatibility: BC 26.0+

3. **Install Extension**
   - Click **Get it now**
   - Select your environment
   - Confirm installation
   - Wait for completion (2-5 minutes)

4. **Verify Installation**
   - Check Extension Management for "BRC Risk"
   - Status should show "Installed" with version 1.0.0.0

### 2. Initial Configuration

BRC Risk Management includes an **Assisted Setup Wizard** that guides you through initial configuration:

1. **Start Assisted Setup**
   - Search for "Assisted Setup"
   - Find "BRC Risk Setup"
   - Click **Start** or **Set up**

2. **Follow Wizard Steps**
   - [API Configuration](configuration/#api-configuration)
   - [Risk Level Setup](configuration/#risk-level-configuration)  
   - [Notification Preferences](configuration/#notification-setup)
   - [Permission Assignment](configuration/#user-permissions)

## Quick Start Checklist

After installation, complete these essential steps:

- [ ] **Run Assisted Setup Wizard**
- [ ] **Configure API connection** with your provider credentials
- [ ] **Set up risk levels** and styling preferences
- [ ] **Assign user permissions** based on roles
- [ ] **Test connection** with sample data fetch
- [ ] **Create initial watchlist** for monitoring
- [ ] **Link existing customers/vendors** to business entities

## Configuration Files

The following configuration areas are available:

### [Prerequisites](prerequisites/)
System requirements, license needs, and external dependencies.

### [Installation](installation/)
Detailed AppSource installation steps and verification procedures.

### [Configuration](configuration/)
API setup, risk levels, notifications, and user permissions.

## Next Steps

Once installation is complete:

1. **[Complete Configuration](configuration/)** - Set up API access and preferences
2. **[Assign Permissions](../reference/permissions/)** - Configure user access levels
3. **[Start User Guide](../user-guide/)** - Begin using the application
4. **[Create Watchlists](../user-guide/advanced-features/#watchlists)** - Set up proactive monitoring

## Support

If you encounter issues during setup:

- **[Troubleshooting Guide](../troubleshooting/)**
- **[Common Issues FAQ](../troubleshooting/faq/)**
- **[Contact Support](../reference/#support-information)**

---

*Installation typically takes 5-15 minutes including assisted setup. Have your API credentials ready before beginning.*