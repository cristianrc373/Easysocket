# Easysocket 🔐
Modulo compilado para python que permite crear comunicaciones sokcet con cifrado asimétrico integrando el módulo pycript

## !ATENCIÓN!
No se deben cambiar los nombres de los ficheros, a pesar de tener unos nombres un tanto particulares podemos importar los módulos simplemente con

<sup>import easysocket, pycript</sup>

*Por defecto easysocket importa pycript*

Con la condición de que estos sean accesibles (ubicados en la carpeta de librerias python) o que se encuentren en mismo direcctorio que el script/programa al que las vamos a importar.

### ¿Como funciona?
Easysocekt tiene un funcionamiento simple para el usuario, está diseñado para enviar datos encriptados desde un cliente (cifrando con clave pública) a un servidor (descifrando los datos con su clave privada),
esto permite una mayor seguridad en las comunicaciones. No debes preocuparte por el 'buffer' empleado en el socket ya que este se negocia de forma automática con cliente/servidor para que no lo tengas que hacer tu.
Los protocolos empleados para seguir una comunicación sincrona entre cliente/servidor son los siguientes:

  HELO --> Iniciar comunicacion con servidor
  
  BUFF --> Indica el tamaño de buffer para el próximo paquete
  
  KEY --> Indica que se va a pasar una clave pública
  
  KEY FOUND --> Respuesta del servidor tras un HELO para indicar al cliente que dispone de la clave publica
  
  KEY NOT FOUND --> Respuesta del servidor tras un HELO para indicar al cliente que no dispone de la clave publica
  
  OK --> La recepción de datos fue exitosa y se puede continuar
  
  ~~ERROR~~--> Error en la recepcion de datos (No implementado)
  
  MSG --> Indica que el próximo paquete es de datos (No se indica en la ayuda de la clase)
  

### __MODO SERVER__
Por defecto para el servidor se escucharán todos los hosts en el puerto 50500 con un máximo de 5 host por puerto simultáneos.

### __MODO CLIENTE__
Para usar este modo se deben pasar los parametros 'host' como ip/nombre
del servidor a la escucha y 'data' como el objeto que intentamos enviar
!Actualmente solo se admiten objetos tipo lista/string/integer!
Los parametros opcionales de esta función son "renew_query", por defecto False
y evita que nos pregunte si queremos renovar la clave publica del servidor (se renovará siempre).
El parametro "port", como su nombre indica es el puerto en "int" al cual vamos a conectarnos.

## Para mas información sobre *pycript* visite 

### Ejemplos de código
·Iniciar servidor-->
```python
from easysocket import *

sock = Easysocket()
sock.init_server()
```
·Iniciar cliente y mandar datos-->
```python
from easysocket import *

sock = Easysocket()
sock.client("127.0.0.1","hola mundo")
```
·Crear objeto con valores personalizados-->
```python
from easysocket import *
#Configurarión que solo afecta al servidor
sock = Easysocket(host="127.0.0.1", port=8888, listen_bind=10) #Solo se permite el acceso a localhost por el puerto 8888 con 10 conexiones simultáneas
```
·Configurar cliente par envío de datos a servidor personalizado-->
```python
from easysocket import *
#Configurarión que solo afecta al cliente
sock = Easysocket()
sock.client(host="127.0.0.1", port=8888, renew_query=True, [123, "Hola mundo"]) #Sen envian los datos a un servidor localhost puerto 8888 y si ya tenemos la clave pública nos pregunta si queremos renovarla
```
