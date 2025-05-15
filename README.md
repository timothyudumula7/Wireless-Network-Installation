# Wireless-Network-Installation
# 🛠️ SOHO Router Installation – Lookout Mountain Project

**Author:** Timothy Udumula  
**Organization:** Lookout Mountain Technologies

This documentation covers a six-cabin router installation using Ubiquiti and MikroTik devices. The content is presented in unified sections for clarity.

---

## 📡 Section 1: IP Address Scheme

Each cabin is assigned both an antenna and router IP for easy management. All devices use a `/24` subnet (`255.255.255.0`).

| Cabin | Ubiquiti Antenna IP | MikroTik AP IP  | SSID / Password  | Notes            |
|-------|---------------------|------------------|------------------|------------------|
| 6     | 192.168.1.25        | 192.168.25.1     | —                | DHCP server      |
| 5     | 192.168.1.30        | 192.168.30.1     | Cabin-5 / ellie777| AP only          |
| 4     | 192.168.1.35        | 192.168.35.1     | Cabin-4 / ellie777| AP only          |
| 3     | 192.168.1.40        | 192.168.40.1     | Cabin-3 / ellie777| AP only          |
| 2     | 192.168.1.45        | 192.168.45.1     | Cabin-2 / ellie777| AP only          |
| 1     | 192.168.1.50        | 192.168.50.1     | Cabin-1 / ellie777| AP only          |

---

## 🖧 Section 2: Network Diagram

```
[ISP/Public IP]
     |
[Cabin 6 Main Router + DHCP]
     |
[Unifi airMAX Lite AP] ──→ [Lightbeam 5AC Antennas] ──→ [Cabin MikroTik Routers]
```

This diagram shows the simplified logical flow from the internet source through the antenna bridges to individual cabin routers.

---

## 🧾 Section 3: Configuration Snippets

### 🔧 Antenna Config – Cabin 3

- Device: Ubiquiti Lightbeam 5AC  
- Static IP: `192.168.1.40`  
- Gateway: `192.168.1.1`  
- Subnet: `255.255.255.0`  
- DHCP: Disabled (handled by Cabin 6)

### 🔧 MikroTik AP Config – Cabin 1

- Device: MikroTik hAP Lite  
- IP Address: `192.168.50.1`  
- Interface: Bridge  
- Mode: AP Bridge  
- SSID: `Cabin-1`  
- Password: `ellie777`  
- DHCP Client: Enabled  
- LAN port 2: Connects to antenna  
- NAT masquerade disabled (operates as AP)

---

## 📝 Section 4: Notes & Testing

- All Ethernet cabling uses **T568-B** standard and was verified.
- Wireless password across all cabins is: **`ellie777`**
- **Traceroute Example (Cabin 3):**
  1. 192.168.40.1 (MikroTik AP)
  2. 192.168.1.1 (Gateway router)
  3. Public IP (`200.x.x.x`)

---

## 🔁 Section 5: Device Flow

### Physical Connection Order

1. **Main Router (Cabin 6)** → Unifi airMAX Lite AP  
2. **airMAX** → Lightbeam 5AC (Point-to-Point)  
3. **Lightbeam 5AC** → MikroTik Router (set as AP)  

All routing, DHCP, and DNS filtering is handled centrally at Cabin 6.

---

✅ Deployment complete. For maintenance or changes, refer to Ubiquiti & MikroTik manuals.
