# Instalación Klipper Ender 3 S1

En este caso, vamos a realizar la instalación de Klipper en una Ender 3 S1 utilizando un PC como servidor.

## Pasos:

1. **Instalar Debian:** Primero, procedemos a instalar Debian en el ordenador desde la web oficial. Una vez completada la instalación, actualizamos los paquetes utilizando el siguiente comando:

   ```bash
   sudo apt update && sudo apt upgrade
   ```

2. **(Opcional) Eliminar paquetes innecesarios:** En este paso, eliminaremos los paquetes que no necesitamos para optimizar el rendimiento y reducir el consumo del servidor. Ejecutamos los siguientes comandos:

   ```bash
   sudo apt-get remove -y --purge x11-common
   sudo apt-get autoremove -y --purge
   sudo apt autoremove --purge
   ```

3. **Verificar e instalar SSH:** Comprobamos si SSH está instalado utilizando el siguiente comando:

   ```bash
   ssh -V
   ```

   Si no está instalado, ejecutamos los siguientes comandos para instalarlo:

   ```bash
   sudo apt-get update
   sudo apt-get install openssh-server
   ```

4. **Comprobar el estado de SSH:** Verificamos que el servicio de SSH esté activo ejecutando el siguiente comando:

   ```bash
   sudo systemctl status sshd
   ```

5. **Instalar y configurar UFW (Uncomplicated Firewall):** Instalamos UFW para activar el Firewall en Debian. Utilizamos los siguientes comandos:

   ```bash
   sudo apt install ufw
   sudo ufw enable
   sudo ufw status verbose
   ```

6. **Habilitar la conexión SSH en el Firewall:** Permitimos la conexión SSH en el Firewall de Debian ejecutando el siguiente comando:

   ```bash
   sudo ufw allow ssh
   sudo systemctl enable ssh
   ```

   Esto activará SSH como un daemon, lo cual significa que se iniciará automáticamente en segundo plano al encender el ordenador.

7. **Instalar KIAUH, Mainsail, etc.:** Sigue el tutorial en este enlace para instalar KIAUH, Mainsail, y otros componentes necesarios: [Tutorial en YouTube](https://www.youtube.com/watch?v=Ib1Dd3rIE2I)

8. **Instalar Klipper en la impresora:** Sigue el tutorial en este enlace para instalar Klipper en la Ender 3 S1: [Tutorial en 3DPrintBeginner](https://3dprintbeginner.com/how-to-install-klipper-on-ender-3-s1/)

9. **(Opcional) Controlar el servidor utilizando htop:** Es recomendable utilizar htop para monitorear los servicios en ejecución. Instálalo ejecutando el siguiente comando:

   ```bash
   sudo apt install htop
   ```
   
10. **(Opcional) Instalación Pi-hole:** Si no queremos utilizar la dirección IP asignada al servidor cada vez que queramos acceder a Mainsail para imprimir con Klipper, podemos instalar Pi-hole y configurar un servidor DNS. Sigue estos pasos:

    ```bash
    wget -O basic-install.sh https://install.pi-hole.net
    sudo bash basic-install.sh
    ```

    Una vez instalado, debemos cambiar el puerto utilizado por Pi-hole, ya que es el mismo que utiliza Mainsail para Klipper (puerto 80). Para ello, cambiamos la configuración en:

    ```bash
    sudo nano /etc/lighttpd/lighttpd.conf
    ```

    Y modificamos el parámetro `server.port = 80` para seleccionar un puerto que no esté ocupado por otro servicio. Luego, reiniciamos el servicio utilizando el siguiente comando:

    ```bash
    sudo service lighttpd restart
    ```

¡Ahora estás listo para controlar tu impresora Ender 3 S1 con Klipper desde tu PC!
