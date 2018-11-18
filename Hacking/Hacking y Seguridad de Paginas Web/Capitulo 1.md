# INTRODUCCIÓN AL PENTEST WEB

Pentest —> test de penetración (en este caso sobre una aplicación web), el cual utiliza un conjunto de pruebas cuya finalidad es la de evaluar la efectividad de los protocolos de seguridad de los servicios informáticos y telepáticos de una organización.


## CLASIFICACIÓN PENTEST

- **Caja negra** —> no se dispone información interna de la organización
- **Caja blanca** —> el pentester dispone de total información sobre el sistema que se va a auditar
- **Caja gris** —>  combinación de caja negra + caja blanca


## METODOLOGÍAS MÁS UTILIZADAS

- **NIST** (National Institute of Standard and Technology)
- **OWASP** (Open Web Application Security Project)
- **OSSTMM** (Open Source Security Testing Methodology Manual)


## ETAPAS

1. **Reconocimiento:** se obtendrá toda la información que esté disponible en medios de acceso público.
		  + *Reconocimiento activo:* el atacante interactuar directamente con la víctima. Ejemplo, mediante ingeniería social
		  + *Reconocimiento pasivo:* ejemplo, hacking con buscadores, herramientas de gestión de red, búsqueda de metadatos o indagación en redes sociales.
2. **Enumeración:** se escanea la red objetivo para obtener una imagen de su arquitectura. Como objetivos determinar rangos de IP, nombres de maquinas, sistemas operativos y versiones, detección de cortafuegos, IDS/IPS, así como servicios activos.
		  + *Herramientas:* map, hping3, traceroute
3. **Análisis:** se busca vulnerabilidad en los dispositivos encontrados en las fases previas.
		  + *Herramientas:* nessus, w3af, acunetix, appscan, nmap
4. **Explotación:** emplear explotación contra servicios y aplicaciones vulnerables. También se realizan pruebas de inyección de código manuales apoyándose en los resultados de los escáneres automatizados, para así eliminar falsos positivos.
  + *Herramientas:* Metasploit, Canvas
5. **Documentación:** documentar la información obtenida.


## PROTOCOLO HTTP

El protocolo HTTP corresponde a “Hyper Text Transfer Protocol”, y es un protocolo de la capa aplicación del modelo OSI.
Este protocolo permite realizar peticiones y respuestas en una arquitectura cliente-servidor.

- Campos de la cabecera de la petición
	Accept —> Indica el tipo de contenido aceptado por el navegador del cliente
	Accept-Charset —> Conjunto de caracteres permitidos
	Accept-Languague —> Idiom esperado por el navegador
	Authorization —> Identificación del cliente ante el servidor
	Content-Encoding —> Codificación del cuerpo de la petición
	Content-Languague —> Idioma del cuerpo de la petición
	Content-Type —> Tipo del cuerpo de la petición
	Date —> Fecha de inicio de la transferencia de datos
	Forwarded —> Campo empleado por equipos intermediarios
	From —> Indica el correo electrónico del cliente
	Referer —> Dirección de origen de la petición del recurso
	User-Agent —> Información del cliente como nombre de la aplicación, sistema operativo, versión, idioma

- Campos de la cabecera de la respuesta
	Content-Encoding —> Codificación del cuerpo de la respuesta
	Content-Language —> Idioma del cuerpo de la respuesta
	Content-Length —> Longitud del cuerpo de la respuesta
	Content-Type —> Tipo del cuerpo de la respuesta
	Date —> Fecha de inicio de la transferencia de la respuesta
	Expires —> Fecha final para utilizar los datos
	Forwarded —> Campo empleado por equipos que se encuentran entre el cliente y el servidor
	Location —> Redirección a una nueva URL
	Server —> Información del servidor

- Códigos de respuesta
	1XX —> Mensaje informativo
	2XX —> La petición ha sido recibida y procesada correctamente
	3XX —> Indica que hay que realizar una redirección
	4XX —> Se ha producido un error en el cliente
	5XX —> Se ha producido un error en el servidor
	
## FINGERPRINTING WEB SERVERS

*Fingerprinting* --> hace referencia a la huella distintiva que permite identificar un sistema (se suele estar haciendo referencia a la identificación de la arquitectura, sistema operativo y servicios a partir de cómo se haya implementado el protocolo TCP/IP).

## TIPO Y VERSIÓN DEL SERVIDOR WEB

- **Etiquetas Server y Vía de la cabecera HTTP:** Consiste en inspecccionar la cabecera HTTP devuelta por el servidor web en busca de la etiqueta <<Server>>.
	
> **Ejemplos**
>  + Server: nginx/0.7.67
>  + Server: Microsoft-IIS/5.0
>  + Server: Oracle-Application-Server-10g OracleAS-Web-Cache-10g/9.0.4.1.0

> **Herramientas**
>  + *netcat* --> nc 192.168.154.138 80 // nc *IP* *puerto*
>  + *telnet* --> telnet 192.168.1.154.138 80 // telnet *IP* *puerto*

Muchos administradores deciden modificar el contenido de la etiqueta <<Server>> para evitar revelar información sobre el software usado.
	
El campo <<Vía>> de la cabecera es utilizado por *proxies* y *gateways* para indicar los protocolos entre el <<User Agent>> y el <<Server>> en las peticiones y entre el servidor de origen y el cliente en las respuestas.
	
- **Identificación a través de páginas de error:** la idea consiste en enviar peitciones mal formadas para que el servidor responda con una página de error. Si el desarrollador/administrador no se ha preocupado de establecer páginas de error personalizadas, entonces se mostrarán los mensajes de error por defecto.

- **Análisis del comportamiento de la respuesta HTTP:**
>  + *Distintos campos en la cabecera.* Cuando se realiza una petición <<HEAD>>, la cabecera de la respuesta puede contener de forma opcional algunos campos. El comportamiento de Apache es el de mostrar <<tags>> como <<Expires>> o <<Vary>>, mientras que Microsoft IIS suele obviarlos.
>  + *Orden de los campos de la cabecera.* En la cabecera de la respuesta de un servidor IIS primero aparece el campo <<Server>> y después el campo <<Date>>. Mientras que en la respuesta de un servidor Apache es al contrario.
>  + *Lista de los métodos permitidos.* Cuando se realiza una petición al servidor con el método <<OPTIONS>>, la respuesta contendrá en el campo <<Allow>> la lista de métodos soportados por dicho servidor. Ese es el comportamiento de Apache, pero en el caso de Microsoft IIS también devuelve el campo <<Public>> con esa información.
>  + *Respuesta ante petición DELETE.* En muchos servidores una petición <<DELETE>> estará permitida, retornando un código de error. La diferencia está en los distintos códigos de error devueltos por Apache y Microsoft IIS.
