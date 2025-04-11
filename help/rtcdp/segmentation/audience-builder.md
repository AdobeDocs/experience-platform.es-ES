---
title: Generador de audiencias en Real-Time Customer Data Platform
description: Aprenda a utilizar el Generador de audiencias en Real-Time Customer Data Platform para crear audiencias.
feature: Get Started, Audiences
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: da87baad-b82a-4a45-89c3-cf20d66fe657
source-git-commit: 3829f506d0b4d78b543b949e8e11806d8fe10b9c
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Generador de audiencias en Real-Time Customer Data Platform

Compilado en Adobe Experience Platform, [!DNL Adobe Real-Time Customer Data Platform] puede usar todas las funcionalidades de Audience Builder que forman parte de [!DNL Experience Platform]. El espacio de trabajo proporciona controles intuitivos para crear y editar reglas, como mosaicos de arrastrar y soltar utilizados para representar las propiedades de datos.

![Generador de audiencias en la sección Cuentas.](../assets/segmentation/audience-builder/audience-builder.png){zoomable="yes"}

## Campos {#fields}

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showfullxdmschema"
>title="Mostrar esquema XDM completo"
>abstract="De forma predeterminada, solo se muestran los campos que contienen datos. Active esta opción para mostrar todos los campos del esquema XDM."

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showrelationselectors"
>title="Mostrar selectores de relación"
>abstract="De forma predeterminada, se utilizan las relaciones estándar para su organización. Active esta opción para mostrar los selectores de relación utilizados."

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showconstrainedfields"
>title="Mostrar campos restringidos"
>abstract="De forma predeterminada, solo se muestran los campos que no tienen restricciones. Active esta opción para mostrar los campos que tienen restricciones."

Al usar el Generador de audiencias para cuentas de, puede usar los atributos de cuenta o las audiencias existentes como campos de la audiencia.

Puede seleccionar el ![icono de configuración](../../images/icons/settings.png) para ajustar la configuración de los campos mostrados.

![Los iconos de configuración están resaltados en el Generador de audiencias.](../assets/segmentation/audience-builder/select-settings.png){zoomable="yes"}

>[!NOTE]
>
>La sección **[!UICONTROL Opciones de campo]** está actualmente en versión beta y solo está disponible para clientes seleccionados. Póngase en contacto con el Servicio de atención al cliente de Adobe para obtener más información.

Se muestra la sección [!UICONTROL Configuración]. En esta sección, puede actualizar qué campos se muestran, así como la relación de los campos.

Para las **[!UICONTROL opciones de campo]**, puede mostrar solo los campos que contienen datos o el esquema XDM completo.

Para la **[!UICONTROL relación de campos]**, puede usar las relaciones estándar para su organización o mostrar los selectores de relación.

![Se muestra el módulo de configuración.](../assets/segmentation/audience-builder/settings.png){width="300"}

### Atributos {#attributes}

La pestaña [!UICONTROL Atributos] le permite examinar los atributos de cuenta que pertenecen a la clase de cuenta empresarial de XDM, así como las oportunidades y los atributos basados en personas. Cada carpeta se puede expandir para mostrar atributos adicionales, donde cada atributo es un mosaico que se puede arrastrar al [lienzo del generador de reglas](#rule-builder-canvas) en el centro del espacio de trabajo.

![La ficha Atributos se muestra en el Generador de audiencias](../assets/segmentation/audience-builder/attributes.png)

Al seleccionar un atributo, puede ver los datos de resumen seleccionando el [icono de información](../../images/icons/info.png). Los datos de resumen incluyen información como valores principales, una explicación de qué es el campo y el porcentaje de cuentas que contienen valores para este atributo.

![Una ventana emergente que muestra una versión completa de los datos de resumen de un atributo.](../assets/segmentation/audience-builder/full-summary-data.png){width="300"}

Si menos del 25% de las cuentas rellenan un atributo, se mostrará el ![icono de aviso de datos](../../images/icons/data-notice.png). Independientemente, se muestran los mismos datos de resumen para el atributo.

![Una ventana emergente que muestra una versión de los datos de resumen de un atributo cuando lo rellenan menos del 25% de las cuentas.](../assets/segmentation/audience-builder/empty-summary-data.png){width="300"}

>[!NOTE]
>
>Los datos de resumen solo están disponibles si el atributo pertenece al esquema de cuenta, persona u oportunidad. Además, los valores superiores solo se muestran si el campo **no** contiene demasiados valores diferentes y si los valores de esos campos se repiten con frecuencia.
>
>Estos datos de resumen se actualizan **diariamente**.

Para obtener una guía más detallada sobre el Generador de audiencias, lea la [guía del usuario del Generador de audiencias](../../segmentation/ui/segment-builder.md){target="_blank"}.

### Públicos {#audiences}

La pestaña **[!UICONTROL Audiencias]** enumera todas las audiencias basadas en personas y en cuentas disponibles en Experience Platform.

Puede situar el cursor sobre el ![icono de información](../../images/icons/info.png) situado junto a una audiencia para ver información sobre la audiencia, incluido su ID, descripción y jerarquía de carpetas para localizar la audiencia.

![Se muestra información sobre la audiencia.](../assets/segmentation/audience-builder/audience-information.png){zoomable="yes"}

## Lienzo del generador de reglas {#rule-builder-canvas}

Una audiencia creada en el Generador de audiencias es una colección de reglas que se utilizan para describir las características o los comportamientos clave de una audiencia de destino. Estas reglas se crean mediante el lienzo del generador de reglas, ubicado en el centro del Generador de audiencias.

Para agregar una regla nueva a la definición del segmento, arrastre un mosaico desde la ficha **[!UICONTROL Campos]** y suéltelo en el lienzo del generador de reglas.

![El lienzo del generador de reglas con un campo agregado.](../assets/segmentation/audience-builder/added-field.png){zoomable="yes"}

Para obtener más información sobre el uso del lienzo del generador de reglas, lea la [documentación del generador de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas){target="_blank"}.

### Contenedores {#containers}

Las reglas de audiencia se evalúan en el orden en que aparecen en la lista. Puede utilizar contenedores para permitir un mayor control sobre el orden de ejecución, mediante el uso de consultas anidadas.

Para obtener más información sobre los contenedores, lea la [documentación del Generador de segmentos](../../segmentation/ui/segment-builder.md#containers){target="_blank"}.

## Propiedades de público {#properties}

La sección **[!UICONTROL Propiedades de audiencia]** muestra información sobre la audiencia, incluido un tamaño estimado de la audiencia. También puede especificar detalles sobre la audiencia, incluido su nombre, descripción y etiquetas.

![Se muestra la sección de propiedades de audiencia para la audiencia en el Generador de audiencias.](../assets/segmentation/audience-builder/audience-properties.png){width="300"}

**[!UICONTROL Cuentas calificadas]** indica el número real de cuentas que coinciden con las reglas de la audiencia. Este número se actualiza cada 24 horas, después de ejecutar el trabajo de segmentación.

**[!UICONTROL Cuentas estimadas]** indica el número aproximado de cuentas basadas en el trabajo de muestra. Puede actualizar este valor después de agregar nuevas reglas o condiciones y seleccionar **[!UICONTROL Actualizar estimación]**.

![Se muestra la sección de estimaciones dentro de la sección de propiedades de la audiencia.](../assets/segmentation/audience-builder/account-estimates.png){width="300"}

Puede seleccionar **[!UICONTROL Ver cuentas]** para ver un ejemplo de las cuentas que cumplen los requisitos para la audiencia con las reglas actuales.

![El botón Ver cuentas está resaltado.](../assets/segmentation/audience-builder/view-accounts.png){width="300"}

La **[!UICONTROL vista de código]** proporciona una descripción con código basado en texto de las reglas de la audiencia.

![Versión de vista de código de la audiencia de la cuenta.](../assets/segmentation/audience-builder/code-view.png)

Puede seleccionar **[!UICONTROL Aplicar etiquetas de acceso]** para aplicar las etiquetas de acceso relevantes para la audiencia. Encontrará más información sobre las etiquetas de acceso en la [guía de administración de etiquetas](../../access-control/abac/ui/labels.md){target="_blank"}.

![Se muestra la ventana emergente Aplicar etiquetas de acceso y control de datos.](../assets/segmentation/audience-builder/apply-access-labels.png)

El resto de la sección de propiedades de la audiencia le permite editar detalles relacionados con la audiencia de la cuenta, incluidos el nombre, la descripción y las etiquetas.

![Se muestran los detalles de las propiedades de audiencia.](../assets/segmentation/audience-builder/audience-details.png){width="300"}

Usted **no puede** cambiar el método de evaluación de las audiencias de cuenta, ya que todas las audiencias de cuenta se evalúan mediante la segmentación por lotes.

## Pasos siguientes {#next-steps}

Audience Builder proporciona un flujo de trabajo enriquecido que le permite crear audiencias a partir de los datos de su cuenta empresarial de XDM.

Para obtener más información acerca del servicio de segmentación para los datos de perfil del cliente, lea la [descripción general del servicio de segmentación](../../segmentation/home.md){target="_blank"}.
