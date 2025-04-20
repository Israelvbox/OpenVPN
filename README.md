# 🛡️ Instalador Automático de OpenVPN

Este script bash automatiza completamente la instalación y configuración de un servidor **OpenVPN**, permitiendo agregar y revocar usuarios fácilmente. Basado en el proyecto original de [Nyr](https://github.com/Nyr/openvpn-install), este fork ofrece una solución todo en uno, ideal para despliegues rápidos en servidores compatibles.

## 📌 Características

- Instalación automatizada de OpenVPN y dependencias.
- Configuración de red, puertos, protocolo y DNS personalizados.
- Soporte para IPv4 e IPv6.
- Reglas de firewall configuradas automáticamente (iptables o firewalld).
- Generación de certificados de cliente y archivos `.ovpn`.
- Gestión de usuarios: añadir, revocar o eliminar clientes desde un menú interactivo.
- Compatible con sistemas Debian, Ubuntu, CentOS, Fedora, AlmaLinux y Rocky Linux.

## ⚙️ Requisitos

- Sistema operativo compatible:
  - Debian 11+
  - Ubuntu 22.04+
  - CentOS 9+
  - Fedora / AlmaLinux / Rocky Linux (versiones modernas)
- Permisos de superusuario (root)
- Dispositivo `/dev/net/tun` habilitado
- `bash`, `curl` o `wget` instalados
- Acceso a Internet

## 🚀 Instalación

```bash
curl -O https://tuservidor.com/ovpn.sh
chmod +x ovpn.sh
sudo ./ovpn.sh
```

## 🧠 Uso

### Primera ejecución

Al ejecutarlo por primera vez, el script te guiará por un asistente interactivo que te pedirá:

- Seleccionar la IP pública si el servidor está detrás de NAT.
- Protocolo (UDP o TCP).
- Puerto.
- Servidor DNS para clientes (Google, 1.1.1.1, OpenDNS, etc.).
- Nombre del primer cliente.

Después de confirmar, instalará OpenVPN, generará los certificados y te creará el archivo `cliente.ovpn` en tu directorio `~/`.

### Menú interactivo (tras la instalación)

Si ejecutas el script nuevamente, verás el siguiente menú:

```
1) Añadir un nuevo cliente
2) Revocar un cliente existente
3) Eliminar OpenVPN
4) Salir
```

### ➕ Añadir cliente

```bash
sudo ./ovpn.sh
# Selecciona la opción 1
# Introduce un nombre único
```

Se generará un archivo `~/nombre_cliente.ovpn`.

### ❌ Revocar cliente

```bash
sudo ./ovpn.sh
# Selecciona la opción 2
# Elige el cliente de la lista
# Confirma la revocación
```

El certificado será revocado y el cliente ya no podrá conectarse.

### 🗑️ Eliminar OpenVPN

```bash
sudo ./ovpn.sh
# Selecciona la opción 3
# Confirma la desinstalación
```

Elimina OpenVPN, los certificados, configuración de firewall y dependencias.

## 📂 Archivos generados

| Ruta                             | Descripción                                                 |
|----------------------------------|-------------------------------------------------------------|
| `/etc/openvpn/server/`           | Configuración del servidor, claves y certificados           |
| `/etc/openvpn/server/easy-rsa/`  | PKI usada para la gestión de certificados                   |
| `~/cliente.ovpn`                 | Archivo de configuración del cliente listo para descargar  |

## 📐 Personalización

Durante la instalación puedes elegir:

- Protocolo: UDP (recomendado) o TCP
- Puerto: por defecto 1194, configurable
- DNS: Google, Cloudflare, OpenDNS, AdGuard, Quad9 o el DNS del sistema

## 🔐 Seguridad

- Cifrado del canal de control usando `tls-crypt`
- Algoritmo de autenticación: `SHA512`
- Certificados con validez de 10 años
- Soporte completo para revocación de certificados

## 🧪 Ejemplo de uso rápido

Para añadir más clientes después:

```bash
sudo ./ovpn.sh
# Opción 1 → Añadir nuevo cliente
```

Para revocar clientes existentes:

```bash
sudo ./ovpn.sh
# Opción 2 → Revocar cliente
```
