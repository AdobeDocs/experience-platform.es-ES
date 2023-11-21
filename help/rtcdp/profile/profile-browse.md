---
keywords: ver perfiles rtcdp;vista de perfil rtcdp;perfiles rtcdp
title: Examen de perfiles en Real-time Customer Data Platform
description: Adobe Real-time Customer Data Platform permite examinar los datos del perfil del cliente en tiempo real mediante la interfaz de usuario de Adobe Experience Platform.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# Examen de perfiles en Real-time Customer Data Platform

El Perfil del cliente en tiempo real crea una vista integral de cada uno de sus clientes individuales, combinando datos de varios canales, incluidos datos en línea, sin conexión, CRM y de terceros. A medida que se agregan perfiles individuales en función de los datos que se introducen en el sistema desde varias fuentes, cada perfil se convierte en una cuenta procesable con marca de tiempo de cada interacción que el cliente tiene con su marca.

En la interfaz de usuario de Adobe Experience Platform, puede ver estos perfiles de solo lectura y ver información importante con respecto a cada uno de sus clientes individuales, incluidas sus preferencias, eventos anteriores, interacciones y las audiencias a las que pertenece el individuo.

Adobe Real-time Customer Data Platform se basa en Adobe Experience Platform y, por lo tanto, puede utilizar las funcionalidades de visualización de perfiles en la interfaz de usuario de Experience Platform. Para obtener una guía detallada para ver los perfiles de los clientes dentro de la interfaz de usuario de Platform, consulte la [Guía del usuario del Perfil del cliente en tiempo real](../../profile/ui/user-guide.md).

## Mejoras de perfil para Real-Time CDP, edición B2B

Además de las funciones de exploración de perfiles admitidas por Adobe Experience Platform, los usuarios de Real-Time CDP, B2B Edition pueden acceder a los atributos y eventos B2B dentro del perfil del cliente en [!UICONTROL Atributos] y [!UICONTROL Eventos] pestañas, respectivamente. Los datos B2B también se pueden utilizar para realizar la segmentación, con esas audiencias que aparecen en el [!UICONTROL Abono a audiencia] pestaña junto a audiencias que no son B2B.

Real-Time CDP, B2B Edition también le permite examinar [!UICONTROL Cuentas], [!UICONTROL Oportunidades], y [!UICONTROL Registros de origen] de entre los orígenes de empresa asociados a un cliente individual.

Para explorar estas mejoras, comience siguiendo los pasos descritos en la sección [Guía del usuario del Perfil del cliente en tiempo real](../../profile/ui/user-guide.md) para examinar un perfil mediante una política de combinación o un área de nombres de identidad.

![](images/b2b-browse-profile.png)

Los detalles del perfil incluyen el acceso a [!UICONTROL Cuentas], [!UICONTROL Oportunidades], y [!UICONTROL Registros de origen] además de la información estándar proporcionada en el perfil del cliente, que también se ha mejorado con eventos y atributos B2B.

![](images/b2b-profile-detail.png)

### Pestaña Cuentas

Seleccionar **[!UICONTROL Cuentas]** para ver una lista de cuentas relacionadas con el perfil. Esta lista incluye información básica del perfil de la cuenta, como el nombre, el sitio web y el sector de la cuenta, así como un vínculo al perfil de la cuenta.

Para obtener más información sobre la visualización y exploración de perfiles de cuenta, comience por leer el [resumen de perfiles de cuenta](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Pestaña Oportunidades

El **[!UICONTROL Oportunidades]** proporciona detalles relacionados con las oportunidades abiertas y cerradas relacionadas con la cuenta. Estas oportunidades se pueden ingerir en Experience Platform desde varias fuentes, pero Real-Time CDP, B2B Edition facilita a los especialistas en marketing la visualización de todas estas oportunidades juntas en un solo lugar.

Cada oportunidad incluye información como el nombre de la oportunidad, su cantidad, fase y si la oportunidad está abierta, cerrada, ganada o perdida.

![](images/b2b-profile-opportunities.png)

### Pestaña Registros de origen

El **[!UICONTROL Registros de origen]** Esta pestaña permite ver fácilmente los registros de varias fuentes procedentes de los orígenes de empresa que contribuyen al perfil único del cliente. Además de las [!UICONTROL Clave de origen de persona] y la dirección de correo electrónico, cada registro de origen también proporciona el tipo de registro (por ejemplo, un registro de &quot;contacto&quot; o &quot;posible cliente&quot;), así como el origen.

![](images/b2b-profile-source-records.png)
