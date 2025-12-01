---
title: "Frequently Asked Questions"
linkTitle: "FAQ"
weight: 10
type: docs
description: >
  Frequently asked questions and quick answers for common BRC Risk Management questions.
---

## Frequently Asked Questions

### General Questions

**Q: What is BRC Risk Management and what does it do?**
A: BRC Risk Management is a Business Central extension that provides automated risk assessment and monitoring of your business partners. It integrates with third-party risk data providers like TIC to fetch credit scores, debt information, and payment history, helping you make informed decisions about customers and vendors.

**Q: Which Business Central versions are supported?**
A: BRC Risk Management requires Business Central SaaS version 26.0 or later. It is not currently available for on-premises installations.

**Q: Do I need a separate subscription for risk data?**
A: Yes, you need an active subscription with a supported risk data provider (like TIC) to access external risk assessment data. The BRC Risk Management app handles the integration and presentation of this data within Business Central.

**Q: Can I use BRC Risk Management without internet access?**
A: No, the app requires outbound internet access to connect to risk data provider APIs. However, once risk data is fetched, it can be viewed offline until the next update.

### Installation and Setup

**Q: How long does installation take?**
A: Installation from AppSource typically takes 5-10 minutes. Initial setup and configuration through the assisted setup wizard takes an additional 15-30 minutes, depending on your configuration needs.

**Q: What information do I need before starting setup?**
A: You'll need:
- API credentials from your risk data provider
- API endpoint URL
- List of users who need access and their required permission levels
- Risk level thresholds and preferences for your organization

**Q: Can I test the system before full deployment?**
A: Yes, we recommend installing in a sandbox environment first to test configuration and train users before deploying to production.

**Q: Do I need special permissions to install the app?**
A: Yes, you need SUPER permission set in Business Central to install extensions from AppSource.

### Using the System

**Q: How often is risk data updated?**
A: Risk data update frequency is configurable per business entity. Options include:
- Manual: Update only when requested
- Weekly: Automatic updates every week
- Monthly: Automatic updates every month  
- Annually: Automatic updates every year

**Q: What happens if risk data provider is unavailable?**
A: The system will retry failed API calls automatically. Previously fetched risk data remains available for viewing, but new updates will be delayed until connectivity is restored.

**Q: Can I see risk information for companies not in my Customer/Vendor list?**
A: Yes, you can create Business Entities for any company and fetch their risk data, even if they're not currently customers or vendors. This is useful for prospect evaluation and competitive analysis.

**Q: How do I know when risk data was last updated?**
A: Each Business Entity shows a "Last Fetch DateTime" field indicating when risk data was most recently retrieved from the API.

### Data and Linking

**Q: Why can't I find a company when searching?**
A: Common reasons include:
- Company name spelling differences
- Company not in risk provider's database
- Company registered in unsupported country
- Try searching by VAT number or registration number instead

**Q: Can one Business Entity be linked to multiple customers?**
A: No, each Business Entity can only be linked to one customer and one vendor to maintain data integrity. However, you can create separate Business Entities if needed.

**Q: What if my customer/vendor has multiple legal entities?**
A: Create separate Business Entities for each legal entity and link them appropriately. This provides more accurate risk assessment for each distinct company.

**Q: Can I manually enter risk data?**
A: You can create Business Entities manually and enter available information, but automatic risk scoring requires API integration with a supported provider.

### Watchlists and Monitoring

**Q: How many watchlists can I create?**
A: There's no hard limit, but we recommend keeping the number reasonable (under 20) for performance reasons. Focus on the most important risk criteria.

**Q: How often are watchlists evaluated?**
A: Watchlists are typically evaluated when risk data is updated. You can also trigger manual evaluation from the watchlist page.

**Q: Can watchlists automatically take actions beyond notifications?**
A: Basic watchlists send notifications. Advanced actions (like blocking transactions or updating credit limits) can be implemented through custom development using integration events.

**Q: Why am I not receiving watchlist notifications?**
A: Check:
- Watchlist is enabled
- Notification settings are correctly configured
- Email/webhook endpoints are accessible
- SMTP settings in Business Central (for email notifications)

### Permissions and Access

**Q: What's the difference between VIEW, EDIT, and ADMIN permission sets?**
A: 
- **VIEW**: Read-only access to risk data, cannot fetch updates or modify data
- **EDIT**: Can fetch risk data, create/modify entities, manage watchlists
- **ADMIN**: Full access including setup configuration and system administration

**Q: Can I give different users access to different types of entities?**
A: The standard permission sets apply to all risk data. For granular control by entity type or other criteria, custom permission sets would need to be created.

**Q: Do users need special Business Central licenses?**
A: BRC Risk Management works with standard Business Central user licenses. Users need appropriate access to Customer/Vendor data based on their role.

### API and Technical

**Q: What happens if I exceed my API call limit?**
A: The system will stop making API calls when limits are reached. You'll need to wait for the limit to reset (typically monthly) or upgrade your subscription with the risk data provider.

**Q: Can I use multiple risk data providers?**
A: Currently, each Business Central environment supports one risk data provider. Contact BrightCom Solutions if you need multi-provider support.

**Q: How is my API key stored securely?**
A: API keys are stored using Business Central's encrypted storage system (IsoStorage) and are never displayed in clear text in the user interface.

**Q: Can I export risk data to other systems?**
A: Risk data can be exported through standard Business Central export functions (Excel, Word, etc.). For automated integration, custom development using integration events is recommended.

### Performance and Troubleshooting

**Q: The system seems slow when fetching risk data. What can I do?**
A: Try:
- Reducing batch sizes for bulk operations
- Scheduling updates during off-peak hours
- Checking your internet connection speed
- Contacting your risk data provider about API performance

**Q: Can I delete old API call logs?**
A: Yes, users with ADMIN permissions can delete old API call ledger entries for maintenance purposes. We recommend keeping at least 3-6 months of history.

**Q: What should I do if risk data looks incorrect?**
A: 
- First, try fetching fresh data to ensure it's current
- Compare with the risk provider's direct interface
- Check risk level threshold configuration
- Contact the risk provider if data discrepancies persist

### Costs and Licensing

**Q: What costs are involved beyond the AppSource app?**
A: Main additional costs:
- Risk data provider subscription (required)
- API usage charges (if applicable)
- Additional Business Central user licenses (if needed)

**Q: How much does a typical risk data provider subscription cost?**
A: Costs vary significantly based on:
- Number of API calls per month
- Geographic coverage needed
- Additional data services required
- Contact TIC or other providers for current pricing

**Q: Are there volume discounts for large numbers of entities?**
A: Contact your risk data provider about volume pricing. The BRC Risk Management app itself has no per-entity charges beyond the AppSource subscription.

### Integration and Customization

**Q: Can BRC Risk Management integrate with our CRM system?**
A: Yes, through custom development using the published integration events. Common integrations include Salesforce, Dynamics 365 Sales, and other CRM platforms.

**Q: Can we add custom fields to risk assessment?**
A: Yes, the system is designed for extensibility. Custom fields can be added to Business Entities, and custom risk calculation logic can be implemented via integration events.

**Q: Is there an API to access BRC Risk data from external systems?**
A: Risk data is stored in standard Business Central tables and can be accessed through Business Central's web services and APIs.

**Q: Can we customize the risk level calculations?**
A: Yes, you can define custom risk levels and thresholds. Advanced custom calculation logic can be implemented through integration events and custom development.

## Getting More Help

**Q: Where can I find more detailed documentation?**
A: Complete documentation is available in the following sections:
- [User Guide](../user-guide/) for daily operations
- [Setup Guide](../setup/) for configuration help
- [Reference Documentation](../reference/) for technical details

**Q: Who should I contact for technical support?**
A: Support escalation path:
1. Your internal Business Central administrator
2. Your Business Central implementation partner
3. BrightCom Solutions (app publisher)
4. Microsoft Business Central support (for platform issues)

**Q: Can I request new features or enhancements?**
A: Yes, feature requests can be submitted to BrightCom Solutions through their support channels. Popular requests are considered for future releases.

---

*Don't see your question here? Check the [Troubleshooting Guide](../troubleshooting/) or contact support.*