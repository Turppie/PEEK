# 🛡️ Configuración de Access Points – Área de Administración

Este documento detalla la configuración de los Access Points (WAP) para la red inalámbrica interna (WIFI-B) destinada al área de Administración en cada sede de Peek. Se utilizan IPs estáticas y autenticación WPA2-PSK.

---

## 📍 1. Sede Madrid

- **VLAN**: Administración  
- **IP del Access Point**: `130.10.0.35`  
- **Máscara de Subred**: `255.255.255.192`  
- **Gateway**: `130.10.0.1`  
- **SSID**: `WIFI_ADMIN_MADRID`  
- **Autenticación**: `WPA2-PSK`  
- **Rango IP sugerido para dispositivos**: `130.10.0.36 – 130.10.0.44`  

### 🔧 Configuración en Packet Tracer:
**En la pestaña GUI del AP:**

- SSID: `WIFI_ADMIN_MADRID`
- Authentication: `WPA2-PSK`
- Passphrase: `adminpeek2024`
- Max Connections: 10 (opcional)
- Channel: Auto o Default

**En la pestaña Config > FastEthernet0:**

- IP Address: `130.10.0.35`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `130.10.0.1`

---

## 📍 2. Sede París

- **VLAN**: Administración  
- **IP del Access Point**: `130.10.64.35`  
- **Máscara de Subred**: `255.255.255.192`  
- **Gateway**: `130.10.64.1`  
- **SSID**: `WIFI_ADMIN_PARIS`  
- **Autenticación**: `WPA2-PSK`  
- **Rango IP sugerido para dispositivos**: `130.10.64.36 – 130.10.64.44`  

### 🔧 Configuración en Packet Tracer:
**En la pestaña GUI del AP:**

- SSID: `WIFI_ADMIN_PARIS`
- Authentication: `WPA2-PSK`
- Passphrase: `adminpeek2024`

**En la pestaña Config > FastEthernet0:**

- IP Address: `130.10.64.35`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `130.10.64.1`

---

## 📍 3. Sede Londres

- **VLAN**: Administración  
- **IP del Access Point**: `130.10.32.35`  
- **Máscara de Subred**: `255.255.255.192`  
- **Gateway**: `130.10.32.1`  
- **SSID**: `WIFI_ADMIN_LONDRES`  
- **Autenticación**: `WPA2-PSK`  
- **Rango IP sugerido para dispositivos**: `130.10.32.36 – 130.10.32.44`  

### 🔧 Configuración en Packet Tracer:
**En la pestaña GUI del AP:**

- SSID: `WIFI_ADMIN_LONDRES`
- Authentication: `WPA2-PSK`
- Passphrase: `adminpeek2024`

**En la pestaña Config > FastEthernet0:**

- IP Address: `130.10.32.35`
- Subnet Mask: `255.255.255.192`
- Default Gateway: `130.10.32.1`

---

## ✅ COMANDOS EN EL SWITCH CONECTADO AL ACCESS POINT

Configura el puerto del switch donde se conecta el Access Point en **modo acceso** y asígnalo a la **VLAN 10 (Administración)**:

```bash
Switch> enable
Switch# configure terminal
Switch(config)# interface fa0/x
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit
```

🔁 Reemplaza fa0/x por el puerto específico al que está conectado el Access Point (por ejemplo: fa0/5).

-Además, asegúrate de que la subinterfaz del router correspondiente a VLAN 10 esté activa y correctamente configurada para permitir el enrutamiento entre VLANs y el acceso a la red.
