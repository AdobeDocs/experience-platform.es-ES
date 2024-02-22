---
title: Audiencias de cuenta
description: Aprenda a crear y utilizar audiencias de cuenta para segmentar perfiles de cuenta en destinos de flujo descendente.
badgeB2B: label="Edición B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edición B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 047930d6-939f-4418-bbcb-8aafd2cf43ba
source-git-commit: 3c0b7c4eee7c790a8ffae95c05a8db6ba7c3b285
workflow-type: tm+mt
source-wordcount: '1039'
ht-degree: 0%

---

# Audiencias de cuenta

>[!AVAILABILITY]
>
>Las audiencias de cuenta solo están disponibles en la [Edición B2B de Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2b) y el [B2P Edition de Real-time Customer Data Platform](../../rtcdp/overview.md#rtcdp-b2p).

Con la segmentación de cuentas, Adobe Experience Platform le permite ofrecer la total facilidad y sofisticación de la experiencia de segmentación de marketing de audiencias basadas en personas a audiencias basadas en cuentas.

Las audiencias de cuenta pueden utilizarse como entrada para destinos basados en cuentas, lo que le permite dirigirse a las personas de esas cuentas en servicios descendentes. Por ejemplo, puede utilizar audiencias basadas en cuentas para recuperar registros de todas las cuentas que lo hagan **no** Tener información de contacto de cualquier persona con el título de Director de operaciones (COO) o Director de marketing (CMO).

## Terminología {#terminology}

Antes de empezar a usar las audiencias de cuenta, revise las diferencias entre los distintos tipos de audiencias:

- **Audiencias de cuenta**: una audiencia de cuenta es una audiencia que se crea mediante **account** datos de perfil. Los datos de perfil de cuenta se pueden utilizar para crear audiencias dirigidas a personas dentro de cuentas de flujo descendente. Para obtener más información sobre los perfiles de cuenta, lea la [resumen del perfil de cuenta](../../rtcdp/accounts/account-profile-overview.md).
- **Audiencias de personas**: una audiencia de personas es una audiencia que se crea mediante **cliente** datos de perfil. Los datos de perfil del cliente se pueden utilizar para crear audiencias dirigidas a la clientela de su empresa. Para obtener más información sobre los perfiles de los clientes, lea la [Resumen del perfil del cliente en tiempo real](../../profile/home.md).
- **Audiencias potenciales**: una audiencia potencial es una audiencia creada con **perspectivas** datos de perfil. Los datos de perfil del cliente potencial se pueden utilizar para crear audiencias de usuarios no autenticados. Para obtener más información sobre los perfiles de clientes potenciales, lea la [resumen del perfil del cliente potencial](../../profile/ui/prospect-profile.md).

## Acceso {#access}

Para acceder a las audiencias de cuenta, seleccione **[!UICONTROL Audiencias]** en el **[!UICONTROL Cuentas]** sección.

![El botón Audiencias se resalta en la sección Cuentas.](../images/ui/account-audiences/select.png)

El [!UICONTROL Examinar] , que muestra una lista de todas las audiencias de la cuenta para la organización.

![Se muestran las audiencias de cuenta que pertenecen a la organización.](../images/ui/account-audiences/browse.png)

Esta vista muestra información sobre la audiencia, incluido el nombre, el recuento de perfiles, el origen, el estado del ciclo vital, la fecha de creación y la fecha de la última actualización.

## Crear audiencias {#create}

Para crear una audiencia de cuenta, seleccione **[!UICONTROL Crear audiencia]** en el [!UICONTROL Examinar] página.

![El [!UICONTROL Crear audiencia] El botón se resalta en la página de exploración de audiencias de la cuenta.](../images/ui/account-audiences/select-create-audience.png)

Aparecerá el Generador de segmentos. Los atributos de cuenta se muestran en la barra de navegación izquierda.

![Se muestra el Generador de segmentos. Tenga en cuenta que solo se muestran los atributos.](../images/ui/account-audiences/segment-builder.png)

Al crear audiencias de cuenta, tenga en cuenta que los eventos se enumeran en **[!UICONTROL People]**, en lugar de ser su propia pestaña, ya que estos atributos están asociados a personas.

![La ubicación para buscar eventos, que se encuentra dentro de [!UICONTROL People] carpeta, aparece resaltada.](../images/ui/account-audiences/attributes.png)

Para obtener más información sobre el uso del Generador de segmentos, lea la [Guía de IU del Generador de segmentos](./segment-builder.md).

## Activar audiencia {#activate}

>[!NOTE]
>
>Solo un número limitado de destinos admite audiencias de cuenta. Asegúrese de que el destino que desee activar admita las audiencias de la cuenta antes de continuar este proceso.

Después de crear la audiencia de la cuenta, puede activarla en otros servicios descendentes.

Seleccione la audiencia que desee activar, seguida de **[!UICONTROL Activar en destino]**.

![El [!UICONTROL Activar en destino] El botón se resalta en el menú de acciones rápidas de la audiencia seleccionada.](../images/ui/account-audiences/activate.png)

El [!UICONTROL Activar destino] página. Para obtener más información sobre el proceso de activación, incluidos los destinos admitidos y los detalles sobre las asignaciones de campo, lea la [activar audiencias de cuenta](/help/destinations/ui/activate-account-audiences.md) tutorial.

## Pasos siguientes {#next-steps}

Después de leer esta guía, ahora tiene una mejor comprensión de cómo crear y utilizar las audiencias de la cuenta en Adobe Experience Platform. Para aprender a utilizar otros tipos de audiencias en Platform, lea la [Guía de IU del servicio de segmentación](./overview.md).

## Apéndice {#appendix}

En la siguiente sección se proporciona información adicional sobre las audiencias de cuenta.

### Validación de segmentación de cuenta {#validation}

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_eventLookbackWindow"
>title="Error de ventana retrospectiva máxima"
>abstract="La ventana retrospectiva máxima para eventos de experiencia es de 30 días."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxDepth"
>title="Error de profundidad máxima del contenedor anidado"
>abstract="La profundidad máxima de los contenedores anidados es **5**. Esto significa que usted **no puede** tener más de cinco contenedores anidados al crear la audiencia."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_combinationMaxBreadth"
>title="Error de cantidad máxima de reglas"
>abstract="El número máximo de reglas dentro de un solo contenedor es **5**. Esto significa que usted **no puede** tener más de cinco reglas dentro de un solo contenedor al crear la audiencia."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_crossEntityMaxDepth"
>title="Error de importe máximo entre entidades"
>abstract="El número máximo de entidades cruzadas que se pueden utilizar dentro de una sola audiencia es **5**. Una entidad cruzada se produce cuando se cambia entre distintas entidades dentro de la audiencia. Por ejemplo, pasar de una cuenta a una persona y a una lista de marketing."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowCustomEntity"
>title="Error de entidad personalizada"
>abstract="Las entidades personalizadas son **no** permitido."

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
>abstract="Los eventos de inSegment son **no** permitido."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowInSegmentByValue"
>title="Error de evento inSegment"
>abstract="Los eventos de inSegment son **no** permitido."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowSequentialEvents"
>title="Error de eventos secuenciales"
>abstract="Los eventos secuenciales son **no** permitido."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_allowMaps"
>title="Error de propiedad de tipo de mapa"
>abstract="Las propiedades de tipo mapa son **no** permitido."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxNestedAggregationDepth"
>title="Error de profundidad máxima de entidad anidada"
>abstract="La profundidad máxima de las matrices anidadas es **5**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_maxObjectNestingLevel"
>title="Error de cantidad máxima de objeto anidado"
>abstract="El número máximo de objetos anidados permitido es **10**."

>[!CONTEXTUALHELP]
>id="platform_audiences_account_constraint_generic"
>title="Infracción de restricción"
>abstract="La audiencia infringe una restricción. Lea el documento vinculado para obtener más información."

Cuando se usan audiencias de cuenta, la audiencia **debe** cumplir con las siguientes restricciones:

>[!NOTE]
>
>La siguiente lista muestra la **predeterminado** restricciones para audiencias de cuenta. Estos valores **mayo** cambiar, según la configuración implementada por el administrador de su organización.

- La ventana retrospectiva máxima para eventos de experiencia es **30 días**.
- La profundidad máxima de los contenedores anidados es **5**.
   - Esto significa que usted **no puede** tener más de cinco contenedores anidados al crear la audiencia.
- El número máximo de reglas dentro de un solo contenedor es **5**.
   - Esto significa que su audiencia **no puede** tiene más de cinco reglas que componen su audiencia.
- El número máximo de entidades cruzadas que se pueden utilizar es **5**.
   - Una entidad cruzada se produce cuando se cambia entre distintas entidades dentro de la audiencia. Por ejemplo, pasar de una cuenta a una persona y a una lista de marketing.
- Entidades personalizadas **no puede** se utilizará.
- El número máximo de valores que se pueden comprobar para un solo campo es **50**.
   - Por ejemplo, si tiene un campo de &quot;Nombre de ciudad&quot;, puede comprobar ese valor con 50 nombres de ciudades.
- Audiencias de cuenta **no puede** use `inSegment` eventos.
- Audiencias de cuenta **no puede** utilice eventos secuenciales.
- Audiencias de cuenta **no puede** utilice mapas.
- La profundidad máxima de las matrices anidadas es **5**.
- El número máximo de objetos anidados es **10**.
