    /*******************************************************/
    /       CREADO POR:                                     /
    /           Maria Bracamonte    10-11147                /
    /           Nelson Saturno      09-10797                /
    /                                                       /
    /                                                       /
    /       Lab. Redes en Computacion                       /
    /       Prof.Kity Alvarez.                              /
    /                                                       /
    /*******************************************************/


ESTACIONAMIENTO MORIAH

    El Centro Comercial Moriah dispone de un estacionamiento de 200 puestos con tres puertas. Cada puerta permite la entrada y salida de vehículos y está dotada de un botón pulsador y un expendedor de tickets. Además dispone de un letrero luminoso donde se puede escribir:
    Estacionamiento con puestos
    Estacionamiento sin puestos

    Se quiere diseñar un sistema informático basado en el paradigma Cliente/Servidor que permita automatizar y controlar dicho estacionamiento.

Incluye:
    Un computador central (sem_svr.c) que va a controlar el sistema completo  junto a los equipos de las puertas (sem_cli.c) que permiten el acceso o salida de vehículos. Este programa se trabajara con Socket UDP y se implementaron metodos de seguridad que garantizan la entrega de informacion y en caso de que haya perdida o duplicados de la data, se volvera a realizar el envio de informacion.


ARCHIVOS DEL PROGRAMA:

-sem_svr.c
Contiene todo lo relacionado al Sistema Central, como comprobacion del carro al entrar, al salir y el monto a pagar. Este siempre debe estar en ejecucion y a la espera de un nuevo auto a entrar.
-sem_cli.c
Contiene todo lo relacionado a los subsitemas del Sistema Central(Las puertas). Esta se iniciara solo cuando un carro vaya a entrar. Conecta con el servidor mediante un puerto y una direccion IP
-header.h
Contiene algunas variables utilizadas en ambos codigos sem_cli y sem_svr y una estructura del lenguaje C para guardar informacion de cada carro.
-makefile.
El compilador de los archivos anteriores y ademas al ejecutar el comando "make clean" se borran los archivos .o.

FUNCIONAMIENTO


1. En la carpeta donde se encuentra el proyecto ejecute el comando 'make clean' en la consola para limpiar el directorio y luego ejecute el comando "make". Se creara el ejecutador del sevirdor y del cliente con los nombres sem_svr y sem_cli respectivamente.
2. Una vez que haga el primer paso, podra ejecurtar el servidor mediante:


 ./sem_svr -l <puerto_sem_svr> -i <bitácora_entrada> -o <bitácora_salida>


    Dónde:
    <puerto_sem_svr>
Es el número de puerto local en que el computador central ofrecerá el servicio
UNICOS PUERTOS DISPONIBLES: 21147 Y 20797

    <bitácora_entrada> Es el nombre de la direccion relativa o absoluta donde se almacena las operaciones de entrada al estacionamiento.
MAX. CARACTERES: 20.

    <bitácora_salida> Es el nombre de la direccion relativa o absoluta donde se almacena las operaciones de salida al estacionamiento.
MAX. CARACTERES: 20



3. Una vez hecho el paso dos, ahora puede ejercutar el cliente en un terminal distinto mediante:


    sem_cli -d <nombre_módulo_atención> -p <puerto_sem_svr> - c <op> -i <identificación_vehiculo>


    Donde:
    <nombre_módulo_atención>
Es el nombre de dominio o la dirección IP(version 4) del equipo en donde se deberá ejecutar el módulo de atención centralizada.
MAX. CARACTERES: 40

    <puerto_sem_svr>
Es el número de puerto remoto en que el módulo de servicio atenderá la comunicación solicitada.
UNICOS PUERTOS DISPONIBLES: 21147 Y 20797

    <op>
Indica si el vehículo va a entrar o salir del estacionamiento, puede tener dos valores e ó s
MAX. CARACTERES: 1

    <identificación_vehículo>
La placa del vehiculo a ingresar
MAX. CARACTERES: 100.


RECORDAR: No importa el orden en que entre cada comando solo importa que cada parametro debe ir con su prefijo, es decir, estas son equivalentes

./sem_svr -i texto.txt -o texto2.txt -l 21147
=
./sem_svr -i texto.txt -l 21147 -o texto2.txt
=
./sem_svr -l 21147 -i texto.txt -o texto2.txt

TANTO PARA EL SERVIDOR COMO PARA CADA CLIENTE.

4.El registro de las entradas y salidas estaran en la misma carpeta donde tendra guardado el programa.

El archivo de entrada tendra:
    La placa de carro a ingresar.
    El identificador del carro que sera un numero entero
    La hora y fecha en que ingreso el carro.

El archivo de salida tendra:
    La placa de carro a salir.
    El identificador del carro que sera un numero entero
    La hora y fecha en que ingreso el carro.
    La hora y fecha en que esta saliendo el carro.
    El monto a pagar.

    El monto se calcula de la siguiente forma:
        La primera hora de estacionamiento cuesta 80 Bs y la fracción (1 hora) cuesta 30 Bs