# Easysocket 🔐
Modulo compilado para python que permite crear comunicaciones sokcet con cifrado asimetrico integrando el modulo pycript

## !ATENCIÓN!
No se deben cambiar los nombres de los ficheros, a pesar de tener unos nombres un tanto particulares podemos importar los modulos simplemente con
### <sup>import easysocket, pycript</sup>
Con la condición de que estos sean accesibles (ubicados en la carpetad e librerias python) o se encuentren en mismo direcctorio que el script/programa al que las vamos a importar.

### ¿Como funciona?
Easysocekt tiene un funcinamiento simple para el usuario, está diseñado para enviar datos encriptados desde un cliente (cifrando con clave pública) a un servidor (descifrando los datos con su clave privada),
esto permite una mayor seguridad en las comunicaciones. No debes preocuparnos por el 'buffer' empleado en el socket ya que este se negocia de forma automatica con cliente/servidor para que no lo tengas que hacer tu.
Los protocolos empleados para seguir una comunicación sincrona entre cliente/servidor son los siguientes:

  HELO --> Iniciar comunicacion con servidor
  
  BUFF --> Indica el tamaño de buffer para el próximo paquete
  
  KEY --> Indica que se va a pasar una clave pública
  
  KEY FOUND --> Respuesta del servidor tras un HELO para indicar al cliente que dispone de la clave publica
  
  KEY NOT FOUND --> Respuesta del servidor tras un HELO para indicar al cliente que no dispone de la clave publica
  
  OK --> La recepción de datos feu exitosa y se puede continuar
  
  ~~ERROR~~--> Error en la recepciond e datos (No implementado)
  
  MSG --> Indica que el proximo paquete son datos (No se indica en la ayuda de la clase)
  

### __MODO SERVER__
Por defecto para el servidor se escucharán todos los hosts en el puerto 50500 con un maximo de 5 host por puerto simultaneos.

### __MODO CLIENTE__
Para usar este modo se deben pasar los parametros 'host' como ip/nombre
del servidor a la escucha y 'data' como el objeto que intentamos enviar
!Actualmente solo se admiten objetos tipo lista/string/integer!
Los parametros opcionales de esta función son "renew_query", por defecto False
y evita que nos pregunte si queremos renovar la clave publica del servidor (se renovará siempre).
El parametro "port", como su nombre indica es el puerto en "int" al cual vamos a conectarnos.

## Para mas información sobre pycript visite 
