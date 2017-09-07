---
layout: post
title: Instalando pip y fabric en Windows
date: 2017-09-06
categories: python pip fabric cryptography windows
---

En el curro me han introducido en un proyecto web implementado en Angular y Django. Yo utilizo Windows y para instalar todas las dependencias de Python para correr el backend hecho en Django me he visto con un problema que detallo a continuación.

Ya tenía instalado Python 2.7 en mi Windows desde hace tiempo. Para instalar todas las dependencias del proyecto, me encontré con el famoso fichero 'requirements.txt'. Tan fácil como: 

    pip install -r requirements.txt

Al no tener la herramienta *pip* instalada en mi ordenador, me he tenido que descargar Python para Windows para reinstalarlo (en mi caso la versión 2.7). Al finalizar el proceso de instalación, el asistente te ofrece la posibilidad de customizar la instalación instalando extensiones, documentación, scripts, etc. Entre todas estas opciones aparecerá *pip*, la cual marcaremos para su instalación. 

Pero no acaba aquí la cosa, ya que tenemos que añadir una nueva variable del sistema para que nuestro sistema operativo reconozca *pip* como comando. Vamos a introducir en la variable *Path* el directorio donde están instalados los scripts de Python. En mi caso:

    C:\Python2.7\Scripts

(Deberíamos tener otro valor en la misma variable que sería *C:\Python2.7\** para ejecutar Python).

Con esto ya podríamos ejecutar el comando *pip* por línea de comandos.

En la documentación del proyecto, para subir los cambios debo hacer:

    fab deploy

Y para eso debo instalar la librería *fabric*, que nos permite administrar paralelamente varios servidores SSH y poder ejecutar tareas definidas por el usuario en todos ellos.

Me dispongo a instalar *fabric* con:

    pip install fabric

Pero, como es habitual en estos casos, y más en Windows, no podía ser todo tan bonito. Error al final, en un rojo de esos que duelen:

    Cannot open include file: 'openssl/opensslv.h': No such file or directory

*fabric* me ha quedado instalado, pero al ejecutar mi deploy se queja de un paquete llamado *cryptography*. Después de estar casi una hora investigando, descargarme e instalarme más "cositas" innecesarias, doy con esta [web](http://slproweb.com/products/Win32OpenSSL.html) gracias, una vez más, a un post en [stackoverflow](https://stackoverflow.com/questions/45089805/pip-install-cryptography-in-windows). De aquí me descargué el fichero *Win64 OpenSSL v1.0.2L*. Al ejecutarlo, se genera un directorio *OpenSSL-Win64* en nuestra partición de Windows. Sólo me quedó ejecutar estas 3 líneas en mi cmd:

    set INCLUDE=C:\OpenSSL-Win32\include;%INCLUDE%
    set LIB=C:\OpenSSL-Win32\lib;%LIB%
    pip install cryptography

¡Y se acabó! Todo funcionando correctamente. Mi backend en local perfectamente instalado.

¡¡Saludos!!



## Referencias

* [Python Windows Downloads](https://www.python.org/downloads/windows/)
* [stackoverflow.com](https://stackoverflow.com/questions/45089805/pip-install-cryptography-in-windows)
* [openSSL Installer](http://slproweb.com/products/Win32OpenSSL.html)