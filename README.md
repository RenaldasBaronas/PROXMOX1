# PROXMOX1


Šiame repository pateikiami Proxmox LXC konteinerio kūrimo pavyzdžiai ir komandos.
# Proxmox LXC konteinerio kūrimo pavyzdys

## 1. LXC kūrimas per GUI

1. Prisijunk prie Proxmox web sąsajos (https://proxmox-server:8006)
2. Kairėje pasirink "Create CT"
3. Įvesk:
   - CT ID: pvz. 101
   - Hostname: pvz. ubuntu-lxc
4. Pasirink šabloną (template), pvz. ubuntu-22.04-standard
5. Nustatyk root slaptažodį
6. Storage: local-lvm arba local
7. Disk size: pvz. 8GB
8. CPU: pvz. 2 cores
9. RAM: pvz. 2048 MB
10. Network:
    - Bridge: vmbr0
    - IPv4: DHCP arba Static
11. Spausti "Finish"

## 2. LXC kūrimas per Proxmox terminalą (PVE shell)

### Atsisiųsti template:
pveam update
pveam download local ubuntu-22.04-standard_22.04-1_amd64.tar.zst

### Sukurti konteinerį:
pct create 101 /var/lib/vz/template/cache/ubuntu-22.04-standard_22.04-1_amd64.tar.zst \
--hostname ubuntu-lxc \
--cores 2 \
--memory 2048 \
--swap 512 \
--rootfs local-lvm:8 \
--net0 name=eth0,bridge=vmbr0,ip=dhcp \
--password Gendalfas123456-
pct start 101
pct enter 101
