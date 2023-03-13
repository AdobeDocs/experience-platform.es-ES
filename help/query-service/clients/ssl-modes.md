---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;conectar;conectarse al servicio de consultas;SSL;ssl;slmode;
title: Opciones SSL del servicio de consultas
description: Obtenga información sobre la compatibilidad SSL con conexiones de terceros al servicio Adobe Experience Platform Query y cómo conectarse mediante el modo de verificación SSL completo.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] Opciones SSL

Para una mayor seguridad, Adobe Experience Platform [!DNL Query Service] proporciona compatibilidad nativa con conexiones SSL para cifrar las comunicaciones cliente/servidor. Este documento describe las opciones SSL disponibles para conexiones de cliente de terceros a [!DNL Query Service] y cómo conectarse mediante el `verify-full` Valor del parámetro SSL.

## Requisitos previos

Este documento supone que ya ha descargado una aplicación cliente de escritorio de terceros para utilizarla con los datos de Platform. En la documentación de la guía de conexión correspondiente encontrará instrucciones específicas sobre cómo incorporar la seguridad SSL al conectarse con un cliente de terceros. Para obtener una lista de todos [!DNL Query Service] clientes admitidos, consulte la [información general sobre conexiones de cliente](./overview.md).

## Opciones SSL disponibles {#available-ssl-options}

Platform admite varias opciones SSL para satisfacer sus necesidades de seguridad de datos y equilibrar la sobrecarga de procesamiento del cifrado y el intercambio de claves.

Las diferentes `sslmode` los valores de parámetro proporcionan diferentes niveles de protección. Al cifrar sus datos en movimiento con certificados SSL, ayuda a evitar ataques &quot;man-in-the-middle&quot; (MITM), escuchas y suplantación de identidad. La siguiente tabla proporciona un desglose de los diferentes modos SSL disponibles y el nivel de protección que proporcionan.

>[!NOTE]
>
> El valor SSL `disable` no es compatible con Adobe Experience Platform debido al cumplimiento de los requisitos de protección de datos.

| sslmode | Protección contra escuchas | Protección MITM | Descripción |
|---|---|---|---|
| `allow` | Parcial | No | La seguridad no es una prioridad, la velocidad y una baja sobrecarga de procesamiento son más importantes. Este modo solo opta por el cifrado si el servidor insiste en él. |
| `prefer` | Parcial | No | No se requiere cifrado, pero la comunicación se cifrará si el servidor la admite. |
| `require` | Sí | No | Se requiere cifrado en todas las comunicaciones. La red es de confianza para conectarse al servidor correcto. No se requiere la validación del certificado SSL del servidor. |
| `verify-ca` | Sí | Depende de la directiva de CA | Se requiere cifrado en todas las comunicaciones. Se requiere la validación del servidor antes de compartir los datos. Esto requiere que configure un certificado raíz en su [!DNL PostgreSQL] directorio principal. [A continuación se proporcionan detalles](#instructions) |
| `verify-full` | Sí | Sí | Se requiere cifrado en todas las comunicaciones. Se requiere la validación del servidor antes de compartir los datos. Esto requiere que configure un certificado raíz en su [!DNL PostgreSQL] directorio principal. [A continuación se proporcionan detalles](#instructions). |

>[!NOTE]
>
>La diferencia entre `verify-ca` y `verify-full` depende de la directiva de la entidad emisora de certificados raíz (CA). Si ha creado su propia CA local para emitir certificados privados para sus aplicaciones, utilizando `verify-ca` a menudo proporciona suficiente protección. Si utiliza una CA pública, `verify-ca` permite conexiones a un servidor que otra persona puede haber registrado con la CA. `verify-full` siempre debe utilizarse con una CA raíz pública.

Al establecer una conexión de terceros con una base de datos de Platform, se recomienda utilizar `sslmode=require` como mínimo, para garantizar una conexión segura para sus datos en movimiento. El `verify-full` Se recomienda utilizar el modo SSL en la mayoría de los entornos confidenciales.

## Configurar un certificado raíz para la verificación del servidor {#root-certificate}

Para garantizar una conexión segura, el uso de SSL debe configurarse tanto en el cliente como en el servidor antes de establecer la conexión. Si SSL solo está configurado en el servidor, el cliente puede enviar información confidencial como contraseñas antes de que se establezca que el servidor requiere una alta seguridad.

De forma predeterminada, [!DNL PostgreSQL] no realiza ninguna verificación del certificado de servidor. Para verificar la identidad del servidor y garantizar una conexión segura antes de enviar datos confidenciales (como parte de SSL) `verify-full` modo ), debe colocar un certificado raíz (autofirmado) en el equipo local (`root.crt`) y un certificado hoja firmado por el certificado raíz en el servidor.

Si la variable `sslmode` El parámetro se ha establecido en `verify-full`, libpq comprobará que el servidor es fiable comprobando la cadena de certificados hasta el certificado raíz almacenado en el cliente. A continuación, comprueba que el nombre de host coincide con el nombre almacenado en el certificado del servidor.

Para permitir la verificación del certificado del servidor, debe colocar uno o más certificados raíz (`root.crt`) en el [!DNL PostgreSQL] en su directorio personal. La ruta de archivo sería similar a `~/.postgresql/root.crt`.

## Habilite el modo de SSL de verificación completa para utilizarlo con un tercero [!DNL Query Service] conexión {#instructions}

Si necesita un control de seguridad más estricto que `sslmode=require`, puede seguir los pasos resaltados para conectar un cliente de terceros a [!DNL Query Service] usando `verify-full` Modo SSL.

>[!NOTE]
>
>Hay muchas opciones disponibles para obtener un certificado SSL. Debido a una creciente tendencia en certificados no fiables, DigiCert se utiliza en esta guía ya que es un proveedor global de confianza de soluciones de alta seguridad TLS/SSL, PKI, IoT y firma.

1. Vaya a [la lista de certificados raíz DigiCert disponibles](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Buscar &quot;[!DNL DigiCert Global Root CA]&quot; de la lista de certificados disponibles.
1. Seleccionar [!DNL **Descargar PEM**] para descargar el archivo en el equipo local.
   ![La lista de certificados raíz DigiCert disponibles con Descargar PEM resaltado.](../images/clients/ssl-modes/digicert.png)
1. Cambie el nombre del archivo del certificado de seguridad a `root.crt`.
1. Copie el archivo en [!DNL PostgreSQL] carpeta. La ruta de archivo necesaria es diferente en función del sistema operativo. Si la carpeta aún no existe, créela.
   - Si utiliza macOS, la ruta es `/Users/<username>/.postgresql`
   - Si utiliza Windows, la ruta es `%appdata%\postgresql`

>[!TIP]
>
>Para encontrar su `%appdata%` ubicación del archivo en un sistema operativo Windows, presione ⊞ **Win + R** y entrada `%appdata%` en el campo de búsqueda.

Después del [!DNL DigiCert Global Root CA] El archivo CRT está disponible en su [!DNL PostgreSQL] carpeta, puede conectarse a [!DNL Query Service] uso del `sslmode=verify-full` o `sslmode=verify-ca` opción.

## Pasos siguientes

Al leer este documento, tiene una mejor comprensión de las opciones SSL disponibles para conectar un cliente de terceros a [!DNL Query Service], y también cómo habilitar el `verify-full` Opción SSL para cifrar los datos en movimiento.

Si aún no lo ha hecho, siga las instrucciones que aparecen en [conexión de un cliente de terceros a [!DNL Query Service]](./overview.md).
