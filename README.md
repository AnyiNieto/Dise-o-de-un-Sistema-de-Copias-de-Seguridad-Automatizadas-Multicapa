# Dise-o-de-un-Sistema-de-Copias-de-Seguridad-Automatizadas-Multicapa
# Sistema de Copias de Seguridad Automatizadas Multicapa

## 1. Arquitectura General del Sistema

- Nivel 1: ______________________________________
- Nivel 2: ______________________________________
- Nivel 3: ______________________________________

_(Explica brevemente la función de cada nivel. Puedes añadir un esquema o diagrama ASCII si lo deseas.)_

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
- Justificación: Redundancia de datos, rendimiento mejorado y costo-eficiencia

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

