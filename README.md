# Dise-o-de-un-Sistema-de-Copias-de-Seguridad-Automatizadas-Multicapa
# Sistema de Copias de Seguridad Automatizadas Multicapa

## 1. Arquitectura General del Sistema

```
+-------------------------------------------------------+
|                       Nivel 1                         |
|                                                       |
|   [ Windows ]    [  MAC  ]    [  Linux ]              |
+-------------------------------------------------------+

                      ↓

+-------------------------------------------------------+
|                       Nivel 2                         |
|                                                       |
| Servidor / NAS / PC        [ RAID Interna ]           |
|                           +------------------+        |
|                           |  Almacenamiento   |        |
|                           |   Local (RAID)    |        |
|                           +------------------+        |
+-------------------------------------------------------+

                      ↓

+-------------------------------------------------------+
|                       Nivel 3                         |
|                                                       |
| Servidor / NAS / PC           [ Nube ]                |
|                              +------------------+     |
|                              |  Almacenamiento   |     |
|                              |    en la nube     |     |
|                              +------------------+     |
+-------------------------------------------------------+
```

 Nivel 1: Clientes o Estaciones de Trabajo
Rol:

Este nivel representa los usuarios finales que interactúan con el sistema.

Son quienes crean, editan y acceden a los datos.

Dispositivos típicos:

Computadoras personales (PCs)

Windows

Mac

Linux


🔹 Nivel 2: Servidor Local o Almacenamiento Interno
Rol:

Actúa como un servidor centralizado local para almacenamiento, respaldo o compartición de archivos dentro de una red local.

Maneja RAID interna, lo que ofrece redundancia y protección de datos.

Dispositivos típicos:

NAS (Network Attached Storage)

PC configurado como servidor con:

Linux Server

Windows Server


🔹 Nivel 3: Servidor en la Nube o Almacenamiento Externo
Rol:

Este nivel se encarga del almacenamiento en la nube o del respaldo remoto.

Proporciona acceso a los datos desde fuera de la red local y protección adicional ante desastres.

Dispositivos / Servicios típicos:

Servidor NAS o PC con sincronización hacia:

Servicios en la nube (Google Drive, Dropbox, OneDrive, etc.)

Plataformas de respaldo online

Servidores virtuales en la nube (AWS, Azure, etc.)


---

## 2. Configuración del Nivel 1: PCs Individuales

### a. Selección de software
- Windows: ______________________
- macOS: ________________________
- Linux: _________________________

_(Explica por qué has elegido cada uno.)_

### b. Programación de copias
- ¿Cómo se configuran las copias incrementales diarias?  
- ¿Cómo se hacen las copias completas semanales?

### c. Destino de las copias
- ¿Dónde se almacenan?  
- ¿Cómo se organizan las carpetas por PC?

---

## 3. Configuración del Nivel 2: Servidor Local Primario

### a. Tipo de hardware elegido
- Opción: NAS 
- Marca/modelo (si aplica): WD My Cloud Home
- Sistema operativo: Técnicamente, está basado en Linux


### b. Tipo de RAID
- Elegido: RAID 5
- Justificación: Redundancia de datos, rendimiento mejorado y costo-eficiencia, puede soportar la falla de un disco sin pérdida de datos. La paridad distribuida permite reconstruir los datos perdidos en caso de que un disco falle y ofrece un buen rendimiento en lectura y escritura. Aunque no es tan rápido como RAID 0, que se centra exclusivamente en el rendimiento, RAID 5 ofrece una buena combinación de rendimiento y redundancia. 

### c. Software de gestión
- Software elegido: Urbackup
- Función principal: UrBackup es un software para realizar copias de seguridad rápido, seguro y eficaz.

---

## 4. Configuración del Nivel 3: Servidor Secundario Remoto

### a. Tipo de servidor remoto
- Opción elegida: NAS remoto / Nube / PC remoto  
- Justificación:

### b. Seguridad de la sincronización
- ¿Cómo se programa la sincronización?
- ¿Qué cifrado se usa?
- ¿Se puede activar doble autenticación?

---

## 5. Automatización del Proceso

- Script de verificación: _(pega o enlaza un ejemplo)_
- Alerta por email: ¿Cómo se configura?
- Prueba de restauración: ¿Cada cuánto tiempo? ¿Cómo?

---

## 6. Justificación del uso de RAID

- ¿Por qué no sustituye al backup?
- ¿Qué pasa si solo tenemos RAID?

---

## 7. Resumen de Software Recomendado

## 7. Resumen de Software Recomendado (con UrBackup)

| Función                          | Software Recomendado                      |
|----------------------------------|-------------------------------------------|
| **Gestión centralizada**         | **UrBackup**                       |
| **Sincronización entre servidores** |  Duplicity              |
| **Monitorización**               | Grafana + Prometheus   |


---

## Bibliografía / Fuentes consultadas

- Fuente 1: [______________________](https://www.profesionalreview.com/mejores-nas-del-mercado/)
- Fuente 2: [______________________](https://www.xataka.com/basics/servidores-nas-que-como-funcionan-que-puedes-hacer-uno)
- Fuente 3: [[______________________]](https://www.tecnozero.com/servidor/tipos-de-raid-cual-elegir/)
- Fuente 4: [[______________________]](https://www.urbackup.org/features.html)
- Fuente 5: [[______________________]](https://cloud.google.com/discover/what-is-prometheus?hl=es-419)
- Fuente 6: [[______________________]](https://wiki.archlinux.org/title/Duplicity)

