# FirmaXadesEpes

Este es un pequeño compilado en .JAR que te permite inyectar las firmas Xades-EPES a tus XML, las facturas firmadas por esta aplicación ya fueron testeadas con éxito utilizando el api que provee el Ministerio de Hacienda de Costa Rica. A continuación, voy a documentar un poco su manera de uso, el entorno que necesitan y como pueden probarlo localmente y en sus aplicaciones PHP, Python, Ruby y Node.js.

## Entorno:
Básicamente como la aplicación está desarrollada en Java usando Maven , lo que necesitan es tener instalados en sus servidores el JAVA (https://www.java.com/en/download/) y JRE java runtime enviroment (http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) . Nada más asegúrense configurar las variables de entorno globales para que sus terminales puedan reconocerles los comandos JAVA.

_PD: Si escriben “java -version” en la consola cmd (Windows) o terminal(Linux,mac) y les aparece la versión de java entonces configuraron bien las variables de entorno._

## Estructura:
El repositorio contiene dos carpetas, la primera llamada __“compilado”__ es donde esta nuestro archivo ejecutable y el compilado de clases que necesita para funcionar. La segunda es completamente opcional se llama __“recursos”__, en ella van a encontrar una demo de una factura sin firmar en formato .xml para que puedan hacer sus pruebas.

En esta carpeta de __recursos__ podrían guadar sus archivos de extensión .p12(__La llave criptográfica que descargar del atv de hacienda__) para leerla, y también podrían usarlo para almacenar sus facturas firmadas.

## Corriendo Localmente:
Teniendo ya configurado java y las variables de entorno en nuestro servidor o computadora personal , además habiendo descargado nuestra llave criptográfica.p12 podemos proceder a firmar los documentos.

### Necesario:
* Factura.xml. _//Factura en formato xml según lo establecido por hacienda_
* Llave.p12. _//Archivo con extensión .p12 que corresponde a la llave criptográfica_
* Pin. _// El pin que desbloquea nuestra llave criptgrafica_

Para ejecutarlo y testearlo localmente abrimos la consola cmd(Windows) o la terminal (Linux , Apple) y ejecutamos lo siguiente.

`java -jar ../ruta_personalizada/compilado/firmar-xades.jar`

Este primer comando ejecuta la aplicación, por __ruta_personalizada__ me refiero a que ubiquen donde clonaron o descargaron este repositorio dentro de la carpeta __FirmaXadesEpes__.

Ahora, les va a dar una __excepción__ por que nuestra aplicación recibe __4 parametros__:
1. Primer parámetro es la ruta en donde esta la llave .p12
2. El segundo parámetro es el pin que desbloquea la llave
3. El tercer parámetro es la factura en formato xml
4. El cuarto parámetro es la locación y nombre que tendrá la factura ya firmada

En este sentido el comando completo seria:

`java -jar ../ruta_personalizada/compilado/firmar-xades.jar ../ruta_personalizada/cert.p12 9865 ../ruta_personalizada/demo-factura.xml ../ruta_personalizada/ demo-factura-firmada.xml`

Si todo sale bien , el archivo __demo-factura-firmada.xml__ debería estar en donde le indicamos en el cuarto parámetro.

## Corriendo con lenguajes ejemplo

### PHP:
`<?php 
   shell_exec("java -jar ../ruta_personalizada/compilado/firmar-xades.jar ../ruta_personalizada/cert.p12 9865 ../ruta_personalizada/demo-factura.xml ../ruta_personalizada/demo-factura-firmada.xml");`

### Python:
`import subprocess
 subprocess.call(['java', '-jar', '../ruta_personalizada/compilado/firmar-xades.jar' , ‘../ruta_personalizada/cert.p12’ , ‘9856’ , ‘../ruta_personalizada/demo-factura.xml’, ‘../ruta_personalizada/demo-factura-firmada.xml’])`

### Ruby:
`IO.popen( [ 'java', '-jar', '../ruta_personalizada/compilado/firmar-xades.jar,"#{ ../ruta_personalizada/cert.p12}", "#{9856}", “#{../ruta_personalizada/demo-factura.xml}” ,”#{ demo-factura.xml ../ruta_personalizada/demo-factura-firmada.xml}” , {SDTERR=>STDOUT} ]`

### Node.JS:
`var exec = require('child_process').exec, child;
child = exec('java -jar ../ruta_personalizada/compilado/firmar-xades.jar ../ruta_personalizada/cert.p12 9865 ../ruta_personalizada/demo-factura.xml ../ruta_personalizada/demo-factura-firmada.xml',
  function (error, stdout, stderr){
    console.log('stdout: ' + stdout);
    console.log('stderr: ' + stderr);
    if(error !== null){
      console.log('exec error: ' + error);
    }
});`

### __PD: Si desean mejorar esta documentación será bienvenido.__

## Contacto:
jonh.m.10@gmail.com
