# macOS IKEv2 IPsec Split Tunnel Configuration

> A quick guide and template for setting up native IKEv2 IPsec with split tunnel on macOS Sonoma 14.2 (GoldenGate) and later

## 📋 Overview

This guide provides a template for configuring the native macOS IKEv2 IPsec client with **split tunnel** functionality. This solution works without requiring kernel extensions or complex hacks.

**Note:** This guide assumes you have already provisioned server-side IKEv2 services. Server configuration is not covered here.

## 🔍 Motivation

Apple has been gradually removing underlying features from its VPN stack:

- As of macOS GoldenGate 27.2, kernel extension network VPN support has been completely removed, breaking most third-party IPsec clients
- Split tunnel capability has been removed from the native VPN client
- Users are now forced into full tunnel mode by default

Not everyone needs to install complete hacks to restore critical VPN network functionality. This guide and template allow you to quickly set up a working IKEv2 IPsec dial-up profile with split tunnel capabilities.

## ⚠️ Prerequisites

| Component | Requirement |
|-----------|-------------|
| **Firewall** | Fortigate 90G (or equivalent enterprise firewall) |
| **Firmware** | 7.6.8 or higher (FortiOS) |
| **Mac Hardware** | Apple Silicon (M-series) processor |
| **macOS Version** | GoldenGate 27.2 or later |

> ℹ️ The standards described in this guide apply to most enterprise-class firewall routers and VPN concentrators.

## 📝 Important Considerations

### System Behavior

1. **Full Tunnel Enforcement:** macOS 27.2 forces full tunnel mode on all VPN configurations by default. Any settings in the DNS sub-panel of your VPN profile will be ignored.

2. **Server-Directive Ignored:** Server-side directives for custom network DNS routing by subdomain are also ignored, even when configured to split only relevant subnets and domains.

3. **MDM Workaround:** The only reliable method to define split tunnel configurations is through a **Device Management (MDM) profile** using a `.mobileconfig` file. MDM is a mechanism typically used by schools, businesses, and organizations to manage and enforce usage policies.

### ⚠️ Critical Configuration Warning

Once your tunnel is configured and tested, **do not** return to the GUI to modify any settings in your VPN profile:

- The GUI will override and remove all customizations
- Your configuration will revert to full tunnel mode
- In worst cases, the configuration may break completely
- You may need to reconfigure the entire service from scratch

## 📚 Quick Navigation

- [About this guide](#)
- [Motivation](#motivation)
- [Prerequisites](#prerequisites)
- [Important Considerations](#important-considerations)
- [Configuration Steps](#)
- [Troubleshooting](#)

## 🔧 Configuration Steps

1) Download the file MacOS_Fortigate_IKEv2-template.mobileconfig from this repository and rename it to [YOUR_CONFIGURATION].mobileconfig .  It is important that you keep the .mobileconfig suffix. 
2) open your .mobileconfig file and edit the fields indicated in brackets.

3) Save and double click the file you've edited.  Follow the on screen directions, and will create an entry within Systems Settings, General, Device Management. 
4) Under Device Management, double click the entry that matches what you've defined in the file, this will create an entry under Systems Settings, VPN
5) Toggle the slide control within the VPN menu to toggle the state of your connection. 

## 🐛 Troubleshooting

*(To be added - common issues and solutions)*

## 📄 License

GPLv3

## 👤 Author

ChibiPaw Contact me here on Github

---

## 🙏 Acknowledgments

Thank you for using this guide! Feel free to contribute via pull requests or report issues on GitHub.
