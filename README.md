# Metaesploitable2
Metaesploitable2
# Metasploitable 2
**Contenido**

        - Instalación de Kali 
        - Instalación de Metasploitable2
        - Practicas
                - Ataque DDoS
                - Ataque mediante vsftps

## Preparación Kali Linux y Metasploitable2
##### Preparando Kali Linux

El virtualizador que usaremos es VirtualBox. Lo primero que haremos será irnos a la página de Kali Linux y descargar el archivo OVA:

https://kali.download/virtual-images/kali-2021.4/kali-linux-2021.4-virtualbox-amd64.7z

![imagen](https://user-images.githubusercontent.com/80277545/146815893-0627a255-e3ed-46dd-94da-05bb3cbbc0b9.png)

Una vez descargado, debemos descomprimirlo y obtener el archivo .OVA:

![imagen](https://user-images.githubusercontent.com/80277545/146817611-3e4ed7ef-879d-4d8a-90b9-f7094e341e17.png)

Ahora abrimos VirtualBox e importamos el archivo .OVA:

![imagen](https://user-images.githubusercontent.com/80277545/146817830-dc69f517-8c4a-42bb-a169-c9d594e9fcab.png)

Una vez instalado tendremos que añadirle otra tarjeta de red, esto lo haremos yendo a la configuración de la máquina > Red > Adaptador2. Lo habilitaremos y añadiremos el "Adaptador sólo-anfritión": 

![imagen](https://user-images.githubusercontent.com/80277545/146818821-d302eb96-32f3-4bef-bd4b-d3835508bbb4.png)

( En caso de no tener el "Adaptador sólo-anfritión", podemos añadirlo desde "archivo" > "Administrador de red anfritión" > Crear ) 

![imagen](https://user-images.githubusercontent.com/80277545/146823922-7d4c0b59-c2fa-495a-b5b4-ab6d452c7bec.png)


La ventaja de hacerlo con este método es que no tenemos que "instalar" desde cero Kali Linux. Una vez finalizado, al iniciar el sistema directamente nos pedirá un usuario y una contraseña.

        usuario : kali
        contraseña : kali

##### Preparando Metasploitable2

Ahora descargaremos Metasploitable2 desde el siguiente enlace, para esto tendremos que rellenar este formulario (pueden ser datos falsos) y descargar el archivo comprimido: 

https://information.rapid7.com/download-metasploitable-2017.html

![imagen](https://user-images.githubusercontent.com/80277545/146821125-89d27534-9f43-406a-8b3a-314ef2dc1369.png)

Una vez descargado y descomprimido nos quedarán los siguientes archivos: 

![imagen](https://user-images.githubusercontent.com/80277545/146821415-49dc4747-6175-4f95-94b8-71931b535dda.png)


Ahora crearemos una nueva máquina virtual con las siguientes características:

![imagen](https://user-images.githubusercontent.com/80277545/146820065-5e61817b-266c-44bc-ac2e-54463689d62b.png)

Daremos en "Next" y dejaremos la memoria RAM asignada en "1024".

Posteriormente crearemos un "Disco duro virtual" :

![imagen](https://user-images.githubusercontent.com/80277545/146820292-ee85fe7f-1d16-438a-b7fe-257227093c3a.png)

De tipo "VDI" y "Reservado dinámicamente" de "10GB".

Una vez creada, nos vamos a "Configuración", "Almacenamiento" y eliminaremos "Metasploitable 2.vdi":

![imagen](https://user-images.githubusercontent.com/80277545/146822046-6d53e649-0459-4f13-8050-5ac2e6a94bbe.png)

Ahora añadiremos el nuevo disco que está dentro de los archivos que descargamos de Metasploitable2:

![imagen](https://user-images.githubusercontent.com/80277545/146822386-a1066bf4-722c-4c69-bc52-99acf64e9629.png)

A esta máquina también le cambiaremos el adaptador red "NAT" a "Adaptador sólo-anfritión":

![imagen](https://user-images.githubusercontent.com/80277545/146823149-188a2bb7-94d2-4540-987f-c3e012b0bd9c.png)


Ahora iniciamos la máquina y nos tendría que salir la siguiente interfaz: 

![imagen](https://user-images.githubusercontent.com/80277545/146822770-0af677c1-8d1f-4c32-bf87-cebd1f3caf5b.png)

El usuario y contraseña es: 

                Usuario : msfadmin
                Contraseña : msfadmin

Una vez dentro ejectuaremos "ifconfig" para saber la IP del eth1:

![imagen](https://user-images.githubusercontent.com/80277545/146823247-d17b9f87-11bf-4d0e-858f-0ba882793b00.png)


## Comprobando conectividad

Una vez estamos dentro de las dos máquinas, desde la de Kali vamos a realizar un ping para comprobar que tiene conectividad. En mi caso, la IP de Metasploitable2 es la 192.168.56.105:

           ping 192.168.56.105

![imagen](https://user-images.githubusercontent.com/80277545/146823628-db34255d-90fd-4beb-a9b3-e0b035b85b73.png)

Si resuelve igual que en la imagen anterior, significa que todo está instalado correctamente. 

Podemos ingresar a la página del servidor si desde nuestro Kali Linux introducimos la IP del mismo:

![imagen](https://user-images.githubusercontent.com/80277545/146824329-c54b8f79-1911-4c92-9383-7ea58c62a5ee.png)

# PRACTICAS: 
## Realizando un ataque DDoS 

( El fin de esta práctica es educativo )

Desde nuestro Kali, vamos a usar un exploit de Metasploit (recordemos que Metasploit simplemente es como una librería de exploits, una librería de herramientas). 

Abriremos una terminal y ejecutaremos:

        sudo -i 
        

Iniciaremos Metasploit en modo superusuario: 

        sudo msfdb init && msfconsole
        
![imagen](https://user-images.githubusercontent.com/80277545/146827302-48d76b0a-6696-4606-b135-684022cd46e2.png)


Una vez dentro de Metasploit buscaremos la herramienta/exploit synflood , esto lo haremos con el parámetro "search"

        search dos synflood
        
![imagen](https://user-images.githubusercontent.com/80277545/146827368-3bce3c42-0b3b-46d1-893d-85a5c8f08aaf.png)


Seleccionaremos la opción "/auxiliary/dos/tcp/synflood" , esto lo haremos con: 

         use 0 

Una vez seleccionado, miraremos los paramtros de la herramienta con "info":

        info
        
![imagen](https://user-images.githubusercontent.com/80277545/146827466-4088f6be-5251-4c56-9531-42ceb6b87c1c.png)

A continuación pondremos la IP de la maquina a atacar, en este caso será la 192.168.56.105 y ejecutaremos un run:

        set rhosts 192.168.56.105
        run

Al instante se inciará el ataque DDoS:

![imagen](https://user-images.githubusercontent.com/80277545/146829014-d9ccfcff-4ecb-4bde-bb84-2cfe65ba03c8.png)


Cuando se esté realizando el ataque, al recargar la página en el navegador, no nos resolverá la petición y se quedará cargando. Esto significará que el servidor está siendo atacado y no puede responder a todas las solicitudes. 

## Realizando inclusión por FTP

A continuación, se mostrará como abrir una backdoor a travéz del puerto 21 del Server. 

Lo primero que haremos es abrir de nuevo el cliente de Metasploit:

          msfconsole

![imagen](https://user-images.githubusercontent.com/80277545/147389766-52816995-29e9-4c44-9e38-03a9c66c83dc.png)

Buscaremos la herramienta que nos permitirá ejecutar el backdoor:

           search vsftp 
           use 0 
           
![imagen](https://user-images.githubusercontent.com/80277545/147389792-096c37fe-b0e6-4c08-a4ce-21993f3dde75.png)

Podemos escribir _info_ para ver todas las opciones del exploit:

![imagen](https://user-images.githubusercontent.com/80277545/147389911-6a23f96a-eca6-4cbf-8f3f-db108e0e943f.png)

A continuación, estableceremos la IP de Metasplotable2:
![imagen](https://user-images.githubusercontent.com/80277545/147389941-d6aecc16-48d3-45df-afd9-3451c3e74ac7.png)
![imagen](https://user-images.githubusercontent.com/80277545/147389960-85db6b2c-72ed-4434-9639-f454f0dd733c.png)

Ahora, simplemente ejecutaremos:

            RUN
            
![imagen](https://user-images.githubusercontent.com/80277545/147389974-b8ebcaa8-db39-4138-8f5f-50a937a74add.png)

En caso de no salir al primer "RUN", tan solo hay que volverlo a ejecutar:

![imagen](https://user-images.githubusercontent.com/80277545/147389986-cd5e4736-19f9-48ef-b542-913fba25fb33.png)

Ahora, tendremos una shell a modo backdoor. Por ejemplo ejecutare un _whoami_ para saber el usuario y un _pwd_ para saber la ruta en la que estoy ubicado:

![imagen](https://user-images.githubusercontent.com/80277545/147390019-e2931a76-fc81-4986-8009-90199c74236b.png)

Y con esto, concluimos el backdoor y la intrusión. 

# Conclusión

Con esto finalizamos la intalación y la practica de Metasploitable2 y Kali Linux, lo suyo sería, a partir de aquí, explorar que posibilidades tenemos para adentrarnos más en el mundo del pentesting. 





