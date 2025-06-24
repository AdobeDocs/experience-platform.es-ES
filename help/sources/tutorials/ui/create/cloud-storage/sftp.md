---
title: Creación de una conexión SFTP Source en la interfaz de usuario
description: Obtenga información sobre cómo crear una conexión de origen SFTP mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 1a00ed27-3c95-4e57-9f94-45ff256bf75c
source-git-commit: 4816a6b627dc6551e351bfe3cdc4bc8c8ea8b17e
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 1%

---

# Crear una conexión de origen [!DNL SFTP] en la interfaz de usuario

Este tutorial proporciona los pasos para crear una conexión de origen [!DNL SFTP] mediante la interfaz de usuario de Adobe Experience Platform.

## Introducción 

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco estandarizado mediante el cual Experience Platform organiza los datos de experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

>[!IMPORTANT]
>
>Se recomienda evitar líneas nuevas o retornos de carro al ingerir objetos JSON con una conexión de origen [!DNL SFTP]. Para solucionar la limitación, utilice un solo objeto JSON por línea y utilice varias líneas para los archivos siguientes.

Si ya tiene una conexión [!DNL SFTP] válida, puede omitir el resto de este documento y continuar con el tutorial sobre [configuración de un flujo de datos](../../dataflow/batch/cloud-storage.md).

### Recopilar credenciales necesarias

Lea la [[!DNL SFTP] guía de autenticación](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials) para ver los pasos detallados sobre cómo recuperar sus credenciales de autenticación.

## Conectar con el servidor [!DNL SFTP]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en la barra de navegación izquierda para acceder al área de trabajo de [!UICONTROL Fuentes]. La pantalla [!UICONTROL Catálogo] muestra una variedad de orígenes con los que puede crear una cuenta.

Puede seleccionar la categoría adecuada del catálogo en la parte izquierda de la pantalla. También puede encontrar la fuente específica con la que desea trabajar utilizando la opción de búsqueda.

En la categoría [!UICONTROL Almacenamiento en la nube], seleccione **[!UICONTROL SFTP]** y luego **[!UICONTROL Agregar datos]**.

![Catálogo de orígenes de Experience Platform con el origen SFTP seleccionado.](../../../../images/tutorials/create/sftp/catalog.png)

Aparecerá la página **[!UICONTROL Conectarse a SFTP]**. En esta página, puede usar credenciales nuevas o existentes.

### Cuenta existente

Para conectar una cuenta existente, selecciona la cuenta FTP o SFTP con la que quieras conectarte y, a continuación, selecciona **[!UICONTROL Siguiente]** para continuar.

![Una lista de cuentas SFTP existentes en la interfaz de usuario de Experience Platform.](../../../../images/tutorials/create/sftp/existing.png)

### Nueva cuenta

>[!TIP]
>
>* Una vez creada, no se puede cambiar el tipo de autenticación de una conexión base de [!DNL SFTP]. Para cambiar el tipo de autenticación, debe crear una nueva conexión base.
>
>* SFTP admite claves OpenSSH de tipo `ed25519`, `RSA` o `DSA`. Asegúrese de que el contenido del archivo de claves comience por `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` y termine por `"-----END [RSA/DSA] PRIVATE KEY-----"`. Si el archivo de clave privada es un archivo en formato PPK, utilice la herramienta PuTTY para convertir de formato PPK a formato OpenSSH.

Si va a crear una cuenta nueva, seleccione **[!UICONTROL Nueva cuenta]** y, a continuación, proporcione un nombre y una descripción opcional para la nueva cuenta de [!DNL SFTP].

![La nueva pantalla de la cuenta para SFTP](../../../../images/tutorials/create/sftp/new.png)

El origen [!DNL SFTP] admite la autenticación básica y la autenticación mediante clave pública SSH.

>[!BEGINTABS]

>[!TAB Autenticación básica]

Para usar la autenticación básica, seleccione **[!UICONTROL Contraseña]** y proporcione los valores apropiados para las siguientes credenciales:

* host
* puerto
* nombre de usuario
* contraseña

Durante este paso, también puede configurar el número máximo de conexiones simultáneas, definir la ruta de acceso de la carpeta y habilitar o deshabilitar la fragmentación para el servidor [!DNL SFTP]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

Para obtener más información acerca de la autenticación, lea la guía sobre [recopilación de credenciales necesarias para [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![La nueva pantalla de cuenta para el origen SFTP que usa autenticación básica](../../../../images/tutorials/create/sftp/password.png)

>[!TAB Autenticación de clave pública SSH]

Para usar credenciales basadas en claves públicas SSH, seleccione **[!UICONTROL clave pública SSH]** y proporcione los valores apropiados para las siguientes credenciales:

* host
* puerto
* nombre de usuario
* contenido de clave privada
* frase de contraseña

Durante este paso, también puede configurar el número máximo de conexiones simultáneas, definir la ruta de acceso de la carpeta y habilitar o deshabilitar la fragmentación para el servidor [!DNL SFTP]. Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y espere unos momentos para que se establezca la conexión.

Para obtener más información acerca de la autenticación, lea la guía sobre [recopilación de credenciales necesarias para [!DNL SFTP]](../../../../connectors/cloud-storage/sftp.md#gather-required-credentials).

![La nueva pantalla de la cuenta para el origen SFTP que usa la clave pública SSH.](../../../../images/tutorials/create/sftp/ssh.png)

>[!ENDTABS]

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión con su cuenta SFTP. Ahora puede continuar con el siguiente tutorial y [configurar un flujo de datos para traer datos de su almacenamiento en la nube a Experience Platform](../../dataflow/batch/cloud-storage.md).
