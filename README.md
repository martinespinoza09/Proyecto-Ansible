# Proyecto-Ansible
# Redes Avanzadas 1

**Martín Espinoza R.**  
**INACAP**

## Descripción

Este proyecto implementa una topología de tres routers MikroTik en GNS3, automatizada con Ansible, utilizando enlaces GRE y protocolo OSPF para el enrutamiento dinámico entre las redes.

## Objetivo

Automatizar la configuración base de routers MikroTik, crear túneles GRE entre los nodos y establecer OSPF para lograr conectividad entre las redes LAN de cada router.

## Topología

La topología está compuesta por tres routers:

- R1
- R2
- R3

Cada router tiene:

- Una interfaz de gestión.
- Una interfaz LAN.
- Dos interfaces WAN.
- Dos túneles GRE hacia los otros routers.

## Direccionamiento IP

### R1
- Gestión: `10.0.0.11/24`
- LAN: `10.1.1.1/24`
- WAN: `198.51.100.1/30` y `198.51.100.5/30`
- GRE hacia R2: `172.16.12.1/30`
- GRE hacia R3: `172.16.13.1/30`

### R2
- Gestión: `10.0.0.12/24`
- LAN: `10.2.2.1/24`
- WAN: `198.51.100.2/30` y `198.51.100.9/30`
- GRE hacia R1: `172.16.12.2/30`
- GRE hacia R3: `172.16.23.1/30`

### R3
- Gestión: `10.0.0.13/24`
- LAN: `10.3.3.1/24`
- WAN: `198.51.100.6/30` y `198.51.100.10/30`
- GRE hacia R1: `172.16.13.2/30`
- GRE hacia R2: `172.16.23.2/30`

## Automatización con Ansible

El proyecto usa:

- `ansible.cfg` para la configuración general.
- `inventory/hosts.ini` para definir los routers MikroTik.
- `group_vars/mikrotik.yml` para variables globales de GRE.
- `host_vars/` para variables específicas de cada router.

### Playbooks

- `01-base.yml`: aplica la configuración base de MikroTik.
- `02-gre.yml`: crea y configura los túneles GRE.
- `03-ospf.yml`: habilita OSPF v2 y anuncia las redes necesarias.

## Validación

La conectividad quedó verificada correctamente:

- Los túneles GRE levantan en los tres routers.
- OSPF forma vecindades en estado `Full`.
- Las rutas dinámicas se aprenden correctamente.
- Hay comunicación entre las redes LAN de R1, R2 y R3.

## Evidencias

Se incluyen capturas de:

- Topología en GNS3.
- Estado de interfaces.
- Vecinos OSPF.
- Tabla de rutas.
- Pruebas de conectividad.

## Persistencia del entorno

Se verificó que el nodo Docker de Ansible conserva los datos al reiniciarse dentro de GNS3, permitiendo trabajar sobre el directorio persistente `/ansible`.

## Conclusión

El proyecto cumple con la automatización de la configuración base, el establecimiento de túneles GRE y el enrutamiento dinámico con OSPF entre los tres routers MikroTik.
