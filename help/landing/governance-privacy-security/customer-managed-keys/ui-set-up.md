---
title: Configurar las claves administradas por el cliente mediante la interfaz de usuario de Platform
description: Obtenga información sobre cómo configurar la aplicación CMK con el inquilino de Azure y enviar el ID de clave de cifrado a Adobe Experience Platform.
exl-id: 5f38997a-66f3-4f9d-9c2f-fb70266ec0a6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---

# Configurar las claves administradas por el cliente mediante la IU de Platform

Este documento cubre el proceso para habilitar la función de claves administradas por el cliente (CMK) en Platform mediante la interfaz de usuario de. Para obtener instrucciones sobre cómo completar este proceso mediante la API, consulte la [Documento de configuración de API CMK](./api-set-up.md).

## Requisitos previos

Para ver y visitar [!UICONTROL Cifrado] en Adobe Experience Platform, debe haber creado una función y asignado el [!UICONTROL Administrar clave gestionada por el cliente] permiso para ese rol. Cualquier usuario que tenga el [!UICONTROL Administrar clave gestionada por el cliente] El permiso puede habilitar CMK para su organización.

Para obtener más información sobre la asignación de funciones y permisos en Experience Platform, consulte la [documentación de configuración de permisos](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=es).

Para habilitar CMK, su [[!DNL Azure] Se debe configurar Key Vault](./azure-key-vault-config.md) con la siguiente configuración:

* [Habilitar protección contra purgas](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar eliminación suave](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configuración del acceso mediante [!DNL Azure] control de acceso basado en roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configuración de un [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## Configuración de la aplicación CMK {#register-app}

Una vez configurado el almacén de claves, el siguiente paso es registrar la aplicación CMK que se vinculará a su [!DNL Azure] inquilino.

### Introducción

Para ver la [!UICONTROL Configuraciones de cifrado] panel, seleccione **[!UICONTROL Cifrado]** en el [!UICONTROL Administration] encabezado de la barra lateral de navegación izquierda.

![El panel de configuración Cifrado con Cifrado y la tarjeta Claves administradas por el cliente resaltadas.](../../images/governance-privacy-security/customer-managed-keys/encryption-configraion.png)

Seleccionar **[!UICONTROL Configurar]** para abrir [!UICONTROL Configuración de claves administradas por el cliente] vista. Este espacio de trabajo contiene todos los valores necesarios para completar los pasos que se describen a continuación y realizar la integración con el almacén de claves de Azure.

### Copiar URL de autenticación {#copy-authentication-url}

Para iniciar el proceso de registro, copie la URL de autenticación de la aplicación para su organización desde el [!UICONTROL Configuración de claves administradas por el cliente] ver y pegarlo en su [!DNL Azure] entorno **[!DNL Key Vault Crypto Service Encryption User]**. Detalles sobre cómo [asignar un rol](#assign-to-role) se proporcionan en la siguiente sección.

Seleccione el icono de copia (![El icono Copiar.](../../images/governance-privacy-security/customer-managed-keys/copy-icon.png)) por el [!UICONTROL URL de autenticación de aplicación].

![El [!UICONTROL Configuración de claves administradas por el cliente] vista con la sección URL de autenticación de aplicación resaltada.](../../images/governance-privacy-security/customer-managed-keys/application-authentication-url.png)

Copie y pegue [!UICONTROL URL de autenticación de aplicación] en un explorador para abrir un cuadro de diálogo de autenticación. Seleccionar **[!DNL Accept]** para agregar la entidad de seguridad del servicio de aplicaciones CMK a su [!DNL Azure] inquilino. Al confirmar la autenticación, se le redirige a la página de aterrizaje del Experience Cloud.

![Cuadro de diálogo de solicitud de permiso de Microsoft con [!UICONTROL Aceptar] resaltado.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

>[!IMPORTANT]
>
>Si tiene varias [!DNL Microsoft Azure] suscripciones, podría conectar potencialmente su instancia de Platform al almacén de claves incorrecto. En este caso, debe intercambiar la variable `common` de la URL de autenticación de la aplicación para el ID de directorio CMK.<br>Copie el ID de directorio CMK de la página Configuración de portal, Directorios y Suscripciones de [!DNL Microsoft Azure] aplicación<br>![El [!DNL Microsoft Azure] página Configuración del portal de la aplicación, Directorios y Suscripciones con el Id. de directorio resaltado.](../../images/governance-privacy-security/customer-managed-keys/directory-id.png)<br>A continuación, péguelo en la barra de direcciones del explorador.<br>![Una página del explorador Google con la sección &quot;común&quot; de la URL de autenticación de la aplicación resaltada.](../../images/governance-privacy-security/customer-managed-keys/common-url-section.png)

### Asignar la aplicación CMK a un rol {#assign-to-role}

Después de completar el proceso de autenticación, vuelva a su [!DNL Azure] Key Vault y seleccione **[!DNL Access control]** en el panel de navegación izquierdo. Desde aquí, seleccione **[!DNL Add]** seguido de **[!DNL Add role assignment]**.

![El [!DNL Microsoft Azure] panel con [!DNL Add] y [!DNL Add role assignment] resaltado.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

La siguiente pantalla le pedirá que elija una función para esta asignación. Seleccionar **[!DNL Key Vault Crypto Service Encryption User]** antes de seleccionar **[!DNL Next]** para continuar.

![El [!DNL Microsoft Azure] panel con el [!DNL Key Vault Crypto Service Encryption User] resaltado.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

En la pantalla siguiente, elija **[!DNL Select members]** para abrir un cuadro de diálogo en el carril derecho. Utilice la barra de búsqueda para localizar la entidad de seguridad de servicio de la aplicación CMK y seleccionarla en la lista. Cuando termine, seleccione **[!DNL Save]**.

>[!NOTE]
>
>Si no encuentra su aplicación en la lista, no se ha aceptado su entidad de servicio en su inquilino. Para asegurarse de que tiene los privilegios correctos, trabaje con su [!DNL Azure] administrador o representante.

Puede verificar la aplicación comparando las variables [!UICONTROL ID de aplicación] proporcionado en la [!UICONTROL Configuración de claves administradas por el cliente] ver con el [!DNL Application ID] proporcionado en la [!DNL Microsoft Azure] descripción general de la aplicación.

![El [!UICONTROL Configuración de claves administradas por el cliente] ver con el [!UICONTROL ID de aplicación] resaltado.](../../images/governance-privacy-security/customer-managed-keys/application-id.png)

Todos los detalles necesarios para verificar las herramientas de Azure se incluyen en la interfaz de usuario de Platform. Este nivel de granularidad se proporciona ya que muchos usuarios desean utilizar otras herramientas de Azure para mejorar su capacidad de monitorizar y registrar el acceso de estas aplicaciones a su almacén de claves. Comprender estos identificadores es fundamental para ese fin y para ayudar a los servicios de Adobe a acceder a la clave.

## Habilitar la configuración de clave de cifrado en el Experience Platform {#send-to-adobe}

Después de instalar la aplicación CMK en [!DNL Azure], puede enviar su identificador de clave de cifrado al Adobe. Seleccionar **[!DNL Keys]** en el panel de navegación izquierdo, seguido del nombre de la clave que desea enviar.

![El panel de Microsoft Azure con la variable [!DNL Keys] objeto y el nombre de clave resaltados.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleccione la última versión de la clave y aparecerá su página de detalles. Desde aquí puede configurar de forma opcional las operaciones permitidas para la clave.

>[!IMPORTANT]
>
>Las operaciones mínimas requeridas que se permiten para la clave son las siguientes **[!DNL Wrap Key]** y **[!DNL Unwrap Key]** permisos. Puede incluir [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], y [!DNL Verify] si quieres.

El **[!UICONTROL Identificador de clave]** El campo muestra el identificador URI de la clave. Copie este valor de URI para utilizarlo en el siguiente paso.

![Los detalles de la clave del panel de Microsoft Azure con la variable [!DNL Permitted operations] y las secciones Copiar URL clave resaltadas.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Una vez que haya obtenido la [!DNL Key vault URI], vuelva a la [!UICONTROL Configuración de claves administradas por el cliente] ver e introducir un elemento descriptivo **[!UICONTROL Nombre de configuración]**. A continuación, añada el [!DNL Key Identifier] tomado de la página de detalles de clave de Azure en el **[!UICONTROL Identificador de clave del almacén de claves]** y seleccione **[!UICONTROL Guardar]**.

![El [!UICONTROL Configuración de claves administradas por el cliente] ver con el [!UICONTROL Nombre de configuración] y el [!UICONTROL Identificador de clave del almacén de claves] secciones resaltadas.](../../images/governance-privacy-security/customer-managed-keys/configuration-name.png)

Se le devolverá a la [!UICONTROL Panel de configuraciones de cifrado]. El estado del [!UICONTROL Claves gestionadas por el cliente] la configuración se muestra como [!UICONTROL Procesando].

![El [!UICONTROL Configuraciones de cifrado] panel con [!UICONTROL Procesando] resaltado en la [!UICONTROL Claves gestionadas por el cliente] Tarjeta de.](../../images/governance-privacy-security/customer-managed-keys/processing.png)

## Verificar el estado de la configuración {#check-status}

Conceda una cantidad de tiempo considerable para el procesamiento. Para comprobar el estado de la configuración, vuelva a la [!UICONTROL Configuración de claves administradas por el cliente] ver y desplazarse hacia abajo hasta el [!UICONTROL Estado de configuración]. La barra de progreso ha avanzado hasta el paso uno de tres y explica que el sistema está validando que Platform tiene acceso a la clave y al almacén de claves.

Hay cuatro estados potenciales de la configuración de CMK. Son las siguientes:

* Paso 1: Valida que Platform tenga la capacidad de acceder a la clave y al almacén de claves.
* Paso 2: El almacén de claves y el nombre de clave están en proceso de añadirse a todos los almacenes de datos de su organización.
* Paso 3: El almacén de claves y el nombre de clave se han añadido correctamente a los almacenes de datos.
* `FAILED`: Se ha producido un problema, relacionado principalmente con la clave, el almacén de claves o la configuración de aplicaciones de varios inquilinos.

## Pasos siguientes

Al completar los pasos anteriores, ha habilitado correctamente CMK para su organización. Los datos que se incorporan a los almacenes de datos principales ahora se cifran y descifran con las claves de su [!DNL Azure] Key Vault.
