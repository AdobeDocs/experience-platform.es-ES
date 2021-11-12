---
title: Grupo de campos de esquema de componentes de persona empresarial XDM
description: Este documento proporciona una descripción general del grupo de campos de esquema de componentes de persona empresarial XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: edf7afc5db219430232a3226dc691570b50a32bd
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 3%

---

# [!UICONTROL Componentes de persona empresarial XDM] grupo de campos de esquema

[!UICONTROL Componentes de persona empresarial XDM] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) que captura varios registros de origen para una persona y otros atributos necesarios para la segmentación de personas.

Cuando se crea un perfil para una persona mediante [Perfil del cliente en tiempo real](../../../profile/home.md) en la edición B2B de CDP en tiempo real, la información utilizada para crear ese perfil puede provenir potencialmente de muchos registros de origen. Por ejemplo, si una persona trabaja para dos empresas diferentes, muchos sistemas CRM crearían una copia duplicada intencionalmente de esa persona, de modo que una copia esté vinculada a la Empresa A, mientras que la otra esté vinculada a la Empresa B. Al introducir esos datos en Adobe Experience Platform, este grupo de campos se utiliza para combinar esos diferentes registros de origen en una sola representación.

El grupo de campos proporciona un nivel raíz `personComponents` , que es una matriz de objetos. Cada objeto de la matriz representa un registro de origen diferente.

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
