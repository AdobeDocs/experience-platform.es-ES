---
title: Grupo de campos de esquema de componentes de persona de negocio XDM
description: Obtenga información acerca del grupo de campos de esquema Componentes de persona de negocio XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 2%

---

# [!UICONTROL Componentes de persona empresarial de XDM] grupo de campos de esquema

[!UICONTROL Componentes de persona empresarial de XDM] es un grupo de campos de esquema estándar para [[!DNL XDM Individual Profile] clase](../../classes/individual-profile.md) que captura varios registros de origen para una persona y otros atributos necesarios para la segmentación de personas.

Cuando se crea un perfil para una persona mediante [Perfil del cliente en tiempo real](../../../profile/home.md) en la edición B2B de Real-Time CDP, la información utilizada para crear ese perfil puede provenir potencialmente de muchos registros de origen. Por ejemplo, si una persona trabaja para dos empresas diferentes, muchos sistemas CRM crearían una copia duplicada intencionalmente de esa persona para que una copia esté vinculada a la compañía A, mientras que la otra está vinculada a la compañía B. Al llevar esos datos a Adobe Experience Platform, este grupo de campos se utiliza para combinar esos registros de origen diferentes en una sola representación.

El grupo de campos proporciona un nivel de raíz `personComponents` , que es una matriz de objetos. Cada objeto de la matriz representa un registro de origen diferente.

>[!IMPORTANT]
>
>Debe seguir los patrones de ingesta tal como se describe en la [documentación de orígenes](../../../rtcdp/sources/b2b.md). No se garantiza que funcionen otros métodos de asignación de campos.
>
>Por ejemplo, cada objeto del `personComponents` La matriz se envía individualmente durante los patrones de ingesta estándar y luego Platform la agrega a la matriz. Si se agrega manualmente una matriz de objetos al componente Persona de negocios, se devolverá un error.
>Debe utilizar la utilidad de generación automática al crear esquemas para los datos B2B. Consulte la documentación para obtener instrucciones sobre cómo utilizar el [Utilidad de generación automática de esquemas y área de nombres B2B](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Si no utiliza la utilidad de generación automática y tiene intención de asignar manualmente el modelo de datos, asegúrese de leer la documentación de [Clases XDM de Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/schemas/b2b.md) antes de asignar los datos.
>
>Consulte la [tutorial de extremo a extremo](../../../rtcdp/b2b-tutorial.md) para obtener información sobre los flujos de trabajo recomendados para los datos B2B.

![](../../images/field-groups/business-person-components.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la cuenta asociada con la persona. |
| `sourceConvertedContactKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para el contacto relacionado si se convirtió este posible cliente. |
| `sourceExternalKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para el sistema de origen desde el que se originaron los datos de la persona. |
| `sourcePersonKey` | [[!UICONTROL Origen B2B]](../../data-types/b2b-source.md) | Un identificador compuesto de la persona. |
| `workEmail` | [[!UICONTROL Correo electrónico]](../../data-types/b2b-source.md) | El ID de correo electrónico de trabajo de la persona. |
| `personGroupID` | Cadena | Un identificador de grupo de la persona. |
| `personScore` | Cadena | Una puntuación generada para la persona por un sistema CRM. |
| `personSource` | Cadena | Un identificador único basado en cadenas para el sistema de origen desde el que se originaron los datos de la persona. |
| `personStatus` | Cadena | El estado actual de marketing o ventas de la persona. |
| `personType` | Cadena | El tipo de persona en un contexto B2B. |
| `sourceAccountID` | Cadena | Un identificador único basado en cadenas para la cuenta en el sistema de origen asociado con la persona. El sistema utiliza este campo como clave externa para buscar las distintas compañías para las que trabaja esta persona. |
| `sourceConvertedContactID` | Cadena | Identificador único basado en cadenas para el contacto relacionado si se convirtió este posible cliente. |
| `sourceExternalID` | Cadena | Identificador único basado en cadenas del sistema de origen desde el que se originaron los datos de la persona. |
| `sourcePersonID` | Cadena | Un identificador único basado en cadenas para la persona. |

{style="table-layout:auto"}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo completado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
