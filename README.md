# Building-and-Securing-a-Small-Network

This project simulates a secure and scalable network design suitable for a university campus or student dormitory. It separates users into VLANs based on departments or floors, assigns IPs dynamically using DHCP, and integrates wireless access for mobile devices. Security measures like port security, DHCP snooping, and Dynamic ARP Inspection prevent unauthorized access and common attacks such as MAC flooding and ARP spoofing. A firewall enforces traffic control between the internal network and external resources. This architecture ensures reliable, segmented, and secure connectivity for students, staff, and guest users—exactly what’s needed in a real campus or dorm environment.

## 🔧 Network Configuration Overview

### 🌐 VLANs
- **VLANs Used**: 10, 20, 30, 40
- **VLAN Purpose**:
  - VLAN 10: Department 1
  - VLAN 20: Department 2
  - VLAN 30: Department 3
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
