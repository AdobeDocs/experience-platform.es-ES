---
keywords: Experience Platform;guía de usuario;inteligencia artificial aplicada al cliente;temas populares;controles de acceso;crear modelo;
solution: Experience Platform
feature: Customer AI
title: Control de acceso para la inteligencia artificial aplicada al cliente
description: Este documento proporciona información sobre el control de acceso basado en atributos para la inteligencia artificial aplicada al cliente.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Control de acceso basado en atributos

>[!IMPORTANT]
>
>Actualmente, el control de acceso basado en atributos solo está disponible en una versión limitada.

[Control de acceso basado en atributos](../../../access-control/abac/overview.md) es una capacidad de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o funcionalidades basadas en atributos. Los atributos pueden ser metadatos añadidos a un objeto, como una etiqueta añadida a un campo o segmento de esquema. Un administrador define directivas de acceso que incluyen atributos para administrar permisos de acceso de usuarios.

Esta funcionalidad le permite etiquetar campos de esquema del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos organizativos o de uso de datos. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir políticas de acceso alrededor de los campos de esquema XDM y administrar mejor el acceso dado a usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Además, el control de acceso basado en atributos permite a los administradores gestionar el acceso a segmentos específicos.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD) y a la información de identificación personal (PII) en todos los flujos de trabajo y recursos de la plataforma. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que correspondan a esos campos.

Debido al control de acceso basado en atributos, algunos campos y funcionalidades tendrían acceso restringido y no estarían disponibles para determinados modelos de servicio de inteligencia artificial aplicada al cliente. Algunos ejemplos son &quot;Identidad&quot;, &quot;Definición de puntuación&quot; y &quot;Clonar&quot;.

![El espacio de trabajo de inteligencia artificial aplicada al cliente con los campos restringidos de los resultados del modelo de servicio resaltados.](../images/user-guide/unavailable-functionalities.png)

En la parte superior del espacio de trabajo de Customer AI **página de perspectivas**, observe que los detalles de la barra lateral, la definición de puntuación, la identidad y los atributos de perfil muestran &quot;Acceso restringido&quot;.

![Espacio de trabajo de inteligencia artificial aplicada al cliente con los campos restringidos del esquema resaltados.](../images/user-guide/access-restricted.png)

Cuando previsualiza conjuntos de datos con esquema restringido en **[!UICONTROL Crear flujo de trabajo de modelo]** página, aparece una advertencia para indicarle que [!UICONTROL Debido a restricciones de acceso, cierta información no se muestra en la vista previa del conjunto de datos.]

![El espacio de trabajo de inteligencia artificial aplicada al cliente con los campos restringidos de los conjuntos de datos de vista previa con resultados de esquema restringidos resaltados.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Después de crear un modelo con información restringida, continúe con la **[!UICONTROL Definir meta]** , se muestra una advertencia en la parte superior: [!UICONTROL Debido a restricciones de acceso, cierta información no se muestra en la configuración.]

![El espacio de trabajo de inteligencia artificial aplicada al cliente con los campos restringidos de los resultados del modelo de servicio resaltados.](../images/user-guide/information-not-displayed-save-and-exit.png)

Cuando se utiliza el control de acceso, la variable **Ver inteligencia artificial aplicada al cliente** y **Administrar inteligencia artificial aplicada al cliente** Los privilegios de conceden acceso a diferentes funcionalidades de la inteligencia artificial aplicada al cliente. El **Administrar inteligencia artificial aplicada al cliente** El permiso le permite **crear**,**actualizar**, **eliminar**, **habilitar**, o **disable** un modelo mientras **Ver inteligencia artificial aplicada al cliente** permite leerlo o verlo. El **crear**, **actualizar** y **eliminar** las acciones se registran mediante registros de auditoría.

Consulte la documentación para aprender [asignación de permisos para el control de acceso](../../../access-control/home.md) o cómo [usar registros de auditoría para monitorizar el acceso y la actividad](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Pasos siguientes

Al leer esta guía, se le han introducido los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar con el [guía del usuario de control de acceso](../overview.md) para ver los pasos detallados sobre cómo usar la variable [!DNL Admin Console] para crear perfiles de producto y asignar permisos para [!DNL Platform].