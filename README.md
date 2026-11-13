# Resumen de Linux Básico — ASIR / ISO

<p align="center">
  <img src="img/logo_mdt.png" alt="Logo MDT" width="120" style="vertical-align: middle; margin-right: 20px;" />
  <img src="img/licencia_cc.png" alt="Licencia Creative Commons BY-NC-SA" width="130" style="vertical-align: middle;" />
</p>

Guía completa y estructurada de **Linux Básico**, basada en los contenidos formativos del ciclo **ASIR** (*Administración de Sistemas Informáticos en Red*) y el módulo **ISO** (*Implantación de Sistemas Operativos*).

Este repositorio organiza de forma modular todos los comandos esenciales, archivos de configuración, sintaxis explicadas con diagramas e imágenes originales, y buenas prácticas en administración de sistemas GNU/Linux.

---

## 📑 Estructura de Contenidos

| Nº | Módulo | Descripción Temática |
| :---: | :--- | :--- |
| **01** | [**Archivos Importantes y Diagnóstico del Sistema**](./01-archivos-importantes-y-sistema.md) | Configuración de red (Debian/Ubuntu), `/etc/fstab`, `/etc/hosts`, logs con `journalctl`, `dmesg`, `syslog`, y diagnóstico de hardware (`uname`, `free`, `df`, `du`). |
| **02** | [**Primeros Comandos, Ayuda y Sesión**](./02-primeros-comandos-y-ayuda.md) | Recursos SMB, ayuda con `man`, `whatis`, `apropos`, historial (`history`, `!N`, `Ctrl+r`), operadores `;` y `&&`, apagado programado (`shutdown`, `poweroff`, `reboot`), y alias. |
| **03** | [**Gestión de Ficheros y Directorios**](./03-ficheros-y-directorios.md) | Visualización (`cat`, `head`, `tail -f`, `diff`, `wc`), navegación con `cd`, listados con `ls`, inodos, enlaces duros y simbólicos (`ln`), y búsquedas con `find -exec`. |
| **04** | [**Empaquetado y Compresión**](./04-empaquetado-y-compresion.md) | Utilidades de compresión y empaquetado: formatos `.zip`, `.tar.gz` y `.tar.bz2`, banderas de compresión, extracción y previsualización. |
| **05** | [**Filtros y Procesamiento de Texto**](./05-filtros-y-procesamiento-texto.md) | Manipulación de datos en tuberías: `sort`, `tr`, `sed`, `grep`, `cut`, `paste`, lenguaje `awk` y uniones relacionales con `join`. |
| **06** | [**Permisos, Usuarios y Seguridad**](./06-permisos-y-seguridad.md) | Identidad (`id`), permisos tradicionales con `chmod` (notación octal y simbólica), máscara `umask`, cambio de dueño con `chown` y atributo especial *Sticky bit*. |
| **07** | [**Gestión de Paquetes y Administración Remota**](./07-gestion-paquetes-y-ssh.md) | Variable de entorno `PATH`, gestión completa con APT (`update`, `upgrade`, `install`, `purge`), generación de claves SSH y transferencia con `scp`. |
| **08** | [**Discos, Particiones y Montaje**](./08-discos-particiones-y-montaje.md) | Particionado con `fdisk`, formato con `mkfs.ext4`, montaje con `mount`/`umount`, entorno `chroot`, y comparativa detallada entre `fdisk -l`, `blkid`, `df -hT` y `lsblk -f`. |

---

## 🚀 Resumen Rápido de Comandos Esenciales (Cheat-Sheet)

### 1. Sistema, Red y Logs
```bash
journalctl -f                            # Ver logs del sistema en tiempo real
journalctl -u servicio.service -f        # Ver logs de un servicio concreto (ej. apache2)
uname -a                                 # Información del kernel y arquitectura
free -h                                  # Uso de memoria RAM y Swap en formato humano
df -hT                                   # Espacio y tipo de FS montados
du -hs /directorio                       # Tamaño total ocupado por una carpeta
netplan apply                            # Aplicar configuración de red (Ubuntu)
systemctl restart networking.service     # Reiniciar red (Debian)
```

### 2. Archivos y Directorios
```bash
ls -lha                                  # Listar todo detallado, ocultos y legible
cd .. ; cd -                             # Subir al directorio padre / volver al anterior
cp -r carpeta_origen destino/            # Copiar directorios recursivamente
mv archivo /nueva/ruta/                  # Mover o renombrar archivos/carpetas
rm -rf carpeta_a_borrar                  # Borrado forzado y recursivo
find / -iname "*.log" -exec rm -f {} \;  # Buscar y ejecutar acciones sobre archivos
ln -s /ruta/destino enlace               # Crear enlace simbólico
```

### 3. Filtros y Flujos de Texto
```bash
grep -rnw '/ruta' -e 'texto'             # Búsqueda recursiva de texto exacto
sort -t: -k2 archivo.txt                 # Ordenar por el 2º campo separado por ":"
cut -d: -f1,3 /etc/passwd               # Extraer columnas 1 y 3 delimitadas por ":"
sed -i 's/antiguo/nuevo/g' fichero       # Sustituir cadenas directamente en el fichero
awk -F: '$3 >= 1000 {print $1, $3}' /etc/passwd  # Extraer usuarios con UID >= 1000
```

### 4. Permisos y Usuarios
```bash
chmod 755 archivo.sh                     # rwxr-xr-x (u=rwx, g=rx, o=rx)
chmod u=rwx,g+r,o-rwx secreto.txt        # Configuración simbólica
chown -R usuario:grupo /directorio       # Modificar propietario y grupo recursivamente
chmod o+t /carpeta_compartida            # Activar Sticky Bit (solo el dueño puede borrar)
```

### 5. Compresión y Empaquetado
```bash
tar -zcvf archivo.tar.gz /carpeta/       # Empaquetar y comprimir en gzip (.tar.gz)
tar -zxvf archivo.tar.gz -C /destino/    # Extraer .tar.gz en carpeta destino
tar -jcvf archivo.tar.bz2 /carpeta/      # Empaquetar y comprimir en bzip2 (.tar.bz2)
tar -jxvf archivo.tar.bz2 -C /destino/   # Extraer .tar.bz2 en carpeta destino
zip -r comprimido.zip carpeta/           # Comprimir carpeta en .zip
unzip comprimido.zip -d /destino/        # Descomprimir archivo .zip
```

### 6. Paquetes y Administración Remota (SSH)
```bash
sudo apt update && sudo apt upgrade -y   # Actualizar índices y paquetes
sudo apt install --reinstall paquete     # Reinstalar paquete
sudo apt purge paquete && sudo apt autoremove  # Eliminar con configuración y limpiar dependencias
ssh-keygen -t ed25519                    # Generar claves SSH
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@servidor  # Copiar clave pública al servidor
scp -r /local/ user@servidor:/remoto/    # Copia remota cifrada por SSH
```

### 7. Almacenamiento y Discos
```bash
sudo fdisk -l                            # Listar tablas de particiones de todos los discos
sudo blkid                               # Ver UUID y tipos de sistemas de ficheros
lsblk -f                                 # Árbol visual de bloques, FS y puntos de montaje
sudo mount /dev/sdb1 /mnt                # Montar partición en /mnt
sudo umount /mnt                         # Desmontar partición
```

---

## 🖼️ Directorio de Imágenes (`img/`)

Todas las ilustraciones, capturas y diagramas de sintaxis extraídos del material original se encuentran organizados con nombres descriptivos en la carpeta [`img/`](./img/):

* `logo_mdt.png`: Logo identificativo del material docente.
* `licencia_cc.png`: Licencia Creative Commons (BY-NC-SA).
* `man_atajos.png`: Atajos de teclado en el manual `man`.
* `shutdown_opciones.png`: Opciones y sintaxis de apagado con `shutdown`.
* `poweroff_fuerza.png`: Forzado de apagado con `poweroff -f`.
* `alias_ejemplos.png`: Creación de alias en terminal.
* `cd_navegacion.png`: Navegación con `cd`.
* `ls_opciones.png`: Modificadores `-l`, `-a`, `-R`, `-d` de `ls`.
* `find_ejemplo.png`: Ejemplo práctico de `find` con `-exec`.
* `zip_sintaxis.png`: Sintaxis de `zip` y `unzip`.
* `targz_sintaxis.png`: Sintaxis de `tar.gz`.
* `tarbz2_sintaxis.png`: Sintaxis de `tar.bz2`.
* `sort_diagrama.png`: Diagrama de campos y opciones de `sort`.
* `tr_sintaxis.png`: Opciones de traducción de caracteres con `tr`.
* `sed_sintaxis.png`: Sustitución de cadenas con `sed`.
* `grep_opciones.png`: Opciones y modificadores de `grep`.
* `cut_ejemplos.png`: Extracción de columnas con `cut`.
* `awk_diagrama.png`: Diagrama de sintaxis condicional de `awk`.
* `join_diagrama.png`: Diagrama relacional de campos con `join`.
* `chmod_tabla_permisos.png`: Estructura de permisos y usuarios en Linux.
* `apt_cuadro_completo.png`: Esquema completo del gestor de paquetes APT.
* `discos_comparativa.png`: Cuadro comparativo de comandos de discos (`fdisk`, `blkid`, `df`, `lsblk`).

---

## 📄 Licencia

Este material se distribuye bajo la licencia **Creative Commons Reconocimiento-NoComercial-CompartirIgual (CC BY-NC-SA)**.
