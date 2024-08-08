# OpenVPN Install Script: Quick and Secure VPN Setup

Easily deploy a secure OpenVPN server on Debian, Ubuntu, Fedora, CentOS, Arch Linux, Oracle Linux, Rocky Linux, and AlmaLinux with this automated script.

## Key Features

- **Quick Setup**: Configure your VPN server in seconds.
- **Customizable Security**: Enhanced encryption settings for maximum security.
- **User Management**: Easily add, remove, or manage clients.
- **Multi-Platform**: Compatible with various Linux distributions.
- **Automated Headless Install**: Fully automated installation for seamless deployment.

## Supported Distributions

| Distribution        | Support        |
| ------------------- | -------------- |
| AlmaLinux 8         | ✅             |
| Amazon Linux 2      | ✅             |
| Arch Linux          | ✅             |
| CentOS 7            | ✅ 🤖          |
| CentOS Stream >= 8  | ✅ 🤖          |
| Debian >= 10        | ✅ 🤖          |
| Fedora >= 35        | ✅ 🤖          |
| Oracle Linux 8      | ✅             |
| Rocky Linux 8       | ✅             |
| Ubuntu >= 18.04     | ✅ 🤖          |

*Note: Distributions marked with 🤖 are regularly tested.*

## Installation Guide

### Step 1: Download the Script

```bash
curl -O https://raw.githubusercontent.com/AnonVM/OpenVPN-Installer/main/setup.sh
chmod +x setup.sh
```

### Step 2: Run the Script

```bash
sudo ./setup.sh
```

Follow the prompts to configure your VPN server.

### Step 3: Manage Clients

After installation, rerun the script to:

- **Add a Client**
- **Remove a Client**
- **Uninstall OpenVPN**

Client configuration files (`.ovpn`) will be saved in your home directory. Use them with your preferred OpenVPN client.

## Automated Headless Installation

You can automate the installation process:

```bash
AUTO_INSTALL=y ./setup.sh
```

Or set environment variables:

```bash
export AUTO_INSTALL=y
./setup.sh
```

Customizable options include:

- `APPROVE_INSTALL=y`
- `APPROVE_IP=y`
- `IPV6_SUPPORT=n`
- `PORT_CHOICE=1`
- `PROTOCOL_CHOICE=1`
- `DNS=1`
- `COMPRESSION_ENABLED=n`
- `CUSTOMIZE_ENC=n`
- `CLIENT=clientname`
- `PASS=1`

To set the server endpoint behind NAT:

```bash
ENDPOINT=$(curl -4 ifconfig.co)
```

For more customization, modify the `installQuestions()` function in the script.

### Headless User Addition

To automate user addition:

```bash
#!/bin/bash
export MENU_OPTION="1"
export CLIENT="foo"
export PASS="1"
./setup.sh
```

## Advanced Security and Encryption

OpenVPN defaults to strong encryption settings, further enhanced by this script:

- **AES-GCM**: Provides confidentiality, integrity, and authenticity.
- **TLS 1.2**: Enforced for optimal security.
- **ECDSA**: Default certificate type for efficiency and security.
- **tls-crypt**: Enabled by default for additional privacy and DoS protection.

## FAQ

### Recommended VPS Providers

- [AnonVM](https://anonvm.wtf): Privacy focused secure hostiing
---

### Recommended OpenVPN Clients

- **Windows**: [Official OpenVPN Community Client](https://openvpn.net/index.php/download/community-downloads.html)
- **Linux**: Use the `openvpn` package from your distribution. [APT repository for Debian/Ubuntu](https://community.openvpn.net/openvpn/wiki/OpenvpnSoftwareRepos)
- **macOS**: [Tunnelblick](https://tunnelblick.net/), [Viscosity](https://www.sparklabs.com/viscosity/), [OpenVPN for Mac](https://openvpn.net/client-connect-vpn-for-mac-os/)
- **Android**: [OpenVPN for Android](https://play.google.com/store/apps/details?id=de.blinkt.openvpn)
- **iOS**: [OpenVPN Connect](https://itunes.apple.com/us/app/openvpn-connect/id590379981)

---

### Is This Script NSA-Proof?

No. Even though this script enhances security, if you're trying to hide from the NSA, a VPN may not be enough. Review your threat models carefully.

---

### Where Can I Find OpenVPN Documentation?

Refer to the [OpenVPN Manual](https://community.openvpn.net/openvpn/wiki/Openvpn24ManPage) for detailed documentation on all options.

## Contributing and Support

### Discuss Changes

Open an issue to discuss significant changes before submitting a PR.

### Code Formatting

We enforce bash styling guidelines using [shellcheck](https://github.com/koalaman/shellcheck) and [shfmt](https://github.com/mvdan/sh). Configuration details are available in our [GitHub Actions file](https://github.com/angristan/openvpn-install/blob/master/.github/workflows/push.yml).

## Security and Encryption Details

> **Warning**: This section has not been updated for OpenVPN 2.5 and later.

### Compression

- **Default**: Compression is disabled to prevent VORACLE attacks.
- **Supported**: LZ0 and LZ4 (v1/v2) algorithms, though not recommended.

### TLS Version

- **Default**: TLS 1.2 enforced with `tls-version-min 1.2`.
- **Support**: TLS 1.2 is available since OpenVPN 2.3.3.

### Certificates

- **Default**: ECDSA with `prime256v1` curve.
- **Supported**: ECDSA curves (`prime256v1`, `secp384r1`, `secp521r1`) and RSA keys (2048, 3072, 4096 bits).

### Data Channel Encryption

- **Default**: AES-128-GCM.
- **Supported Ciphers**: AES-GCM and AES-CBC with varying key lengths.

### Control Channel Encryption

- **Default**: `TLS-ECDHE-*` with AES-128-GCM and SHA256.
- **Supported**: Configurable based on certificate type (ECDSA or RSA).

### Diffie-Hellman Key Exchange

- **Default**: ECDH with `prime256v1`.
- **Supported**: ECDH and classic DH keys.

### HMAC Digest Algorithm

- **Default**: SHA256.
- **Supported**: SHA256, SHA384, SHA512.

### `tls-auth` and `tls-crypt`

- **Default**: `tls-crypt` enabled for privacy and DoS protection.
- **Supported**: Both `tls-auth` and `tls-crypt`.
