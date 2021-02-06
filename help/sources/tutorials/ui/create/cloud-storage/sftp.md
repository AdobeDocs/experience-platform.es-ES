---
keywords: Experience Platform;inicio;temas populares;SFTP;sftp
solution: Experience Platform
title: Creación de una conexión de origen SFTP en la interfaz de usuario
topic: overview
type: Tutorial
description: Obtenga información sobre cómo crear una conexión de origen SFTP mediante la interfaz de usuario de Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---


# Creación de una conexión de origen SFTP en la interfaz de usuario

>[!NOTE]
>
>El conector SFTP está en versión beta. Consulte la [información general de las fuentes](../../../../home.md#terms-and-conditions) para obtener más información sobre el uso de conectores con etiquetas beta.

Este tutorial proporciona los pasos para crear una conexión de origen SFTP mediante la interfaz de usuario de Adobe Experience Platform.

## Primeros pasos

Este tutorial requiere un conocimiento práctico de los siguientes componentes de Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El esquema estandarizado por el cual el Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de la composición](../../../../../xdm/schema/composition.md) de esquemas: Obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) del Editor de esquemas: Obtenga información sobre cómo crear esquemas personalizados mediante la interfaz de usuario del Editor de Esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):: Proporciona un perfil de consumo unificado y en tiempo real basado en datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Se recomienda evitar nuevas líneas o retornos de carro al ingerir objetos JSON con una conexión de origen SFTP. Para evitar la limitación, utilice un único objeto JSON por línea y varias líneas para los archivos posteriores.

Si ya tiene una conexión SFTP válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar las credenciales necesarias

Para conectarse a SFTP, debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con el servidor SFTP. |
| `username` | El nombre de usuario con acceso al servidor SFTP. |
| `password` | La contraseña del servidor SFTP. |
| `privateKeyContent` | Contenido de clave privada SSH codificada en Base64. Formato SSH de clave privada OpenSSH (RSA/DSA). |
| `passPhrase` | La frase de contraseña o la contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido con contraseña, este parámetro debe usarse con la frase de contraseña de PrivateKeyContent como valor. |

Una vez recopiladas las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva cuenta SFTP para conectarse a Platform.

## Conectarse al servidor SFTP

Inicie sesión en [Adobe Experience Platform](https://platform.adobe.com) y, a continuación, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al espacio de trabajo [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes para los que puede crear una cuenta de entrada.

Puede seleccionar la categoría adecuada en el catálogo a la izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar mediante la opción de búsqueda.

En la categoría [!UICONTROL Cloud almacenamiento], seleccione **[!UICONTROL SFTP]**. Si es la primera vez que utiliza este conector, seleccione **[!UICONTROL Configurar]**. De lo contrario, seleccione **[!UICONTROL Añadir datos]** para crear una nueva conexión SFTP.

![catálogo](../../../../images/tutorials/create/sftp/catalog.png)

Aparece la página **[!UICONTROL Conectar con SFTP]**. En esta página, puede usar credenciales nuevas o existentes.

### Nueva cuenta

Si está utilizando nuevas credenciales, seleccione **[!UICONTROL Nueva cuenta]**. En el formulario de entrada que aparece, especifique un nombre, una descripción opcional y sus credenciales. Cuando termine, seleccione **[!UICONTROL Conectar]** y, a continuación, deje transcurrir algún tiempo para que se establezca la nueva conexión.

El conector SFTP proporciona diferentes tipos de autenticación para el acceso. En **[!UICONTROL Autenticación de cuenta]** seleccione **[!UICONTROL Contraseña]** para utilizar una credencial basada en contraseña.

![connect-password](../../../../images/tutorials/create/sftp/password.png)

También puede seleccionar **[clave pública SSH]** y conectar su cuenta SFTP mediante una combinación de [!UICONTROL contenido de clave privada] y [!UICONTROL frase de contraseña].

>[!IMPORTANT]
>
>El conector SFTP admite una clave RSA/DSA OpenSSH. Asegúrese de que el contenido del archivo clave inicio con `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir del formato PPK al formato OpenSSH.

![connect-ssh](../../../../images/tutorials/create/sftp/ssh.png)

| Credencial | Descripción |
| ---------- | ----------- |
| Contenido de clave privada | Contenido de clave privada SSH codificada en Base64. La clave privada SSH debe tener el formato OpenSSH. |
| Frase de contraseña | Especifica la frase de contraseña o la contraseña para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de contraseña. Si PrivateKeyContent está protegido con contraseña, este parámetro debe usarse con la frase de contraseña de PrivateKeyContent como valor. |

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta de FTP o SFTP con la que desea conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![existente](../../../../images/tutorials/create/sftp/existing.png)

## Pasos siguientes

Siguiendo este tutorial, ha establecido una conexión con su cuenta de FTP o SFTP. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos del almacenamiento de nube a la plataforma](../../dataflow/batch/cloud-storage.md).