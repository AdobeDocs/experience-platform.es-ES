---
title: Conecte su cuenta de PathFactory a Experience Platform a través de la IU de
description: Aprenda a conectar su cuenta de PathFactory a Experience Platform a través de la interfaz de usuario de.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 2%

---

# Conecte su cuenta de [!DNL PathFactory] a Experience Platform mediante la interfaz de usuario

Este tutorial proporciona pasos sobre cómo conectar los datos de [!DNL PathFactory] visitantes, sesiones y vistas de página a Adobe Experience Platform a través de la interfaz de usuario.

## Introducción

Este tutorial requiere una comprensión práctica de los siguientes componentes de Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): El marco de trabajo estandarizado mediante el cual [!DNL Experience Platform] organiza los datos de la experiencia del cliente.
   * [Aspectos básicos de la composición de esquemas](../../../../../xdm/schema/composition.md): obtenga información sobre los componentes básicos de los esquemas XDM, incluidos los principios clave y las prácticas recomendadas en la composición de esquemas.
   * [Tutorial del editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Aprenda a crear esquemas personalizados mediante la interfaz de usuario del editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): proporciona un perfil de consumidor unificado y en tiempo real basado en los datos agregados de varias fuentes.

Si ya tiene una cuenta de [!DNL PathFactory], puede omitir el resto de este documento y continuar con el tutorial de [introducción de datos de automatización de marketing en Experience Platform mediante la interfaz de usuario](../../dataflow/marketing-automation.md).

### Recopilar credenciales necesarias {#gather-credentials}

Para acceder a su cuenta de PathFactory en Experience Platform, debe proporcionar los siguientes valores:

| Credencial | Descripción |
| ---------- | ----------- |
| Nombre de usuario | Su nombre de usuario de cuenta de PathFactory. Esto es esencial para identificar su cuenta en el sistema. |
| Contraseña | La contraseña asociada a su cuenta de PathFactory. Asegúrese de que se mantenga seguro para evitar el acceso no autorizado. |
| Dominio | El dominio asociado con su cuenta de PathFactory. Normalmente, hace referencia al identificador único de la dirección URL de PathFactory. |
| Token de acceso | Un token único utilizado para la autenticación de API para garantizar la comunicación segura entre sus sistemas y PathFactory. |
| Extremos de API | Puntos finales específicos de API para acceder a los datos: visitantes, sesiones y vistas de páginas. Cada extremo corresponde a diferentes conjuntos de datos que puede recuperar. **Nota:** Están predefinidos por [!DNL PathFactory] y son específicos de los datos a los que desea tener acceso: <ul><li>**Extremo de visitantes**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Punto final de sesiones**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Extremo de vistas de página**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Para obtener instrucciones detalladas sobre cómo proteger y usar sus credenciales, y para obtener información sobre cómo obtener y actualizar su token de acceso, visite el [Centro de soporte de PathFactory](https://support.pathfactory.com/categories/adobe/). Este recurso ofrece guías completas sobre la administración de las credenciales y la garantía de una integración de API eficaz y segura.


## Conectar su cuenta de [!DNL PathFactory]

En la interfaz de usuario de Experience Platform, seleccione **[!UICONTROL Fuentes]** en el panel de navegación izquierdo para acceder al área de trabajo [!UICONTROL Fuentes]. El [!UICONTROL catálogo] muestra una variedad de orígenes admitidos por Experience Platform.

Puede seleccionar la categoría adecuada de la lista de categorías. También puede utilizar la barra de búsqueda para filtrar por un origen específico.

En la categoría [!UICONTROL Automatización de marketing], seleccione **[!UICONTROL PathFactory]** y, a continuación, **[!UICONTROL Configurar]**.

![El catálogo de orígenes con el origen PathFactory seleccionado.](../../../../images/tutorials/create/pathfactory/catalog.png)

Aparecerá la página **[!UICONTROL Conectar con PathFactory]**. En esta página, puede crear una cuenta nueva o utilizar una cuenta existente.

### Nueva cuenta

Para crear una cuenta nueva, selecciona **[!UICONTROL Cuenta nueva]** y proporciona un nombre para tu cuenta, una descripción opcional y las credenciales de autenticación que corresponden a tu cuenta de [!DNL PathFactory].

Cuando termine, seleccione **[!UICONTROL Conectarse al origen]** y deje pasar un tiempo para que se establezca la nueva conexión.

![Interfaz de la nueva cuenta donde puede autenticar una nueva cuenta para PathFactory.](../../../../images/tutorials/create/pathfactory/new.png)

### Cuenta existente

Si ya tiene una cuenta, seleccione **[!UICONTROL Cuenta existente]** y luego seleccione la cuenta que desee usar en la lista que aparece.

![Interfaz de cuenta existente donde puede seleccionar de una lista de cuentas existentes de PathFactory.](../../../../images/tutorials/create/pathfactory/existing.png)

## Pasos siguientes

Al seguir este tutorial, ha establecido una conexión entre su cuenta de [!DNL PathFactory] y Experience Platform. Ahora puede continuar con el siguiente tutorial y [crear un flujo de datos para introducir los datos de automatización de marketing en Experience Platform](../../dataflow/marketing-automation.md).
