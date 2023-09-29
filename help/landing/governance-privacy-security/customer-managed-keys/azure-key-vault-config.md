---
title: Configurar un Azure Key Vault
description: Obtenga información sobre cómo crear una nueva cuenta empresarial con Azure o utilizar una cuenta empresarial existente y crear el almacén de claves.
source-git-commit: a0df05cde19e97d4abdad7abd19eafea8efe1096
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Configuración de un [!DNL Azure] Key Vault

Las claves administradas por el cliente (CMK) solo admiten claves de un [!DNL Microsoft Azure] Key Vault. Para empezar, debe trabajar con [!DNL Azure] para crear una nueva cuenta empresarial o utilice una cuenta empresarial existente y siga los pasos a continuación para crear el almacén de claves.

>[!IMPORTANT]
>
>Solo los niveles de servicio Premium y Standard para [!DNL Azure] Se admiten los Key Vault. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] y [!DNL Azure Payments HSM] no son compatibles. Consulte la [[!DNL Azure] documentación](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) para obtener más información sobre los servicios de administración de claves ofrecidos.

>[!NOTE]
>
>La documentación siguiente solo cubre los pasos básicos para crear Key Vault. Fuera de esta guía, debe configurar el almacén de claves según las políticas de su organización.

Inicie sesión en [!DNL Azure] y utilice la barra de búsqueda para localizar **[!DNL Key vaults]** en la lista de servicios.

![La función de búsqueda en [!DNL Microsoft Azure] con [!DNL Key vaults] resaltado en los resultados de búsqueda.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

El **[!DNL Key vaults]** después de seleccionar el servicio. Desde aquí, seleccione **[!DNL Create]**.

![El [!DNL Key vaults] panel en [!DNL Microsoft Azure] con [!DNL Create] resaltado.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Mediante el formulario proporcionado, rellene los detalles básicos de Key Vault, incluido un nombre y un grupo de recursos asignado.

>[!WARNING]
>
>Aunque la mayoría de las opciones se pueden dejar como valores predeterminados, **asegúrese de activar las opciones de protección de eliminación suave y depuración**. Si no activa estas funciones, podría arriesgarse a perder el acceso a los datos si se elimina el almacén de claves.
>
>![El [!DNL Microsoft Azure] [!DNL Create a Key Vault] flujo de trabajo con protección de eliminación y depuración suave resaltada.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

A partir de aquí, siga con el flujo de trabajo de creación de Key Vault y configure las diferentes opciones según las políticas de su organización.

Una vez que llegue al **[!DNL Review + create]** paso, puede revisar los detalles de Key Vault mientras pasa por la validación. Una vez validada, seleccione **[!DNL Create]** para completar el proceso.

![La página de revisión y creación de Microsoft Azure Key Vaults tiene resaltada la opción Crear.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurar opciones de red {#configure-network-options}

Si Key Vault está configurado para restringir el acceso público a ciertas redes virtuales o deshabilitar por completo el acceso público, debe conceder [!DNL Microsoft] una excepción de cortafuegos.

Seleccionar **[!DNL Networking]** en el panel de navegación izquierdo. En **[!DNL Firewalls and virtual networks]**, seleccione la casilla de verificación **[!DNL Allow trusted Microsoft services to bypass this firewall]**, luego seleccione **[!DNL Apply]**.

![El [!DNL Networking] pestaña de [!DNL Microsoft Azure] con [!DNL Networking] y [!DNL Allow trusted Microsoft surfaces to bypass this firewall] excepción resaltada.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generar una clave {#generate-a-key}

Una vez creado un almacén de claves, puede generar una clave nueva. Vaya a **[!DNL Keys]** y seleccione **[!DNL Generate/Import]**.

![El [!DNL Keys] pestaña de [!DNL Azure] con [!DNL Generate import] resaltado.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Utilice el formulario proporcionado para proporcionar un nombre para la clave y seleccione **RSA** para el tipo de clave. Como mínimo, la variable **[!DNL RSA key size]** debe ser al menos **3072** bits según lo requerido por [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] también es compatible con RSA 3027.

>[!NOTE]
>
>Recuerde el nombre que proporciona para la clave, ya que es necesario enviar la clave al Adobe.

Utilice los controles restantes para configurar la clave que desee generar o importar. Cuando termine, seleccione **[!DNL Create]**.

![El panel Crear una clave con [!DNL 3072] bits resaltados.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La clave configurada aparece en la lista de claves del almacén.

![El [!DNL Keys] espacio de trabajo con el nombre de clave resaltado.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Pasos siguientes

Para continuar con el proceso único de configuración de la función de claves administradas por el cliente, continúe con el [API](./api-set-up.md) o [IU](./ui-set-up.md) guías de configuración de claves administradas por el cliente.
