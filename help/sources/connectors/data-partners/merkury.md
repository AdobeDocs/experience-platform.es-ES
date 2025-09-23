---
title: Resumen de Source de resolución de identidad empresarial de Merkury
description: Obtenga información sobre cómo conectar la resolución de identidades de Experience Enterprise a Adobe Experience Platform mediante la interfaz de usuario.
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

Adobe Experience Platform es compatible con la ingesta de datos desde una aplicación de socio de datos. La compatibilidad con socios de datos incluye [!DNL Merkury Enterprise Identity Resolution].

Puede usar [!DNL Merkury] por [!DNL Merkle] para reconocer a más visitantes digitales, incluso sin usar cookies, y ofrecer las experiencias relevantes y personalizadas que necesita el cliente.

Puede usar la **ID de persona** como parte de la fuente [!DNL Merkury] para combinar todo lo que su organización conoce sobre un individuo en un único perfil completo. Estos detalles pueden incluir lo siguiente:

- Comportamientos digitales
- Preferencias de compra
- Información de identificación, como nombre, dirección de correo electrónico, dirección física o ID de dispositivo.

Puede dar formato a los datos introducidos como Experience Data Model (XDM) JSON, XDM Parquet o delimitado. Cada paso del proceso está integrado en el trabajo de las fuentes

![Ilustración del flujo de trabajo de procesamiento de datos para el origen Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

## LISTA DE PERMITIDOS de direcciones IP

Para poder utilizar conectores de origen, debe agregar a la lista de permitidos las direcciones IP necesarias para la región. Si no agrega estas direcciones IP, es posible que los conectores de origen no funcionen correctamente o que produzcan errores. Para obtener instrucciones detalladas y la lista de direcciones IP permitidas, lee la página [lista de permitidos de direcciones IP](../../ip-address-allow-list.md).

## Restricciones de nomenclatura para archivos y directorios

A continuación se muestra una lista de restricciones que debe tener en cuenta al nombrar el archivo o directorio de almacenamiento en la nube.

- Los nombres de componentes de directorio y archivo no pueden superar los 255 caracteres.
- Los nombres de directorio y archivo no pueden terminar con una barra diagonal (`/`). Si se proporciona, se eliminará automáticamente.
- Los siguientes caracteres de URL reservadas deben ser de escape correcto: `! ' ( ) ; @ & = + $ , % # [ ]`
- No se permiten los siguientes caracteres: `" \ / : | < > * ?`.
- No se permiten caracteres de ruta de URL no válidos. Los puntos de código como `\uE000`, si bien son válidos en los nombres de archivo NTFS, no son caracteres Unicode válidos. Además, algunos caracteres ASCII o Unicode, como los caracteres de control (0x00 a 0x1F, \u0081, etc.), tampoco están permitidos. Para las reglas que rigen las cadenas Unicode en HTTP/1.1, consulte [RFC 2616, Section 2.2: Basic Rules](https://www.ietf.org/rfc/rfc2616.txt) y [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- No se permiten los siguientes nombres de archivo: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, carácter de punto (.) y dos caracteres de punto (..).

## Requisitos previos

Debe cumplir los siguientes requisitos previos para poder empezar a usar el origen [!DNL Merkury]:

- Debe completar la configuración de [!DNL Merkury] con su equipo de [!DNL Merkury].
- Debe recuperar sus credenciales (clave de acceso, clave secreta y nombre del contenedor) de su equipo [!DNL Merkury]. 

>[!NOTE]
>
>Una ruta de acceso de archivo como `myBucket/folder/subfolder/subsubfolder/abc.csv` puede llevarle únicamente a obtener acceso a `subsubfolder/abc.csv`. Si desea acceder a la subcarpeta, puede especificar el parámetro de contenedor como myBucket y folderPath como folder/subfolder para garantizar que la exploración de archivos comience en la subcarpeta en lugar de `subsubfolder/abc.csv`.

## Próximos pasos

Al leer este documento, ha completado la configuración de requisitos previos necesaria para llevar los datos de su cuenta de [!DNL Merkury] a Experience Platform. Ahora puede continuar con la guía de [conexión [!DNL Merkury] a Experience Platform mediante la interfaz de usuario](../../tutorials/ui/create/data-partners/merkury.md).
