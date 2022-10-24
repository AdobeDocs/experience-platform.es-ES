---
keywords: ver perfiles rtcdp;vista de perfil rtcdp;perfiles rtcdp
title: Exploración de perfiles en Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform le permite examinar los datos del perfil del cliente en tiempo real mediante la interfaz de usuario de Adobe Experience Platform.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Exploración de perfiles en Real-time Customer Data Platform

El perfil del cliente en tiempo real crea una vista holística de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. Como los perfiles individuales se agregan en función de los datos que se introducen en el sistema desde varias fuentes, cada perfil se convierte en una cuenta procesable con marca de tiempo de cada interacción que el cliente tenga con su marca.

En la interfaz de usuario de Adobe Experience Platform, puede ver estos perfiles de solo lectura y ver información importante sobre cada uno de sus clientes, incluidas sus preferencias, eventos pasados, interacciones y los segmentos a los que pertenece el individuo.

Adobe Real-time Customer Data Platform se basa en Adobe Experience Platform y, por lo tanto, puede utilizar las funciones de visualización de perfiles de la interfaz de usuario del Experience Platform. Para obtener una guía detallada sobre la visualización de perfiles de clientes dentro de la interfaz de usuario de Platform, consulte la [Guía del usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md).

## Mejoras de perfil para Real-Time CDP, B2B Edition

Además de las funciones de exploración de perfiles compatibles con Adobe Experience Platform, los usuarios de Real-Time CDP y B2B Edition pueden acceder a los atributos y eventos B2B dentro del perfil del cliente en la [!UICONTROL Atributos] y [!UICONTROL Eventos] , respectivamente. Los datos B2B también se pueden utilizar para realizar segmentaciones, en las que los segmentos aparecen bajo el [!UICONTROL Pertenencia a segmentos] junto a los segmentos que no sean B2B.

Real-Time CDP, B2B Edition también le permite explorar [!UICONTROL Cuentas], [!UICONTROL Oportunidades]y [!UICONTROL Registros de origen] desde las fuentes empresariales asociadas a un cliente individual.

Para explorar estas mejoras, comience por seguir los pasos descritos en la sección [Guía del usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md) para examinar un perfil combinando directiva o área de nombres de identidad.

![](images/b2b-browse-profile.png)

El detalle del perfil incluye el acceso a [!UICONTROL Cuentas], [!UICONTROL Oportunidades]y [!UICONTROL Registros de origen] además de la información estándar proporcionada en el perfil del cliente que también se ha mejorado con los eventos y atributos B2B.

![](images/b2b-profile-detail.png)

### Ficha Cuentas

Select **[!UICONTROL Cuentas]** para ver una lista de cuentas relacionadas con el perfil. Esta lista incluye información básica del perfil de la cuenta, como el nombre, el sitio web y el sector de la cuenta, así como un vínculo al perfil de la cuenta.

Para obtener más información sobre la visualización y exploración de perfiles de cuenta, comience por leer la [información general sobre perfiles de cuenta](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Ficha Oportunidades

La variable **[!UICONTROL Oportunidades]** proporciona detalles relacionados con las oportunidades abiertas y cerradas relacionadas con la cuenta. Estas oportunidades pueden ser incorporadas en Experience Platform de múltiples fuentes, sin embargo, Real-Time CDP, B2B Edition facilita a los especialistas en marketing ver todas estas oportunidades juntas en un solo lugar.

Cada oportunidad incluye información como el nombre de la oportunidad, su cantidad, etapa y si la oportunidad está abierta, cerrada, ganada o perdida.

![](images/b2b-profile-opportunities.png)

### Ficha Registros de origen

La variable **[!UICONTROL Registros de origen]** permite ver fácilmente los múltiples registros de origen procedentes de las fuentes empresariales que contribuyen al perfil único del cliente. Además del [!UICONTROL Clave de origen de persona] y dirección de correo electrónico, cada registro de origen también proporciona el tipo de registro (por ejemplo, un registro de &quot;contacto&quot; o &quot;posible cliente&quot;), así como la fuente.

![](images/b2b-profile-source-records.png)
