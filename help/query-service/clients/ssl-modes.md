---
keywords: Experience Platform;inicio;temas populares;servicio de consulta;servicio de consulta;conexión;conexión al servicio de consulta;SSL;ssl;sslmode;
title: Opciones SSL del servicio de consulta
description: Obtenga información sobre la compatibilidad con SSL para conexiones de terceros con el servicio de consulta de Adobe Experience Platform y cómo conectar con el modo SSL verificado-completo.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: 75e97efcb68439f1b837af93b62c96f43e5d7a31
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 1%

---

# [!DNL Query Service] Opciones SSL

Para mayor seguridad, Adobe Experience Platform [!DNL Query Service] proporciona compatibilidad nativa con conexiones SSL para cifrar comunicaciones cliente/servidor. Este documento cubre las opciones SSL disponibles para conexiones de cliente de terceros con [!DNL Query Service] y cómo conectar usando la variable `verify-full` Valor del parámetro SSL.

## Requisitos previos

Este documento supone que ya ha descargado una aplicación de cliente de escritorio de terceros para usarla con los datos de Platform. Encontrará instrucciones específicas sobre cómo incorporar la seguridad SSL al conectarse con un cliente de terceros en su respectiva documentación de guía de conexión. Para una lista de todos [!DNL Query Service] clientes compatibles, consulte la [información general sobre conexiones de cliente](./overview.md).

## Opciones de SSL disponibles {#available-ssl-options}

Platform admite varias opciones SSL para adaptarse a sus necesidades de seguridad de datos y equilibrar la sobrecarga de procesamiento del cifrado y el intercambio de claves.

Los diferentes `sslmode` los valores de parámetro proporcionan diferentes niveles de protección. Al cifrar los datos en movimiento con certificados SSL, ayuda a evitar ataques, escuchas y suplantación de &quot;man-in-the-middle&quot; (MITM). La siguiente tabla proporciona un desglose de los diferentes modos SSL disponibles y el nivel de protección que proporcionan.

>[!NOTE]
>
> El valor SSL `disable` no es compatible con Adobe Experience Platform debido al cumplimiento de los requisitos de protección de datos.

| sslmode | Protección contra borrado | Protección MITM | Descripción |
|---|---|---|---|
| `allow` | Parcial | No | La seguridad no es una prioridad, la velocidad y una sobrecarga de procesamiento baja son más importantes. Este modo solo opta por el cifrado si el servidor insiste en él. |
| `prefer` | Parcial | No | No se requiere cifrado, pero la comunicación se cifrará si el servidor la admite. |
| `require` | Sí | No | Se requiere cifrado en todas las comunicaciones. Se confía en que la red se conecte al servidor correcto. No es necesario validar el certificado SSL del servidor. |
| `verify-ca` | Sí | Depende de la directiva CA | Se requiere cifrado en todas las comunicaciones. La validación del servidor es necesaria antes de que se compartan los datos. Esto requiere que configure un certificado raíz en su [!DNL PostgreSQL] directorio raíz. [A continuación se proporcionan detalles](#instructions) |
| `verify-full` | Sí | Sí | Se requiere cifrado en todas las comunicaciones. La validación del servidor es necesaria antes de que se compartan los datos. Esto requiere que configure un certificado raíz en su [!DNL PostgreSQL] directorio raíz. [A continuación se proporcionan detalles](#instructions). |

>[!NOTE]
>
>La diferencia entre `verify-ca` y `verify-full` depende de la directiva de la entidad emisora de certificados raíz (CA). Si ha creado su propia entidad emisora local para emitir certificados privados para sus aplicaciones, mediante `verify-ca` a menudo proporciona suficiente protección. Si se utiliza una CA pública, `verify-ca` permite conexiones a un servidor que otra persona puede haber registrado en la CA. `verify-full` siempre debe usarse con una CA raíz pública.

Al establecer una conexión de terceros con una base de datos de Platform, se recomienda utilizar `sslmode=require` como mínimo para garantizar una conexión segura para sus datos en movimiento. La variable `verify-full` El modo SSL se recomienda para su uso en la mayoría de los entornos con distinción de seguridad.

## Configuración de un certificado raíz para la verificación del servidor {#root-certificate}

Para garantizar una conexión segura, el uso de SSL debe configurarse tanto en el cliente como en el servidor antes de realizar la conexión. Si el SSL solo está configurado en el servidor, el cliente puede enviar información confidencial, como contraseñas, antes de establecer que el servidor requiere una alta seguridad.

De forma predeterminada, [!DNL PostgreSQL] no realiza ninguna verificación del certificado del servidor. Para verificar la identidad del servidor y garantizar una conexión segura antes de que se envíen datos confidenciales (como parte del SSL) `verify-full` ), debe colocar un certificado raíz (autofirmado) en el equipo local (`root.crt`) y un certificado de hoja firmado por el certificado raíz en el servidor.

Si la variable `sslmode` se establece en `verify-full`, libpq comprobará que el servidor es de confianza comprobando la cadena de certificados hasta el certificado raíz almacenado en el cliente. Luego verifica que el nombre de host coincida con el nombre almacenado en el certificado del servidor.

Para permitir la verificación de certificados del servidor, debe colocar uno o más certificados raíz (`root.crt`) en el [!DNL PostgreSQL] en su directorio de inicio. La ruta del archivo sería similar a `~/.postgresql/root.crt`.

## Habilitar el modo SSL verificado-completo para utilizarlo con un tercero [!DNL Query Service] connection {#instructions}

Si necesita un control de seguridad más estricto que `sslmode=require`, puede seguir los pasos resaltados para conectar un cliente de terceros a [!DNL Query Service] using `verify-full` Modo SSL.

>[!NOTE]
>
>Hay muchas opciones disponibles para obtener un certificado SSL. Debido a la creciente tendencia en los certificados no fiables, DigiCert se utiliza en esta guía, ya que son un proveedor global fiable de soluciones de firma y TLS/SSL, PKI, IoT y TLS de alta seguridad.

1. Vaya a [la lista de certificados raíz de DigiCert disponibles](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Buscar &quot;[!DNL DigiCert Global Root CA]&quot; de la lista de certificados disponibles.
1. Select [!DNL **Descargar PEM**] para descargar el archivo en el equipo local.
   ![La lista de certificados raíz DigiCert disponibles con la opción Descargar PEM resaltada.](../images/clients/ssl-modes/digicert.png)
1. Cambie el nombre del archivo del certificado de seguridad a `root.crt`.
1. Copie el archivo en el [!DNL PostgreSQL] carpeta. La ruta de archivo necesaria es diferente en función del sistema operativo. Si la carpeta no existe, créela.
   - Si utiliza macOS, la ruta es `/Users/<username>/.postgresql`
   - Si utiliza Windows, la ruta es `%appdata%\postgresql`

>[!TIP]
>
>Para encontrar su `%appdata%` ubicación de archivo en un sistema operativo Windows, presione ⊞ **Win + R** y entrada `%appdata%` en el campo de búsqueda.

Después de la [!DNL DigiCert Global Root CA] El archivo CRT está disponible en su [!DNL PostgreSQL] carpeta, puede conectarse a [!DNL Query Service] usando la variable `sslmode=verify-full` o `sslmode=verify-ca` .

## Pasos siguientes

Al leer este documento, tiene una mejor comprensión de las opciones SSL disponibles para conectar un cliente de terceros a [!DNL Query Service]y también cómo habilitar la variable `verify-full` Opción SSL para cifrar los datos en movimiento.

Si aún no lo ha hecho, siga las instrucciones de [conexión de un cliente de terceros a [!DNL Query Service]](./overview.md).
