---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - php
  - ruby
  - csharp

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introducción
Bienvenido a la documentación oficial del API de PagoFacil. A través de esta guía podrás configurar los servicios de cobro necesarios para que nuestra plataforma se adapte a tu negocio de forma rápida y efectiva

# Tarjeta no Presente
La API ofrece la posibilidad de procesar los pagos mediante un Servicio Web (Web Service) manteniedo a los clientes en su sitio web mientras la transacción se ejecuta en segundo plano.

La API de PagoFácil tiene la capacidad de:
- Diseñar y alojar sus páginas de pago.
- Mantener a los clientes en su sitio en lugar de hacer que paguen en otra página; PagoFácil permanece invisible.
- Respuesta de las transacciones en tiempo real.
- Estar implementada con los formatos más comun es de intercambio, tanto para web como para apps.
- Constriurise mediante un arreglo de nombre valor, un estándar del sector que utiliza servicios Web
- Envía todos los datos en línea mediante Secure Socket Layer (SSL).

## Métodos de implementación
- WebForm: Ésta forma es muy simple con solo añadir código HTML que se muestra en la sección correspondiente.
- ThirdParty: Se necesita tener conocimientos más avanzados de programación para crear los clientes (SOAP, REST, etc.) y consumir el servicio.

## Credenciales API
Para acceder al API es necesario proporcionar el número de sucursal y el número de usuario para identificarse y relacionar las transacciones con su cuenta.

Utiliza los siguientes datos para poder hacer pruebas:

- `idSucursal: 60f961360ca187d533d5adba7d969d6334771370`
- `idUsuario: 62ad6f592ecf2faa87ef2437ed85a4d175e73c58`

**Nota**: *Al realizar el registro se proporcionan esos datos (Entorno Producción y Entorno de Pruebas) correspondientes a tu cuenta. Las transacciones realizadas en el Entorno de Pruebas no se verán reflejadas en el panel de administración.*

## Ambientes API

Para poder hacer pruebas se utilizara el entorno de desarrollo (Development), una vez finalizadas las pruebas podrán utilizar las dirección del entorno de producción, es importante mencionar que para transacciones realizadas con Visa o MasterCard, la respuesta se dará de forma aleatoria (puede ser Aprobada o Declinada) aunque los datos estén correctos, para los casos de American Express, la respuesta será satisfactoria siempre y cuando los datos requeridos sean correctos.

**Desarrollo:**

- (webform)    = `https://www.pagofacil.net/st/public/Payform`
- (soap)    = `https://www.pagofacil.net/st/public/Wsstransaccion/`
- (soap wsdl)  = https://www.pagofacil.net/st/public/Wsstransaccion/?wsdl`
- (rest xml)   = `https://www.pagofacil.net/st/public/Wsrtransaccion/`
- (rest json)   = `https://www.pagofacil.net/st/public/Wsrtransaccion/index/format/json?`
- (json)    = `https://www.pagofacil.net/st/public/Wsjtransaccion/`

**Producción:**
- (webform) = `https://www.pagofacil.net/ws/public/Payform`
- (soap)    = `https://www.pagofacil.net/ws/public/Wsstransaccion/`
- (soap wsdl) = `https://www.pagofacil.net/ws/public/Wsstransaccion/?wsdl`
- (rest xml)   = `https://www.pagofacil.net/ws/public/Wsrtransaccion/`
- (rest json)   = `https://www.pagofacil.net/ws/public/Wsrtransaccion/index/format/json?`
- (json)    = `https://www.pagofacil.net/ws/public/Wsjtransaccion/`

## Parámetros
Parámetro | Tipo | Requerido | Descripción | Categoría
--------- | ------- | -----------| -----------| -----------
Nombre| En este campo vendrá el nombre del tarjetahabiente | varchar(50) | Sí |Tarjeta de Crédito
Apellidos|En este campo vendrán los apellidos del tarjetahabiente|varchar(50)|Si|Tarjeta de Crédito
numeroTarjeta|Numero del plástico de la tarjeta de crédito sin guiones o espacios|Si|varchar(16)|Tarjeta de Crédito
Cvt|Código de verificación de tarjeta,usualmente impreso en el área de firma de la tarjeta, utilizado para validar que la tarjeta usada en la compra pertenezca a la persona que generó la orden|Si|int(4)|Tarjeta de Crédito
mesExpiracion|El mes en el cual el plástico expira MM|Si|int(2)|Tarjeta de Crédito
anyoExpiracion|El año en el cual el plástico expira MM|Si|int(2)|Tarjeta de Crédito
**Monto***|El monto(MXP) del cargo a la tarjeta|Si|Decimal|Establecimiento
idSucursal|En caso de contar con varias sucursales se podrá utilizar este alfanumérico identificador para distinguir las transacciones|Si|Varchar(60) alfanumérico sin espacios|Establecimiento
idUsuario|Sera el identificador de la empresa ante PagoFácil|Si|Varchar(60)|Establecimiento
idServicio|Este identificador le indica al motor de PagoFácil que servicio será el que se consumirá: 1=WebForm, 3=ThirdParty(ssl)|Si|Int|Producto PagoFácil
Email|En este campo vendrá el correo de la persona a la que se le enviara el correo con el resumen de la transacción|Si|mail (200)|Datos Personales Cliente
Teléfono|Se debe incluir el teléfono del tarjetahabiente|Si|varchar(10)|Datos Personales Cliente
Celular|Campo reservado el número de celular del tarjetahabiente|Si|varchar(10)|Datos Personales Cliente
calleyNumero|Campo para registro de la calle y numero del tarjetahabiente|Si|varchar(45)|Datos Personales Cliente
Colonia|Campo para registro de la colonia del tarjetahabiente|Si|varchar(30)|Datos Personales Cliente
municipio|Campo para registro del municipio del tarjetahabiente|Si|varchar(30)|Datos Personales Cliente
Estado|Campo para registro del estado del tarjetahabiente|Si|varchar(45)|Datos Personales Cliente
País|Campo para registro del país del tarjetahabiente|Si|varchar(50)|Datos Personales Cliente
idPedido|Campo para que el establecimiento pueda ligar la transacción con algún identificador de su producto o servicio. Es importante que sea único este identificador. Nota: sin espacios|No|varchar(60) alfanumérico|Establecimiento
param1|Variable adicional de uso especificado por el comercio|No|varchar(60) alfanumérico sin espacios|Datos Establecimiento
param2|Variable adicional de uso especificado por el comercio|No|varchar(60) alfanumérico sin espacios|Datos Establecimiento
param3|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
param4|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
param5|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
httpUserAgent|Identificador de Browser|No|varchar(150)|Datos Establecimiento
ip|Ip del servidor el cual envía la petición|No|varchar(16)|Datos Establecimiento

*El monto se debe especificar en Pesos Mexicanos (MXP), la conversión de divisas queda del lado del cliente

## Parámetros opcionales
### Redirección de respuesta para WebForm
Variable| Descripción | Requerido | Longitud | Categoría
--------|--------|--------|--------|--------
redireccion|Si queremos que nos redireccione la respuesta a nuestro portal, para saber los datos de la transacción necesitamos agregar esta variable al formulario con el valor de "1".|No|int(1)|Configuración Motor
urlResponse|Necesitamos indicar la URL a donde se redireccionara la respuesta, los datos se pasaran mediante GET en formato StringQuery. Ejemplo: “http://www.mipagina.com/resp uesta.php|No|varchar(150)|Configuración Motor

### Notificaciones de correo
Variable| Descripción | Requerido | Longitud | Categoría
--------|--------|--------|--------|--------
noMail|El motor por default envía una notificación via correo electrónico al comprador, en caso de que desees tu enviar el correo para evitar la doble notificación, basta con agregar este campo con valor de “1” para idicarle al motor que no envie notificación por parte de PagoFácil|No|int(1)|Configuración Motor

### Cambio divisa
Variable| Descripción | Requerido | Longitud | Categoría
--------|--------|--------|--------|--------
divisa| variable para indicar que le monto que se envía es en dólares y que el motor tiene realizar la coversión*|No|constante(3)USD|Configuración Motor
*Por el momento solo se contemplan Dolares y el valor de la constante es ‘USD’, el factor de cambio

## Respuesta
Variable| Descripción | Requerido | Longitud | Categoría
--------|--------|--------|--------|--------
autorizado|Este campo nos indicara si la transacción fue exitosa(1) o declinada (0)|Si|bool(1)|Request PagoFácil
autorizacion|Contendra el no de autorización del banco|No|Int|Request PagoFácil
transaccion|Identificador de PagoFácil para la transacción realizada|No|varchar(50)|Request PagoFácil
Texto|Describe si una tranasaccion tuvo un error o fue exitosa|No|varchar(100)|Request PagoFácil
Error|Es un elemento array en donde en caso de error mandara los mensajes con el formato ‘campo’=>’error’|No|Array|Request PagoFácil
Mode|Nos indica si la transacción se realizo en el entorno de prueba (R) o producción (P)|No|Varchar(1)|Request PagoFácil
TransIni|Indica la hora en que la transaccion se llevo acabo|No|DateTime(22)|Request PagoFácil
TransFin|Indica la hora en que la transacción termino|No|DateTime(22)|Request PagoFácil
param1|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
param2|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
param3|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
param4|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
param5|Variable adicional de uso especificado por el comercio|No|varchar(60)|Datos Establecimiento
TipoTC|Indica el tipo de tarjeta con el que se esta realizando la transacción|No|varchar(30)|Request PagoFácil
Data|En este arreglo de datos vendrán los datos que se enviaron originalmente|si|Array|Request PagoFácil

## Usando webform
Copiar y pegar el siguiente código HTML en tu página

`
<form target="_blank" name="formularioPago" method="post" action="https://stcore.pagofacil.net/Payform">
  <input type="hidden" value="ba3b2748672431ebeebeed1327c14959a94a74be" name="idSucursal">
  <input type="hidden" value="ce4287a4093e4fca1928f2cde9bf041ee7de8292" name="idUsuario">
  <input type="hidden" value="1" name="idServicio">
  <input type="hidden" value="1372109726" name="idPedido">
  <input type="hidden" value="36" name="monto">
  <input class="" name="submit" type="submit" value="compra">
</form>
`

Ó partiremos del siguiente formulario de ejemplo con el cual podremos enviar los datos:

`
<h1>Probando el WS de transacciones Third Party</h1>
<form id="transaccion" name="transaccion" enctype="application/x-www-form-urlencoded" action="" method="post">
  <label for="nombre" class="required">Nombre Titular:</label>
  <input type="text" name="nombre" id="nombre" >
  <label for="apellidos" class="required">Apellidos titular:</label>
  <input type="text" name="apellidos" id="apellidos" >
  <label for="numeroTarjeta" class="required">Numero Tarjeta:</label>
  <input type="text" name="numeroTarjeta" id="numeroTarjeta" >
  <label for="cp" class="required">CP:</label>
  <input type="text" name="cp" id="cp" >
  <label for="cvt" class="required">CVT: (Código de seguridad de  la tarjeta)</label>
  <input type="text" name="cvt" id="cvt" >
  <label for="monto" class="required">Monto:</label>
  <input type="text" name="monto" id="monto" >
  <label for="mesExpiracion" class="required">MesExpiracion:</label>
  <input type="text" name="mesExpiracion" id="mesExpiracion" >
  <label for="anyoExpiracion" class="required">AnyoExpiracion:</label>
  <input type="text" name="anyoExpiracion" id="anyoExpiracion" >
  <label for="idSucursal" class="required">idSucursal:</label>
  <input type="text" name="idSucursal" id="idSucursal" value="1">
  <label for="idServicio" class="required">idServicio:</label>
  <input type="text" name="idServicio" id="idServicio" value="3">
  <label for="idUsuario" class="required">idUsuario:</label>
  <input type="text" name="idUsuario" id="idUsuario" value="1">
  <label for="email" class="optional">email:</label>
  <input type="text" name="email" id="email" >
  <label for="telefono" class="required">Telefono (10 dígitos):</label>
  <input type="text" name="telefono" id="telefono" >
  <label for="celular" class="required">Celular (10 dígitos):</label>
  <input type="text" name="celular" id="celular" >
  <label for="calleyNumero" class="required">calleyNumero:</label>
  <input type="text" name="calleyNumero" id="calleyNumero" >
  <label for="colonia" class="required">colonia:</label>
  <input type="text" name="colonia" id="colonia" >
  <label for="municipio" class="required">municipio:</label>
  <input type="text" name="municipio" id="municipio" >
  <label for="estado" class="required">estado:</label>
  <input type="text" name="estado" id="estado" >
  <label for="pais" class="required">pais:</label>
  <input type="text" name="pais" id="pais" >
  <label for="param1" class="optional">param1:</label>
  <input type="text" name="param1" id="param1" >
  <label for="param2" class="optional">param2:</label>
  <input type="text" name="param2" id="param2" >
  <label for="param3" class="optional">param3:</label>
  <input type="text" name="param3" id="param3" >
  <label for="param4" class="optional">param4:</label>
  <input type="text" name="param4" id="param4" >
  <label for="param5" class="optional">param5:</label>
  <input type="text" name="param5" id="param5" >
  <input type="submit" name="submit" id="submitbutton"
  value="submit">
</form>
`

Una vez llenado el formulario con los datos del comprador o dueño de la tarjeta de crédito, envíamos la información para generar la siguiente estructura:

`
[nombre]         => Juan
[apellidos]      => López Hernández
[numeroTarjeta]  => 557956789123456
[cvt]            => 123
[cp]             => 11560
[mesExpiracion]  => 10
[anyoExpiracion] => 15
[monto]          => 100
[idSucursal]     => (Proporcionados por Ejecutivo)
[idUsuario]      => (Proporcionados por Ejecutivo)
[idServicio]     => 3 ([WebForm = 1, ThirdParty = 3])
[email]          => comprador@correo.com
[telefono]       => 5550220910
[celular]        => 5550123456
[calleyNumero]   => Anatole France 311
[colonia]        => Polanco
[municipio]      => Miguel Hidalgo
[estado]         => Distrito Federal
[pais]           => Mexico
[param1]         => (En caso de que se necesiten pasar valores)
[param2]         => (En caso de que se necesiten pasar valores)
[param3]         => (En caso de que se necesiten pasar valores)
[param4]         => (En caso de que se necesiten pasar valores)
[param5]         => (En caso de que se necesiten pasar valores)
`

Estructura de la respuesta exitosa:

`
[autorizado] => 1
[autorizacion] => 346878
[transaccion] => T-PFE1S1I573
[texto] => Transaction has been successful!- Approved
[mode] => R
[TransIni] => 15:34:06 pm  14/11/2012  
[TransFin] => 15:34:07 pm 14/11/2012
[param1] =>
[param2]  =>
[param3]  =>
[param4]  =>
[param5]  =>
[TipoTC] =>
[data] => Array
  (
  [nombre] => Juan
  [apellidos] => López Hernández
  [numeroTarjeta] => 5579********3456
  [cvt] => 123
  [cp] => 11560
  [mesExpiracion] => 10
  [anyoExpiracion] => 15
  [monto] => 100
  [idSucursal] => (Proporcionados por Ejecutivo)
  [idUsuario] => (Proporcionados por Ejecutivo)
  [idServicio] => 3 ([WebForm = 1, ThirdParty = 3])
  [email] => comprador@correo.com
  [telefono] => 5550220910
  [celular] => 5550123456
  [calleyNumero] => Anatole France 311
  [colonia] => Polanco
  [municipio] => Miguel Hidalgo
  [estado] => Distrito Federal
  [pais] => Mexico
  [param1] =>
  [param2] =>
  [param3] =>
  [param4] =>
  [param5] =>
  )
`

En caso de que la transacción fuera incorrecta nos generaría el siguiente código.

`
[autorizado] => 0
[transaccion] => n/a
[autorizacion] => n/a
[texto] => Errores en los datos de entrada Validacions Transaccion
[error] => Array (
    [idSucursal] => Falta el campo: 'idSucursal'
    [monto] => Falta el campo: 'monto'
    [idUsuario] => idUsuario 0 no encontrado
)
[TransIni] => 17:01:05 pm 14/11/2012
[TransFin]  =>  17:01:06 pm 14/11/2012
[param1] => 1
[param2] => 2
[param3] => 3
[param4] =>
[param5] =>
[TipoTC] =>
[data] => Array
  (
  [nombre] => Juan
  [apellidos] => López Hernández
  [numeroTarjeta] => 5579567890123456
  [cvt] => 123
  [cp] => 11560
  [mesExpiracion] => 10
  [anyoExpiracion] => 15
  [monto] =>
  [idSucursal] =>
  [idUsuario] =>
  [idServicio] => 3 ([WebForm = 1, ThirdParty = 3])
  [email] => comprador@correo.com
  [telefono] => 5550220910
  [celular] => 5550123456
  [calleyNumero] => Anatole France 311
  [colonia] => Polanco
  [municipio] => Miguel Hidalgo
  [estado] => Distrito Federal
  [pais] => Mexico
  [param1] =>
  [param2] =>
  [param3] =>
  [param4] =>
  [param5] =>
  )
`

## Ejemplos de consumo de Web Service
### Rest (XML)
`
https://stcore.pagofacil.net/Wsrtransaccion/?method=transaccion&data[nombre]=Juan&data[apellidos]=Lopez&data[numeroTarjeta]=5579567890123456&data[cvt]=123&data[cp]=11560&data[mesExpiracion]=10&data[anyoExpiracion]=15&data[monto]=100&data[idSucursal]=1&data[idUsuario]=1&data[idServicio]=3&data[email]=comprador@correo.com&data[telefono]=5550220910&data[celular]=5550123456&data[calleyNumero]=Anatole France 311&data[colonia]=Polanco&data[municipio]=Miguel Hidalgo&data[estado]=Distrito Federal&data[pais]=Mexico&data[param1]=&data[param2]=&data[param3]=&data[param4]=&data[param5]=
`

### Rest (JSON)
`
https://stcore.pagofacil.net/Wsrtransaccion/index/format/json?method=transaccion&data[nombre]=Juan&data[apellidos]=Lopez&data[numeroTarjeta]=5579567890123456&data[cvt]=123&data[cp]=11560&data[mesExpiracion]=10&data[anyoExpiracion]=15&data[monto]=100&data[idSucursal]=1&data[idUsuario]=1&data[idServicio]=3&data[email]=comprador@correo.com&data[telefono]=5550220910&data[celular]=5550123456&data[calleyNumero]=Anatole France 311&data[colonia]=Polanco&data[municipio]=Miguel Hidalgo&data[estado]=Distrito Federal&data[pais]=Mexico&data[param1]=&data[param2]=&data[param3]=&data[param4]=&data[param5]=
`

# Cargos Recurrentes
## Ambientes

- Desarrollo:

`
(soap)= https://stcore.pagofacil.net/Wssrecurrentes/
(soap wsdl) = https://stcore.pagofacil.net/Wssrecurrentes/?wsdl
(rest xml) = https://stcore.pagofacil.net/Wsrrecurrentes/
(rest json) = https://stcore.pagofacil.net/Wsrrecurrentes/index/format/json?
(json) = https://stcore.pagofacil.net/Wsjrecurrentes/
`

- Producción:

`
(soap) = https://www.pagofacil.net/ws/public/Wssrecurrentes/
(soap wsdl) = https://www.pagofacil.net/ws/public/Wssrecurrentes/?wsdl
(rest xml) = https://www.pagofacil.net/ws/public/Wsrrecurrentes/
(rest json) = https://www.pagofacil.net/ws/public/Wsrrecurrentes/index/format/json?
(json) = https://www.pagofacil.net/ws/public/Wsjrecurrentes/
`

## Métodos
- transaccion
- vercargo

Los cargos recurrentes se manejarán de la misma forma que las transacciones normales, los campos que se enviarán son los siguientes:

## Parámetros
### Crear Transacción
Parámetro | Tipo | Requerido | Descripción | Categoría
--------- | ------- | -----------| -----------| -----------
Nombre| En este campo vendrá el nombre del tarjetahabiente | varchar(50) | Sí |Tarjeta de Crédito
Apellidos|En este campo vendrán los apellidos del tarjetahabiente|varchar(50)|Si|Tarjeta de Crédito
numeroTarjeta|Numero del plástico de la tarjeta de crédito sin guiones o espacios|Si|varchar(16)|Tarjeta de Crédito
Cvt|Código de verificación de tarjeta,usualmente impreso en el área de firma de la tarjeta, utilizado para validar que la tarjeta usada en la compra pertenezca a la persona que generó la orden|Si|int(4)|Tarjeta de Crédito
Cp|Código postal de la dirección donde vive el tarjetahabiente|Sí|varchar(9)|Datos Personales Cliente
mesExpiracion|El mes en el cual el plástico expira MM|Si|int(2)|Tarjeta de Crédito
anyoExpiracion|El año en el cual el plástico expira MM|Si|int(2)|Tarjeta de Crédito
**Monto***|El monto(MXN) del cargo a la tarjeta|Si|Decimal|Establecimiento
idSucursal|En caso de contar con varias sucursales se podrá utilizar este alfanumérico identificador para distinguir las transacciones|Si|Varchar(60) alfanumérico sin espacios|Establecimiento
idUsuario|Sera el identificador de la empresa ante PagoFácil|Si|Varchar(60)|Establecimiento
idServicio|Este identificador le indica al motor de PagoFácil que servicio será el que se consumirá: 1=WebForm, 3=ThirdParty(ssl)|Si|Int|Producto PagoFácil
Email|En este campo vendrá el correo de la persona a la que se le enviara el correo con el resumen de la transacción|Si|mail (200)|Datos Personales Cliente
Teléfono|Se debe incluir el teléfono del tarjetahabiente|Si|varchar(10)|Datos Personales Cliente
Celular|Campo reservado el número de celular del tarjetahabiente|Si|varchar(10)|Datos Personales Cliente
calleyNumero|Campo para registro de la calle y numero del tarjetahabiente|Si|varchar(45)|Datos Personales Cliente
Colonia|Campo para registro de la colonia del tarjetahabiente|Si|varchar(30)|Datos Personales Cliente
municipio|Campo para registro del municipio del tarjetahabiente|Si|varchar(30)|Datos Personales Cliente
Estado|Campo para registro del estado del tarjetahabiente|Si|varchar(45)|Datos Personales Cliente
País|Campo para registro del país del tarjetahabiente|Si|varchar(50)|Datos Personales Cliente
idCliente|Identificador del contrato donde se autoriza el cargo recurrente por parte del dueño de la tarjeta|No|varchar(10) alfanumérico|Establecimiento
diaPago|Día en el que se estarán realizando los cobros|No|Int(2)|Datos Establecimiento
fechaIniCobro|Fecha a partir de la cual se empezará a cobrar|Sí|Fecha en formato dd-mm-yyyy|Datos Establecimiento
fechaFinCobro|Fecha en la cual expira el cobro|Sí|Fecha en formato dd-mm-yyyy|Datos Establecimiento
httpUserAgent|Identificador de Browser|No|varchar(150)|Datos Establecimiento
ip|Ip del servidor el cual envía la petición|No|varchar(16)|Datos Establecimiento
cargo|Identificador de Browser|No|varchar(150)|Datos Establecimiento
cargo|Si se va a registrar un cobro al momento del registro|No|int(1)|Datos Establecimiento

### Ver Transacción
Parámetro | Tipo | Requerido | Descripción | Categoría
--------- | ------- | -----------| -----------| -----------
idRecurrente|El identificador con el que se registró el cargo en PagoFacil|Sí|varchar(50)|Tarjeta de Crédito
idSucursal|El Apikey de la sucursal a la que le pertenece el cargo recurrente|Sí|varchar(20)|Tarjeta de Crédito

## Realizando Pruebas:
A lo largo de la implementación seguramente será necesario realizar pruebas antes de pasar a los entornos de producción, tanto del aplicativo como de PagoFácil, por lo que será bueno recordar que PagoFácil maneja dos entornos independientes, el entorno de pruebas o sandbox y el entorno de producción.
Para poder verificar las transacciones podemos utilizar el Manager que proporcionamos.
- `Producción https://manager.pagofacil.net`
- `Pruebas http://stmanager.pagofacil.net`
El usuario por default es el que se capturó en el formulario al momento de registrarse en PagoFácil.

# Pagos en efectivo
## Introducción

Nuestra API proporciona 3 métodos para implementar el proceso de pagos en efectivo en tu sitio web.
Éstos se mencionan a continuación:

### Tiendas de conveniencia

Establecimiento | Código | Monto máximo
--------- | ------- | -----------
OXXO | OXXO | 15,000.00 MXN
Seven eleven | SEVEN_ELEVEN | 15,000.00 MXN
Extra | EXTRA | 5,000.00 MXN
Chedraui | CHEDRAUI | 5,000.00 MXN
Farmacia Benavides | FARMACIA_BENAVIDES | 5,000.00 MXN
Farmacia Esquivar | FARMACIA_ESQUIVAR | 5,000.00 MXN

## Realizar una orden/cargo

```php
<?php
$host = 'https://stapi.pagofacil.net/cash/charge';
$params = array(
'branch_key' => 'ba3b2748672431ebeebeed1327c14959a94a74be',
'user_key' => 'ce4287a4093e4fca192
8f2cde9bf041ee7de8292',
'order_id' => 'tienda_pedro_001',
'product' => 'camara fotografica de 15 mega pixeles',
'amount' => '6500.99',
'store_code' => 'OXXO',
'customer' => 'pedro perez',
'email' => 'pedro@pagofacil.net',
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $host);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_POST, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($params));
$result = curl_exec($ch);
curl_close($ch);
$data = json_decode($result, true);
?>
```

```ruby
require "net/http"
require "uri"
uri = URI.parse("https://stapi.pagofacil.net/cash/charge")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE
request = Net::HTTP::Post.new(uri.request_uri)
request.set_form_data({
"branch_key" => "ba3b2748672431ebeebeed1327c14959a94a74be",
"user_key" => "ce4287a4093e4fca1928f2cde9bf041ee7de8292",
"order_id" => "tienda_pedro_001",
"product" => "camara fotografica de 15 mega pixeles",
"amount" => "6500.99",
"store_code" => "OXXO",
"customer" => "pedro perez",
"email" => "pedro@pagofacil.net"
})
response = http.request(request)
puts response.body
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Net;
using System.IO;
namespace ConsoleApplication1
{
  class Program
  {
    static void Main(string[] args)
    {
     WebRequest request = WebRequest.Create(
         "https://stapi.pagofacil.net/cash/charge"
     );
      string param =
      "branch_key=ba3b2748672431ebeebeed1327c14959a94a74be" +
      "&user_key=ce4287a4093e4fca1928f2cde9bf041ee7de8292" +
      "&order_id=tienda_pedro_001" +
      "&product=camara fotografica de 15 mega pixeles" +
      "&amount=6500.99" +
      "&store_code=OXXO" +
      "&customer=pedro perez" +
      "&email=pedro@pagofacil.net";
      request.Method = "POST";
      request.ContentType = "application/x-­­www-form-urlencoded";
      request.ContentLength = param.Length;
      byte[] paramsList = Encoding.UTF8.GetBytes(param);
      Stream writer = request.GetRequestStream();
      writer.Write(paramsList, 0, paramsList.Length);
      writer.Close();
      WebResponse response = request.GetResponse();
      string result = (new StreamReader(response.GetResponseStream())).ReadToEnd();
      Console.WriteLine(result);
      response.Close();
      }
    }
}
```
### HTTP Request

* Producción:
`POST https://www.pagofacil.net/ws/public/cash/charge`
* Stage:
`POST https://stapi.pagofacil.net/cash/charge`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
branch_key | String(100) | Api key sucursal
user_key | String(100) | Api key usuario
order_id | String(45) | Tú identificador para la orden de compra. NOTA: debe ser único e irrepetible para cada orden
product | String(100) | Descripción del producto o nombre del producto
amount | Double(8,2) | Monto (MXN) a pagar
store_code | String(30) | Código de la tienda de conveniencia
customer | String(100) | Nombre del comprador
email | String(100) | E-mail del comprador

## Consultar una orden/cargo

```php
<?php
$host = 'https://stapi.pagofacil.net/cash/charge';
$params = array(
'branch_key' => 'ba3b2748672431ebeebeed1327c14959a94a74be',
'user_key' => 'ce4287a4093e4fca192
8f2cde9bf041ee7de8292',
'reference' => 'reference001'
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $host);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPGET, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($params));
$result = curl_exec($ch);
curl_close($ch);
$charge = json_decode($result, true);
?>
```

```ruby
require "net/http"
require "uri"
uri = URI.parse("https://stapi.pagofacil.net/cash/charge")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE
request = Net::HTTP::Get.new(uri.request_uri)
request.set_form_data({
"branch_key" => "ba3b2748672431ebeebeed1327c14959a94a74be",
"user_key" => "ce4287a4093e4fca1928f2cde9bf041ee7de8292",
"reference" => "reference001",
})
response = http.request(request)
puts response.body
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Net;
using System.IO;
namespace ConsoleApplication1
{
  class Program
  {
    static void Main(string[] args)
    {
     WebRequest request = WebRequest.Create(
         "https://stapi.pagofacil.net/cash/charge"
     );
      string param =
      "branch_key=ba3b2748672431ebeebeed1327c14959a94a74be" +
      "&user_key=ce4287a4093e4fca1928f2cde9bf041ee7de8292" +
      "&reference=reference001" +
      request.Method = "GET";
      request.ContentType = "application/x-­­www-form-urlencoded";
      request.ContentLength = param.Length;
      byte[] paramsList = Encoding.UTF8.GetBytes(param);
      Stream writer = request.GetRequestStream();
      writer.Write(paramsList, 0, paramsList.Length);
      writer.Close();
      WebResponse response = request.GetResponse();
      string result = (new StreamReader(response.GetResponseStream())).ReadToEnd();
      Console.WriteLine(result);
      response.Close();
      }
    }
}
```
### HTTP Request

* Producción:
`GET https://www.pagofacil.net/ws/public/cash/charge`
* Stage:
`GET https://stapi.pagofacil.net/cash/charge`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
branch_key | String(100) | Api key sucursal
user_key | String(100) | Api key usuario
reference | String(45) | dentificador enviado por PagoFácil al realizar una orden/cargo

## Reporte de órdenes /cargos

```php
<?php
$host = 'https://stapi.pagofacil.net/cash/charges';
$params = array(
'branch_key' => 'ba3b2748672431ebeebeed1327c14959a94a74be',
'user_key' => 'ce4287a4093e4fca1928f2cde9bf041ee7de8292',
'secret_key' => 's3cr3tK3y',
'date_start' => '2017-01-01 12:00:00',
'date_end' => '2017-01-01 12:00:00',
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL, $host);
curl_setopt($ch, CURLOPT_SSL_VERIFYPEER, false);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
curl_setopt($ch, CURLOPT_HTTPGET, true);
curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($params));
$result = curl_exec($ch);
curl_close($ch);
$charge = json_decode($result, true);
?>
```

```ruby
require "net/http"
require "uri"
uri = URI.parse("https://stapi.pagofacil.net/cash/charges")
http = Net::HTTP.new(uri.host, uri.port)
http.use_ssl = true
http.verify_mode = OpenSSL::SSL::VERIFY_NONE
request = Net::HTTP::Get.new(uri.request_uri)
request.set_form_data({
"branch_key" => "ba3b2748672431ebeebeed1327c14959a94a74be",
"user_key" => "ce4287a4093e4fca1928f2cde9bf041ee7de8292",
"secret_key" => "s3cr3tK3y",
"date_start" => "2017-01-01 12:00:00",
"date_end" => "2017-01-01 12:00:00",
})
response = http.request(request)
puts response.body
```

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Net;
using System.IO;
namespace ConsoleApplication1
{
  class Program
  {
    static void Main(string[] args)
    {
     WebRequest request = WebRequest.Create(
         "https://stapi.pagofacil.net/cash/charges"
     );
      string param =
      "branch_key=ba3b2748672431ebeebeed1327c14959a94a74be" +
      "&user_key=ce4287a4093e4fca1928f2cde9bf041ee7de8292" +
      "&reference=reference001" +
      "&secret_key=s3cr3tK3y" +
      "&date_start=2017-01-01 12:00:00" +
      "&date_end=2017-01-01 12:00:00";
      request.Method = "GET";
      request.ContentType = "application/x-­­www-form-urlencoded";
      request.ContentLength = param.Length;
      byte[] paramsList = Encoding.UTF8.GetBytes(param);
      Stream writer = request.GetRequestStream();
      writer.Write(paramsList, 0, paramsList.Length);
      writer.Close();
      WebResponse response = request.GetResponse();
      string result = (new StreamReader(response.GetResponseStream())).ReadToEnd();
      Console.WriteLine(result);
      response.Close();
      }
    }
}
```
### HTTP Request

* Producción:
`GET|POST https://www.pagofacil.net/ws/public/cash/charges`
* Stage:
`GET|POST https://stapi.pagofacil.net/cash/charges`

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
branch_key | String(100) | Api key sucursal
user_key | String(100) | Api key usuario
secret_key | String(64) | Clave privada. **NOTA**: debe solicitarla a soporte@pagofacil.net
date_start | String(19) | Fecha inicial del reporte, formato AAAA-MM-­DD HH:MM:SS
date_end | String(19) | Fecha inicial del reporte, formato AAAA-MM-­DD HH:MM:SS

# Cobro vía token

Al hacer uso del webservice para realizar la integración de cobros vía token, se solicita que el envió de los parámetros sea en un formato JSON con la información requerida dependiendo de la operación que se busca ejecutar.

La información se solicita que se envié de manera encriptada bajo el algoritmo de **AES 128** el cual contendrá los datos a procesar.
La llave de cifrado se solicitará a **soporte@pagofacil.net** indicando el tema de “Llave de encriptación” indicando el nombre con el que se dio de alta en PagoFácil.

Una vez que se tenga la llave de cifrado, se procederá a formar la petición en base a los parámetros de la operación que se desea ejecutar.
Ejemplo:
```
{
  idSucursal":"e147ee31531d815e2307g8o953k929ab599deb98",
  "idUsuario":"f541b3f11f0f9b3fuhiolikof22f6d711f2af58",
  "nombre":"Cliente",
  "apellidos":"apellido cliente",
  "calleyNumero":"Anatole France 311",
  "colonia":"Polanco",
  "municipio":"Milpa Alta",
  "estado":"CDMX",
  "cp":"11000",
  "telefono":"6789543210",
  "celular":"5565434504",
  "email":"comprador@mail.com",
  "numeroTarjeta":"4111111111111111",
  "cvt":"314",
  "mesExpiracion":"12",
  "anyoExpiracion":"21"
}
```
Esta cadena se procederá a encriptar bajo el algoritmo mencionado anteriormente y se procederá a enviarla por POST a los EndPoint indicados dependiendo de la operación.

Por cada operación se mandarán 2 campos vía POST:
- idUsuario: Se obtiene el en manager de PagoFácil.
- data : contenido de los parámetros cifrados (este varia por cada operación).

## Alta de un token:
Se utiliza para dar de alta una tarjeta bancaria por primera vez, esta devolverá los parámetros correspondientes para proceder a realizar un pago con esta mista tarjeta.

### HTTP Request

* Producción:
`POST https://www.pagofacil.net/ws/public/CobroToken/Altatoken`
* Stage:
`POST https://www.pagofacil.net/st/public/CobroToken/Altatoken`

### Parámetros
Campo|Tipo|Descripción|Requerido
--------- | ------- | ----------- | -----------
nombre|varchar (60)|Nombre del titular de la tarjeta|Si
apellidos|varchar (60)|Apellidos del titular de la tarjeta|Si
calleyNumero|varchar (45)|Dirección del titular de la tarjeta|Si
colonia|varchar(30)|Colonia del titular de la tarjeta|Si
municipio|varchar (30)|Ciudad del titular de la tarjeta|Si
estado|varchar (45)|Estado del titular de la tarjeta|Si
cp|varchar (9)|Código Postal del titular de la tarjeta|Si
telefono|varchar(10)|Teléfono del titular de la tarjeta|Si
celular|varchar(10)|Numero de celular del titular de la tarjeta|Si
email|mail (200)|Email del titular de la tarjeta|Si
numeroTarjeta|varchar (16)|Número de cuenta|Si
cvt|int(4)|Código de verificación de tarjeta, usualmente impreso en el área de firma de la tarjeta, utilizado para validar que la tarjeta usada pertenezca a la persona que genero la compra|Si
mesExpiracion|int (2)|Mes de expiración de tarjeta|Si
anyoExpiracion|int (2)|Año de expiración de tarjeta|Si
idSucursal|Varchar(60) alfanumérico|En caso de contar con varias sucursales se podrá utilizar este identificador para distinguir las transacciones|Si
IdUsuario|Varchar(60) alfanumérico|Sera el identificador de la empresa ante PagoFácil|Si

### Respuesta
Campo|Tipo|Descripción|Requerido
--------- | ------- | ----------- | -----------
token|String (26)|Referencia o número de seguimiento generada por PagoFacil|Si
autorizado|bool(1)|Este campo nos indicara si la transacción fue exitosa (1) o declinada (0)|Si
autorizacion|Int|No de Autorización de la bóveda. **NOTA**: Este campo sera requerido para solicitar la baja de Token.|Si
texto|String(100)|Describe si una transacción tuvo un error o fue exitosa. *Token generado/Error en generación de Token* |Si
error|Array|Array el cual en caso de error contiene los mensajes con el formato ‘campo’=>’error’|No
data|Array|Array que contiene los datos que se enviaron originalmente|Si

## Baja de un token:
Dar de baja un token al cual ya no se le vayan a realizar cargos.

### HTTP Request

* Producción:
`POST https://www.pagofacil.net/ws/public/CobroToken/Bajatoken`
* Stage:
`POST https://www.pagofacil.net/st/public/CobroToken/Bajatoken`

### Parámetros

Campo|Tipo|Descripción|Requerido
--------- | ------- | ----------- | -----------
token|Varchar (26)|Referencia o número de seguimiento generada por Pago Fácil|Si
autorizacion|Varchar (26)|Dato generado y retornado al cliente (autorización) cuando se dio de alta el Token|Si
idSucursal|Varchar(60)|Credenciales API|Si
idUsuario|Varchar(60)|Credenciales API|Si

### Respuesta
Campo|Tipo|Descripción|Requerido
--------- | ------- | ----------- | -----------
token|String (26)|Token Eliminado|Si
autorizado|bool(1)|Este campo nos indicara si la transacción fue exitosa (1) o declinada (0)|Si
autorizacion|Int|Número requerido para dar de baja un token.|Si
texto|String(100)|Describe si una transacción tuvo un error o fue exitosa:|Token generado eliminado/Error en eliminación de Token|Si
error|Array|Array el cual en caso de error contiene los mensajes con el formato ‘campo’=>’error’|No
data|Array|Array que contiene los datos que se enviaron originalmente|Si

## Realizar cobro a la tarjeta bancaria.

Realizar un cobro a una tarjeta bancaria.

### HTTP Request

* Producción: `POST https://www.pagofacil.net/ws/public/CobroToken/Transacciontoken`
* Stage:
`POST https://www.pagofacil.net/st/public/CobroToken/Transacciontoken`

### Parámetros

Campo|Tipo|Descripción|Requerido
--------- | ------- | ----------- | -----------
idSucursal|varchar (100)|Credenciales API|Si
idUsuario|varchar (100)|Credenciales API|Si
token|varchar (26)|Dato proporcionado al cliente al Tokenizar Tarjeta|Si
monto|Decimal|El monto (MXP) del cargo a la tarjeta|Si
idPedido|varchar(60)|Campo para que el establecimiento pueda ligar la transacción con algún identificador de su producto o servicio. Nota: es importante que sea único este identificador|No
param1|varchar(60)|Variable adicional de uso especificado por el comercio|No
param2|varchar(60)|Variable adicional de uso especificado por el comercio|No
param3|varchar(60)|Variable adicional de uso especificado por el comercio|No
param4|varchar(60)|Variable adicional de uso especificado por el comercio|No
param5|varchar(60)|Variable adicional de uso especificado por el comercio|No

### Respuesta

Campo|Tipo|Descripción|Requerido
--------- | ------- | ----------- | -----------
Token|String (26)|Token de la tarjeta del cliente|Si
autorizado|Bool (1)|Este campo nos indicara si la transacción fue exitosa (1) o declinada (0)|Si
Transaccion|String(50)|Identificador de PagoFácil para la transacción realizada|No
texto|String(100)|Describe si una transacción tuvo un error o fue exitosa|No
error|array|Array el cual en caso de error contiene los mensajes con el formato ‘campo’=>’error’|No
mode|Nvarchar (1)|Indica si la transacción se realizó en el entorno de prueba (R) o producción (P)|No
transIni|DateTime(22)|Hora en la que la transacción inicio|No
transFin|DateTime(22)|Hora en la que la transacción finalizo|No
data|Array|Array que contiene los datos que se enviaron originalmente|Si

# Tarjeta Presente
Para la interacción de Pago Fácil con sistemas externos se brindan herramientas por medio de servicios web de tipo REST para que una empresa pueda utilizar los productos de tarjeta presente interactuando con los sistemas de su empresa.

## Proceso de la interacción con Pago Móvil
- Los dispositivos de Pago Fácil realizan el proceso de cobro de las tarjetas bancarias.
- Los servidores de Pago Fácil reciben la información y realizan el proceso de autorización del cobro con la banca.
- Pago fácil recibe la información sobre la transacción sobre la transacción y la registra en los sistemas internos.
- Devuelve el resultado sobre la transacción bancaria. Si esta fue autorizada o denegada.
- Pago Fácil envía la información de la transacción al comercio para que la registre en sus sistemas internos, esto se realiza en tiempo real por medio de un webhook cada vez que se realiza una transacción en los dispositivos de Pago Fácil.

Campo|Tipo|Requerido|Descripción|
--------- | ------- | ----------- | -----------
IdPedido|Texto(12)|Sí|Identificador único de la operación
usuario|Texto(8)|Sí|Usuario del dispositivo móvil
nbReferencia|Texto(40)|Sí|Referencia única del Comercio para conciliar un cargo con su aplicación, se sugiere ID de cliente, factura, pedido, etc.
nombreTarjetahabiente|Texto(40)|Sí|Nombre completo del tarjeta habiente.
numeroTarjeta|Texto(16)|Sí|Muestra el los datos de la tarjeta bancaria que realiza la transacción. Enmascara los números intermedios
marca|Texto(10)|Sí|Marca de la tarjeta del tarjeta habiente (MasterCard, Visa o AMEX)
Monto|Texto|Sí|Importe de la transacción. El importe se regresa sin comas (en caso de miles), con punto y 2 decimales. Ejemplo: 12345.45
plan|Texto(2)|Sí|Tipo de Cobro (Contado o Meses sin Intereses: 00, 03, 06, 09, 12)
TipoTC|Texto(7)|Sí|Tipo de tarjeta. (DEBITO O CREDITO)
autorizado|Texto(1)|Sí|Respuesta proporcionada por centro de pagos. 1 : Autorizado, 2: Denegado
autorizacion|Texto(8)|Sí|Número de autorización de la solicitud de cobro.
trans_fin|Texto(19)|Sí|Fecha en la que se registró la operación consultada
tipoOperacion|Texto(11)|Sí|Tipo de la operación que se realizo  (Venta, Cancelación, etc.)
numerSerieDispositivo|Texto(40)|Sí|# de serie o ID del dispositivo
mesExpiracion|Texto(2)|Sí|Mes de expiración de la TDC
anyoExpiracion|Texto(2)|Sí|Año de expiración de la TDC
nb_version|Texto(50)|Sí|Tipo de dispositivo por el cual se realizo la transacción
Propina|Texto(40)|No|Propina de la transacción. Solo se enviá si la transacción se realiza bajo una cuenta de restaurante. El importe se regresa sin comas (en caso de miles), con punto y 2 decimales. Ejemplo: 12345.45
IdSucursal|Texto(40)|Sí|Llave de la sucursal de PagoFácil. Estas se encuentran en el Manager de PagoFácil
idUsuario|Texto(40)|Sí|Llave de la sucursal de PagoFácil. Estas se encuentran en el Manager de PagoFáci
