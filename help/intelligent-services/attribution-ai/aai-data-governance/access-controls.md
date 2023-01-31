---
keywords: Experience Platform;inicio;temas populares;control de acceso;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Control de acceso para la Attribution AI
description: Este documento proporciona información sobre el control de acceso basado en atributos para la Attribution AI.
source-git-commit: 2cce166592c4d4b7f9d62bc3385fb8ccdd74c958
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# Control de acceso

El control de acceso para la Attribution AI se proporciona a través de Adobe Experience Platform en la [Adobe Admin Console](https://adminconsole.adobe.com/). Esta funcionalidad aprovecha los perfiles de producto del Admin Console, que vinculan a los usuarios con permisos y entornos limitados.

Para obtener más información sobre el control de acceso, consulte la [información general sobre el control de acceso](../../access-control/home).

## Control de acceso basado en atributos

>[!IMPORTANT]
>
>El control de acceso basado en atributos está disponible actualmente solo en una versión limitada.

[Control de acceso basado en atributos](../../../help/access-control/abac/overview.md) es una función de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funciones basadas en atributos. Los atributos pueden ser metadatos agregados a un objeto, como una etiqueta agregada a un campo o segmento de esquema. Un administrador define políticas de acceso que incluyen atributos para administrar los permisos de acceso de los usuarios.

Esta funcionalidad le permite etiquetar campos de esquema del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos organizativos o de uso de datos. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir las políticas de acceso que rodean los campos de esquema XDM y administrar mejor el acceso dado a los usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Además, el control de acceso basado en atributos permite a los administradores administrar el acceso a segmentos específicos.

Mediante el control de acceso basado en atributos, los administradores pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD) y a la información de identificación personal (PII) en todos los flujos de trabajo y recursos de Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que se correspondan con esos campos.

Debido al control de acceso basado en atributos, es posible que algunos campos y funcionalidades tengan acceso restringido y no estén disponibles para determinados modelos de servicio de Attribution AI. Algunos ejemplos son &quot;Identidad&quot;, &quot;Definición de puntuación&quot; y &quot;Clonar&quot;.

En la parte superior del espacio de trabajo de Attribution AI **página perspectivas**, los detalles que aparecen en la barra lateral tienen acceso restringido.

![Espacio de trabajo de Attribution AI con los campos de esquema restringidos resaltados.](./images/user-guide/access-restricted.png)

Si selecciona conjuntos de datos con esquemas restringidos en la variable **[!UICONTROL Creación del flujo de trabajo del modelo]** , aparece un signo de advertencia junto al nombre del conjunto de datos con el mensaje : [!UICONTROL Se excluye la información restringida].

![Espacio de trabajo de Attribution AI con los campos restringidos del conjunto de datos resaltados.](./images/user-guide/restricted-info-excluded.png)

Cuando se obtienen vistas previas de conjuntos de datos con esquema restringido en la variable **[!UICONTROL Creación del flujo de trabajo del modelo]** , aparece una advertencia que indica que [!UICONTROL Debido a las restricciones de acceso, cierta información no se muestra en la vista previa del conjunto de datos.]

![El espacio de trabajo de Attribution AI con los resultados de campos de esquema de vista previa restringidos resaltados.](./images/user-guide/restricted-dataset-preview.png)

Después de crear un modelo con información restringida y continuar con el **[!UICONTROL Definir objetivo]** , aparece una advertencia en la parte superior: [!UICONTROL Debido a restricciones de acceso, cierta información no se muestra en la configuración.]

![El espacio de trabajo de Attribution AI con los campos restringidos de los resultados del modelo resaltados.](./images/user-guide/information-not-displayed-save-and-exit.png)

## Pasos siguientes

Al leer esta guía, se le han introducido los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar con el [guía del usuario de control de acceso](./ui/overview.md) para ver los pasos detallados sobre cómo usar la variable [!DNL Admin Console] para crear perfiles de producto y asignar permisos para [!DNL Platform].
