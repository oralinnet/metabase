# Metabase Installation Guide

This repository contains installation guides and configuration files for setting up Metabase on Linux systems. Metabase is an open-source business intelligence and analytics tool that lets you visualize and share data across your organization.

## 📋 Overview

This guide provides step-by-step instructions for installing and configuring Metabase with proper security measures and system service management.

## 🔧 Prerequisites

- Linux operating system (Ubuntu/CentOS/RHEL recommended)
- Root or sudo access
- JDK-21
- Minimum system requirements:
  - 2 CPU cores
  - 2GB RAM
  - 2GB storage space

## 📦 Installation

Detailed installation instructions can be found in [metabase.md](metabase.md). The installation process includes:

1. JDK-21 Installation
2. User and Directory Setup
3. Logging Configuration
4. Metabase Installation
5. Systemd Service Configuration
6. Service Activation
7. Firewall Setup

## 🚀 Quick Start

```bash
# Clone this repository
git clone https://github.com/oralinnet/metabase.git

# Navigate to the repository
cd metabase-installation

# Follow the instructions in metabase.md
```

## 📁 Repository Structure

metabase-installation/
├── README.md
├── metabase.md
└── configs/
└── metabase.service


## ⚙️ Configuration

The default configuration:
- Port: 3000
- Log file: `/var/log/metabase.log`
- Installation directory: `/opt/metabase`
- Service user: `metabase`

## 🔒 Security Considerations

- The service runs under a dedicated system user
- Proper file permissions are configured
- Systemd service isolation is implemented
- Logging is configured for audit purposes

## 🛟 Troubleshooting

Common issues and solutions:
1. If Metabase fails to start, check logs:
   ```bash
   journalctl -u metabase.service
   ```
2. For permission issues:
   ```bash
   ls -l /opt/metabase
   ls -l /var/log/metabase.log
   ```

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📞 Support

If you encounter any issues:
1. Check the [troubleshooting section](#troubleshooting)
2. Review the logs
3. Open an issue in this repository

## ✨ Acknowledgments

- [Official Metabase Documentation](https://www.metabase.com/docs/latest/)
- [OpenJDK Project](https://openjdk.org/)

---