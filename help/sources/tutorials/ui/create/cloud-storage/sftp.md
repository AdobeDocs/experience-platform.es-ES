---
keywords: Experience Platform;inicio;temas populares;SFTP;sftp
solution: Experience Platform
title: Crear una conexión de origen SFTP en la interfaz de usuario
topic-legacy: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen SFTP mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: ade0da445b18108a7f8720404cc7a65139ed42b1
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Crear una conexión de origen [!DNL SFTP] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL SFTP] mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición](../../../../../xdm/schema/composition.md) del esquema: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de cliente unificado y en tiempo real basado en datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Se recomienda evitar nuevas líneas o retornos de carro al introducir objetos JSON con una conexión de origen [!DNL SFTP]. Para solucionar la limitación, utilice un único objeto JSON por línea y utilice líneas múltiples para los archivos posteriores.

Si ya tiene una conexión [!DNL SFTP] válida, puede omitir el resto de este documento y continuar con el tutorial sobre la [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para conectarse a [!DNL SFTP], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con su servidor [!DNL SFTP]. |
| `port` | Puerto del servidor [!DNL SFTP] al que se está conectando. Si no se proporciona, el valor predeterminado es `22`. |
| `username` | El nombre de usuario con acceso a su servidor [!DNL SFTP]. |
| `password` | La contraseña de su servidor [!DNL SFTP]. |
| `privateKeyContent` | El contenido de clave privada SSH codificada Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `passPhrase` | La frase de contraseña o contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido por contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como valor. |

Una vez que haya reunido las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta [!DNL SFTP] para conectarse a Platform.

## Conectarse al servidor [!DNL SFTP]

En la interfaz de usuario de Platform, seleccione **[!UICONTROL Sources]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Sources]. La pantalla [!UICONTROL Catalog] muestra una variedad de fuentes con las que puede crear una cuenta entrante.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. Alternativamente, puede encontrar la fuente específica con la que desea trabajar usando la opción de búsqueda.

En la categoría [!UICONTROL Cloud storage], seleccione **[!UICONTROL SFTP]** y, a continuación, seleccione **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/sftp/catalog.png)

Aparece la página **[!UICONTROL Connect to SFTP]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de FTP o SFTP con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/sftp/existing.png)

### Nueva cuenta

Si está creando una cuenta nueva, seleccione **[!UICONTROL New account]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva cuenta [!DNL SFTP].

#### Autenticar con contraseña

[!DNL SFTP] admite distintos tipos de autenticación para el acceso. En **[!UICONTROL Account authentication]** seleccione **[!UICONTROL Password]** y, a continuación, proporcione los valores de host y puerto a los que conectarse, junto con su nombre de usuario y contraseña.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

#### Autenticar con clave pública SSH

Para utilizar credenciales SSH basadas en claves públicas, seleccione **[!UICONTROL SSH public key]** y proporcione los valores de host y puerto, así como la combinación de contenido de clave privada y frase de contraseña.

>[!IMPORTANT]
>
>SFTP admite una clave OpenSSH de tipo RSA o DSA. Asegúrese de que el contenido del archivo clave comienza por `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` y termina por `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir del formato PPK al formato OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh-public-key.png)

| Credencial | Descripción |
| ---------- | ----------- |
| Contenido de clave privada | El contenido de clave privada SSH codificada Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| Frase de contraseña | Especifica la frase de contraseña o contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido por contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como su valor. |


## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta SFTP. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para importar los datos del almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
