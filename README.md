# Dise-o-de-un-Sistema-de-Copias-de-Seguridad-Automatizadas-Multicapa
# Sistema de Copias de Seguridad Automatizadas Multicapa

## 1. Arquitectura General del Sistema

```
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

🔹 Nivel 1: Clientes o Estaciones de Trabajo
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

- Windows: 
Veeam: Soporta copias incrementales, compresión y cifrado. Ideal para backups empresariales.
Cobian: Open-source, permite programación flexible y es liviano.
EaseUS: Interfaz intuitiva, permite clonación de discos y backups rápidos.

- macOS: 
Time Machine: Integrado en macOS, fácil de configurar y permite recuperación completa del sistema.
Carbon Copy Cloner: Crea copias exactas y booteables, útil para migraciones.

- Linux: 
Timeshift: Similar a Time Machine, ideal para restaurar el sistema.
Deja Dup: Interfaz gráfica sencilla, cifrado incluido.

_(Explica por qué has elegido cada uno.)_

### b. Programación de copias
- ¿Cómo se configuran las copias incrementales diarias?  

Abre Veeam y selecciona "File Level Backup".
Elige las carpetas/archivos a respaldar.
En "Schedule", activa la opción "Daily".
Selecciona "Incremental backup" y programa la hora (ej. 20:00 todos los días).
Guarda la configuración.

- ¿Cómo se hacen las copias completas semanales?

1. Windows (Veeam Agent Free)
Abre Veeam y selecciona "Backup Job" → "Entire Computer" (o "File Level" para carpetas).
En "Schedule", elige "Weekly" y marca el día (ej. Domingo).
Asegúrate de seleccionar "Active Full Backup" (no incremental).
Configura la hora (ej. 23:00) y guarda.

2. macOS (Time Machine o Carbon Copy Cloner)
Time Machine: Ya hace copias completas automáticas cuando el disco está conectado (no necesita configuración adicional).
Carbon Copy Cloner:
Crea una nueva tarea → "Clone" (origen y destino).
En "Schedule", elige "Weekly" y el día.
Selecciona "Delete older backups" para evitar saturar el disco.

3. Linux (Timeshift o rsync)
Timeshift:
Abre Timeshift → "Schedule" → Activa "Weekly".
Elige el día y hora (ej. Domingo a las 22:00).
Asegúrate de que el tipo de backup sea "RSync" (para copias completas eficientes).
rsync + cron:

Edita crontab (crontab -e) y añade:
0 22 * * 0 rsync -a --delete /ruta/origen /ruta/backup_completo
(Se ejecutará todos los domingos a las 22:00).

### c. Destino de las copias
- ¿Cómo se organizan las carpetas por PC?

1. En el servidor:
Crear carpeta principal: /backups
Dentro, hacer una carpeta por PC:
/backups/PC1, /backups/PC2, etc.

2. En cada PC:

Windows (Veeam):
Elegir "Backup a carpeta compartida"
Poner ruta: \\IP_servidor\backups\NombrePC
Poner usuario/contraseña del servidor si pide

Mac (Time Machine):
Ir a Time Machine > Seleccionar disco
Elegir "Conectar servidor"
Poner: smb://IP_servidor/backups/NombreMac

Linux (Terminal):
Montar carpeta del servidor:
sudo mount -t cifs //IP_servidor/backups/NombreLinux /mnt/backup -o user=usuario
Usar rsync para copiar:
rsync -av /tus/archivos /mnt/backup

---

## 3. Configuración del Nivel 2: Servidor Local Primario

### a. Tipo de hardware elegido
- Opción: NAS 
- Marca/modelo (si aplica): WD My Cloud Home
- Precio: Entre 240 euros 
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

#!/bin/bash

# Configuración básica
BACKUP_DIR="/backups"
LOG_FILE="/tmp/backup_check.log"

# Verificar si existe el backup más reciente
if [ -z "$(ls -A $BACKUP_DIR)" ]; then
    echo "[ERROR] No hay backups en $BACKUP_DIR" > $LOG_FILE
    exit 1
fi

# Obtener el backup más nuevo
LATEST=$(ls -t $BACKUP_DIR | head -1)

# Verificar si el backup está vacío o es muy pequeño
if [ $(du -m "$BACKUP_DIR/$LATEST" | cut -f1) -lt 1 ]; then
    echo "[ERROR] El backup $LATEST está vacío o es muy pequeño" > $LOG_FILE
    exit 1
fi

# Si todo está bien
echo "[OK] Backup verificado: $LATEST" > $LOG_FILE
exit 0

- Alerta por email: ¿Cómo se configura?

#!/bin/bash

# Configuración
BACKUP_DIR="/backups"
EMAIL_ADMIN="admin@tudominio.com"
SERVER_NAME=$(hostname)

# Verificar backups
if [ -z "$(ls -A $BACKUP_DIR)" ]; then
    MENSAJE="[ALERTA] No hay backups en $BACKUP_DIR (Servidor: $SERVER_NAME)"
    echo "$MENSAJE" | mail -s "⚠️ Falla en Backup" "$EMAIL_ADMIN"
    exit 1
fi

# Verificar tamaño mínimo (ejemplo: 1MB)
LATEST=$(ls -t $BACKUP_DIR | head -1)
if [ $(du -m "$BACKUP_DIR/$LATEST" | cut -f1) -lt 1 ]; then
    MENSAJE="[ALERTA] Backup $LATEST está vacío/corrupto (Servidor: $SERVER_NAME)"
    echo "$MENSAJE" | mail -s "⚠️ Backup corrupto" "$EMAIL_ADMIN"
    exit 1
fi

# Si todo está bien (opcional: notificación de éxito)
echo "[OK] Backup $LATEST verificado" | mail -s "✓ Backup OK" "$EMAIL_ADMIN"
exit 0

- Prueba de restauración: ¿Cada cuánto tiempo? ¿Cómo?

📅 Frecuencia recomendada para pruebas de restauración

Tipo de Backup	           Frecuencia de Prueba
Backups críticos          (BDs, servidores)	Semanal o mensual
Backups no críticos       (archivos estáticos)	Trimestral
Entornos regulados        (HIPAA, GDPR) Mensual (obligatorio)

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

