---
keywords: ver perfiles rtcdp;vista de perfil rtcdp;perfiles rtcdp
title: Examen de perfiles en Real-Time Customer Data Platform
description: Adobe Real-Time Customer Data Platform permite examinar los datos del perfil del cliente en tiempo real mediante la interfaz de usuario de Adobe Experience Platform.
feature: Get Started, Profiles
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Examen de perfiles en Real-Time Customer Data Platform

El Perfil del cliente en tiempo real crea una vista integral de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. A medida que se agregan perfiles individuales en función de los datos que se introducen en el sistema desde varias fuentes, cada perfil se convierte en una cuenta procesable con marca de tiempo de cada interacción que el cliente tiene con su marca.

En la interfaz de usuario de Adobe Experience Platform, puede ver estos perfiles de solo lectura y ver información importante con respecto a cada uno de sus clientes individuales, incluidas sus preferencias, eventos anteriores, interacciones y las audiencias a las que pertenece el individuo.

Adobe Real-Time Customer Data Platform se basa en Adobe Experience Platform y, por lo tanto, puede utilizar las funcionalidades de visualización de perfiles de la interfaz de usuario de Experience Platform. Para obtener una guía detallada sobre la visualización de perfiles de clientes en la interfaz de usuario de Experience Platform, consulte la [guía del usuario del Perfil del cliente en tiempo real](../../profile/ui/user-guide.md).

## Mejoras de perfil para Real-Time CDP, B2B edition

Además de las funciones de exploración de perfiles admitidas por Adobe Experience Platform, Real-Time CDP, los usuarios de B2B edition pueden acceder a los atributos y eventos B2B dentro del perfil del cliente en las pestañas [!UICONTROL Attributes] y [!UICONTROL Events], respectivamente. Los datos B2B también se pueden usar para realizar la segmentación, y esas audiencias aparecen en la pestaña [!UICONTROL Audience membership] del cliente junto con audiencias que no son B2B.

Real-Time CDP, B2B edition también le permite examinar [!UICONTROL Accounts], [!UICONTROL Opportunities] y [!UICONTROL Source records] desde los orígenes empresariales asociados a un cliente individual.

Para explorar estas mejoras, comience por seguir los pasos descritos en la [guía del usuario del perfil del cliente en tiempo real](../../profile/ui/user-guide.md) para examinar un perfil mediante la política de combinación o el área de nombres de identidad.

![](images/b2b-browse-profile.png)

Los detalles del perfil incluyen acceso a las pestañas [!UICONTROL Accounts], [!UICONTROL Opportunities] y [!UICONTROL Source records], además de la información estándar proporcionada en el perfil del cliente, que también se ha mejorado con eventos y atributos B2B.

![](images/b2b-profile-detail.png)

Para obtener más información sobre los detalles del perfil proporcionados en la interfaz de usuario de Experience Platform, consulte la sección [detalles de la documentación del panel Perfiles](../../dashboards/guides/profiles.md#browse-profiles).

### Pestaña Cuentas

Seleccione **[!UICONTROL Accounts]** para ver una lista de cuentas relacionadas con el perfil. Esta lista incluye información básica del perfil de la cuenta, como el nombre, el sitio web y el sector de la cuenta, así como un vínculo al perfil de la cuenta.

Para obtener más información sobre cómo ver y explorar perfiles de cuenta, comience por leer la [descripción general de los perfiles de cuenta](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Pestaña Oportunidades

La ficha **[!UICONTROL Opportunities]** proporciona detalles relacionados con las oportunidades abiertas y cerradas relacionadas con la cuenta. Estas oportunidades se pueden ingerir en Experience Platform desde varias fuentes. Sin embargo, Real-Time CDP y B2B edition facilitan a los especialistas en marketing la tarea de ver todas estas oportunidades juntas en un solo lugar.

Cada oportunidad incluye información como el nombre de la oportunidad, su cantidad, fase y si la oportunidad está abierta, cerrada, ganada o perdida.

![](images/b2b-profile-opportunities.png)

### Pestaña registros de Source

La pestaña **[!UICONTROL Source records]** le permite ver fácilmente los registros de varios orígenes procedentes de los orígenes de empresa que contribuyen al perfil único del cliente. Además de [!UICONTROL Person source key] y la dirección de correo electrónico, cada registro de origen también proporciona el tipo de registro (por ejemplo, un registro de &quot;contacto&quot; o &quot;posible cliente&quot;), así como el origen.

![](images/b2b-profile-source-records.png)
