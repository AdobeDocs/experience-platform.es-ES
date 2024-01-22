---
title: Migración de destino de pinterest a una nueva API. Acción del cliente requerida.
description: Pinterest está desaprobando la API de anunciante v4 que actualmente utiliza el destino de Pinterest en Real-Time CDP. Comprenda sus elementos de acción para una transición sin problemas a la nueva API sin interrupciones para sus campañas de Pinterest.
hide: true
hidefromtoc: true
exl-id: c965235c-4208-4c28-9ac5-eb4c0061515d
source-git-commit: e3341ec6f62844858ecda7dd4db70d085f0bf217
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Actualización del destino de pinterest a una nueva API. Acción del cliente requerida para el 18 de enero de 2024.

>[!IMPORTANT]
>
>Los elementos de acción del cliente de esta página se aplican a usted si su organización ha configurado flujos de datos para exportar datos a Pinterest antes del 16 de noviembre de 2023, la fecha en que se creó el nuevo **[!UICONTROL Pinterest]** El destino de, que utiliza la última API de Pinterest, se añadió al catálogo de destinos.

## ¿Qué está sucediendo?

Pinterest ha desaprobado la API de anunciante v4 que utilizaba [Pinterest destination](/help/destinations/catalog/advertising/pinterest.md) en Real-Time CDP. El Adobe ha actualizado el destino para utilizar el [API de anunciante v5](https://developers.pinterest.com/docs/getting-started/migration/). Lea esta página para comprender los elementos de su acción con el fin de realizar una transición sin problemas a la nueva API sin interrupciones para sus campañas de Pinterest.

## ¿Por qué se me notifica?

Hemos identificado su organización como si tuviera flujos de datos activos para activar audiencias en Pinterest.

## ¿Cuál es el plan?

Adobe ha lanzado una nueva tarjeta de destino de Pinterest que aprovecha la API de Pinterest v5 y conservará los flujos de datos existentes en la nueva conexión.

## ¿Debo hacer algo para mantener mis audiencias activadas en funcionamiento?

Sí, antes del 18 de enero de 2024, debe autenticarse en el nuevo destino de Pinterest con su cuenta de anunciante de Pinterest en Real-Time CDP. Consulte las instrucciones detalladas a continuación.

### Volver a autenticar en Pinterest {#reauthenticate}

1. Ir a **[!UICONTROL Destinos > Cuentas]** y utilice el filtro de la pantalla para filtrar solo el destino de Pinterest.
   ![Filtrar solo cuentas de Pinterest](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-acconts-only.png)
2. En el **Pinterest** destino, seleccione el símbolo de tres puntos ... y seleccione **[!UICONTROL Editar detalles]**.
   ![Seleccione Editar detalles](/help/destinations/assets/catalog/advertising/pinterest-migration/edit-details-pinterest.png)
3. Seleccionar **[!UICONTROL Volver a conectar OAuth]** e inicie sesión en su cuenta de Pinterest.
   ![Seleccione Volver a conectar OAuth](/help/destinations/assets/catalog/advertising/pinterest-migration/reconnect-oauth-pinterest.png)
4. Continúe con el elemento de acción en la sección siguiente

### Habilitar flujos a un nuevo destino {#disable-old-enable-new-flows}

A continuación, debe habilitar los flujos de datos en el nuevo  **[!UICONTROL Pinterest]** Tarjeta de.

1. Ir a **[!UICONTROL Destinos > Examinar]** y utilice el filtro de la pantalla para filtrar el **[!UICONTROL Pinterest]** solo destino.
   ![Filtre los flujos de datos de Pinterest solo en la pestaña Examinar](/help/destinations/assets/catalog/advertising/pinterest-migration/filter-pinterest-browse.png)
2. Seleccione el nombre de la conexión hipervinculada (campaña de fidelización en el ejemplo de captura de pantalla anterior) a la **[!UICONTROL Pinterest]** y cambie el **[!UICONTROL Activar]** cambiar a **el**.
   ![Activar para conexiones nuevas y desactivar para conexiones antiguas](/help/destinations/assets/catalog/advertising/pinterest-migration/enable-disable-toggle-new-destination.png)

<!--

While no disruption to your campaigns is expected, remember to check in the Pinterest UI that everything works as expected.

-->

## ¿Puede compartir algunos cronogramas de alto nivel?

Sí, consulte lo siguiente:

**Para el 16 de noviembre de 2023**: el nuevo destino está listo y debería ver dos tarjetas de Pinterest en paralelo en el catálogo hasta que Pinterest deje de admitir la antigua API v4. Todos los flujos de datos existentes en la tarjeta de Pinterest actual se copian en el nuevo destino.

![Destino de Pinterest antiguo y nuevo en paralelo](/help/destinations/assets/catalog/advertising/pinterest-migration/pinterest-two-cards-side-by-side.png)

<!--

>[!IMPORTANT]
>
>After November 16th, 2023 the legacy Pinterest destination is marked **[!UICONTROL Deprecating]**. <span class="preview">Any changes that you make to dataflows to the (Deprecating) Pinterest destination after November 16th will *not* be automatically carried over to the new Pinterest destination. </span>
>For example, we *do not recommend* that you activate new audiences to the old destination after November 16th. If you do that, you will then have to follow the [regular activation steps](/help/destinations/ui/activate-segment-streaming-destinations.md) to add the audience to the new destination once the customer actions are taken.

-->

**Para el 15 de diciembre de 2023**: <span class="preview">Acción del cliente 1</span>. Debe volver a autenticarse en Pinterest para que la nueva tarjeta esté conectada a Pinterest. Ver instrucciones completas en [esta sección](#reauthenticate).

<span class="preview">Acción del cliente 2</span>A continuación, debe habilitar los flujos de datos en la nueva tarjeta. Ver instrucciones completas en [esta sección](#disable-old-enable-new-flows).

<!--

>[!IMPORTANT]
>
>After December 15th, 2023, Adobe does not guarantee the integrity of dataflows to the old **[!UICONTROL (Deprecating) Pinterest]** destination.

-->

**Después del 18 de enero de 2024**: <span class="preview">Pinterest ha desactivado el acceso a la API del anunciante V4. Los clientes de Real-Time CDP que no hayan actualizado al nuevo destino encontrarán ahora que sus flujos de datos al destino de Pinterest fallan. [Volver a autenticar en Pinterest](#reauthenticate) y [habilitar los flujos de datos](#disable-old-enable-new-flows) al destino actualizado para reanudar las campañas en Pinterest.</span>

<!--

## Other items to note

After you enable the dataflows on the new destination card and disable the dataflows on the old destination cards, you should see no disruption in your campaigns or in the numbers of qualified profiles in the audiences coming in from Adobe Real-Time CDP.

-->
