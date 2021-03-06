# CONFIGURACIÓN DE RED


## Problemas de los servicios de red en linux

En debian, si tenemos la interfaz gráfica instalada tenemos dos servicios de red:

  1. NetworkManager (de la interfaza gráfica)
  2. networking

Debemos desabilitar y parar uno de ellos en este caso desabilitaremos el de la interfaz gráfica (NetworkManager)

```bash
# Esto para el servicio
-> systemctl stop NetworkManager
```

```bash
# Esto arranca el servicio
-> systemctl start NetworkManager
```

```bash
# Esto deshabilita el servicio
-> systemctl disable NetworkManager
```

```bash
# Esto habilita el servicio
-> systemctl enable NetworkManager
```

```sh
# Esto muestra el estado del servicio/s
-> systemctl status NetworkManager
-> systemctl status networking
```

## Fichero de configuarción de red

El fichero para grabar la configuración de red permanentemente es /etc/network/interfaces

## COMANDO IP

### Mostrar las interfaces de red

- Sintaxis: ip \<address|addr|a\> [show dev interfaz]
- Sustituye a `ifconfig`

```bash
$ ip a
$ ip addr
$ ip address
$ ip a show dev enp0s3
```

### Mostrar tabla de enrutamiento

- Sintaxis: ip route 
- Sustituye a `route -n`

```bash
$ ip route
$ ip ro
$ ip r
```

### Configuar una interfaz de red

- Sintaxis: ip \<address|addr|a\> \<add|del> direccion dev disposito

```bash
-> ip a add 192.168.10.20/24 dev enp0s3
```

```bash
-> ip a del 192.168.10.20/24 dev enp0s3
```

### Ver puertas de enlace

```bash
$ ip r
$ ip ro
$ ip route
```

### Añadir/borrar una puerta de enlace
- sintaxis: ip route \<add|del\> \<dirección\> via \<gateway\> 
```bash
# Debemos tener una ip dentro de la misma red
-> ip r add 20.0.0.0/24 via 192.168.10.254
```

```bash
-> ip r del 20.0.0.0/24
```

### Borrar configuración de red del dispositivo

```bash
-> ip a flush dev enp0s3
```

### Fichero de configuración de red

- El fichero de configuración de red **en debian** es **/etc/network/interfaces** 
- Configuración manual:

```
auto enp0s3
iface enp0s3 inet static
address 192.168.1.101
netmask 255.255.255.128
gateway 192.168.1.1
```
- Configuración automática

```
auto enp0s3
iface enp0s3 inet dhcp
```