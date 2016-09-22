###Enviando formularios HTML y Query Strings

En muchas aplicaciones de Internet, tales como el comercio electrónico y el motor de búsqueda, se requieren los clientes para presentar información adicional al servidor (por ejemplo, el nombre, la dirección, las palabras clave de búsqueda). Basado en los datos presentados, el servidor toma una acción apropiada y produce una respuesta personalizada.

Los clientes suelen presentarse con un formulario (producidos utilizando la etiqueta ` <form>` de HTML). Una vez que se llenan los datos solicitados y se pulsa el botón de enviar, el navegador empaqueta los datos del formulario y las envía al servidor, usando ya sea una petición GET o una solicitud POST.

La siguiente es un ejemplo de una etiqueta `<form>` en HTML, que se produce por la siguiente secuencia de comandos HTML:

	 <Html>
	<Head> <title> Un formulario HTML de ejemplo </ title> </ head>
	 <Bod>
	  <H2 align= "left"> un formulario de entrada de datos de ejemplo HTML </ h2>
	  <Form method = "get" action = "/ bin / proceso">
    Introduzca su nombre: <input type = "text" name = "nombre de usuario"> <br />
    Introduzca su contraseña: <input type = nombre de "contraseña" = "contraseña"> <br />
    ¿Cuál año?
    <Input type = "radio" nombre = valor "año" = "2" /> Año 1
    <Input type = "radio" nombre = valor "año" = "2" /> Año 2
    <Input type = "radio" nombre = valor "año" = "3" /> <br /> Año 3
    Asunto registrado:
    <Input type = "checkbox" name = "sujeto" value = "e101" /> E101
    <Input type = "checkbox" name = "sujeto" value = "E102" /> E102
    <Input type = "checkbox" name = "sujeto" value = "e103" /> <br /> E103
    Elija un día:
    <Select name = "día">
      <Option value = "mon"> Lunes </ option>
      <Option value = "casarse"> Miércoles </ option>
      <Option value = "fri"> Viernes </ option>
    </ Select> <br />
    <Filas de área de texto = "3" cols = "30"> Introduzca su petición especial aquí </ textarea> <br />
    <Input type = "submit" value = "ENVIAR" />
    <Input type = "reset" value = "CLEAR" />
    <Input type = "hidden" name = "acción" value = "registro" />
	   </ Form>
	 </ Body>
	 </ Html> 


![1](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_SampleForm.png)

####Un formulario que contiene campos. Los tipos de campo incluyen:

- Cuadro de texto: producida por  `<input type="text">`
- Caja de contraseña: producida por `<input type="password">.`
- Botón de radio: producida por `<input type="radio">.`
- Checkbox: producida por `<input type="checkbox">.`
- Selección: producida por `<select>y <option>.`
- Área de texto: producida por `<textarea>.`
- Botón de envío: producida por `<input type="submit">.`
- Botón de reinicio: producida por `<input type="reset">.`
- El campo oculto: producida por `<input type="hidden">`.
- Botón: producida por `<input type="button">`.

Cada campo tiene un nombre y puede tomar en un determinado valor. Una vez que el cliente rellena los campos y pulsa el botón de enviar, el navegador reúne cada nombre con su respectivo valor, los empaqueta en pares " nombre = valor", y concatena todos los campos juntos usando " &" como separador de campo. Esto se conoce como una cadena de consulta . Se enviará la cadena de consulta al servidor como parte de la solicitud.

>nombre1 = valor1  &  nombre2 = valor2  &  nombre3 = valor3  & ...

Los caracteres especiales no están permitidos dentro de la cadena de consulta. Ellos deben ser reemplazados por un " %" seguido del código ASCII en hexadecimal. Por ejemplo, " ~" se sustituye por " %7E", " #" por " %23" y así sucesivamente. Como es espacio blanco es bastante común, puede ser sustituido por cualquiera " %20" o " +" (el carácter " +"  debe ser sustituido por " %2B"). Este proceso de sustitución se llama codificación URL , y el resultado es una cadena de consulta con codificación URL . Por ejemplo, supongamos que hay 3 campos dentro de un formulario, con "nombre = Peter Lee", "direccion = # 123 Ave feliz" y "language = C ++", la cadena de consulta con codificación URL es:

>nombre = + Peter Lee & dirección =% 23123 + + feliz Ave & Language = C% 2B% 2B

La cadena de consulta se puede enviar al servidor por medio del método GET o POST, el cual se especifica en el atributo " method" de  `<form>.`

	<form method = " obtener | post" action = " URL ">

Si se utiliza el método GET, la cadena de consulta con codificación URL se añade detrás de la URI de solicitud después de un carácter " ?", es decir,

> GET URI de solicitud  ? Cadena de consulta  HTTP versión
(otras cabeceras de petición opcional)
(linea en blanco)
(Cuerpo de la petición opcional) 

Usar la solicitud GET para enviar la cadena de consulta tiene los siguientes inconvenientes:
- La cantidad de datos se puede agregar detrás URI de solicitud es limitado. Si esta cantidad excede un umbral específico del servidor, el servidor devolverá un error "414 URI de la solicitud demasiado grande".
- La cadena de consulta con codificación URL aparecería en el cuadro de dirección del navegador.
El método POST supera estos inconvenientes. Si se utiliza el método de solicitud POST, la cadena de consulta se enviará en el cuerpo del mensaje de solicitud, donde la cantidad no está limitada. Las cabeceras de petición Content-Typey Content-Lengthse se utilizan para notificar al servidor el tipo y la longitud de la cadena de consulta. La cadena de consulta no aparecerá en el cuadro de dirección del navegador. El método POST se discutirá más adelante.

**Ejemplo**

La siguiente formulario HTML se utiliza para recopilar el nombre de usuario y contraseña en un menú de inicio de sesión.

	<Html>
	<Head> <title> Iniciar sesión </ title> </ head>
	 <Body>
	  <H2> LOGIN </ h2>
	  <Form method = "get" action = "/ bin / login">
    Nombre de usuario: <input type = "text" name = "usuario" size = "25" /> <br />
	    Contraseña: <input type = nombre de "contraseña" = tamaño "PW" = "10" /> <br /> <br />
	    <Input type = "hidden" name = "acción" value = "entrada" />
	    <Input type = "submit" value = "ENVIAR" />
	   </ Form>
	 </ Body>
	 </ Html> 

![imagen1](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_LoginForm.png)

El método de la petición  GET se utiliza para enviar la cadena de consulta. Supongamos que el usuario introduce "Peter Lee" como nombre de usuario, "123456" como contraseña; y pulse el botón Enviar. La siguiente petición GET es:

	 GET / bin / login? User = + Peter Lee & PW = 123456 & Action = HTTP entrada / 1.1
	Accept: image / gif, image / jpeg, * / *
	Árbitro: http://127.0.0.1:8000/login.html
	Accept-Language: en-us
	 Accept-Encoding: gzip, desinfle
	User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Anfitrión: 127.0.0.1:8000
	Conexión: Keep-Alive


 
Tenga en cuenta que aunque la contraseña que introduzca no se muestra en la pantalla, se muestra claramente en el cuadro de dirección del navegador. Nunca se debe enviar la contraseña sin un cifrado adecuado.
	
	http://127.0.0.1:8000/bin/login?user=Peter+Lee&pw=123456&action=login 

###URL y URI

**URL (Uniform Resource Locator)**

Un URL (Uniform Resource Locator), que se define en el RFC 2396, se utiliza para identificar de forma exclusiva un recurso a través de Internet. URL tiene la siguiente sintaxis:

	 protocolo : // nombre de host : puerto / ruta-y-nombre-archivo
	  
Hay 4 partes en una dirección URL:

- Protocolo : El protocolo de capa de aplicación utilizado por el cliente y el servidor, por ejemplo, HTTP, FTP y telnet.

- Nombre de host : El nombre de dominio DNS (por ejemplo, www.nowhere123.com) o la dirección IP (por ejemplo, 192.128.1.2) del servidor.

- Puerto : El número de puerto TCP que el servidor está a la escucha de peticiones entrantes de los clientes.

- Ruta-y-nombre-archivo : El nombre y la ubicación del recurso solicitado, bajo el directorio base de documentos del servidor.

Por ejemplo, en el URL `http://www.nowhere123.com/docs/index.html`, 
el protocolo de comunicación es HTTP; el nombre de host es `www.nowhere123.com`. El número de puerto no se ha especificado en la URL, y adquiere el número predeterminado, que es el puerto TCP 80 para HTTP [STD 2]. La ruta y el nombre del archivo para el recurso que se encuentra es " /docs/index.html".

Otros ejemplos de URL son:

	ftp://www.ftp.org/docs/test.txt
	mailto: user@test101.com
	news: soc.culture.singapore
	telnet: //www.nowhere123.com/ 
	
**URL codificada**

Una URL no puede contener caracteres especiales, como blanco o '~'. Los caracteres especiales se codifican, en forma de %xx, donde xx es el código ASCII hexadecimal. Por ejemplo, '~'se codifica como %7e; '+'se codifica como %2b. Un espacio en blanco puede ser codificada como %20 o '+'. La dirección URL después de la codificación se llama URL codificada .

**URI (Uniform Resource Identifier)**

URI (Uniform Resource Identifier), definido en RFC3986, es más general que el URL, puede incluso localizar un fragmento dentro de un recurso. La sintaxis URI para el protocolo HTTP es:

	 http: // host: puerto / ruta de solicitud de parámetros-# nameAnchor 

- Los parámetros de la petición, en forma de pares nombre = valor, se separan de la URL por una '?'. Los pares nombre = valor están separados por una '&'.

-  `#nameAnchor` identifica un fragmento dentro del documento HTML, que se define a través de la etiqueta de anclaje `<a name=" anchorName ">...</a>`

- La URL se reescribe para el manejo de la sesión, por ejemplo, " ...;sessionID=xxxxxx".

###Método"POST" 

El método de solicitud POST se utiliza para enviar datos adicionales a el servidor (por ejemplo, la presentación de los datos del formulario HTML o subir un archivo). La emisión de una URL HTTP desde el navegador siempre activa una solicitud GET. Para desencadenar una solicitud POST, puede utilizar un formulario HTML con el atributo method="post"o escribir su propio programa de red. Para la presentación de los formularios HTML, la petición POST es la misma que la petición GET, excepto que la cadena de consulta con codificación URL se envía en el cuerpo de la solicitud, en lugar de adjuntó detrás de la URI de solicitud .

La solicitud POST toma la siguiente sintaxis:

	 POSTAL  URI de solicitud  HTTP versión
	 Content-Type: tipo MIME 
	Content-Length: número-de-bytes
	(otras cabeceras de petición opcional)
  
	(Cadena de consulta con codificación URL) 

Las cabeceras de petición Content-Type y Content-Lengthes son necesarias  en la solicitud POST para informar al servidor el tipo y la longitud del cuerpo de la petición.

**Ejemplo: Envío de formularios de datos mediante POST**

Utilizamos el mismo script HTML como el anterior, pero cambiamos el método de la petición POST.

	<Html>
	<Head> <title> Iniciar sesión </ title> </ head>
	 <Body>
	  <H2> LOGIN </ h2>
	  <form method = "post" action = "/ bin / login">
    Nombre de usuario: <input type = "text" name = "usuario" size = "25" /> <br />
    Contraseña: <input type = nombre de "contraseña" = tamaño "PW" = "10" /> <br /> <br />
    <Input type = "hidden" name = "acción" value = "entrada" />
    <Input type = "submit" value = "ENVIAR" />
	   </ Form>
	 </ Body>
	 </ Html> 

Supongamos que el usuario introduce "Peter Lee" como nombre de usuario y "123456" como contraseña, y pulsa el botón de enviar, la siguiente petición POST sería generada por el navegador:

	POSTAL / bin / login HTTP / 1.1
	Anfitrión: 127.0.0.1:8000
	Accept: image / gif, image / jpeg, * / *
	Árbitro: http://127.0.0.1:8000/login.html
	Accept-Language: en-us
	Content-Type: application / x-www-form-urlencoded
	 Accept-Encoding: gzip, desinfle
	User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Content-Length: 37
	Conexión: Keep-Alive
	Cache-Control: no-cache
   
	User = + Peter Lee & PW = 123456 & Action = login 
	
Tenga en cuenta que la cabecera Content-Type informa al servidor que  los datos se codifican en URL (con un  MIME type especial application/x-www-form-urlencoded), y la cabecera Content-Lengthe indica al servidor el número de bytes a leer en el cuerpo del mensaje.

**POSTAL vs GET para el envío de formularios**

Como se mencionó en la sección anterior,  POST tiene las siguientes ventajas en comparación con GET en el envío de la cadena de consulta:

- La cantidad de datos que pueden ser enviada es ilimitada, mientras se mantengan en el cuerpo de la petición, que generalmente se envía al servidor en un flujo de datos independiente.

- La cadena de consulta no se muestra en el cuadro de dirección del navegador.

Tenga en cuenta que aunque la contraseña no se muestra en el cuadro de dirección del navegador,  se transmite al servidor en texto claro, y se expone a ser vista en la red. Por lo tanto, el envío de la contraseña 
mediante una solicitud POST absolutamente no es seguro.

###Subir archivos mediante la petición POST multipart/form-data

El "RFC 1867: Form-based File upload in HTML"  especifica cómo un archivo se puede cargar en el servidor mediante una petición POST de un formulario HTML. Un nuevo atributo type="file" se añadió a la etiqueta `<input>` del código `<form>` para soportar la carga de archivos. Los datos que se  cargan en el método POST no es una URL codificada (en la norma application/x-www-form-urlencoded), sino que utiliza un nuevo tipo MIME multipart/form-data.

**Ejemplo**

El  siguiente formulario HTML puede ser utilizado para la carga de archivos:
	
	<Html>
	<Head> <title> Carga de archivos </ title> </ head>
	 <Body>
	  <H2> Carga de archivos </ h2>
	  <form method = "post" enctype = "multipart / form-data" action = "servlet / UploadServlet">
    ¿Quién es usted: <input type = "text" name = "nombre de usuario" /> <br />
    Seleccione el archivo a subir:
	    <input type = "file" name = "fileID" /> <br />
	    <Input type = "submit" value = "ENVIAR" />
	   </ Form>
	 </ Body>
	 </ Html> 
	 
![](https://www.ntu.edu.sg/home/ehchua/programming/webprogramming/images/HTML_FileUploadForm.png)

Cuando el navegador encuentra una etiqueta `<input>` con el atributo type="file", se muestra un cuadro de texto y un botón "Examinar ...", para permitir al usuario elegir el archivo para ser cargado.

Cuando el usuario hace clic en el botón de enviar, el navegador envía los datos del formulario y el contenido del archivo (s) seleccionado. El antiguo tipo de codificación " application/x-www-form-urlencoded" es ineficiente para el envío de datos binarios y los caracteres no ASCII. Un nuevo tipo de medio "multipart/form-data" se utiliza en su lugar.
Cada parte identifica el nombre de entrada en el formulario HTML original, y el tipo de contenido si el medio es conocido, o como "application/octet-stream" de otra manera.

El nombre de archivo local original podría ser suministrado como un parámetro " filename" o en el " Content-Disposition: form-data" de cabecera.

Un ejemplo del mensaje POST de carga de archivos es la siguiente:

	POST / bin / carga HTTP / 1.1
	Anfitrión: test101
	Accept: image / gif, image / jpeg, * / *
	Accept-Language: en-us
	Content-Type: multipart / form-data; boundary = --------------------------- 7d41b838504d8
	 Accept-Encoding: gzip, desinfle
	User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Content-Length: 342
	Conexión: Keep-Alive
	Cache-Control: no-cache
   
	----------------------------- 7d41b838504d8 Content-Disposition: form-data; name = "nombre de usuario" 
	 Peter Lee
	----------------------------- 7d41b838504d8 Content-Disposition: form-data; name = "fileID"; filename = "C: \ temp.html" Content-Type: text / plain 
	<H1> Página de inicio en el servidor principal </ h1> 
	----------------------------- 7d41b838504d8-- 

Servlet 3.0 proporciona soporte integrado para la carga de archivos de procesamiento. Leer " Carga de archivos en Servlet 3.0 ".

###Método de petición "CONNECT" 

La petición "CONNECT" se utiliza para pedir a un proxy  establecer una conexión con otro host  y simplemente retransmitir el contenido, en lugar de intentar analizar o almacenar en caché el mensaje. Esto a menudo se utiliza para realizar una conexión a través de un proxy.

(En construcción)

###Otros Métodos de petición

PUT: Pregunta el servidor para almacenar los datos.
DELETE: Pregunta el servidor para eliminar los datos.
Por consideraciones de seguridad, PUT y DELETE no son compatibles con la mayor parte del servidor de producción.
Los métodos de extensión (también códigos de error y cabeceras) se pueden definir para extender la funcionalidad del protocolo HTTP.

(En construcción)

###Negociación de contenido

Como se mencionó anteriormente, HTTP soporta negociación de contenido entre el cliente y el servidor. Un cliente puede utilizar encabezados de solicitudes adicionales (como Accept, Accept-Language, Accept-Charset, Accept-Encoding) para indicar al servidor lo que puede manejar o el contenido que se prefiere. Si el servidor posee varias versiones de un mismo documento en un formato diferente, devolverá el formato que el cliente prefiera. Este proceso se llama negociación de contenido .

###Negociación Content-Type 

El servidor utiliza un archivo de configuración MIME llamado ("conf\mime.types") para mapear la extensión de archivo a un tipo de soporte , de modo que pueda determinar el tipo de medio del archivo mirando su extensión de archivo. Por ejemplo, las extensiones de archivo " .htm", " .html" están asociados con el tipo de medio MIME " text/html", las extensiones de archivo " .jpg", " .jpeg" están asociados con " image/jpeg". Cuando un archivo se devuelve al cliente, el servidor tiene que poner un encabezado Content-Type de respuesta para informar al cliente el tipo de soporte de los datos.

Para la negociación de tipo de contenido, supongamos que el cliente solicita un archivo " logo", sin especificar su tipo, y envía una cabecera " Accept: image/gif, image/jpeg,...". Si el servidor tiene 2 formatos de la " logo": " logo.gif" y " logo.jpg" y el archivo de configuración MIME tiene las siguientes entradas:

	image/gif       gif
	image/jpeg      jpeg jpg jpe 


El servidor devolverá " logo.gif" al cliente, basada en la cabecera  Accept del cliente , y en el mapeo del archivo MIME type. El servidor incluirá una cabecera "Content-type: image/gif"  en su respuesta.

Se muestra el trace del mensaje:

	GET / logotipo de HTTP / 1.1
	Accept: image / gif, image / x-xbitmap, image / jpeg, imagen / pjpeg,
	  application / x-shockwave-flash, application / vnd.ms-excel, 
	  application / vnd.ms-powerpoint, la aplicación / pdf, * / *
	Accept-Language: en-us
	 Accept-Encoding: gzip, desinfle
	User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Anfitrión: test101: 8080
	Conexión: Keep-Alive
	(linea en blanco) 
	 HTTP / 1.1 200 OK
	Fecha: Dom 29 Feb 2004 01:42:22 GMT
	Servidor: Apache / 1.3.29 (Win32)
	Content-Location: logo.gif
	Variar: negociar, aceptar
	TCN: elección
	Última modificación: Mie 21 Feb de 1996 19:45:52 GMT
	ETag: "0-916-312b7670; 404142de"
	Accept-Ranges: bytes
	Content-Length: 2326
	Keep-alive: timeout = 15, max = 100
	Conexión: Keep-Alive
	Content-Type: image / gif
	(linea en blanco)
	(Cuerpo omitida) 

Sin embargo, si el servidor tiene 3 archivos "logo" , " logo.gif", " logo.html", " logo.jpg" y " Accept: */*" se utilizó:

	 GET / logotipo de HTTP / 1.1
	Aceptar: * / *
	Accept-Language: en-us
	 Accept-Encoding: gzip, desinfle
	User-Agent: Mozilla / 4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Anfitrión: test101: 8080
	Conexión: Keep-Alive
	(linea en blanco) 
	 HTTP / 1.1 200 OK
	Fecha: Dom 29 Feb 2004 01:48:16 GMT
	Servidor: Apache / 1.3.29 (Win32)
	Content-Location: logo.html
	Variar: negociar, aceptar
	TCN: elección
	Últim	a modificación: Vie 20 Feb de 2004 04:31:17 GMT
	ETag: "0-10-40358d95; 404144c1"
	Accept-Ranges: bytes
	Content-Length: 16
	Keep-alive: timeout = 15, max = 100
	Conexión: Keep-Alive
	Content-Type: text / html
	(linea en blanco)
	(Cuerpo omitida) 
	 Aceptar: * / * 

Las siguientes directivas de configuración de Apache son relevantes para la negociación de tipo de contenido:

- La directiva TypeConfig se puede utilizar para especificar la ubicación del archivo de asignación MIME:
 
		 TypeConfig conf / mime.types 
 
- La directiva AddType se puede utilizar para incluir la asignación de tipos MIME adicionales en el archivo de configuración:

		AddType tipo MIME  extensión1 [ extensión2 ]

- La directiva DefaultType da el tipo MIME de una extensión de archivo desconocido (en la cabecera Content-Type de la respuesta)
 
		 texto DefaultType / plain

###Negociación lenguaje y "Options MultiView"

La directiva "Options MultiView" es la forma más simple de implementar la negociación de idioma. Por ejemplo:

	AddLanguage en .en
	<Directory "C:/_javabin/Apache1.3.29/htdocs">
      Options Indexes MultiViews
	</Directory>

Supongamos que el cliente solicita "index.html" y envia un " Accept-Language: en-us". Si el servidor tiene " test.html", " test.html.en" y " test.html.cn", basada en la preferencia del cliente ", test.html.en" será devuelto. ( " en" incluye " en-us".)

Una traza de mensaje es el siguiente:

	
	GET /index.html HTTP/1.1
	Accept: */*
	Accept-Language: en-us
	Accept-Encoding: gzip, deflate
	User-Agent: Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1)
	Host: test101:8080
	Connection: Keep-Alive
	(blank line)
	HTTP/1.1 200 OK
	Date: Sun, 29 Feb 2004 02:08:29 GMT
	Server: Apache/1.3.29 (Win32)
	Content-Location: index.html.en
	Vary: negotiate
	TCN: choice
	Last-Modified: Sun, 29 Feb 2004 02:07:45 GMT
	ETag: "0-13-40414971;40414964"
	Accept-Ranges: bytes
	Content-Length: 19
	Keep-Alive: timeout=15, max=100
	Connection: Keep-Alive
	Content-Type: text/html
	Content-Language: en
	(blank line)
	(body omitted)

La directiva  AddLanguage es necesaria para asociar un código de idioma con una extensión de archivo, similar a la asignación de tipo MIME / archivo.
Tenga en cuenta que la directiva "Options All"  no incluye la opción "MultiViews" . Es decir, hay que activar de forma explícita MultiViews.
La directiva LanguagePriority se puede utilizar para especificar la preferencia del idioma en caso de empate durante la negociación de contenido o si el cliente no expresa una preferencia. Por ejemplo:

	 <IfModule mod_negotiation.c>
	   LanguagePriority es da nl et fr el it ja KR no pl pt pt-br
	 </ IfModule> 

###Juego de caracteres Negociación

Un cliente puede utilizar el encabezado de la solicitud Accept-Charset para negociar con el servidor el conjunto de caracteres que prefiere.

	Accept-Charset: charset-1 , charset-2 , ...

Los conjuntos de caracteres comúnmente encontradas incluyen: ISO-8859-1 (Latin-I), ISO-8859-2, ISO-8859-5, Big5 (chino tradicional), GB2312 (chino simplificado), UCS2 (2 bytes Unicode), UCS4 (4 bytes Unicode), UTF-8 (Unicode codificada), y etc.

Del mismo modo, la directiva AddCharset se utiliza para asociar la extensión de archivo con el conjunto de caracteres. Por ejemplo:
	
	AddCharset ISO-8859-8      .iso8859-8
	AddCharset ISO-2022-JP     .jis .big5 
	AddCharset Big5            .Big5
	AddCharset de WINDOWS-1251 .cp-1251
	AddCharset CP866           .cp866
	AddCharset ISO-8859-5      .Iso-ru
	AddCharset KOI8-R          .koi8-r
	AddCharset UCS-2           .ucs2
	AddCharset UCS-4           .ucs4
	AddCharset UTF-8           .utf8 

###La negociación de codificación

Un cliente puede utilizar la cabecera Accept-Encoding para indicar al servidor el tipo de codificación que soporta. Los esquemas de codificación comunes son: " x-gzip (.gz, .tgz)" y " x-compress (.Z)".

	Accept-Encoding: Codificación-método-1, codifica-método-2 , ...
	
Del mismo modo, la dingdirectiva AddEnco se utiliza para asociar la extensión de archivo con el esquema de una codificación. Por ejemplo:

	AddEncoding x-compress .Z
	AddEncoding x-gzip .gz .tgz 
	
###Conexiones persistentes (keep-alive) 

En HTTP / 1.0, el servidor cierra la conexión TCP después de entregar la respuesta por defecto ( Connection: Close). Es decir, cada una de las conexiones  TCP sirve sólo una petición. Esta no es muy eficiente si muchas  páginas HTML contienen hipervínculos  (la etiqueta `<a href="url">`) a otros recursos (como imágenes, scripts - ya sea local o desde un servidor remoto). Si descarga una página que contiene 5 imágenes en línea, el navegador tiene que establecer una conexión TCP 6 veces en el mismo servidor.
El cliente puede negociar con el servidor y pedir al servidor no cerrar la conexión después de la entrega de la respuesta, de modo que otra petición puede ser enviada a través de la misma conexión. Esto se conoce como conexión persistente (keep-alive). Las conexiones persistentes mejoran en gran medida la eficiencia de la red. Para HTTP / 1.0, la conexión por defecto es no persistente. Para solicitar conexión persistente, el cliente debe incluir un encabezado de solicitud " Connection: Keep-alive" en el mensaje de petición de negociar con el servidor.

Para HTTP / 1.1, la conexión por defecto es persistente. El cliente no tiene que enviar la cabecera " Connection: Keep-alive". En su lugar, el cliente puede desear enviar el encabezado " Connection: Close" para pedir al servidor cerrar la conexión después de la entrega de la respuesta.
Conexión persistente es extremadamente útil para páginas web con muchas imágenes pequeñas en línea y otros datos asociados, ya que todos estos pueden ser descargadas a través de la misma conexión. Los beneficios para la conexión persistente son:

- Ahorro de tiempo de CPU y de recursos en la apertura y cierre de conexión TCP en el cliente, proxy, puertas de enlace, y el servidor de origen.

- La solicitud se puede "pipelinear". Es decir, un cliente puede hacer varias solicitudes sin esperar a  cada respuesta, con el fin de utilizar la red de manera más eficiente.

- Una respuesta más rápida ya que ningún tiempo necesario para realizar el hadshaking de apertura de TCP.

En el servidor Apache, varias directivas de configuración están relacionados con las conexiones persistentes:

La directiva KeepAlive  decide si admite conexiones persistentes. Esta toma valor de encendido o apagado.
	 
	 KeepAlive On | Off 

La directiva MaxKeepAliveRequests establece el número máximo de solicitudes que se pueden enviar a través de una conexión persistente. Se puede establecer en 0 para permitir que un número ilimitado de solicitudes. Se recomienda establecer en un número alto para un mejor rendimiento y eficiencia de la red.

	 MaxKeepAliveRequests 200 
	 
La  directiva KeepAliveTimeOut  establece el tiempo de espera en segundos para que una conexión persistente espere a la siguiente solicitud.

	 KeepAliveTimeout 10 
	 
###Rango de descarga
	 Accept-Ranges: bytes
	Transfer-Encoding: fragmentada 

(En construcción)

###Control de caché

El cliente puede enviar un encabezado de solicitud " Cache-control: no-cache" para indicar al proxy  obtener una nueva copia del servidor original, incluso si existe una copia en caché local. Por desgracia, servidor HTTP / 1.0 no entiende esta cabecera, pero puede usar un encabezado de la solicitud más antigua " Pragma: no-cache". Usted podría incluir ambas cabeceras en su solicitud.

	  Pragma: no-cache
	 Cache-Control: no-cache 
(Más, En construcción)

###REFERENCIAS Y RECURSOS

- Especificaciones HTTP W3C en http://www.w3.org/standards/techs/http
- RFC 2616 "Protocolo de transferencia de hipertexto HTTP / 1.1" de 1999 @ http://www.ietf.org/rfc/rfc2616.txt .
- RFC 1945 "Protocolo de transferencia de hipertexto HTTP / 1.0", 1996 - @ http://www.ietf.org/rfc/rfc1945.txt .
- ETS 2: "Assigned Numbers", de 1994.
- STD 5: "Protocolo de Internet (IP)" de 1981.
- STD 6: "User Datagram Protocol (UDP)", 1980.
- STD 7: "Protocolo de Control de Transmisión (TCP)", de 1983.
- RFC 2396: "Identificadores uniformes de recursos (URI): Sintaxis Genérica", de 1998.
- RFC 2045: "Multipurpose Internet Mail Extension (MIME) Parte 1: Formato de los mensajes de Internet cuerpos", de 1996.
- RFC 1867: "carga basado en el Formulario de HTML", 1995 (desfasadas por el RFC2854).
- RFC 2854: "El text / html tipo de medio", de 2000.
- Mutlipart servlet para la carga de archivos @ www.servlets.com

> Written with [StackEdit](https://stackedit.io/).
