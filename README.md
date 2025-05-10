# Building-and-Securing-a-Small-Network

This project simulates a secure and scalable network for a small business environment. It uses VLANs to segment departments, assigns IPs dynamically through DHCP, and provides wireless connectivity for mobile users. Security features like port security, DHCP snooping, and Dynamic ARP Inspection protect the network from unauthorized access and attacks such as MAC flooding and ARP spoofing. This setup ensures reliable, organized, and protected communication across all departments and services.

## 🔧 Network Configuration Overview

### 🌐 VLANs
- **VLANs Used**: 10, 20, 30, 40
- **VLAN Purpose**:
  - VLAN 10: HR
  - VLAN 20: Finance
  - VLAN 30: IT
  - VLAN 40: Servers/Other
- **802.1Q Trunking**: Enabled between Router and Switches

### 🔁 VTP (VLAN Trunking Protocol)
- **VTP Domain**: `departmnets`
- **VTP Mode**:
  - 2 Right-side Switches: `Client`
- **VTP Password**: `159`

### ⚙️ EtherChannel (LACP)
- **Protocol Used**: LACP
- **Purpose**: Link aggregation between switches

### 📡 Router Configuration
- **Router-on-a-Stick** (IEEE 802.1Q subinterfaces)
  - `G0/0.10`, `G0/0.20`, `G0/0.30`, `G0/0.40`
- **DHCP Pools**:
  - VLAN 10, 20, and 30 each have a separate DHCP pool
  - DNS Server: `10.10.10.1`
- **DHCP Relay Information**: Trusted (`ip dhcp relay information trust-all`)

### 📶 Wireless Access Point
- **Assigned VLAN**: 30
- **Security**: WPA2-PSK
- **Password**: `12345678`
  
- **Assigned VLAN**: 10
- **Security**: WPA2-PSK
- **Password**: `87654321`
  
### 🔐 Port Security
- **Enabled On**: All access ports on all switches
- **Settings**:
  - `switchport port-security`
  - `switchport port-security mac-address sticky`
  - `switchport port-security maximum 1`
  - `switchport port-security violation shutdown`
- **Note**: All unused ports are manually shut down using `shutdown`

### 🛡️ Security Features

#### ✅ DHCP Snooping
- **Enabled VLANs**: 10, 20, 30, 40
- **Trusted Port**: Uplink to the multilayer switch

#### ✅ Dynamic ARP Inspection (DAI)
- **Enabled VLANs**: 10, 20, 30, 40
- **Trusted Port**: Uplink to the multilayer switch

### 📧 Email Server
An internal email server was deployed as part of the network infrastructure to facilitate communication between users across VLANs. The domain used for the email system is:

- **Domain Name**: `systememail.com`

#### Features:
- Supports sending and receiving internal mail within the campus network
- Connected to DNS for name resolution
- Accessible from multiple VLANs while protected by ACLs

This setup simulates a realistic enterprise or educational environment where internal communication is securely managed without depending on external mail services.

