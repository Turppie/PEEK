# Configuración de Red de Invitados VLAN 80 por Sede
---
## **1. Madrid**

### Subred usada:
- **130.10.65.0/28**
    - Gateway: `130.10.65.1`
    - Access Router (WRT300N): `130.10.65.2`
    - DHCP pool: `130.10.65.3 - 130.10.65.14`
    - Broadcast: `130.10.65.15`

### Comandos:

```bash
ip dhcp excluded-address 130.10.65.1 130.10.65.2

ip dhcp pool INVITADOS_MADRID
  network 130.10.65.0 255.255.255.240
  default-router 130.10.65.1
  dns-server 8.8.8.8

interface FastEthernet0/0.80
 encapsulation dot1Q 80
 ip address 130.10.65.1 255.255.255.240
```

## **2. París**
### Subred usada:
- **130.10.65.16/28**
    - Gateway: `130.10.65.17`
    - Access Router (WRT300N): `130.10.65.18`
    - DHCP pool: `130.10.65.19` - `130.10.65.30`
    - Broadcast: `130.10.65.31`

### Comandos:

```bash
ip dhcp excluded-address 130.10.65.17 130.10.65.18

ip dhcp pool INVITADOS_PARIS
  network 130.10.65.16 255.255.255.240
  default-router 130.10.65.17
  dns-server 8.8.8.8

interface FastEthernet0/0.80
 encapsulation dot1Q 80
 ip address 130.10.65.17 255.255.255.240
```
## **3. Londres**
### Subred usada:
- **130.10.65.32/28**
    - Gateway: `130.10.65.33`
    - Access Router (WRT300N): `130.10.65.34`
    - DHCP pool: `130.10.65.35` - `130.10.65.46`
    - Broadcast: `130.10.65.47`

### Comandos:
```bash
ip dhcp excluded-address 130.10.65.33 130.10.65.34

ip dhcp pool INVITADOS_LONDRES
  network 130.10.65.32 255.255.255.240
  default-router 130.10.65.33
  dns-server 8.8.8.8

interface FastEthernet0/1.80
 encapsulation dot1Q 80
 ip address 130.10.65.33 255.255.255.240
``` 
---
# NOTAS IMPORTANTES

- Los pings no son constantes entre los dispositivos y con el access router.
- Los dispositicos hacen ping con el router (falla a veces)
- No hay access list implementada

---
# Visualización recomendada de este MD

Para una mejor experiencia de lectura de este documento en tu equipo:

- **Abre este archivo (`README.md`) en [Visual Studio Code](https://code.visualstudio.com/).**
- Instala la extensión gratuita **Markdown Preview Enhanced** desde la Marketplace de VS Code para una visualización optimizada.
- Alternativamente, puedes usar cualquier visor de archivos `.md` de tu preferencia, como **Typora**, **Obsidian** o previsualizadores web como **StackEdit**.

Para previsualizar en VS Code con la extensión instalada, abre el archivo y presiona:
- `Ctrl + Shift + V` (Windows/Linux) o `Cmd + Shift + V` (Mac) para activar la vista previa.

---