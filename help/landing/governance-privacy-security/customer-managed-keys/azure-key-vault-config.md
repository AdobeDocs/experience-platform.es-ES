---
title: Configurar un Azure Key Vault
description: Obtenga información sobre cómo crear una nueva cuenta empresarial con Azure o utilizar una cuenta empresarial existente y crear el almacén de claves.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# Configurar un almacén de claves [!DNL Azure]

Las claves administradas por el cliente (CMK) solo admiten claves de un almacén de claves de [!DNL Microsoft Azure]. Para comenzar, debe trabajar con [!DNL Azure] para crear una nueva cuenta empresarial o usar una cuenta empresarial existente y seguir los pasos a continuación para crear el almacén de claves.

>[!IMPORTANT]
>
>Solo se admiten los niveles Standard, Premium y Managed HSM para [!DNL Azure] Key Vault. [!DNL Azure Dedicated HSM] y [!DNL Azure Payments HSM] no son compatibles. Consulte la [[!DNL Azure] documentación](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) para obtener más información sobre los servicios de administración de claves que se ofrecen.

>[!NOTE]
>
>La documentación siguiente solo cubre los pasos básicos para crear Key Vault. Fuera de esta guía, debe configurar el almacén de claves según las políticas de su organización.

Inicie sesión en el portal [!DNL Azure] y utilice la barra de búsqueda para encontrar **[!DNL Key vaults]** en la lista de servicios.

![Característica de búsqueda en [!DNL Microsoft Azure] con [!DNL Key vaults] resaltada en los resultados de búsqueda.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

La página **[!DNL Key vaults]** aparece después de seleccionar el servicio. Desde aquí, seleccione **[!DNL Create]**.

![El panel [!DNL Key vaults] de [!DNL Microsoft Azure] con [!DNL Create] resaltado.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Mediante el formulario proporcionado, rellene los detalles básicos de Key Vault, incluido un nombre y un grupo de recursos asignado.

>[!WARNING]
>
>Aunque la mayoría de las opciones se pueden dejar como valores predeterminados, **asegúrese de habilitar las opciones de protección de eliminación suave y purga**. Si no activa estas funciones, podría arriesgarse a perder el acceso a los datos si se elimina el almacén de claves.
>
>![Flujo de trabajo [!DNL Microsoft Azure] [!DNL Create a Key Vault] con protección de eliminación y purga suave resaltada.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

A partir de aquí, siga con el flujo de trabajo de creación de Key Vault y configure las diferentes opciones según las políticas de su organización.

Una vez que llegue al paso **[!DNL Review + create]**, puede revisar los detalles de Key Vault mientras pasa por la validación. Una vez superada la validación, seleccione **[!DNL Create]** para completar el proceso.

![La página de Microsoft Azure Key Vaults Revise y cree una página con la opción Crear resaltada.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configuración del acceso {#configure-access}

A continuación, habilite el control de acceso basado en funciones de Azure para su almacén de claves. Seleccione **[!DNL Access configuration]** en la sección [!DNL Settings] de la navegación izquierda y, a continuación, seleccione **[!DNL Azure role-based access control]** para habilitar la configuración. Este paso es esencial, ya que la aplicación CMK debe asociarse posteriormente a un rol de Azure. La asignación de una función está documentada en los flujos de trabajo [API](./api-set-up.md#assign-to-role) y [UI](./ui-set-up.md#assign-to-role).

![Se resaltó el panel [!DNL Microsoft Azure] con [!DNL Access configuration] y [!DNL Azure role-based access control].](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurar opciones de red {#configure-network-options}

Si Key Vault está configurado para restringir el acceso público a ciertas redes virtuales o deshabilitar por completo el acceso público, debe conceder a [!DNL Microsoft] una excepción de firewall.

Seleccione **[!DNL Networking]** en el panel de navegación izquierdo. En **[!DNL Firewalls and virtual networks]**, active la casilla de verificación **[!DNL Allow trusted Microsoft services to bypass this firewall]** y, a continuación, seleccione **[!DNL Apply]**.

![Se resaltó la ficha [!DNL Networking] de [!DNL Microsoft Azure] con la excepción [!DNL Networking] y [!DNL Allow trusted Microsoft surfaces to bypass this firewall].](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Generar una clave {#generate-a-key}

Una vez creado un almacén de claves, puede generar una clave nueva. Vaya a la ficha **[!DNL Keys]** y seleccione **[!DNL Generate/Import]**.

![La ficha [!DNL Keys] de [!DNL Azure] con [!DNL Generate import] resaltado.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Use el formulario proporcionado para proporcionar un nombre para la clave y seleccione **RSA** o **RSA-HSM** para el tipo de clave. Como mínimo, **[!DNL RSA key size]** debe tener al menos **3072** bits, tal como lo requiere [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] también es compatible con RSA 3027.

>[!NOTE]
>
>Recuerde el nombre que proporciona para la clave, ya que es necesario enviar la clave al Adobe.

Utilice los controles restantes para configurar la clave que desee generar o importar. Cuando termine, seleccione **[!DNL Create]**.

![Panel [!DNL Create a key] con [!DNL 3072] bits resaltados.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

La clave configurada aparece en la lista de claves del almacén.

![Espacio de trabajo [!DNL Keys] con el nombre de clave resaltado.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Pasos siguientes

Para continuar con el proceso único de configuración de la característica de claves administradas por el cliente, continúa con las guías de configuración de claves administradas por el cliente de [API](./api-set-up.md) o de [IU](./ui-set-up.md).
