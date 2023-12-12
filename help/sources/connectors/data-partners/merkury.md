---
title: Información general sobre la fuente de resolución de identidad de Merkury Enterprise
description: Obtenga información sobre cómo conectar la resolución de identidades de Experience Enterprise a Adobe Experience Platform mediante la interfaz de usuario.
badge: Beta
source-git-commit: 12f73ac2578b6c5b024cc4ebdd75cd945c7b55c9
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>El [!DNL Merkury Enterprise Identity Resolution] el origen está en versión beta. Lea el [información general de orígenes](../../home.md#terms-and-conditions) para obtener más información sobre el uso de fuentes etiquetadas como beta.

Adobe Experience Platform es compatible con la ingesta de datos desde una aplicación de socio de datos. El soporte para socios de datos incluye [!DNL Merkury Enterprise Identity Resolution].

Puede utilizar [!DNL Merkury] por [!DNL Merkle] para reconocer a más visitantes digitales, incluso sin el uso de cookies, y ofrecer las experiencias relevantes y personalizadas que el cliente necesita.

Puede utilizar el **ID de persona** como parte de [!DNL Merkury] fuente para combinar todo lo que su organización conoce sobre un individuo en un único perfil completo. Estos detalles pueden incluir lo siguiente:

- comportamientos digitales
- preferencias de compra
- información de identificación, como un nombre, una dirección de correo electrónico, una dirección física o un ID de dispositivo.

Puede dar formato a los datos introducidos como Experience Data Model (XDM) JSON, XDM Parquet o delimitado. Cada paso del proceso está integrado en el trabajo de las fuentes

![Ilustración del flujo de trabajo de procesamiento de datos para la fuente Mercury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## LISTA DE PERMITIDOS de direcciones IP

Se debe agregar una lista de direcciones IP a una lista de permitidos antes de trabajar con conectores de origen. Si no se agregan las direcciones IP específicas de la región a la lista de permitidos, pueden producirse errores o no rendimiento al utilizar fuentes. Consulte la [LISTA DE PERMITIDOS de direcciones IP](../../ip-address-allow-list.md) para obtener más información.

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben evitarse correctamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Puntos de código como `\uE000`, aunque son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para ver las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, sección 2.2: Reglas básicas](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Requisitos previos

Debe cumplir los siguientes requisitos previos para poder empezar a utilizar el [!DNL Merkury] fuente:

- Debe completar su [!DNL Merkury] configure con su [!DNL Merkury] equipo.
- Debe recuperar sus credenciales (clave de acceso, clave secreta y nombre del contenedor) de su [!DNL Merkury] equipo. 

>[!NOTE]
>
>Una ruta de archivo como `myBucket/folder/subfolder/subsubfolder/abc.csv` puede permitirle acceder únicamente a `subsubfolder/abc.csv`. Si desea acceder a la subcarpeta, puede especificar el parámetro de contenedor como myBucket y folderPath como folder/subfolder para garantizar que la exploración de archivos comience en la subcarpeta en lugar de en `subsubfolder/abc.csv`.

## Pasos siguientes

Al leer este documento, ha completado la configuración de requisitos previos necesaria para obtener datos de su [!DNL Merkury] cuenta para el Experience Platform. Ahora puede continuar con la guía de [conectador [!DNL Merkury] al Experience Platform mediante la interfaz de usuario de](../../tutorials/ui/create/data-partners/merkury.md).
