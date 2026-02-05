# BrightCom Documentation Platform

Welcome to the BrightCom documentation platform! This GitHub repository drives
and maintains our public documentation site optimized for Business Central
Copilot Chat integration.

## 🎯 Purpose

This documentation platform is designed to:

- **Business Central Copilot Chat Ready**: URL structure optimized for maximum 2
  path segments for perfect Copilot integration
- **Living Documentation**: Keep our documentation current and always relevant
- **Community Driven**: Make it easy to request clarifications, improvements, or
  expansions
- **Up-to-Date Solutions**: Simple process to keep pace with our evolving
  solutions

## 🌐 Live Site

**Production Site**: https://dev.brightcom.se

## 🏗️ Architecture

### URL Structure (Copilot Optimized)

- **Root Level Products**: All BRC products at root level (e.g.,
  `/brc-connect/`, `/brc-logistics/`)
- **Flat Navigation**: Maximum 2 path segments for Business Central Copilot Chat
  compatibility
- **Clean URLs**: No content contamination between different apps

## 🤝 Contributing

We welcome feedback and contributions! Here's how you can help:

### 📝 Report Documentation Issues

Use our **streamlined issue reporting** with pre-filled templates:

- Click "Create documentation issue" on any page
- GitHub issue templates automatically populate with page context
- Page URL is pre-filled for easy reference

### 🐛 Request Content or Improvements

Visit our
[Issues](https://github.com/BrightComSolutions/BrightCom-PublicDocs/issues)
section to:

- Request new documentation
- Suggest improvements
- Report missing information
- Ask for clarification

### 📋 Issue Templates Available

- **Documentation Issue**: Report problems with existing content
- **Content Request**: Request new documentation or additional content

## 🛠️ Technical Details

### Built With

- **Hugo**: Static site generator (v0.151.0+)
- **Docsy Theme**: v0.13.0 with custom enhancements
- **GitHub Pages**: Hosting and deployment
- **Custom Templates**: Enhanced GitHub issue integration

### Local Development

```bash
# Clone repository
git clone https://github.com/BrightComSolutions/BrightCom-PublicDocs.git

# Run development server
hugo server --bind 0.0.0.0 --port 1313

# Build for production
hugo --minify
```

## 🎯 Business Central Copilot Integration

This documentation platform is specifically optimized for Business Central
Copilot Chat:

- **URL Compliance**: All product documentation uses 1-2 path segments maximum
- **Clean Structure**: Each BRC app can be configured with isolated, clean URLs
- **No Cross-Contamination**: Documentation is organized to prevent content
  mixing between apps

Perfect for configuring Business Central Copilot Chat with URLs like:

- `dev.brightcom.se/brc-connect/`
- `dev.brightcom.se/brc-logistics/`
- `dev.brightcom.se/partner-solutions/`

---

**Questions?** Create an issue or reach out to the BrightCom team!
