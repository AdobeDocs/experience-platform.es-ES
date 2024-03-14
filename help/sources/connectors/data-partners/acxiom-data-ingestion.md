---
title: Ingesta de datos de Acxiom
description: Aprenda a ingerir [!DNL Acxiom] Acceda a los datos de Real-time Customer Data Platform, enriquezca los perfiles de origen, mejore las audiencias y actívelos en los canales de marketing.
badge: Beta
source-git-commit: 9419da451616ca7f087ecea7aa66a6c10a474fb3
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>El [!DNL Acxiom Prospecting Data Import] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Utilice el [!DNL Acxiom Data Ingestion] origen de ingesta [!DNL Acxiom] datos en Real-time Customer Data Platform y enriquecer perfiles de origen. A continuación, puede utilizar su [!DNL Acxiom]: perfiles de origen enriquecidos para mejorar las audiencias y activarse en todos los canales de marketing.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Lea el siguiente documento para obtener información sobre cómo configurar su [!DNL Acxiom Data Ingestion] cuenta de origen.

## Requisitos previos {#prerequisites}

Para conectar su [!DNL Acxiom Data Ingestion] cuenta al Experience Platform, debe proporcionar valores para las siguientes credenciales de autenticación:

| Credencial | Descripción |
| --- | --- |
| [!DNL Acxiom] clave de autenticación | La clave de autenticación. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| [!DNL Amazon S3] tecla de acceso | ID de clave de acceso para el bloque. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| [!DNL Amazon S3] clave secreta | El ID de clave secreta de su cubo. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |
| Nombre del segmento | Este es el espacio en el que se compartirán los archivos. Puede recuperar este valor desde la variable [!DNL Acxiom] equipo. |

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Configuración de permisos en el Experience Platform

Debe tener ambos **[!UICONTROL Ver orígenes]** y **[!UICONTROL Administrar fuentes]** permisos habilitados para su cuenta con el fin de conectar su [!DNL Acxiom Data Ingestion] cuenta para el Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de IU de control de acceso](../../../access-control/ui/overview.md).

### Restricciones de nomenclatura para archivos y directorios

Las restricciones enumeradas a continuación deben tenerse en cuenta al nombrar el archivo o directorio de almacenamiento en la nube:

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben evitarse correctamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Puntos de código como `\uE000`, aunque son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para obtener datos de su [!DNL Acxiom] cuenta para el Experience Platform. Ahora puede continuar con la guía de [conectador [!DNL Acxiom Data Ingestion] al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
