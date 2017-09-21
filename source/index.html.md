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
