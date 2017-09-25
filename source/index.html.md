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
--------- | ------- | -----------
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
