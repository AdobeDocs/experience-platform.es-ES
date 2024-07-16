---
title: Ingesta de datos de Acxiom
description: Aprenda a ingerir  [!DNL Acxiom] datos en Real-time Customer Data Platform, enriquecer perfiles de origen, mejorar audiencias y activarlos en varios canales de marketing.
badge: Beta
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# [!DNL Acxiom Data Ingestion]

>[!NOTE]
>
>El origen [!DNL Acxiom Prospecting Data Import] está en la versión beta. Lea [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de orígenes etiquetados como beta.

Utilice el origen [!DNL Acxiom Data Ingestion] para introducir datos de [!DNL Acxiom] en Real-time Customer Data Platform y enriquecer perfiles de origen. A continuación, puede usar sus perfiles de origen enriquecidos con [!DNL Acxiom] para mejorar las audiencias y activarlos en todos los canales de marketing.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Lea el documento siguiente para obtener información sobre cómo configurar su cuenta de origen de [!DNL Acxiom Data Ingestion].

## Requisitos previos {#prerequisites}

Para conectar su cuenta de [!DNL Acxiom Data Ingestion] al Experience Platform, debe proporcionar valores para las siguientes credenciales de autenticación:

| Credencial | Descripción |
| --- | --- |
| Clave de autenticación [!DNL Acxiom] | La clave de autenticación. Puede recuperar este valor del equipo [!DNL Acxiom]. |
| Clave de acceso de [!DNL Amazon S3] | ID de clave de acceso para el bloque. Puede recuperar este valor del equipo [!DNL Acxiom]. |
| clave secreta [!DNL Amazon S3] | El ID de clave secreta de su cubo. Puede recuperar este valor del equipo [!DNL Acxiom]. |
| Nombre del segmento | Este es el espacio en el que se compartirán los archivos. Puede recuperar este valor del equipo [!DNL Acxiom]. |

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

### Configuración de permisos en el Experience Platform

Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Acxiom Data Ingestion] al Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/ui/overview.md).

### Restricciones de nomenclatura para archivos y directorios

Las restricciones enumeradas a continuación deben tenerse en cuenta al nombrar el archivo o directorio de almacenamiento en la nube:

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para llevar los datos de su cuenta de [!DNL Acxiom] al Experience Platform. Ahora puede continuar con la guía de [conexión [!DNL Acxiom Data Ingestion] al Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
