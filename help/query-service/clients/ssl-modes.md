---
keywords: Experience Platform;inicio;temas populares;servicio de consultas;servicio de consultas;conectar;conectarse al servicio de consultas;SSL;ssl;slmode;
title: Opciones SSL del servicio de consultas
description: Obtenga información sobre la compatibilidad SSL con conexiones de terceros al servicio Adobe Experience Platform Query y cómo conectarse mediante el modo de verificación SSL completo.
exl-id: 41b0a71f-165e-49a2-8a7d-d809f5f683ae
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 1%

---

# [!DNL Query Service] opciones SSL

Para aumentar la seguridad, Adobe Experience Platform [!DNL Query Service] proporciona compatibilidad nativa con conexiones SSL para cifrar las comunicaciones cliente/servidor. Este documento describe las opciones SSL disponibles para las conexiones de cliente de terceros a [!DNL Query Service] y cómo conectarse mediante el valor del parámetro SSL `verify-full`.

## Requisitos previos

Este documento supone que ya ha descargado una aplicación cliente de escritorio de terceros para usarla con sus datos de Experience Platform. En la documentación de la guía de conexión correspondiente encontrará instrucciones específicas sobre cómo incorporar la seguridad SSL al conectarse con un cliente de terceros. Para obtener una lista de todos los [!DNL Query Service] clientes admitidos, consulte la [descripción general de las conexiones de cliente](./overview.md).

## Opciones SSL disponibles {#available-ssl-options}

Experience Platform admite varias opciones SSL para adaptarse a sus necesidades de seguridad de datos y equilibrar la sobrecarga de procesamiento del cifrado y el intercambio de claves.

Los diferentes valores de parámetro `sslmode` proporcionan niveles de protección diferentes. Al cifrar sus datos en movimiento con certificados SSL, ayuda a evitar ataques &quot;man-in-the-middle&quot; (MITM), escuchas y suplantación de identidad. La siguiente tabla proporciona un desglose de los diferentes modos SSL disponibles y el nivel de protección que proporcionan.

>[!NOTE]
>
> Adobe Experience Platform no admite el valor SSL `disable` debido al cumplimiento de los requisitos de protección de datos.

| sslmode | Protección contra escuchas | Protección MITM | Descripción |
|---|---|---|---|
| `allow` | Sí | No | Se requiere cifrado en todas las comunicaciones. La red es de confianza para conectarse al servidor correcto. |
| `prefer` | Sí | No | Se requiere cifrado en todas las comunicaciones. La red es de confianza para conectarse al servidor correcto. |
| `require` | Sí | No | Se requiere cifrado en todas las comunicaciones. La red es de confianza para conectarse al servidor correcto. No se requiere la validación del certificado SSL del servidor. |
| `verify-ca` | Sí | Depende de la directiva de CA | Se requiere cifrado en todas las comunicaciones. Se requiere la validación del servidor antes de compartir los datos. Esto requiere que configure un certificado raíz en el directorio principal de [!DNL PostgreSQL]. [A continuación se proporcionan detalles](#instructions) |
| `verify-full` | Sí | Sí | Se requiere cifrado en todas las comunicaciones. Se requiere la validación del servidor antes de compartir los datos. Esto requiere que configure un certificado raíz en el directorio principal de [!DNL PostgreSQL]. [A continuación se proporcionan detalles](#instructions). |

>[!NOTE]
>
>La diferencia entre `verify-ca` y `verify-full` depende de la directiva de la entidad emisora de certificados (CA) raíz. Si ha creado su propia CA local para emitir certificados privados para sus aplicaciones, el uso de `verify-ca` suele proporcionar suficiente protección. Si se usa una CA pública, `verify-ca` permite conexiones a un servidor que otra persona podría haber registrado con la CA. `verify-full` siempre debe usarse con una CA raíz pública.

Al establecer una conexión de terceros con una base de datos de Experience Platform, se recomienda usar `sslmode=require` como mínimo para garantizar una conexión segura para los datos en movimiento. Se recomienda el modo SSL `verify-full` para utilizarlo en la mayoría de los entornos confidenciales.

## Configurar un certificado raíz para la verificación del servidor {#root-certificate}

>[!IMPORTANT]
>
>Los certificados TLS/SSL en entornos de producción para la API interactiva de Postgres del servicio de consulta se actualizaron el miércoles, 24 de enero de 2024.<br>Aunque se trata de un requisito anual, en esta ocasión el certificado raíz de la cadena también ha cambiado, ya que el proveedor de certificados TLS/SSL de Adobe ha actualizado su jerarquía de certificados. Esto puede afectar a ciertos clientes de Postgres si a su lista de autoridades de certificación les falta el certificado raíz. Por ejemplo, un cliente CLI de PSQL puede necesitar que se agreguen los certificados raíz a un archivo explícito `~/postgresql/root.crt`; de lo contrario, esto puede provocar un error. Por ejemplo, `psql: error: SSL error: certificate verify failed`. Consulte la [documentación oficial de PostgreSQL](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) para obtener más información sobre este problema.<br>El certificado raíz que desea agregar se puede descargar desde [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

Para garantizar una conexión segura, el uso de SSL debe configurarse tanto en el cliente como en el servidor antes de establecer la conexión. Si SSL solo está configurado en el servidor, el cliente puede enviar información confidencial como contraseñas antes de que se establezca que el servidor requiere una alta seguridad.

De manera predeterminada, [!DNL PostgreSQL] no realiza ninguna verificación del certificado del servidor. Para comprobar la identidad del servidor y garantizar una conexión segura antes de enviar datos confidenciales (como parte del modo SSL `verify-full`), debe colocar un certificado raíz (autofirmado) en el equipo local (`root.crt`) y un certificado hoja firmado por el certificado raíz en el servidor.

Si el parámetro `sslmode` está establecido en `verify-full`, libpq comprobará que el servidor es de confianza comprobando la cadena de certificados hasta el certificado raíz almacenado en el cliente. A continuación, comprueba que el nombre de host coincide con el nombre almacenado en el certificado del servidor.

Para permitir la verificación del certificado del servidor, debe colocar uno o más certificados raíz (`root.crt`) en el archivo [!DNL PostgreSQL] del directorio particular. La ruta de acceso del archivo sería similar a `~/.postgresql/root.crt`.

## Habilitar el modo SSL de verificación completa para utilizarlo con una conexión de terceros [!DNL Query Service] {#instructions}

Si necesita un control de seguridad más estricto que `sslmode=require`, puede seguir los pasos indicados para conectar un cliente de terceros a [!DNL Query Service] mediante el modo SSL `verify-full`.

>[!NOTE]
>
>Hay muchas opciones disponibles para obtener un certificado SSL. Debido a una creciente tendencia en certificados no fiables, DigiCert se utiliza en esta guía ya que es un proveedor global de confianza de soluciones de alta seguridad TLS/SSL, PKI, IoT y firma.

1. Vaya a [la lista de certificados raíz DigiCert disponibles](https://www.digicert.com/kb/digicert-root-certificates.htm)
1. Busque &quot;[!DNL DigiCert Global Root G2]&quot; de la lista de certificados disponibles.
1. Seleccione [!DNL **Descargar PEM**] para descargar el archivo en su equipo local.
   ![Lista de certificados raíz DigiCert disponibles con PEM de descarga resaltado.](../images/clients/ssl-modes/digicert.png)
1. Cambie el nombre del archivo del certificado de seguridad a `root.crt`.
1. Copie el archivo en la carpeta [!DNL PostgreSQL]. La ruta de archivo necesaria es diferente en función del sistema operativo. Si la carpeta aún no existe, créela.
   - Si usa macOS, la ruta de acceso es `/Users/<username>/.postgresql`
   - Si utiliza Windows, la ruta es `%appdata%\postgresql`

>[!TIP]
>
>Para encontrar la ubicación del archivo `%appdata%` en un sistema operativo Windows, presione ⊞ **Win + R** y escriba `%appdata%` en el campo de búsqueda.

Una vez que el archivo CRT [!DNL DigiCert Global Root G2] esté disponible en la carpeta [!DNL PostgreSQL], podrá conectarse a [!DNL Query Service] mediante la opción `sslmode=verify-full` o `sslmode=verify-ca`.

## Pasos siguientes

Al leer este documento, tiene una mejor comprensión de las opciones SSL disponibles para conectar un cliente de terceros a [!DNL Query Service], y también de cómo habilitar la opción SSL de `verify-full` para cifrar los datos en movimiento.

Si aún no lo ha hecho, siga las instrucciones sobre [conectar un cliente de terceros a [!DNL Query Service]](./overview.md).
