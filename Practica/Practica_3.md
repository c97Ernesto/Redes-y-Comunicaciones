# Práctica 3 - Capa de Aplicación
## DNS (Domain Name Server)

### Introducción
1. **Investigue y describa cómo funciona el DNS. ¿Cuál es su objetivo?**
   
    El objetivo del Sistema de Nombres de Dominio consiste en traducir los nombres de dominio en direcciones IP (proceso conocido como "foward lookup"). Es un proceso organizado jerárquicamente.
    El número de estaciones que recorre una solicitud y el orden en que esto sucede depende de diversos factores, como por ejemplo del SO o de si utilizan UPD(User Datagram Protocol) o NetBIOS sobre TCP/IP como protocolos. Sin embargo **_la resolución de nombres a través de los diferentes servidores en el DNS siempre se realiza de la misma manera_**:
    1. Tras iniciar una consulta de una página web (ej, www.unlp.edu.ar) en el cliente, se encomienda la resolución de nombres primero localmente en el navegador (funciona como interfaz entre una aplicación y un servidor DNS). Este comprueba si hay una entrada para el nombre de dominio en el **_archivo host_** y por medio de este archivo de texto ya se puede realizar la resolición de nombres directamente en el ordenador, al menos siempre y cuando se haya asignado previamente una dirección IP a un nombre de host de manera manual. Debido a que el archivo de hosts es un vestigio de tiempos anteriores al sistema de nombres de dominio, que lo ha reemplazado, la mayoría de usuarios no se encarga de su mantenimiento, de ahí que tampoco suponga una gran ayuda para la resolución de nombres.
    2. Si no hay ninguna entrada en el archivo hosts para la página web solicitada, la aplicación o el sistema operativo pasa a buscar el nombre de dominio en el caché (memoria temporal) del cliente. Si ya se visitó la página web solicitada o cualquier otra del mismo sitio web y los datos ya están disponibles en el caché, la dirección IP se obtiene aquí.
    3. Si el resolver local no ha podido llevar a cabo la resolución de nombres en el caché, se recurre entonces al servidor de nombres de la red, que es normalmente el router que posibilita la conexión a Internet. El servidor de nombres del router, tras haber realizado una consulta (si corresponde) en su propio caché y no haber encontrado lo que buscaba, solicita al servidor de nombres de tu proveedor de Internet (provider) la dirección IP de la página web.
    4. El servidor DNS de tu proveedor intenta averiguar cuál es la dirección IP del nombre de dominio mediante una comparación con su base de datos. Para recabar información al respecto, los servidores de dominio también utilizan resolvers.
    5. Si aun así no se logra ningún resultado, el servidor DNS del proveedor se pone en contacto con un servidor raíz de nombres de dominio (root name server) y le reclama información adicional sobre el dominio de nivel superior (TLD) de la página web solicitada (la última parte de un nombre de dominio es la que representa al TLD; por ejemplo, .com o .es). En el archivo de la zona raíz del DNS root server aparece información sobre el servidor de nombres de dominio de nivel superior (servidor de nombres TLD) encargado de proporcionar más información para un TLD determinado. La información que sea acorde con la petición realizada se transmite al servidor de nombres del proveedor de Internet. En el caso del nombre de dominio “www.ionos.es”, el root server remitiría al servidor de nombres de dominio de nivel superior de Red.es, que es la entidad responsable del registro de los nombres de dominio .es.
    6. Tras ello, el servidor de nombres del proveedor de Internet emite una petición al servidor de nombres de dominio de nivel superior, pero en este caso tampoco obtiene una respuesta definitiva, sino que se reenvía: los servidores de nombres de dominio de nivel superior actúan meramente de transmisores. Estos informan a los servidores de nombres solicitantes acerca de los servidores DNS autoritativos en los que se deposita el nombre de dominio buscado.
    7. En este paso, el servidor de nombres del proveedor se dirige al servidor de nombres autoritativo responsable del nombre de dominio y obtiene finalmente la dirección IP deseada.
    8. En último lugar, el servidor de nombres del proveedor transmite la dirección IP al servidor DNS de tu router, el cual la entrega a tu resolver local, desde donde se transfiere a tu browser, de tal forma que puede solicitar, cargar y mostrar la página web.
   


2. **¿Qué es un root server? ¿Qué es un generic top-level domain (gtld)?**
   
    Un root name server (**_servidor raíz de nombres de dominio_**) también conocido como **_root server_** es un servidor que desempeña una función esencial en lo relativo a la traducción de los nombres de dominio en direcciones IP: este **_da respuesta a las solicitudes de los clientes (requests) en la zona raíz del sistema de nombres de dominio_** (la zona raíz señala el nivel más alto en el espacio de nombes de dominio DNS). Este tipo de servidores raíz no se encargarán por si mismos de la resolución de nombres de dominio, sino que proporcionan la información a los clientes sobre los servidores DNS de los que pueden recibir datos sobre la dirección IP solicitada. </br>
    Hay un número limitado de root servers en todo el mundo y son administrados por diferentes organizaciones. Estos no almacenan toda la información de Internet, sino que apuntan a otros servidores (servidores TLD) que contienen información más específica.</br>



    Un gTLD o Dominio de Nivel Superior Genérico

3. **¿Qué es una respuesta del tipo autoritativa?**



4. **¿Qué diferencia una consulta DNS recursiva de una iterativa?**
5. **¿Qué es el resolver?**
6. **Describa para qué se utilizan los siguientes tipos de registros de DNS:**
   1. A
   2. MX
   3. PTR
   4. AAAA
   5. SRV
   6. NS
   7. CNAME
   8. SOA
   9. TXT