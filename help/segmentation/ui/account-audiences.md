---
title: Audiencias de cuenta
description: Aprenda a crear y utilizar audiencias de cuenta para segmentar perfiles de cuenta en destinos de flujo descendente.
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edición B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 27%

---

# Públicos de la cuenta

>[!AVAILABILITY]
>
>Las audiencias de cuenta solo están disponibles en [B2B Edition de Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) y en [B2P Edition de Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

Con la segmentación de cuentas, Adobe Experience Platform le permite ofrecer la total facilidad y sofisticación de la experiencia de segmentación de marketing de audiencias basadas en personas a audiencias basadas en cuentas.

Las audiencias de cuenta pueden utilizarse como entrada para destinos basados en cuentas, lo que le permite dirigirse a las personas de esas cuentas en servicios descendentes. Por ejemplo, puede usar audiencias basadas en cuentas para recuperar registros de todas las cuentas que **no** tienen información de contacto de cualquier persona con el título de Director de operaciones (COO) o Director de marketing (CMO).

## Terminología {#terminology}

Antes de empezar a usar las audiencias de cuenta, revise las diferencias entre los distintos tipos de audiencias:

- **Audiencias de cuenta**: una audiencia de cuenta es una audiencia que se crea usando los datos de perfil de **account**. Los datos de perfil de cuenta se pueden utilizar para crear audiencias dirigidas a personas dentro de cuentas de flujo descendente. Para obtener más información sobre los perfiles de cuenta, lea [descripción general del perfil de cuenta](../../rtcdp/accounts/account-profile-overview.md).
- **Audiencias de personas**: una audiencia de personas es una audiencia creada con datos de perfil de **cliente**. Los datos de perfil del cliente se pueden utilizar para crear audiencias dirigidas a la clientela de su empresa. Para obtener más información sobre los perfiles de los clientes, lea [Descripción general del perfil del cliente en tiempo real](../../profile/home.md).
- **Audiencias clientes potenciales**: una audiencia cliente potencial es una audiencia creada con datos de perfil de **cliente potencial**. Los datos de perfil del cliente potencial se pueden utilizar para crear audiencias de usuarios no autenticados. Para obtener más información sobre los perfiles de clientes potenciales, lea la [descripción general del perfil de clientes potenciales](../../profile/ui/prospect-profile.md).

## Acceso {#access}

Para acceder a las audiencias de la cuenta, seleccione **[!UICONTROL Audiencias]** en la sección **[!UICONTROL Cuentas]**.

![El botón Audiencias está resaltado en la sección Cuentas.](../images/ui/account-audiences/select.png)

Se muestra la página [!UICONTROL Examinar], que muestra una lista de todas las audiencias de la cuenta para la organización.

![Se muestran las audiencias de cuenta que pertenecen a la organización.](../images/ui/account-audiences/browse.png)

Esta vista muestra información sobre la audiencia, incluido el nombre, el recuento de perfiles, el origen, el estado del ciclo vital, la fecha de creación y la fecha de la última actualización.

También puede utilizar la funcionalidad de búsqueda y filtrado para buscar y ordenar rápidamente audiencias de cuenta específicas. Encontrará más información sobre esta característica en la [descripción general de Audience Portal](./audience-portal.md#manage-audiences).

## Crear público {#create}

>[!NOTE]
>
>Las audiencias de la cuenta se evalúan mediante la segmentación **batch** y se evaluarán cada 24 horas.

Para crear una audiencia de cuenta, selecciona **[!UICONTROL Crear audiencia]** en la página [!UICONTROL Examinar].

![El botón [!UICONTROL Crear audiencia] está resaltado en la página de exploración de audiencias de la cuenta.](../images/ui/account-audiences/select-create-audience.png)

Aparecerá el Generador de segmentos. Los atributos y audiencias de la cuenta se muestran en la barra de navegación izquierda. En la ficha [!UICONTROL Atributos], puede agregar atributos creados y personalizados por Platform.

![Se muestra el Generador de segmentos. Observe que sólo se muestran los atributos y las audiencias.](../images/ui/account-audiences/segment-builder.png)

Al crear audiencias de cuenta, tenga en cuenta que los eventos se enumeran en **[!UICONTROL Personas]**, en lugar de ser su propia pestaña, ya que estos atributos están asociados a personas.

![Se resalta la ubicación para buscar eventos, que se encuentra dentro de la carpeta [!UICONTROL Personas].](../images/ui/account-audiences/attributes.png)

En la ficha [!UICONTROL Audiencias], puede agregar audiencias basadas en personas creadas anteriormente a partir de al crear su propia audiencia de cuenta.

![La ficha Audiencias del Generador de segmentos está resaltada.](../images/ui/account-audiences/audiences.png)

Para obtener más información sobre el uso del Generador de segmentos, lea la [guía de la interfaz de usuario del Generador de segmentos](./segment-builder.md).

## Activar público {#activate}

>[!NOTE]
>
>Solo un número limitado de destinos admite audiencias de cuenta. Asegúrese de que el destino que desee activar admita las audiencias de la cuenta antes de continuar este proceso.

Después de crear la audiencia de la cuenta, puede activarla en otros servicios descendentes.

Seleccione la audiencia que desee activar, seguida de **[!UICONTROL Activar en destino]**.

![El botón [!UICONTROL Activar en destino] está resaltado en el menú de acciones rápidas para la audiencia seleccionada.](../images/ui/account-audiences/activate.png)

Aparecerá la página [!UICONTROL Activar destino]. Para obtener más información sobre el proceso de activación, incluidos los destinos admitidos y los detalles sobre las asignaciones de campos, lea el tutorial [activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md).

## Pasos siguientes {#next-steps}

Después de leer esta guía, ahora tiene una mejor comprensión de cómo crear y utilizar las audiencias de la cuenta en Adobe Experience Platform. Para aprender a utilizar otros tipos de audiencias en Platform, lea la [Guía de la interfaz de usuario del servicio de segmentación](./overview.md).

## Apéndice {#appendix}

En la siguiente sección se proporciona información adicional sobre las audiencias de cuenta.

### Validación de la segmentación de cuentas {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Error de ventana retrospectiva máxima"
>abstract="La ventana retrospectiva máxima para eventos de Experience es de 30 días."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Error de profundidad máxima de contenedores anidados"
>abstract="La profundidad máxima de los contenedores anidados es **5**. Esto significa que **no puede** tener más de cinco contenedores anidados al crear el público."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Error de cantidad máxima de reglas"
>abstract="El número máximo de reglas dentro de un solo contenedor es **5**. Esto significa que **no puede** tener más de cinco reglas dentro de un solo contenedor al crear el público."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Error de importe máximo entre entidades"
>abstract="El número máximo de entidades cruzadas que se pueden utilizar dentro de una sola audiencia es **5**. Una entidad cruzada se produce cuando se cambia entre distintas entidades dentro del público. Por ejemplo, pasar de una cuenta a una persona y a una lista de marketing."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Error de entidad personalizada"
>abstract="**No** se permiten entidades personalizadas."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_b2bBuiltInEntities"
>title="Error de entidad B2B no válido"
>abstract="Solo se permiten utilizar las siguientes entidades B2B: `_xdm.context.account`, `_xdm.content.opportunity`, `_xdm.context.profile`, `_xdm.context.experienceevent`, `_xdm.context.account-person`, `_xdm.classes.opportunity-person`, `_xdm.classes.marketing-list-member`, `_xdm.classes.marketing-list`, `_xdm.context.campaign-member`, y `_xdm.classes.campaign`."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_rhsMaxOptions"
>title="Error de valores máximos"
>abstract="El número máximo de valores que se pueden comprobar para un solo campo es **50**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByReference"
>title="Error de evento inSegment"
>abstract="**No** se permiten eventos inSegment."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="Error de evento inSegment"
>abstract="**No** se permiten eventos inSegment."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Error de eventos secuenciales"
>abstract="**No** se permiten eventos secuenciales."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Error de propiedad de tipo de mapa"
>abstract="**No** se permiten propiedades de tipo de mapa."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Error de profundidad máxima de entidades anidadas"
>abstract="La profundidad máxima de las matrices anidadas es **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Error de cantidad máxima de objetos anidados"
>abstract="El número máximo de objetos anidados permitido es **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Infracción de restricción"
>abstract="El público infringe una restricción. Lea el documento vinculado para obtener más información."

Al usar audiencias de cuenta, la audiencia **debe** cumplir con las siguientes restricciones:

>[!NOTE]
>
>La siguiente lista muestra las restricciones **default** para las audiencias de cuenta. Estos valores **pueden** cambiar, según la configuración implementada por el administrador de su organización.

- La ventana retrospectiva máxima para eventos de experiencia es de **30 días**.
- La profundidad máxima de los contenedores anidados es de **5**.
   - Esto significa que **no puede** tener más de cinco contenedores anidados al crear el público.
- El número máximo de reglas dentro de un solo contenedor es **5**.
   - Esto significa que la audiencia **no puede** tener más de cinco reglas que compongan la audiencia.
- El número máximo de entidades cruzadas que se pueden usar es **5**.
   - Una entidad cruzada se produce cuando se cambia entre distintas entidades dentro del público. Por ejemplo, pasar de una cuenta a una persona y a una lista de marketing.
- No se pueden usar las entidades personalizadas **1}.**
- El número máximo de valores que se pueden comprobar para un solo campo es **50**.
   - Por ejemplo, si tiene un campo de &quot;Nombre de ciudad&quot;, puede comprobar ese valor con 50 nombres de ciudades.
- Las audiencias de cuenta **no pueden** usar `inSegment` eventos.
- Las audiencias de cuenta **no pueden** usar eventos secuenciales.
- Las audiencias de cuenta **no pueden** usar mapas.
- La profundidad máxima de las matrices anidadas es **5**.
- El número máximo de objetos anidados es de **10**.
