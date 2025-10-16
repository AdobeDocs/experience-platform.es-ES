---
title: Información general sobre eventos de flujo capilar
description: Aprenda a transmitir datos de Capillary a Experience Platform.
badge: Beta
exl-id: 3b8eb2f6-3b4a-4b91-89d4-b6d9027c6ab4
source-git-commit: 428aed259343f56a2bf493b40ff2388340fffb7b
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 1%

---

# [!DNL Capillary Streaming Events]

>[!AVAILABILITY]
>
>El origen [!DNL Capillary Streaming Events] está en la versión beta. Lea los [términos y condiciones](../../home.md#terms-and-conditions) en la descripción general de orígenes para obtener más información sobre el uso de orígenes etiquetados como beta.

[!DNL Capillary Technologies] es una plataforma líder de lealtad y participación, en la que confían más de 300 marcas en todo el mundo. Utilice el origen [!DNL Capillary Streaming Events] para permitir que su empresa transmita sin problemas perfiles de clientes, datos de fidelidad y eventos transaccionales de [!DNL Capillary] a Adobe Experience Platform. Conecte el origen de [!DNL Capillary] para habilitar la personalización en tiempo real, la segmentación de audiencia avanzada y la orquestación de campaña omnicanal.

Al integrar [!DNL Capillary] con Experience Platform, puede:

* Sincroniza **puntos de fidelidad, niveles y recompensas** en tiempo real.
* Enviar **datos transaccionales** a Experience Platform para su análisis y activación.
* Aproveche Real-Time CDP, Experience Platform y Adobe Journey Optimizer para la segmentación, orquestación de recorrido y personalización.

## Requisitos previos

Antes de conectar [!DNL Capillary] a Adobe Experience Platform, asegúrese de que dispone de lo siguiente:

* Una **ID de organización de Adobe** válida y acceso a una zona protegida de Experience Platform habilitada.
* Debe tener los permisos para **[!UICONTROL Ver fuentes]** y **[!UICONTROL Administrar fuentes]** habilitados en su cuenta para conectar su cuenta de [!DNL Capillary] a Experience Platform. Póngase en contacto con el administrador del producto para obtener los permisos necesarios. Para obtener más información, lea la [guía de la interfaz de usuario de control de acceso](../../../access-control/ui/overview.md).

### Creación de un esquema

Debe crear un esquema del Modelo de datos de experiencia (XDM) para describir un conjunto de datos que pueda almacenar los posibles campos y tipos de datos que se enviarán desde [!DNL Capillary].

1. Inicie sesión en Adobe Experience Platform y acceda a Experience Platform mediante el inicio de sesión de su organización.
2. En el panel de navegación izquierdo, seleccione **[!UICONTROL Esquemas]** para abrir el área de trabajo [!UICONTROL Esquemas].
3. Seleccione **[!UICONTROL Crear esquema]** en la esquina superior derecha.
4. En el cuadro de diálogo Crear esquema, elija entre **[!UICONTROL Creación manual]** (Agregue campos y grupos de campos usted mismo) o **[!UICONTROL Creación asistida por ML]** (Cargue un archivo CSV y utilice el aprendizaje automático para generar un esquema recomendado).
5. Elija una clase base para el esquema (por ejemplo, XDM Individual Profile, XDM ExperienceEvent u Other). Si selecciona **[!UICONTROL Otros]**, puede seleccionar entre las clases personalizadas o estándar disponibles.
6. Escriba un nombre y una descripción descriptivos para el esquema.
7. Utilice el Editor de esquemas para lo siguiente: Agregar grupos de campos (bloques de campos reutilizables), definir campos individuales (personalizar nombres, tipos de datos y opciones) y, opcionalmente, crear tipos de datos o grupos de campos personalizados si los existentes no se ajustan a sus necesidades.
8. Revise la estructura de esquema en el lienzo. Seleccione **[!UICONTROL Finish]** para crear el esquema.
9. (Opcional) Edite campos, agregue descripciones y ajuste grupos de campos según sea necesario en el Editor de esquemas.

Para obtener instrucciones detalladas sobre cómo crear un esquema XDM, lea la guía de [creación de un esquema con el editor de esquemas](../../../xdm/tutorials/create-schema-ui.md).

### Crear un conjunto de datos

A continuación, debe crear un conjunto de datos que haga referencia al esquema que acaba de crear.

1. En la interfaz de usuario de Experience Platform, seleccione [!UICONTROL Conjuntos de datos] en el panel de navegación izquierdo para abrir el área de trabajo [!UICONTROL Conjuntos de datos].
2. Seleccione **[!UICONTROL Crear conjunto de datos]** en la parte superior derecha.
3. En las opciones de creación, seleccione **[!UICONTROL Crear conjunto de datos a partir del esquema]**.
4. En la lista, busque y seleccione el esquema XDM creado anteriormente. Cuando encuentre el esquema, seleccione **[!UICONTROL Siguiente]**.
5. Introduzca un nombre único y descriptivo para el conjunto de datos.
6. De forma opcional, agregue una descripción que ayude a los usuarios futuros a identificar el conjunto de datos.
7. Seleccione **[!UICONTROL Finalizar]** para crear el conjunto de datos.

Para obtener instrucciones detalladas sobre cómo crear un conjunto de datos, lea la [guía de IU de conjuntos de datos](../../../catalog/datasets/user-guide.md).

## Conectar [!DNL Capillary Streaming Events] a Experience Platform

Una vez que haya completado la configuración del requisito previo para [!DNL Capillary], lea el [[!DNL Capillary Streaming Events] tutorial de la interfaz de usuario](../../tutorials/ui/create/loyalty/capillary.md) para saber cómo puede conectar su cuenta y transmitir datos de [!DNL Capillary] a Experience Platform.
