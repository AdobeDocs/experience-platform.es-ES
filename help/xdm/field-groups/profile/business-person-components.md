---
title: Grupo de campos de esquema de componentes de persona empresarial XDM
description: Este documento proporciona una descripción general del grupo de campos de esquema de componentes de persona empresarial XDM.
exl-id: 965b89f4-59f5-43f4-8778-3549e15b44d4
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 2%

---

# [!UICONTROL Componentes de persona empresarial XDM] grupo de campos de esquema

[!UICONTROL Componentes de persona empresarial XDM] es un grupo de campos de esquema estándar para la variable [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) que captura varios registros de origen para una persona y otros atributos necesarios para la segmentación de personas.

Cuando se crea un perfil para una persona mediante [Perfil del cliente en tiempo real](../../../profile/home.md) en la edición B2B de Real-Time CDP, la información utilizada para crear ese perfil puede provenir potencialmente de muchos registros de origen. Por ejemplo, si una persona trabaja para dos empresas diferentes, muchos sistemas CRM crearían una copia duplicada intencionalmente de esa persona, de modo que una copia esté vinculada a la Empresa A, mientras que la otra esté vinculada a la Empresa B. Al introducir esos datos en Adobe Experience Platform, este grupo de campos se utiliza para combinar esos diferentes registros de origen en una sola representación.

El grupo de campos proporciona un nivel raíz `personComponents` , que es una matriz de objetos. Cada objeto de la matriz representa un registro de origen diferente.

>[!IMPORTANT]
>
>Debe seguir los patrones de ingesta como se describe en la sección [documentación de fuentes](../../../rtcdp/sources/b2b.md). No se garantiza que funcionen otros métodos de asignación de campos.
>
>Por ejemplo, cada objeto de la variable `personComponents` la matriz se envía de forma individual durante los patrones de ingesta estándar y, a continuación, Platform la agrega a la matriz. Si se agrega manualmente una matriz de objetos al componente de persona comercial, se devolverá un error.
>Debe utilizar la utilidad de generación automática al crear esquemas para los datos B2B. Consulte la documentación para obtener instrucciones sobre cómo utilizar la variable [Área de nombres B2B y utilidad de generación automática de esquemas](../../../sources/connectors/adobe-applications/marketo/marketo-namespaces.md). Si no utiliza la utilidad de generación automática y desea asignar manualmente el modelo de datos, asegúrese de leer la documentación en la [Clases XDM de Adobe Real-time Customer Data Platform B2B Edition](../../../rtcdp/schemas/b2b.md) antes de asignar los datos.
>
>Consulte la [tutorial completo](../../../rtcdp/b2b-tutorial.md) para obtener información sobre los flujos de trabajo recomendados para datos B2B.

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
