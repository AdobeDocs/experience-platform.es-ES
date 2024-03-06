---
title: Importación de datos de prospección de Acxiom
description: Aprenda a conectar los datos de prospección de Acxiom a Adobe Experience Platform y Adobe Real-time Customer Data Platform mediante la interfaz de usuario.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>El [!DNL Acxiom Prospecting Data Import] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform es compatible con la ingesta de datos desde una aplicación de socio de datos. La compatibilidad con socios de datos e identidad incluye [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]La importación de datos de prospección de para Adobe Real-time Customer Data Platform es un proceso para ofrecer las audiencias de clientes potenciales más productivas posibles. [!DNL Acxiom] toma los datos de origen de Real-Time CDP a través de una exportación segura y los ejecuta a través de un sistema de higiene y resolución de identidades galardonado. Se genera un archivo de datos que se puede utilizar como lista de supresión. Este archivo de datos se compara con el [!DNL Acxiom Global] base de datos, que permite personalizar las listas de clientes potenciales para su importación.

Puede usar el complemento [!DNL Acxiom] origen para recuperar y asignar respuestas desde el [!DNL Acxiom] servicio de cliente potencial que utiliza [!DNL Amazon S3] como punto de caída.

## Requisitos previos

Para acceder al bloque en Experience Platform, debe proporcionar valores válidos para las siguientes credenciales:

| Credencial | Descripción |
| --- | --- |
| [!DNL Acxiom] clave de autenticación | La clave de autenticación. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| [!DNL Amazon S3] tecla de acceso | ID de clave de acceso para el bloque. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| [!DNL Amazon S3] clave secreta | El ID de clave secreta de su cubo. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| Nombre del segmento | Este es el espacio en el que se compartirán los archivos. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |

### Permisos

Debe tener ambos **[!UICONTROL Ver orígenes]** y **[!UICONTROL Administrar fuentes]** permisos habilitados para su cuenta con el fin de conectar su [!DNL Acxiom Prospecting Data Import] cuenta para el Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de IU de control de acceso](../../../access-control/abac/ui/permissions.md).

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nomenclatura para archivos y directorios

Las restricciones enumeradas a continuación deben tenerse en cuenta al nombrar el archivo o directorio de almacenamiento en la nube:

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben evitarse correctamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Puntos de código como `\uE000`, aunque son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para obtener datos de su [!DNL Acxiom] cuenta para el Experience Platform. Ahora puede continuar con la guía de [conectador [!DNL Acxiom Prospecting Data Import] al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).