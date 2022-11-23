---
title: Claves gestionadas por el cliente en Adobe Experience Platform
description: Aprenda a configurar sus propias claves de cifrado para los datos almacenados en Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: 47b3de5035f93f8a4288a0fec0a9111a979d7442
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 1%

---

# Claves gestionadas por el cliente en Adobe Experience Platform

Los datos almacenados en Adobe Experience Platform se cifran en reposo mediante claves a nivel de sistema. Si utiliza una aplicación creada sobre Platform, puede optar por utilizar sus propias claves de cifrado, lo que le otorga un bueno control sobre la seguridad de los datos.

Este documento cubre el proceso para habilitar la función de claves gestionadas por el cliente (CMK) en Platform.

## Requisitos previos

Para habilitar CMK, su [!DNL Azure] Key Vault debe configurarse con la siguiente configuración:

* [Habilitar protección de depuración](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar eliminación suave](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configuración del acceso mediante [!DNL Azure] control de acceso basado en roles](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

## Resumen del proceso

CMK está incluido en el Escudo de la Salud y en las ofertas del Escudo de la privacidad y la seguridad del Adobe. Una vez que su organización haya adquirido una licencia para una de estas ofertas, puede iniciar un proceso único para configurar la función.

>[!WARNING]
>
>Después de configurar CMK, no puede revertir a claves administradas por el sistema. Usted es responsable de administrar sus claves de forma segura y de proporcionar acceso a su aplicación Key Vault, Key y CMK dentro de [!DNL Azure] para evitar perder acceso a sus datos.

El proceso es el siguiente:

1. [Configure un [!DNL Azure] Key Vault](#create-key-vault) en función de las políticas de su organización, [generar una clave de cifrado](#generate-a-key) que en última instancia se compartirá con Adobe.
1. Uso de llamadas de API para [configuración de la aplicación CMK](#register-app) con su [!DNL Azure] inquilino.
1. Uso de llamadas de API para [enviar su ID de clave de cifrado a Adobe](#send-to-adobe) e inicie el proceso de habilitación de la función.
1. [Comprobar el estado de la configuración](#check-status) para verificar si se ha habilitado CMK.

Una vez completado el proceso de configuración, todos los datos introducidos en Platform en todos los entornos limitados se cifrarán con su [!DNL Azure] configuración de claves. Para utilizar CMK, aprovechará [!DNL Microsoft Azure] que pueden formar parte de sus [programa de vista previa pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Configure un [!DNL Azure] Key Vault {#create-key-vault}

CMK solo admite claves de un [!DNL Microsoft Azure] Key Vault. Para empezar, debe trabajar con [!DNL Azure] para crear una nueva cuenta de empresa, o utilice una cuenta de empresa existente y siga los pasos a continuación para crear Key Vault.

>[!IMPORTANT]
>
>Solo los niveles de servicio Premium y Standard para [!DNL Azure] Se admite Key Vault. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] y [!DNL Azure Payments HSM] no son compatibles. Consulte la [[!DNL Azure] documentación](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) para obtener más información sobre los servicios de administración clave ofrecidos.

>[!NOTE]
>
>La siguiente documentación solo cubre los pasos básicos para crear la bóveda de claves. Fuera de esta guía, debe configurar el almacén de claves según las políticas de su organización.

Inicie sesión en la [!DNL Azure] portal y utilice la barra de búsqueda para localizar **[!DNL Key vaults]** en la lista de servicios.

![Buscar y seleccionar bóvedas clave](../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

La variable **[!DNL Key vaults]** aparece después de seleccionar el servicio. Desde aquí, seleccione **[!DNL Create]**.

![Crear almacén de claves](../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Mediante el formulario proporcionado, rellene los detalles básicos del almacén de claves, incluidos un nombre y un grupo de recursos asignado.

>[!WARNING]
>
>Mientras que la mayoría de las opciones se pueden dejar como valores predeterminados, **asegúrese de habilitar las opciones de protección de eliminación y depuración de software**. Si no activa estas funciones, puede correr el riesgo de perder el acceso a los datos si se elimina el almacén de claves.
>
>![Habilitar protección de depuración](../images/governance-privacy-security/customer-managed-keys/basic-config.png)

A partir de aquí, continúe con el flujo de trabajo de creación de bóvedas de claves y configure las diferentes opciones según las políticas de su organización.

Una vez que llegue al **[!DNL Review + create]** , puede revisar los detalles del almacén de claves mientras pasa por la validación. Una vez aprobada la validación, seleccione **[!DNL Create]** para completar el proceso.

![Configuración básica del almacén de claves](../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

### Configurar las opciones de red

Si el almacén de claves está configurado para restringir el acceso público a ciertas redes virtuales o deshabilitar el acceso público por completo, debe conceder a Microsoft una excepción de firewall.

Select **[!DNL Networking]** en el panel de navegación izquierdo. En **[!DNL Firewalls and virtual networks]**, seleccione la casilla de verificación **[!DNL Allow trusted Microsoft services to bypass this firewall]** y, a continuación, seleccione **[!DNL Apply]**.

![Configuración básica del almacén de claves](../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generar una clave {#generate-a-key}

Una vez creado un almacén de claves, puede generar una clave nueva. Vaya a la **[!DNL Keys]** y seleccione **[!DNL Generate/Import]**.

![Generar una clave](../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilice el formulario proporcionado para proporcionar un nombre para la clave y seleccione **RSA** para el tipo de clave. Como mínimo, la variable **[!DNL RSA key size]** debe ser **3072** bits requeridos por [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] también es compatible con RSA 3027.

>[!NOTE]
>
>Recuerde el nombre que proporcione para la clave, ya que se utilizará en un paso posterior cuando [envío de la clave al Adobe](#send-to-adobe).

Utilice los controles restantes para configurar la clave que desee generar o importar. Cuando termine, seleccione **[!DNL Create]**.

![Configurar clave](../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La clave configurada aparece en la lista de claves del almacén.

![Clave añadida](../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Configuración de la aplicación CMK {#register-app}

Una vez que tenga configurado el almacén de claves, el siguiente paso es registrarse en la aplicación CMK que se vinculará a su [!DNL Azure] inquilino.

### Primeros pasos

El registro de la aplicación CMK requiere que realice llamadas a las API de Platform. Para obtener más información sobre cómo recopilar los encabezados de autenticación necesarios para realizar estas llamadas, consulte la [Guía de autenticación de API de plataforma](../../landing/api-authentication.md).

Mientras que la guía de autenticación proporciona instrucciones sobre cómo generar su propio valor único para el `x-api-key` encabezado de solicitud, todas las operaciones de API de esta guía utilizan el valor estático `acp_provisioning` en su lugar. Debe proporcionar sus propios valores para `{ACCESS_TOKEN}` y `{ORG_ID}`, sin embargo.

En todas las llamadas de API que se muestran en esta guía, `platform.adobe.io` se usa como ruta raíz, que toma como valor predeterminado la región de VA7. Si su organización utiliza una región diferente, `platform` debe ir seguido de un guión y del código de región asignado a su organización: `nld2` para NLD2 o `aus5` para AUS5 (por ejemplo: `platform-aus5.adobe.io`). Si no conoce la región de su organización, póngase en contacto con el administrador del sistema.

### Buscar una URL de autenticación

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

Una respuesta correcta devuelve un valor `applicationRedirectUrl` , que contiene la dirección URL de autenticación.

```json
{
    "id": "byok",
    "name": "acpebae9422Caepcmkmultitenantapp",
    "applicationUri": "https://adobe.com/acpebae9422Caepcmkmultitenantapp",
    "applicationId": "e463a445-c6ac-4ca2-b36a-b5146fcf6a52",
    "applicationRedirectUrl": "https://login.microsoftonline.com/common/oauth2/authorize?response_type=code&client_id=e463a445-c6ac-4ca2-b36a-b5146fcf6a52&redirect_uri=https://adobe.com/acpebae9422Caepcmkmultitenantapp&scope=user.read"
}
```

Copie y pegue el `applicationRedirectUrl` en un navegador para abrir un cuadro de diálogo de autenticación. Select **[!DNL Accept]** para agregar la entidad de seguridad del servicio de aplicaciones CMK al [!DNL Azure] inquilino.

![Aceptar solicitud de permiso](../images/governance-privacy-security/customer-managed-keys/app-permission.png)

### Asignar la aplicación CMK a una función {#assign-to-role}

Después de completar el proceso de autenticación, vuelva a su [!DNL Azure] Key Vault y seleccione **[!DNL Access control]** en el panel de navegación izquierdo. Desde aquí, seleccione **[!DNL Add]** seguido de **[!DNL Add role assignment]**.

![Agregar asignación de funciones](../images/governance-privacy-security/customer-managed-keys/add-role-assignment.png)

La siguiente pantalla le pedirá que elija una función para esta asignación. Select **[!DNL Key Vault Crypto Service Encryption User]** antes de seleccionar **[!DNL Next]** para continuar.

![Seleccionar función](../images/governance-privacy-security/customer-managed-keys/select-role.png)

En la siguiente pantalla, seleccione **[!DNL Select members]** para abrir un cuadro de diálogo en el carril derecho. Utilice la barra de búsqueda para localizar la entidad de seguridad de servicio de la aplicación CMK y selecciónela en la lista. Cuando termine, seleccione **[!DNL Save]**.

>[!NOTE]
>
>Si no encuentra la aplicación en la lista, la entidad de seguridad del servicio no se ha aceptado en el inquilino. Trabaje con su [!DNL Azure] administrador o representante para asegurarse de que dispone de los privilegios correctos.

## Habilitar la configuración de clave de cifrado en el Experience Platform {#send-to-adobe}

Después de instalar la aplicación CMK en [!DNL Azure], puede enviar el identificador de la clave de cifrado a Adobe. Select **[!DNL Keys]** en el panel de navegación izquierdo, seguido del nombre de la clave que desea enviar.

![Seleccionar clave](../images/governance-privacy-security/customer-managed-keys/select-key.png)

Seleccione la última versión de la clave y aparecerá su página de detalles. Desde aquí puede configurar opcionalmente las operaciones permitidas para la clave. Como mínimo, se debe conceder la clave **[!DNL Wrap Key]** y **[!DNL Unwrap Key]** permisos.

La variable **[!UICONTROL Identificador de clave]** muestra el identificador de URI de la clave. Copie este valor de URI para utilizarlo en el siguiente paso.

![Copiar URL de clave](../images/governance-privacy-security/customer-managed-keys/copy-key-url.png)

Una vez obtenido el URI de almacén de claves, puede enviarlo mediante una solicitud de POST al extremo de configuración CMK.

>[!NOTE]
>
>Solo el almacén de claves y el nombre de clave se almacenan con Adobe, no con la versión de clave.

**Solicitud**

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
| `name` | Un nombre para la configuración. Asegúrese de recordar este valor, ya que será necesario para comprobar el estado de la configuración en una [paso posterior](#check-status). El valor distingue entre mayúsculas y minúsculas. |
| `type` | El tipo de configuración. Debe definirse en `BYOK_CONFIG`. |
| `imsOrgId` | Su ID de la organización IMS. Debe ser el mismo valor que se proporciona en la variable `x-gw-ims-org-id` encabezado. |
| `configData` | Contiene los siguientes detalles sobre la configuración:<ul><li>`providerType`: Debe definirse en `AZURE_KEYVAULT`.</li><li>`keyVaultKeyIdentifier`: El URI de almacén de claves que ha copiado [previous](#send-to-adobe).</li></ul> |

**Respuesta**

Una respuesta correcta devuelve los detalles del trabajo de configuración.

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
    "imsOrgId": "{IMS_ORG}",
    "status": "NEW"
  },
  "status": "CREATED"
}
```

El trabajo debe completar el procesamiento en unos minutos.

## Compruebe el estado de la configuración {#check-status}

Para comprobar el estado de la solicitud de configuración, puede realizar una solicitud de GET.

**Solicitud**

Debe adjuntar la variable `name` de la configuración que desea comprobar a la ruta (`config1` en el ejemplo siguiente) e incluya un `configType` parámetro de consulta establecido en `BYOK_CONFIG`.

```shell
curl -X GET \
  https://platform.adobe.io/data/infrastructure/manager/customer/config/config1?configType=BYOK_CONFIG \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: acp_provisioning' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Respuesta**

Una respuesta correcta devuelve el estado del trabajo.

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
  "imsOrgId": "{IMS_ORG}",
  "subscriptionId": "cf978863-7325-47b1-8fd9-554b9fdb6c36",
  "id": "4df7886b-a122-4391-880b-47888d5c5b92",
  "rowType": "BYOK_KEY"
}
```

La variable `status` puede tener uno de estos cuatro valores con los siguientes significados:

1. `RUNNING`: Valida que Platform tiene la capacidad de acceder a la clave y al almacén de claves.
1. `UPDATE_EXISTING_RESOURCES`: El sistema está agregando el nombre de clave y la bóveda de claves a los almacenes de datos en todos los entornos limitados de su organización.
1. `COMPLETED`: Se han añadido el almacén de claves y el nombre de clave a los almacenes de datos.
1. `FAILED`: Se ha producido un problema, principalmente relacionado con la clave, el almacén de claves o la configuración de la aplicación de varios inquilinos.

## Pasos siguientes

Al completar los pasos anteriores, habilitó correctamente CMK para su organización. Los datos introducidos en Platform ahora se cifrarán y descifrarán mediante las claves incluidas en su [!DNL Azure] Key Vault. Si desea revocar el acceso de Platform a sus datos, puede quitar la función de usuario asociada con la aplicación del almacén de claves dentro de [!DNL Azure].

Después de deshabilitar el acceso a la aplicación, puede tardar entre unos minutos y 24 horas en que los datos ya no estén accesibles en Platform. El mismo retraso se aplica para que los datos vuelvan a estar disponibles cuando se vuelva a habilitar el acceso a la aplicación.

>[!WARNING]
>
>Una vez que la aplicación Key Vault, Key o CMK esté deshabilitada y ya no se pueda acceder a los datos en Platform, ya no será posible realizar ninguna operación descendente relacionada con esos datos. Asegúrese de comprender los impactos descendentes de la revocación del acceso de Platform a sus datos antes de realizar cambios en la configuración.
