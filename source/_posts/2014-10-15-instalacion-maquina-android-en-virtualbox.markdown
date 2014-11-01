---
layout: post
title: "Instalación máquina Android en VirtualBox"
date: 2014-10-15 19:51:52 +0200
comments: true
categories: [Android, VirtualBox]
---

Vamos a instalar una ISO Android 4.2 en VirtualBox y configurarla para que actúe como un smartphone. <!-- more -->

#Creacción máquina virtual
- Creamos una **nueva máquina virtual**. 
- **Nombre:** Android_4-2 
- **Sistema Operativo:** Linux **Versión:** 2.6
- **Memoria:** 512MB
- Creamos un nuevo disco virtual (VDI), reservado dinámicamente y con tamaño máximo de 8GB. 
- Le damos a crear. 
- Una vez creada la máquina virtual, le damos a **Configuración**.
- En **Almacenamiento** en el controlador IDE que aparecerá vacío le añadimos nuestra ISO Android.   
- En **Red** seleccionamos Adaptador puente e iniciamos la máquina virtual. 

#Instalación ISO de Android
- Al iniciar la máquina virtual, estamos iniciando la ISO que pusimos en la unidad CD del controlador IDE. 
- Instalamos el Sistema Operativo Android en `Installation - Install Android-x86 to harddisk`.
- Le damos a `Create/Modify partitions`
- `New`, `Primary` y le ponemos el tamaño por defecto. 
- `Bootable`
- `Write`
- Salimos. 
- Instalamos en *ext3*, formateamos e instalamos el `Boot loader GRUB`. 
- Le decimos que sea de escritura y lectura para que podamos añadir archivos a la memoria. 
- Reiniciamos la máquina y sacamos la ISO de la unidad de CD. 

#Configuración máquina virtual
- Una vez creada, la iniciamos en el **Debug Mode**.
- Montamos la partición en L/E con el siguiente comando: 
```
mount -o remount,rw /mnt
```
- Ahora editamos el fichero menu.lst con vi: 
```
vi /mnt/grub/menu.lst 
```
- Copiamos la primera entrada de las dos, se copia con *Y* y pegamos con *p*. Lo hacemos línea a línea. 
- En la línea del `kernel` añadimos la siguiente línea al final. Debemos entrar en el modo edición con la tecla *i*: 
```
DPI=160 UVESA_MODE=320x480
```
- Salimos del modo edición con la tecla *Esc* y escribimos *:wq* para salir guardando los cambios. 
- Añadimos a través del terminal de Linux la configuración al VirtualBox: 
```
VBoxManage setextradata "Android_4-2" "CustomVideoMode1" "320x480x16"
```
- Salimos con *exit* y apagamos la máquina. 
- La iniciamos eligiendo la opción que hemos creado en el GRUB e instalamos Android siguiendo los pasos.

#Configurar ADB
- Para poder conectarnos a la máquina virtual desde el terminal desde cualquier directorio, añadimos la ruta del ADB al path. 
- Para ello, creamos el fichero **.bashrc** en nuestro directorio `/home` si no existe.
- Y le añadimos las siguientes líneas: 
```
export PATH=${PATH}:/home/user/ruta-SDK/platform-tools
export PATH=${PATH}:/home/user/ruta-SDK/tools
``` 

#Conectarnos a la máquina virtual
- Desde la máquina virtual entramos en el modo consola con `Alt + F1` y tecleamos *netcfg* para ver la IP de la máquina. 
- Para conectarnos utilizaremos: 
```
adb connect IP
```
- Y para comprobar, miramos la lista de los dispositivos conectados: 
```
adb devices
```
- Para quitar el modo consola del emulador y volver al modo gráfico pulsamos `Alt + F7`.
