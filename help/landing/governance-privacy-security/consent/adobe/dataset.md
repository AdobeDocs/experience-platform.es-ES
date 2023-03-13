---
keywords: Experience Platform;inicio;temas populares
solution: Experience Platform
title: Configurar un conjunto de datos para capturar datos de consentimiento y preferencia
description: Obtenga información sobre cómo configurar un esquema y un conjunto de datos del Modelo de datos de experiencia (XDM) para capturar datos de consentimiento y preferencia en Adobe Experience Platform.
exl-id: 61ceaa2a-c5ac-43f5-b118-502bdc432234
source-git-commit: 5a14eb5938236fa7186d1a27f28cee15fe6558f6
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Configurar un conjunto de datos para capturar datos de consentimiento y preferencia

Para que Adobe Experience Platform procese los datos de consentimiento/preferencia del cliente, esos datos deben enviarse a un conjunto de datos cuyo esquema contenga campos relacionados con consentimientos y otros permisos. Específicamente, este conjunto de datos debe basarse en [!DNL XDM Individual Profile] y habilitado para su uso en [!DNL Real-Time Customer Profile].

Este documento proporciona información sobre los pasos necesarios para configurar un conjunto de datos para procesar los datos de consentimiento en Experience Platform. Para obtener una descripción general del flujo de trabajo completo para procesar los datos de consentimiento/preferencia en Platform, consulte la [resumen del procesamiento de consentimiento](./overview.md).

>[!IMPORTANT]
>
>Los ejemplos de esta guía utilizan un conjunto estandarizado de campos para representar los valores de consentimiento del cliente, tal como se definen en la variable [[!UICONTROL Detalles de consentimiento y preferencia] grupo de campos de esquema](../../../../xdm/field-groups/profile/consents.md). La estructura de estos campos pretende proporcionar un modelo de datos eficiente para cubrir muchos casos de uso comunes de recopilación de consentimiento.
>
>Sin embargo, también puede definir sus propios grupos de campos para representar el consentimiento según sus propios modelos de datos. Consulte con su equipo legal para obtener la aprobación de un modelo de datos de consentimiento que se ajuste a sus necesidades comerciales, en función de las siguientes opciones:
>
>* El grupo de campos de consentimiento estandarizado
>* Un grupo de campos de consentimiento personalizado creado por su organización
>* Una combinación del grupo de campos de consentimiento estandarizado y los campos adicionales proporcionados por un grupo de campos de consentimiento personalizado


## Requisitos previos

Este tutorial requiere una comprensión práctica de los siguientes componentes de Adobe Experience Platform:

* [Modelo de datos de experiencia (XDM)](../../../../xdm/home.md): El marco estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de experiencia del cliente.
   * [Conceptos básicos de composición de esquemas](../../../../xdm/schema/composition.md): Obtenga información acerca de los componentes básicos de los esquemas XDM.
* [Perfil del cliente en tiempo real](../../../../profile/home.md): consolida los datos de clientes de diferentes fuentes en una vista completa y unificada, a la vez que ofrece una cuenta procesable con marca de tiempo de cada interacción de clientes.

>[!IMPORTANT]
>
>En este tutorial se da por hecho que conoce el [!DNL Profile] esquema en Platform que desea utilizar para capturar información de atributos del cliente. Independientemente del método que utilice para recopilar datos de consentimiento, este esquema debe ser [habilitado para Perfil del cliente en tiempo real](../../../../xdm/ui/resources/schemas.md#profile). Además, la identidad principal del esquema no puede ser un campo directamente identificable que esté prohibido utilizar en publicidad basada en intereses, como una dirección de correo electrónico. Consulte a su asesor legal si no está seguro de qué campos están restringidos.

## [!UICONTROL Detalles de consentimiento y preferencia] estructura del grupo de campos {#structure}

El [!UICONTROL Detalles de consentimiento y preferencia] grupo de campos proporciona campos de consentimiento estandarizados a un esquema. Actualmente, este grupo de campos solo es compatible con esquemas basados en la variable [!DNL XDM Individual Profile] clase.

El grupo de campos proporciona un único campo de tipo de objeto, `consents`, cuyas subpropiedades capturan un conjunto de campos de consentimiento estandarizados. El siguiente JSON es un ejemplo del tipo de datos `consents` espera tras la ingesta de datos:

```json
{
  "consents": {
    "collect": {
      "val": "y",
    },
    "share": {
      "val": "y",
    },
    "personalize": {
      "content": {
        "val": "y"
      }
    },
    "marketing": {
      "preferred": "email",
      "any": {
        "val": "y"
      },
      "push": {
        "val": "n",
        "reason": "Too Frequent",
        "time": "2019-01-01T15:52:25+00:00"
      }
    },
    "idSpecific": {
      "email": {
        "jdoe@example.com": {
          "marketing": {
            "email": {
              "val": "n"
            }
          }
        }
      }
    }
  },
  "metadata": {
    "time": "2019-01-01T15:52:25+00:00"
  }
}
```

>[!NOTE]
>
>Para obtener más información sobre la estructura y el significado de las subpropiedades en `consents`, consulte la información general de la [[!UICONTROL Detalles de consentimiento y preferencia] grupo de campos](../../../../xdm/field-groups/profile/consents.md).

## Añada los grupos de campos requeridos a su [!DNL Profile] esquema {#add-field-group}

Para recopilar datos de consentimiento mediante el estándar de Adobe, debe tener un esquema habilitado para el perfil que contenga los dos grupos de campos siguientes:

* [!UICONTROL Detalles de consentimiento y preferencia]
* [!UICONTROL IdentityMap] (necesario si se utiliza el SDK web o móvil de Platform para enviar señales de consentimiento)

En la IU de Platform, seleccione **[!UICONTROL Esquemas]** en el panel de navegación izquierdo, seleccione la opción **[!UICONTROL Examinar]** para mostrar una lista de esquemas existentes. Aquí, seleccione el nombre del [!DNL Profile]Esquema habilitado para que desee agregar campos de consentimiento a. Las capturas de pantalla de esta sección utilizan el esquema &quot;Miembros socio&quot; creado en la [tutorial de creación de esquemas](../../../../xdm/tutorials/create-schema-ui.md) como ejemplo.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-schema.png)

>[!TIP]
>
>Puede utilizar las funcionalidades de búsqueda y filtrado del espacio de trabajo para facilitar la búsqueda del esquema. Consulte la guía de [exploración de recursos XDM](../../../../xdm/ui/explore.md) para obtener más información.

El [!DNL Schema Editor] , mostrando la estructura del esquema en el lienzo. En el lado izquierdo del lienzo, seleccione **[!UICONTROL Añadir]** en el **[!UICONTROL Grupos de campos]** sección.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-field-group.png)

El **[!UICONTROL Agregar grupo de campos]** aparece el cuadro de diálogo. Desde aquí, seleccione **[!UICONTROL Detalles de consentimiento y preferencia]** de la lista. Si lo desea, puede utilizar la barra de búsqueda para reducir los resultados y localizar más fácilmente el grupo de campos.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-group-dialog.png)

A continuación, busque la **[!UICONTROL IdentityMap]** grupo de campos de la lista y selecciónelo también. Una vez que ambos grupos de campos se muestren en el carril derecho, seleccione **[!UICONTROL Adición de grupos de campos]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/identitymap.png)

El lienzo vuelve a aparecer y muestra que la variable `consents` y `identityMap` se han añadido campos de a la estructura de esquema. Si necesita campos de consentimiento y preferencia adicionales no capturados por el grupo de campos estándar, consulte la sección del apéndice sobre [adición de campos de consentimiento y preferencia personalizados al esquema](#custom-consent). De lo contrario, seleccione **[!UICONTROL Guardar]** para finalizar los cambios en el esquema.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/save-schema.png)

>[!IMPORTANT]
>
>Si está creando un nuevo esquema o editando un esquema existente que no se ha habilitado para el perfil, debe [habilitar el esquema para el perfil](../../../../xdm/ui/resources/schemas.md#profile) antes de guardar.

Si el esquema editado lo utiliza el [!UICONTROL Conjunto de datos de perfil] especificado en la secuencia de datos del SDK web de Platform, ese conjunto de datos ahora incluirá los nuevos campos de consentimiento. Ahora puede volver a la [guía de procesamiento de consentimiento](./overview.md#merge-policies) para continuar con el proceso de configuración de Experience Platform para procesar los datos de consentimiento. Si no ha creado ningún conjunto de datos para este esquema, siga los pasos de la sección siguiente.

## Cree un conjunto de datos basado en el esquema de consentimiento {#dataset}

Una vez creado un esquema con campos de consentimiento, debe crear un conjunto de datos que, en última instancia, introduzca los datos de consentimiento de los clientes. Este conjunto de datos debe estar habilitado para [!DNL Real-Time Customer Profile].

Para empezar, seleccione **[!UICONTROL Conjuntos de datos]** en el panel de navegación izquierdo, seleccione **[!UICONTROL Crear conjunto de datos]** en la esquina superior derecha.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/create-dataset.png)

En la página siguiente, seleccione **[!UICONTROL Crear conjunto de datos a partir de esquema]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/from-schema.png)

El **[!UICONTROL Crear conjunto de datos a partir de esquema]** flujo de trabajo aparece, empezando por **[!UICONTROL Seleccionar esquema]** paso. En la lista proporcionada, busque uno de los esquemas de consentimiento que creó anteriormente. Si lo desea, puede utilizar la barra de búsqueda para reducir los resultados y localizar el esquema con mayor facilidad. Seleccione el botón de opción situado junto al esquema deseado y, a continuación, seleccione **[!UICONTROL Siguiente]** para continuar.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/select-dataset-schema.png)

El **[!UICONTROL Configurar conjunto de datos]** aparece el paso. Proporcione un nombre y una descripción únicos y fácilmente identificables para el conjunto de datos antes de seleccionar **[!UICONTROL Finalizar]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/dataset-details.png)

Aparecerá la página de detalles del conjunto de datos recién creado. Si el conjunto de datos se basa en el esquema de series temporales, el proceso se completa. Si el conjunto de datos se basa en el esquema de registros, el paso final del proceso es habilitar el conjunto de datos para utilizarlo en [!DNL Real-Time Customer Profile].

En el carril derecho, seleccione **[!UICONTROL Perfil]** alternar.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/profile-toggle.png)

Finalmente, seleccione **[!UICONTROL Activar]** en la ventana emergente de confirmación para habilitar el esquema para [!DNL Profile].

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/enable-dataset.png)

El conjunto de datos ahora está guardado y habilitado para su uso en [!DNL Profile]. Si planea utilizar el SDK web de Platform para enviar datos de consentimiento al perfil, debe seleccionar este conjunto de datos como [!UICONTROL Conjunto de datos de perfil] al configurar su [secuencia de datos](../../../../edge/datastreams/overview.md).

## Pasos siguientes

Al seguir este tutorial, ha añadido campos de consentimiento a una [!DNL Profile]Esquema habilitado para, cuyo conjunto de datos se utilizará para introducir datos de consentimiento mediante el SDK web de Platform o la ingesta directa de XDM.

Ahora puede volver a la [resumen del procesamiento de consentimiento](./overview.md#merge-policies) para seguir configurando Experience Platform para procesar los datos de consentimiento.

## Apéndice

La siguiente sección contiene información adicional sobre la creación de un conjunto de datos para la ingesta de datos de consentimiento y preferencia del cliente.

### Añadir campos de consentimiento y preferencia personalizados al esquema {#custom-consent}

Si necesita capturar señales de consentimiento adicionales fuera de las representadas por el estándar [!UICONTROL Detalles de consentimiento y preferencia] Grupo de campos, puede utilizar componentes XDM personalizados para mejorar el esquema de consentimiento y adaptarlo a sus necesidades empresariales particulares. Esta sección describe los principios básicos de cómo personalizar el esquema de consentimiento para introducir estas señales en el perfil.

>[!IMPORTANT]
>
>Los SDK web y móvil de Platform no admiten campos personalizados en sus comandos de cambio de consentimiento. Actualmente, la única manera de introducir campos de consentimiento personalizados en el perfil es a través de [ingesta por lotes](../../../../ingestion/batch-ingestion/overview.md) o una [conexión de origen](../../../../sources/home.md).

Se recomienda encarecidamente que utilice el [!UICONTROL Detalles de consentimiento y preferencia] grupo de campos como línea de base para la estructura de los datos de consentimiento y agregue campos adicionales según sea necesario, en lugar de intentar crear toda la estructura desde cero.

Para agregar campos personalizados a la estructura de un grupo de campos estándar, primero debe crear un grupo de campos personalizados. Después de agregar el [!UICONTROL Detalles de consentimiento y preferencia] grupo de campos al esquema, seleccione el **más (+)** en el menú **[!UICONTROL Grupos de campos]** , y luego seleccione **[!UICONTROL Crear nuevo grupo de campos]**. Proporcione un nombre y una descripción opcional para el grupo de campos y seleccione **[!UICONTROL Agregar grupo de campos]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field-group.png)

El [!DNL Schema Editor] vuelve a aparecer con el nuevo grupo de campos personalizados seleccionado en el carril izquierdo. En el lienzo, aparecen controles que le permiten agregar campos personalizados a la estructura del esquema. Para añadir un nuevo campo de consentimiento o preferencia, seleccione el **más (+)** junto al icono `consents` objeto.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/add-custom-field.png)

Aparece un nuevo campo dentro de `consents` objeto. Dado que está agregando un campo personalizado a un objeto XDM estándar, el nuevo campo se crea bajo un objeto que tiene un espacio de nombres en el ID de inquilino.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/nested-tenantId.png)

En el carril derecho debajo de **[!UICONTROL Propiedades del campo]**, proporcione un nombre y una descripción para el campo. Al seleccionar el campo **[!UICONTROL Tipo]**, debe utilizar el tipo de datos estándar adecuado para un campo de consentimiento o preferencia personalizado:

* [[!UICONTROL Campo de consentimiento genérico]](../../../../xdm/data-types/consent-field.md)
* [[!UICONTROL Campo de preferencias de marketing genéricas]](../../../../xdm/data-types/marketing-field.md)
* [[!UICONTROL Campo de preferencias de marketing genéricas con suscripciones]](../../../../xdm/data-types/marketing-field-subscriptions.md)
* [[!UICONTROL Campo de preferencias de personalización genéricas]](../../../../xdm/data-types/personalization-field.md)

Cuando termine, seleccione **[!UICONTROL Aplicar]**.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-properties.png)

El campo de consentimiento o preferencia se agrega a la estructura de esquema. Tenga en cuenta que la variable [!UICONTROL Ruta] que se muestra en el carril derecho contiene `_tenantId` namespace. Este área de nombres debe incluirse siempre que se haga referencia a la ruta de este campo en las operaciones de datos.

![](../../../images/governance-privacy-security/consent/adobe/dataset-prep/field-added.png)

Siga los pasos anteriores para seguir agregando los campos de consentimiento y preferencia que necesita. Cuando termine, seleccione **[!UICONTROL Guardar]** para confirmar los cambios.

Si no ha creado ningún conjunto de datos para este esquema, continúe con la sección sobre [creación de un conjunto de datos](#dataset).
