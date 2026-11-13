# 01. Archivos Importantes y Diagnóstico del Sistema

Este módulo recopila los archivos fundamentales de configuración y logs de las distribuciones Linux (especialmente Debian y Ubuntu), así como los comandos para consultar el estado del hardware, memoria y sistema operativo.

---

## 1. Archivos Importantes de Configuración y Logs

| Archivo / Comando | Descripción | Ejemplo / Uso |
| :--- | :--- | :--- |
| `journalctl -f` | Monitoreo de logs del sistema en tiempo real (systemd). | Filtrar por servicio Apache:<br>`journalctl -u apache2.service -f` |
| `/var/log/syslog` | Registro histórico de eventos del sistema (Syslog tradicional). | *Nota: en Debian/Ubuntu modernos no viene por defecto; instalar con:*<br>`sudo apt install rsyslog` |
| `dmesg` | Muestra los mensajes del buffer del kernel (registro del arranque y hardware detectado). | `dmesg \| grep -i eth` |
| `/etc/network/interfaces`<br>`/etc/resolv.conf` | Configuración tradicional de interfaces de red y servidores DNS en Debian. | Reiniciar servicio de red en Debian:<br>`systemctl restart networking.service` |
| `/etc/netplan/50-cloud-init.yaml` | Configuración de red declarativa mediante Netplan en Ubuntu Server. | Aplicar cambios en la red:<br>`sudo netplan apply` |
| `/etc/hostname` | Contiene el nombre del equipo (*hostname*). | Editar o consultar: `cat /etc/hostname` |
| `/etc/hosts` | Resolución estática de nombres de dominio local (DNS local). | `192.168.0.35 debian1` |
| `/etc/fstab` | Tabla de sistemas de archivos y puntos de montaje automáticos al inicio. | Configuración de discos, particiones y montajes persistentes. |
| `/etc/apt/sources.list` | Listado de repositorios de software de APT. | Configuración de orígenes de paquetes oficiales y de terceros. |
| `.bashrc`<br>`.bash_profile`<br>`.bash_logout` | Scripts de configuración del terminal y entorno de usuario: perfiles de sesión, alias, variables de entorno y limpieza al salir. | Editar variables o alias del usuario:<br>`nano ~/.bashrc` |

---

## 2. Información del Sistema y Diagnóstico

Comandos esenciales para inspeccionar las características del sistema operativo, memoria RAM, CPU y almacenamiento.

| Comando | Descripción | Ejemplo de Sintaxis |
| :--- | :--- | :--- |
| `lsb_release -a` | Muestra información detallada de la distribución Linux instalada. | Alternativa estándar:<br>`cat /etc/os-release` |
| `gnome-shell --version` | Muestra la versión instalada del entorno gráfico GNOME. | `gnome-shell --version` |
| `uname -a` | Información completa del kernel, versión del sistema y arquitectura de la máquina. | `uname -a` |
| `free` | Muestra el estado de la memoria RAM y la memoria de intercambio (*Swap*). | En megabytes: `free -m`<br>Formato legible para humanos: `free -h` |
| `df -hT` | Muestra el espacio libre y ocupado en los sistemas de archivos montados, indicando el tipo de FS (`-T`). | `df -hT` |
| `du -h [directorio]` | Muestra el tamaño ocupado por carpetas y ficheros. | Tamaño total de un directorio sin desglosar subcarpetas:<br>`du -hs /home` |
| `lsblk` ; `fdisk -l` | Información de bloques, dispositivos de disco y particiones. | Consultar UUID de dispositivos:<br>`blkid -s UUID` |

---

## 📌 Enlaces Relacionados
- [Ir al índice principal (README.md)](./README.md)
- [Módulo siguiente: 02. Primeros Comandos y Ayuda](./02-primeros-comandos-y-ayuda.md)
