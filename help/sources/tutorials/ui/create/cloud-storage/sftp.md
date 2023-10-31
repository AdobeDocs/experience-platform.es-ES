---
title: Creación de una conexión de origen SFTP en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen SFTP mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Crear un [!DNL SFTP] conexión de origen en la interfaz de usuario

Este tutorial proporciona los pasos para crear una [!DNL SFTP] conexión de origen mediante la IU de Adobe Experience Platform.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Se recomienda evitar líneas nuevas o retornos de carro al ingerir objetos JSON con un [!DNL SFTP] conexión de origen. Para solucionar la limitación, utilice un solo objeto JSON por línea y utilice varias líneas para los archivos siguientes.

Si ya tiene un válido [!DNL SFTP] conexión, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Para conectarse a [!DNL SFTP], debe proporcionar valores para las siguientes propiedades de conexión:

| Credencial | Descripción |
| ---------- | ----------- |
| `host` | El nombre o la dirección IP asociados con su [!DNL SFTP] servidor. |
| `port` | El [!DNL SFTP] puerto del servidor al que se está conectando. Si no se proporciona, el valor predeterminado es `22`. |
| `username` | El nombre de usuario con acceso a su [!DNL SFTP] servidor. |
| `password` | La contraseña de su [!DNL SFTP] servidor. |
| `privateKeyContent` | El contenido de clave privada SSH codificado en Base64. El tipo de clave OpenSSH debe clasificarse como RSA o DSA. |
| `passPhrase` | La contraseña o frase de paso para descifrar la clave privada si el archivo de clave o el contenido de la clave están protegidos por una frase de paso. Si PrivateKeyContent está protegido con contraseña, este parámetro debe utilizarse con la frase de contraseña de PrivateKeyContent como valor. |
| `maxConcurrentConnections` | Este parámetro le permite especificar un límite máximo para el número de conexiones simultáneas que Platform creará al conectarse al servidor SFTP. Debe configurar este valor para que sea inferior al límite establecido por SFTP. **Nota**: Cuando esta configuración está habilitada para una cuenta SFTP existente, solo afectará a flujos de datos futuros y no a flujos de datos existentes. |
| Ruta de carpeta | La ruta a la carpeta a la que desea proporcionar acceso. [!DNL SFTP] origen, puede proporcionar la ruta de la carpeta para especificar el acceso del usuario a la subcarpeta que elija. |

Una vez que haya recopilado las credenciales necesarias, puede seguir los pasos a continuación para crear una nueva [!DNL SFTP] para conectarse a Platform.

## Conéctese a su [!DNL SFTP] server

En la IU de Platform, seleccione **[!UICONTROL Fuentes]** desde la barra de navegación izquierda para acceder a [!UICONTROL Fuentes] workspace. El [!UICONTROL Catálogo] La pantalla muestra una variedad de fuentes con las que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En el [!UICONTROL Almacenamiento en la nube] categoría, seleccionar **[!UICONTROL SFTP]** y luego seleccione **[!UICONTROL Añadir datos]**.

![El catálogo de fuentes del Experience Platform con la fuente SFTP seleccionada.](../../../../images/tutorials/create/sftp/catalog.png)

El **[!UICONTROL Conectar con SFTP]** página. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, seleccione la cuenta FTP o SFTP con la que desee conectarse y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas SFTP existentes en la interfaz de usuario de Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nueva cuenta

>[!TIP]
>
>* Una vez creado, no se puede cambiar el tipo de autenticación de una [!DNL SFTP] conexión base. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.
>
>* SFTP admite una clave OpenSSH de tipo RSA o DSA. Asegúrese de que el contenido del archivo de claves comience por `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` y termina por `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir de formato PPK a formato OpenSSH.

Si está creando una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva [!DNL SFTP] cuenta.

![La nueva pantalla de la cuenta para el SFTP](../../../../images/tutorials/create/sftp/new.png)

El [!DNL SFTP] source admite la autenticación básica y la autenticación mediante clave pública SSH.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para utilizar la autenticación básica, seleccione **[!UICONTROL Contraseña]** y, a continuación, proporcione los valores de host y puerto a los que conectarse, junto con su nombre de usuario y contraseña. Durante este paso, también puede designar la ruta a la subcarpeta a la que desea proporcionar acceso. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![La nueva pantalla de cuenta para el origen SFTP mediante autenticación básica](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticación de clave pública SSH]

Para utilizar credenciales SSH basadas en claves públicas, seleccione **[!UICONTROL Clave pública SSH]**  y, a continuación, proporcione los valores de host y puerto, así como el contenido de clave privada y la combinación de frase de contraseña. Durante este paso, también puede designar la ruta a la subcarpeta a la que desea proporcionar acceso. Cuando termine, seleccione **[!UICONTROL Conectar con el origen]**.

![La nueva pantalla de la cuenta para el origen SFTP mediante clave pública SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta SFTP. Ahora puede continuar con el siguiente tutorial y [configure un flujo de datos para traer datos de su almacenamiento en la nube a Platform](../../dataflow/batch/cloud-storage.md).
