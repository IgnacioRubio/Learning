# INTRODUCCIÓN AL PENTEST WEB

**Pentest,** test de penetración (en este caso sobre una aplicación web), el cual utiliza un conjunto de pruebas cuya finalidad es la de evaluar la efectividad de los protocolos de seguridad de los servicios informáticos y telepáticos de una organización.


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
> + *Reconocimiento activo:* el atacante interactuar directamente con la víctima. Ejemplo, mediante ingeniería social
> + *Reconocimiento pasivo:* ejemplo, hacking con buscadores, herramientas de gestión de red, búsqueda de metadatos o indagación en redes sociales.
2. **Enumeración:** se escanea la red objetivo para obtener una imagen de su arquitectura. Como objetivos determinar rangos de IP, nombres de maquinas, sistemas operativos y versiones, detección de cortafuegos, IDS/IPS, así como servicios activos.
> + *Herramientas:* map, hping3, traceroute
3. **Análisis:** se busca vulnerabilidad en los dispositivos encontrados en las fases previas.
> + *Herramientas:* nessus, w3af, acunetix, appscan, nmap
4. **Explotación:** emplear explotación contra servicios y aplicaciones vulnerables. También se realizan pruebas de inyección de código manuales apoyándose en los resultados de los escáneres automatizados, para así eliminar falsos positivos.
> + *Herramientas:* Metasploit, Canvas
5. **Documentación:** documentar la información obtenida.


## PROTOCOLO HTTP

El protocolo HTTP corresponde a “Hyper Text Transfer Protocol”, y es un protocolo de la capa aplicación del modelo OSI.
Este protocolo permite realizar peticiones y respuestas en una arquitectura cliente-servidor.

- **Campos de la cabecera de la petición**

Campo | Descripción
----- | -----------
Accept | Indica el tipo de contenido aceptado por el navegador del cliente
Accept-Charset | Conjunto de caracteres permitidos
Accept-Languague | Idiom esperado por el navegador
Authorization | Identificación del cliente ante el servidor
Content-Encoding | Codificación del cuerpo de la petición
Content-Languague | Idioma del cuerpo de la petición
Content-Type | Tipo del cuerpo de la petición
Date | Fecha de inicio de la transferencia de datos
Forwarded | Campo empleado por equipos intermediarios
From | Indica el correo electrónico del cliente
Referer | Dirección de origen de la petición del recurso
User-Agent | Información del cliente como nombre de la aplicación, sistema operativo, versión, idioma

- **Campos de la cabecera de la respuesta**

Campo | Descripción
------|------------
Content-Encoding | Codificación del cuerpo de la respuesta
Content-Language | Idioma del cuerpo de la respuesta
Content-Length | Longitud del cuerpo de la respuesta
Content-Type | Tipo del cuerpo de la respuesta
Date | Fecha de inicio de la transferencia de la respuesta
Expires | Fecha final para utilizar los datos
Forwarded | Campo empleado por equipos que se encuentran entre el cliente y el servidor
Location | Redirección a una nueva URL
Server | Información del servidor

- **Códigos de respuesta**

Código | Descripción
-------|------------
1XX | Mensaje informativo
2XX | La petición ha sido recibida y procesada correctamente
3XX | Indica que hay que realizar una redirección
4XX | Se ha producido un error en el cliente
5XX | Se ha producido un error en el servidor

## FINGERPRINTING WEB SERVERS

**Fingerprinting,** hace referencia a la huella distintiva que permite identificar un sistema (se suele estar haciendo referencia a la identificación de la arquitectura, sistema operativo y servicios a partir de cómo se haya implementado el protocolo TCP/IP).


## TIPO Y VERSIÓN DEL SERVIDOR WEB

- **Etiquetas Server y Vía de la cabecera HTTP:** Consiste en inspecccionar la cabecera HTTP devuelta por el servidor web en busca de la etiqueta "Server".
	
> **Ejemplos**
>  + Server: nginx/0.7.67
>  + Server: Microsoft-IIS/5.0
>  + Server: Oracle-Application-Server-10g OracleAS-Web-Cache-10g/9.0.4.1.0

> **Herramientas**
>  + *netcat* --> nc 192.168.154.138 80 // nc *IP* *puerto*
>  + *telnet* --> telnet 192.168.1.154.138 80 // telnet *IP* *puerto*

Muchos administradores deciden modificar el contenido de la etiqueta "Server" para evitar revelar información sobre el software usado.
	
El campo "Vía" de la cabecera es utilizado por *proxies* y *gateways* para indicar los protocolos entre el "User Agent" y el "Server" en las peticiones y entre el servidor de origen y el cliente en las respuestas.
	
- **Identificación a través de páginas de error:** la idea consiste en enviar peitciones mal formadas para que el servidor responda con una página de error. Si el desarrollador/administrador no se ha preocupado de establecer páginas de error personalizadas, entonces se mostrarán los mensajes de error por defecto.

- **Análisis del comportamiento de la respuesta HTTP:**
>  + *Distintos campos en la cabecera.* Cuando se realiza una petición "HEAD", la cabecera de la respuesta puede contener de forma opcional algunos campos. El comportamiento de Apache es el de mostrar "tags" como "Expires" o "Vary", mientras que Microsoft IIS suele obviarlos.
>  + *Orden de los campos de la cabecera.* En la cabecera de la respuesta de un servidor IIS primero aparece el campo "Server" y después el campo "Date". Mientras que en la respuesta de un servidor Apache es al contrario.
>  + *Lista de los métodos permitidos.* Cuando se realiza una petición al servidor con el método "OPTIONS", la respuesta contendrá en el campo "Allow" la lista de métodos soportados por dicho servidor. Ese es el comportamiento de Apache, pero en el caso de Microsoft IIS también devuelve el campo "Public" con esa información.
>  + *Respuesta ante petición DELETE.* En muchos servidores una petición "DELETE" estará permitida, retornando un código de error. La diferencia está en los distintos códigos de error devueltos por Apache y Microsoft IIS.


## TECNOLOGÍAS EMPLEADAS EN EL SERVIDOR WEB

- **Cabecera X-Powered-By.** Inspeccionando la cabecera de la respuesta de dicho servidor en busca del campo <<X-Powered-By>> (también el campo "X-AspNet-Version" cuando esté presente).

- **Extensiones de los scripts.** A través de la extensión del script indicado en la URL se determina el tipo de lenguaje empleado.

Extensión | Descripción
----------|------------
.jsp | *Java Server Page* permite el desarrollo de aplicaciones web en Java multiplataforma
.php | Lenguaje de scripting para desarrollo dinámico de aplicaciones web en el lado del servidor. En muchas ocasiones se utiliza en servidores web **Apache**
.asp/.aspx | *Actuve Server Page* es un lenguaje de scripting server side que permite generar dinámicamente páginas web. Mientras que asp está basado en VBscript, asp.net (aspx) está orientado a objetos y puede estar escrito en lenguajes soportados por .NeT Framework, como VB.net, C#, JScript.net. Estas extensiones son empleadas por **Microsoft IIS.**
.cfm | *Macromedia ColdFusion Server* lenguaje de scripting para desarrollo de aplicaciones web dinámicas y acceso a bases de datos en el lado servidor
.do | *Java Struts* en Struts, los Servlets ayudan a mpaear las peticiones hechas por un navegador hacia el ServerPage adecuado. El identificador que viene antes del .do es el que le indicará la acción que debe ejecutar al servidor de aplicaciones (por ejemplo, **Tomcat**)
.wsdl | *Web Services Description Language* es una interfaz en formato XML que describe los servicios web ofrecidos (describe sus tipos de datos, formato de los mensajes, tipos de puertos, protocolos válidos) y la forma de acceder a ellos

- **Contenido de las cookies.** En algunas tecnologías se suelen usar identificadores característicos como campos de sus cookies.

> **Ejemplos**  
> ASPSESSIONIDFBEDIWXIOB=CEDUILKHGBEURJFCBUOMNEWS => Suele corresponder a **Microsoft IIS**  
> PHPSESSID=acfirg7v0e4ndwrtl4mnwuifci => Suele corresponder a **Apache**  
> CFID=658356, CFTOKEN=89346587 => Suele corresponder a **ColdFusion**


## HERRAMIENTAS AUTOMATIZADAS

- **Httprint.** Se trata de una herramienta de *fingerprinting* para servidores web que permite llevar a cabo el proceso de identificación incluso cuando hay presentes "web application firewalls", como ModSecurity, o esté ofuscado o cambiado el contenido del banner del servidor web. También es capaz de detectar dispositivos con servicios web habilitados, como puntos de acceso wifi, routers, switches o impresoras. Para ello, el programa buscará coincidencias entre la firma del servidor objetivo y una base de datos de firmas editable y ampliable que tiene la herramienta (signature.txt).

```shell
httprint {-h <host> | -i <input file> | -x <nmap xml file>} -s <signatures> [... options]

-h <host>		host can be either an IP address, a symbolic name, an IP range or a URL
-i <input text file>	file containing list of hosts as described above in text format
-x <nmap xml file>	nmap -oX option generated cml file as input file. Ports which can be consider as http ports are taken 
			from the nmapportlist.txt file
-s <signatures>		file containing http fignerprint signatures

Options:

-o <output file>	output in html format
-oc <output file>	output in csv format
-ox <output file>	output in xml format
-noautossl		disable automatic detection of SSL
-tp <ping timeout>	ping timeout in miliseconds. Default is 400 ms. Maxium 30000 ms
-ct <1-100>		default is 75. Do not change
-ua <User Agent>	deafault is Mozilla/4.0 (compatible; MSIE 5.01; Windows NT 5.0)
-t <timeout>		connection/read timeout in miliseconds

```

> **Ejemplo**  
> ```shell
> ./httprint -h 192.168.56.101 -s signatures.txt
>```

- **Nmap.** Se trata de una herramienta que permite escanear redes para la realización de auditorías de seguridad. Una característica muy potente de este programa es el llamado *Nmap Script Engine (NSE),* un motor que permite que la herramienta incorpore scripts.  
Windows, los scripts se encontrarán en el directorio *C:\Program Files\Nmap\scripts*, y en Linux en */usr/share/nmap/scripts* o */usr/local/share/nmap/scripts*. Nuevos scripts deberán ser colocarse en esa carpeta.

Script | Descripción
-------|------------
http-enum | Enumera directorios usados por aplicaciones y servidores web populares
http-headers | Realiza una petición HEAD de la carpeta raíz del servidor web y devuelve la cabecera HTTP de la respuesta
http-methods | Devuelve las opciones soportadas por un servidor web, enviando para ello una petición HTTP OPTIONS
http-favicon | Obtiene el favicon de la web objetivo y lo compara con una base de datos de iconos empleados por aplicaciones web populares. Si hay una coincidencia, se muestra el nombre de la aplicación web que lo usa. En caso contrartio, se muestra el has MD5 del icono
http-php-version | Intenta devolver la versión de PHP de un servidor web
http-robots.txt | Busca páginas que no deben ser rastreadas por crawlers en el fichero robots.txt de la ríaz del servidor
http-sitemap-generator | Muestra la estructura de directorios, indicando los tipos de ficheros que contienen
http-waf-detect | Envía payloads maliciosos al servidor web para comprobar si está protegido por algún IDS, IPS o WAF
http-waf-fingerprint | Intenta detectar la presencia de waf, así como su tipo y versión

> **Example**  
> ```shell
> nmap -sV --script=http-enum,http-methods 192.168.56.101
> ```


- **WhatWeb.** Es una herramienta cuyo objetivo es la de realizar un proceso de fingerprinting de servidores web, gestores de contenidos (CMS), frameworks para blogs, librerías JavaScript, dispositivos con acceso webm etc. Entre la información obtenida se encuentra el modelo y versión del servidor, tecnologías empleadas, direcciones de correo, páginas de error...  

Para realizar  ese proceso *WhatWeb* dispone de una gran cantidad de plugins.  

El programa se puede configurar con diversos niveles de agresividad:

Nivel | Descripción
------|------------
1 (Pasive) | Hace una petición HTTP por objetivo, excepto cuando se produce una redirección
2 (Polite) | Reservada para usos futuros
3 (Agressive) | Cuando se produce una coincidencia del objetivo con un plugin de forma pasiva, entonces este nivel lanzará funciones más específicas de plugins realizando un descubrimiento más agresivo
4 (Heavy) | Realiza un descubrimiento que genera mucho más ruido mediante funciones para todos los plugins

Algunas características:
  + *Torificar* la herramienta (permite que las pruebas sean lanzadas estableciendo un proxy Tor)
  + Editar la cabera HTTP de las peticiones
  + Seguir las redirecciones hasta cierto nivel
  + El spider de WhatWeb puede rastrear recursivamente los enlaces de la web ojetivo
  + Indicar el número máximo de hilos que realizarán las tareas de descubrimiento
  + Devolver la salida en diferentes formatos (XML, log, JSON, RubyObject, MongoDB, etc)
  
> **Tor**  
> El término *Torificar* hace referencia al uso de la red Tor, cuyas siglas corresponde a The Onion Router.  
> *Tor* es un proyecto cuyo objetivo principal es el desarrollo de una red de comunicaciones de uso público, en la que la comunicación de los usuarios se encamina por múltiples nodos, que permiten ofuscar el origen de la conexión, de este modo ofrece a los usuarios que quieran utilizarlo una herramienta que permita obtener cierto anonimato en Internet.

```shell
whatweb [options] <URLs>

TARGET SELECTION:
 <TARGET>			Enter URLs, hostname, IP addresses, or nmap-format IP ranges
 --input-file=FILE, -i		Read targets from a file
 
AGREESION:
 --agresion, -a=LEVEL		Set the aggression level. Default 1
 				1. Stealthy, makes one HTTP request per target and also follows redirects
				3. Aggresive, if a level 1 plugin is matched, addional request will be made

PLUGINS:
 --list-plugins, -l		List all plugins
 --info-plugins, -I=[SEARCH]	List all plugins with detailed information. Optionally search with a keyword
 --search-plugins=STRING	Search for STRING in HTTP responses. Reports with a plugin named Grep
 
OUTPUT:
 --verbose, -v			Verbose output includes plugin descriptions. Use twice for debuggind
 --colour, --color=WHEN		Control whether coour is used. WHEN may be 'never', 'always', or 'auto
 
HELP & MISCELLANEOUS:
 --short-help			This short usage help
 --help, -h			Complete usage help
```

> **Example**  
> + Scan example.com  
> ```shell
> whatweb example.com
> ```  
> + Scan reddit.com slashdot.org with verbose plugin description
> ```shell
> whatweb -v reddit.com slashdot.org
> ``` 
> + An aggressive scan of wired.com detects the exact version of WordPress
> ```shell
> whatweb -a 3 www.wired.com
> ```  
> + Scan the local network quickly and suppress erros
> ```shell
> whatweb --no-erros 192.168.0.0/24
> ```  
> + Scan the local network for HTTPS website
> ```shell
> whatweb --no-erros --url-prefix https://192.168.0.0/24
> ```  
> + Scan for corssdomain policies in the Alex Top 1000
> ```shell
> whatweb -i plugin-development/alexa-top-100.txt \ --url-suffix /crossdomain.xml -p crossdomain_xml
> ```


- **BlindElephant.** Es una herramienta escrita en Python cuyo objetvio es la de descubrir la versión de aplicaciones web conocidas, frameworks para blogs, gestores de contenidos populares (CMS), como Wordpress, Drupal, Joomla, phpMyAdmin, etc. Y, para ello, se han precalculado los hashes de las distintas versiones de dichas plataformas web para contrastarlas con ficheros estáticos de rutas conocidas, y así poder hacer una aproximación del modelo y versión del objetivo en función de las respuestas obtenidas. Se trata de una técnica de detección no invasiva y rápida.

```shell
BlindElephant.py [options] url appName

OPTIONS:
 -h, --help					show this help message and exit
 -p PLUGINNAME, --pluginName=PLUGINNAME		fingerprint version of plugin (should apply to web app given in appname)
 -s, --skip					skip fingerprinting webpp, just fingerprint plugin
 -n NUMPROBES, --numProbes=NUMPROBES		number of files to fetch (more may increase accuracy). Default: 15
 -w, --winnow					if more than one version are returned, use winnowing to attempt to narrow it 
 						down (up to numProbes additional request)
 -l, --list					list supported webapps and plugins
 -u, --updateDB					Pull latest DB files from repo (may require root if blindelephan was installed with root
```

## INFORMATION GATHERING

Esta fase de recolección de información es una de las más tempranas en un proceso de auditoría.


- **Ingenería social.** Por ingenería social se entiende cualquier técnica usada que pretende aprovecharse del factor humano para la consecución de revelaciones de información.


- **Información de registro de nombre de domino.** Cuando se registra un nombre de dominio público en Interner o cuando se solicita la propiedad de una dirección IP pública, o un rango de las mismas, esta queda asociada a un registro con información diversa sobre el titular del servicio. En muchas ocasiones, entre esta información de registro se encuentran datos de interés, como servidores DNS o direcciones de correo electrónico de administradores. El protocolo que permite la consulta de esta información se denomina *whois*, y es posible trabajar con el mismo a través de herramientas de línea de comando o de portales web que ofrecen una sencilla interfaz para el usuario.


- **Consultas de zona DNS**
> Los servidores *DNS* (Domain Name System) son aquellos encargados de realizar la traducción de nombres de dominio, más sencillos de recordar por las personas, a sus correspondientes direcciones IP en Internet, que son los parámetros que realmente se usan en las comunicaciones de red.

Una zona DNS es un registro de información que presenta todas las entradas necesarias para la correcta resolución DNS de los servicios asociados a un nombre de dominio, como podrían ser los nombres de host presentes bajo dicho nombre de dominio o los servidores de correo electrónico encargados de gestionar este servicio. Cada una de estas entradas presentará, entre otros datos, un tipo y un valor.

 + Las entradas de tipo **MX** tendrían como valor una cadena de texto que indetificará el servidor de correo electrónico. Por ejemplo, si se está consultando la zona DNS del nombre de dominio "ejemplo.como", un valor para el registro MX podría ser "smtp.ejemplo.com"
 + Las entradas de tipo **NS** tendrán como valor una cadena de texto que identificará el servidor de DNS. Para "ejemplo.com", un valor para el registro MS podría ser "ns1.ejemplo.com"
 
> **Herramientas**  
> + Nslookup. Herramienta tradicional para la realización de consultas DNS (su nombre procede de name server lookup). Sin embargo, la corporación *Internet Systems Consortium* la ha catalagoda como anticuada. Con nslookup puede operarse de forma interactiva o no-interactiva  
> + Dig. Se trata de una potente herramienta de consultas DNS que sustituiría a nslookup  
> + Host. Herramienta más sencilla, pero de gran utilidad para consultas de menos extensión, que permite realizar resoluciones de nombres en las que no se precisan tantos detalles


## HACKING CON BUSCADORES

Una técnica que complementaría a la fase de information gathering consiste en usar los propios motores de búsqueda de Internet para localizar información sensible, o útil para un posible atacante, sobre el objetivo.

- **Google.**

Operador | Descripción
---------|------------
site | mediante este operador se restringe la búsqueda tan solo a páginas que estén dentro del sitio web o dominio especificado. Este operador es de gran utilidad para acotar las búsquedas cuando ya se conocen el sitio o los sitios web objetivo de ataque
intitle | gracias a este operador, la cadena introducida será buscada tan solo en el partado de título de las páginas web. Si se desea introducir más de un término de búsqueda --deberán estar todos presentes en el título de la página web-- se usará la variante **allintitle**.
inurl | el patarón de búsqueda introducido deberá estar localizado en la propia URL de la página web. De igual forma que en el caso anterio, si se desea introducir más de un parámetro, se usará el operador **allinurl**. Por ejemplo, si se introdujese la cadena de búsqueda "allinurl: ejemplo hacking", uno de los posibles resultados sería la web presente en la URL: *http//www.**ejemplo**.com/subdir/**hacking**.html*
intext | la cadena de búsqueda introducida deberá estar localizada en el texto de la página web. De igual forma que en los casos anteriores, si se desea introducir más de un parámetro, se usará más de un parámetro, se usará el operador **allintext**
filetype | acota la búsqueda a las páginas, o recursos ofrecidos a través de servidores web, cuya extensión sea la indicada a continuación del operador. Estas búsquedas son de gran utilidad para localizar posibles documentos o ficheros sensibles que, por error u olvido, se han dejado dentro de los directorio públicos de un sitio web

> **Ejemplos**  
> + filetype: sql -> buscará ficheros con extensión SQL  
> + intitle: "Index of" .bash_history -> el fichero *.bash_history* contiene los últimos comandos introducidos por un usuario que, en algunos casos, podrían incluso contener contraseñas pasadas como parámetros a comandos  
> + inurl: admin.php -> localización de portales de administradores de sitios web, muchos de ellos compuestos por gestores de contenidos públicos. Este tipo de búsqueda se emplea para lanzar ataques de fuerza bruta sobre las páginas de autenticación, que suele haber para poder acceder a la zona de administración del portal


- **SHODAN.** [https://www.shodan.io/](SHODAN) surgió como un portal permitiendo la indexación de servicios a través de los banners o firmas expuestas por los servidores.  

Actualmente, SHODAN pertmite realizar búsquedas, intrudocuendo diversos criterios o patrones.

Filtro | Descripción
---------|------------
city | filtro que permite, a través de la geolocalización de la dirección del servidor, acotar la búsqueda a ciudades concretas
country | actuando sobre los países. En caso de usar el filtro de *city*, es recomendable emplear este para evitar confusiones de ciudades con el mismo nombre
os | posibilita restringir la búsqueda a servicios que estén ejecutandose sobre sistemas operativos específicos
port | puerto del servicio que se va a buscar
