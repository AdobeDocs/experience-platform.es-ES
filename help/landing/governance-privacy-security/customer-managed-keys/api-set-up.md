---
title: Configurar las claves administradas por el cliente mediante la API
description: Obtenga información sobre cómo configurar la aplicación CMK con el inquilino de Azure y enviar el ID de clave de cifrado a Adobe Experience Platform.
exl-id: c9a1888e-421f-4bb4-b4c7-968fb1d61746
source-git-commit: 4f08e8fcc8d53b981af60226f1397a1d1ac4d8dc
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# Configurar las claves administradas por el cliente mediante la API

Este documento describe el proceso para habilitar la función de claves administradas por el cliente (CMK) en Adobe Experience Platform mediante la API. Para obtener instrucciones sobre cómo completar este proceso mediante la interfaz de usuario, consulte la [Documento de configuración de IU CMK](./ui-set-up.md).

## Requisitos previos

Para ver y visitar [!UICONTROL Cifrado] en Adobe Experience Platform, debe haber creado una función y asignado el [!UICONTROL Administrar clave gestionada por el cliente] permiso para ese rol. Cualquier usuario que tenga el [!UICONTROL Administrar clave gestionada por el cliente] El permiso puede habilitar CMK para su organización.

Para obtener más información sobre la asignación de funciones y permisos en Experience Platform, consulte la [documentación de configuración de permisos](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html?lang=es).

Para habilitar CMK, su [[!DNL Azure] Se debe configurar Key Vault](./azure-key-vault-config.md) con la siguiente configuración:

* [Habilitar protección contra purgas](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar eliminación suave](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configuración del acceso mediante [!DNL Azure] control de acceso basado en roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)
* [Configuración de un [!DNL Azure] Key Vault](./azure-key-vault-config.md)

## Configuración de la aplicación CMK {#register-app}

Una vez configurado el almacén de claves, el siguiente paso es registrarse en la aplicación CMK que se vinculará a su [!DNL Azure] inquilino.

### Introducción

El registro de la aplicación CMK requiere que realice llamadas a las API de Platform. Para obtener más información sobre cómo recopilar los encabezados de autenticación necesarios para realizar estas llamadas, consulte la [Guía de autenticación de Platform API](../../api-authentication.md).

Mientras que la guía de autenticación proporciona instrucciones sobre cómo generar su propio valor único para el requerido `x-api-key` encabezado de solicitud, todas las operaciones de API de esta guía utilizan el valor estático `acp_provisioning` en su lugar. Debe seguir proporcionando sus propios valores para `{ACCESS_TOKEN}` y `{ORG_ID}`, sin embargo.

En todas las llamadas API que se muestran en esta guía, `platform.adobe.io` se utiliza como ruta raíz, que toma como valor predeterminado la región VA7. Si su organización utiliza una región diferente, `platform` debe ir seguido de un guión y del código de región asignado a su organización: `nld2` para NLD2 o `aus5` para AUS5 (por ejemplo: `platform-aus5.adobe.io`). Si no conoce la región de su organización, póngase en contacto con el administrador del sistema.

### Buscar una URL de autenticación {#fetch-authentication-url}

Para iniciar el proceso de registro, realice una solicitud de GET al extremo de registro de la aplicación para recuperar la URL de autenticación necesaria para su organización.

**Solicitud**

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/byok/app-registration \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve un `applicationRedirectUrl` , que contiene la dirección URL de autenticación.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copie y pegue `applicationRedirectUrl` Dirección en un explorador para abrir un cuadro de diálogo de autenticación. Seleccionar **[!DNL Accept]** para agregar la entidad de seguridad del servicio de aplicaciones CMK a su [!DNL Azure] inquilino.

![Cuadro de diálogo de solicitud de permiso de Microsoft con [!UICONTROL Aceptar] resaltado.](../../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Asignar la aplicación CMK a un rol {#assign-to-role}

Después de completar el proceso de autenticación, vuelva a su [!DNL Azure] Key Vault y seleccione **[!DNL Access control]** en el panel de navegación izquierdo. Desde aquí, seleccione **[!DNL Add]** seguido de **[!DNL Add role assignment]**.

![El tablero de Microsoft Azure con [!DNL Add] y [!DNL Add role assignment] resaltado.](../../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

La siguiente pantalla le pedirá que elija una función para esta asignación. Seleccionar **[!DNL Key Vault Crypto Service Encryption User]** antes de seleccionar **[!DNL Next]** para continuar.

>[!NOTE]
>
>Si tiene el [!DNL Managed-HSM Key Vault] , debe seleccionar la variable **[!DNL Managed HSM Crypto Service Encryption User]** función de usuario.

![El panel de Microsoft Azure con la variable [!DNL Key Vault Crypto Service Encryption User] resaltado.](../../images/governance-privacy-security/customer-managed-keys/select-role.png)

En la pantalla siguiente, elija **[!DNL Select members]** para abrir un cuadro de diálogo en el carril derecho. Utilice la barra de búsqueda para localizar la entidad de seguridad de servicio de la aplicación CMK y seleccionarla en la lista. Cuando termine, seleccione **[!DNL Save]**.

>[!NOTE]
>
>Si no encuentra su aplicación en la lista, no se ha aceptado su entidad de servicio en su inquilino. Para asegurarse de que tiene los privilegios correctos, trabaje con su [!DNL Azure] administrador o representante.

## Habilitar la configuración de clave de cifrado en el Experience Platform {#send-to-adobe}

Después de instalar la aplicación CMK en [!DNL Azure], puede enviar su identificador de clave de cifrado al Adobe. Seleccionar **[!DNL Keys]** en el panel de navegación izquierdo, seguido del nombre de la clave que desea enviar.

![El panel de Microsoft Azure con la variable [!DNL Keys] objeto y el nombre de clave resaltados.](../../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleccione la última versión de la clave y aparecerá su página de detalles. Desde aquí puede configurar de forma opcional las operaciones permitidas para la clave.

>[!IMPORTANT]
>
>Las operaciones mínimas requeridas que se permiten para la clave son las siguientes **[!DNL Wrap Key]** y **[!DNL Unwrap Key]** permisos. Puede incluir [!DNL Encrypt], [!DNL Decrypt], [!DNL Sign], y [!DNL Verify] si quieres.

El **[!UICONTROL Identificador de clave]** El campo muestra el identificador URI de la clave. Copie este valor de URI para utilizarlo en el siguiente paso.

![Los detalles de la clave del panel de Microsoft Azure con la variable [!DNL Permitted operations] y las secciones Copiar URL clave resaltadas.](../../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Una vez que haya obtenido el URI del almacén de claves, puede enviarlo mediante una solicitud del POST al punto de conexión de configuración CMK.

>[!NOTE]
>
>Solo el almacén de claves y el nombre de clave se almacenan con el Adobe, no la versión de la clave.

**Solicitud**

+++ Una solicitud de ejemplo para enviar el URI de almacén de claves al extremo de configuración CMK.

```shell
curl -X POST \
  https://platform.adobe.io/data/infrastructure/manager/customer/config \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -d '{
        "name": "Config1",
        "type": "BYOK_CONFIG",
        "imsOrgId": "{ORG_ID}",
        "configData": {
          "providerType": "AZURE_KEYVAULT",
          "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4"
        }
      }'
```

| Propiedad | Descripción |
| --- | --- |
| `name` | Un nombre para la configuración. Asegúrese de recordar este valor porque es necesario para comprobar el estado de la configuración a las [etapa posterior](#check-status). El valor distingue entre mayúsculas y minúsculas. |
| `type` | El tipo de configuración. Debe definirse en `BYOK_CONFIG`. |
| `imsOrgId` | Su ID de organización. Este ID debe tener el mismo valor que se proporciona en la variable `x-gw-ims-org-id` encabezado. |
| `configData` | Esta propiedad contiene los siguientes detalles sobre la configuración:<ul><li>`providerType`: debe configurarse como `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: URI de almacén de claves que ha copiado [anterior](#send-to-adobe).</li></ul> |

+++

**Respuesta**

+++ La respuesta correcta devuelve los detalles del trabajo de configuración.

```json
{
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "config": {
    "configData": {
      "keyVaultUri": "https://adobecmkexample.vault.azure.net",
      "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
      "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
      "keyName": "Config1",
      "providerType": "AZURE_KEYVAULT"
    },
    "name": "acpcf978863Aaepcmkmultitenantapp",
    "type": "BYOK_CONFIG",
    "imsOrgId": "{ORG_ID}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

+++

El trabajo debe completar el procesamiento en unos minutos.

## Verificar el estado de la configuración {#check-status}

Para comprobar el estado de la solicitud de configuración, puede realizar una solicitud de GET.

**Solicitud**

Debe adjuntar el `name` de la configuración que desea comprobar en la ruta (`config1` en el ejemplo siguiente) e incluya un `configType` parámetro de consulta establecido en `BYOK_CONFIG`.

+++ Una solicitud de ejemplo para comprobar el estado de la solicitud de configuración.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

+++

**Respuesta**

+++ La respuesta correcta devuelve el estado del trabajo.

```json
{
  "name": "acpcf978863Aaepcmkmultitenantapp",
  "type": "BYOK_CONFIG",
  "status": "COMPLETED",
  "configData": {
    "keyVaultUri": "https://adobecmkexample.vault.azure.net",
    "keyVaultKeyIdentifier": "https://adobecmkexample.vault.azure.net/keys/adobeCMK-key/7c1d50lo28234cc895534c00d7eb4eb4",
    "keyVersion": "7c1d50lo28234cc895534c00d7eb4eb4",
    "keyName": "Config1",
    "providerType": "AZURE_KEYVAULT"
  },
  "imsOrgId": "{ORG_ID}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

+++

El `status` puede tener uno de los cuatro valores con los significados siguientes:

1. `RUNNING`: valida que Platform puede acceder a la clave y al almacén de claves.
1. `UPDATE_EXISTING_RESOURCES`: el sistema está agregando el almacén de claves y el nombre de claves a los almacenes de datos en todos los entornos limitados de su organización.
1. `COMPLETED`: el almacén de claves y el nombre de claves se han agregado correctamente a los almacenes de datos.
1. `FAILED`: Se ha producido un problema, relacionado principalmente con la clave, el almacén de claves o la configuración de aplicaciones de varios inquilinos.

## Pasos siguientes

Al completar los pasos anteriores, ha habilitado correctamente CMK para su organización. Los datos que se incorporan a los almacenes de datos principales ahora se cifran y descifran con las claves de su [!DNL Azure] Key Vault. Para obtener más información sobre el cifrado de datos en Adobe Experience Platform, consulte la [documentación de cifrado](../encryption.md).
