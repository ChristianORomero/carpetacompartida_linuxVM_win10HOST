
---

Pequeña guía rápida que nos permitirá crear y compartir carpetas y archivos entre máquinas virtuales que hayamos creado para sistemas Linux y nuestro equipo Host, en este caso un equipo con Windows 11, esto nos permitirá las siguientes ventajas como Técnicos IT:

    - Transferencia inmediata de archivos sin necesidad de herramientas externas
    - Eliminación de pasos intermedios como usar USB, cloud o correo
    - Prueba de software en distintos sistemas operativos sin duplicar archivos
    - Desarrollo y prueba de scripts que funcionan en ambos entornos
    - Mantenimiento de copias de seguridad en ambos sistemas
    - Recuperación rápida en caso de fallo en uno de los sistemas
    - Testear de problemas de clientes en diferentes entornos
    - Preparar soluciones multiplataforma

---

### Instalar VirtualBox Guest Additions en Kali Linux

Abre consola en Kali y ejecuta:

```
sudo apt update
sudo apt install -y virtualbox-guest-x11
```

Reinicia Kali (VM) tras la instalación
```cmd
sudo reboot
```

### Configurar carpeta compartida en VirtualBox

1. Apaga la VM Kali para configurar la carpeta compartida
    
2. En VirtualBox, ve a:
    
    - **Configuración > Carpetas compartidas**
    - Haz clic en el icono de carpeta con el `+`
    - **Ruta de la carpeta**: selecciona la carpeta en el host que quieres usar para compartir archivos o crea una nueva (ej; `C:\Users\Cristian\KaliShare`)
    - **Nombre de la carpeta**: por ejemplo `KaliShare`
        ![[Notas/imgs/2.png]]
        
    - Marca **Montaje automático - Auto-mount**
    - ![[Notas/imgs/3.png]]
    
    - Marca **Hacer permanente**
        
3. Inicia la máquina virtual Kali de nuevo


- Cambiamos la distribución de teclado rápidamente para esta sesión a español y comprobamos que se ha montado correctamente la carpeta compartida:

![[Notas/imgs/4.png]]

- Puede ocurrir que por permisos no te permite acceder a la carpeta compartida, ejecuta este comando que añade nuestro usuario al grupo "vboxsf", lo que nos da permisos de acceso y modificación de archivos en estas carpetas compartidas (requiere cerrar sesión o reinicio posterior):

```cmd
sudo usermod -aG vboxsf $USER
```

*Luego reinicia Kali para aplicar los permisos*

```bash
sudo reboot
```


- Si por ejemplo quiero pasar esta carpeta con scripts de bash de diagnóstico a PC Host (Win10) desde dónde los he creado (Kali Linux) usaremos la carpeta compartida que hemos creado previamente:

![[Notas/imgs/5.png]]

- Al crear los scripts y la carpeta directamente en la carpeta compartida que hemos montado, automáticamente desde el equipo host tengo acceso directo

![[Notas/imgs/6.png]]

- Si por lo que sea he trabajado en otro directorio diferente a la carpeta compartida podemos pasar los archivos de forma fácil de la siguiente manera:

```cmd
cp -r ~/ruta/scripts /media/sf_KaliShare/
```

- Si por lo que sea no puedes ver la carpeta compartida o no aparece recomiendo ejecutar este comando para mostrar la lista de mounts:

```cmd
ls /media/ | grep sf
```

![[Notas/imgs/7.png]]

Si siguiese sin aparecer, comprueba lo siguiente:

- Que las **Guest Additions** de VB estén instaladas correctamente
![[Notas/imgs/8.png]]

- Que marcaste **"Montaje automático"** o "Automount"
- Que la carpeta está marcada como **permanente**
- Reinicia si fue tu primer mount

---
