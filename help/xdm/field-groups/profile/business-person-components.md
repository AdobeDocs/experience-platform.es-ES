---
title: Grupo de campos de esquema de componentes de persona empresarial XDM
description: Este documento proporciona una descripción general del grupo de campos de esquema de componentes de persona empresarial XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: b5cdd72238f7b4519de1c789f4294b9698415327
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 3%

---

# [!UICONTROL XDM Business Person ] Componentes Grupo de campos de esquema (Beta)

>[!IMPORTANT]
>
>Este grupo de campos está disponible como parte de la Plataforma de datos de clientes en tiempo real B2B Edition, que actualmente está en versión beta. La documentación y la funcionalidad están sujetas a cambios.

[!UICONTROL Los ] componentes de persona empresarial XDM son un grupo de campos de esquema estándar para la  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) clase que captura varios registros de origen para una persona y otros atributos que son necesarios para la segmentación de personas.

Cuando se crea un perfil para una persona a través de [Perfil del cliente en tiempo real](../../../profile/home.md) en la edición B2B de CDP en tiempo real, la información utilizada para crear ese perfil puede provenir potencialmente de muchos registros de origen. Por ejemplo, si una persona trabaja para dos empresas diferentes, muchos sistemas CRM crearían una copia duplicada intencionalmente de esa persona, de modo que una copia esté vinculada a la Empresa A, mientras que la otra esté vinculada a la Empresa B. Al introducir esos datos en Adobe Experience Platform, este grupo de campos se utiliza para combinar esos diferentes registros de origen en una sola representación.

El grupo de campos proporciona un campo `personComponents` de nivel raíz, que es una matriz de objetos. Cada objeto de la matriz representa un registro de origen diferente.

![](../../images/field-groups/business-person-components.png)

| Propiedad | Tipo de datos | Descripción |
| --- | --- | --- |
| `sourceAccountKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la cuenta asociada a la persona. |
| `sourceConvertedContactKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Un identificador compuesto para el contacto relacionado si este posible cliente se ha convertido. |
| `sourceExternalKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto del sistema de origen desde el que se originaron los datos de la persona. |
| `sourcePersonKey` | [[!UICONTROL Fuente B2B]](../../data-types/b2b-source.md) | Identificador compuesto de la persona. |
| `workEmail` | [[!UICONTROL Dirección de correo electrónico]](../../data-types/b2b-source.md) | El ID de correo electrónico de trabajo de la persona. |
| `personGroupID` | Cadena | Identificador de grupo de la persona. |
| `personScore` | Cadena | Puntuación generada para la persona por un sistema CRM. |
| `personSource` | Cadena | Identificador único basado en cadenas para el sistema de origen desde el que se originaron los datos de la persona. |
| `personStatus` | Cadena | El estado actual de marketing o ventas de la persona. |
| `personType` | Cadena | Tipo de persona en un contexto B2B. |
| `sourceAccountID` | Cadena | Identificador único basado en cadenas para la cuenta en el sistema de origen asociado a la persona. Este campo se utiliza como clave externa por el sistema para buscar las diferentes empresas para las que esta persona trabaja. |
| `sourceConvertedContactID` | Cadena | Identificador único basado en cadenas para el contacto relacionado si se convirtió este posible cliente. |
| `sourceExternalID` | Cadena | Identificador único basado en cadenas para el sistema de origen desde el que se originaron los datos de la persona. |
| `sourcePersonID` | Cadena | Identificador exclusivo basado en cadenas para la persona. |

{style=&quot;table-layout:auto&quot;}

Para obtener más información sobre el grupo de campos, consulte el repositorio XDM público:

* [Ejemplo rellenado](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-components.schema.json)
