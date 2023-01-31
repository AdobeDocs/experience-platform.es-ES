---
keywords: Experience Platform;guía del usuario;ai del cliente;temas populares;controles de acceso;crear modelo;
solution: Experience Platform
feature: Customer AI
title: Control de acceso para Customer AI
description: Este documento proporciona información sobre el control de acceso basado en atributos para Customer AI.
source-git-commit: 66d20dc1141ff33211635ba74d320350f8b27fb7
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Control de acceso basado en atributos

>[!IMPORTANT]
>
>El control de acceso basado en atributos está disponible actualmente solo en una versión limitada.

[Control de acceso basado en atributos](../../../access-control/abac/overview.md) es una función de Adobe Experience Platform que permite a los administradores controlar el acceso a objetos específicos o a funciones basadas en atributos. Los atributos pueden ser metadatos agregados a un objeto, como una etiqueta agregada a un campo o segmento de esquema. Un administrador define políticas de acceso que incluyen atributos para administrar los permisos de acceso de los usuarios.

Esta funcionalidad le permite etiquetar campos de esquema del Modelo de datos de experiencia (XDM) con etiquetas que definen ámbitos organizativos o de uso de datos. En paralelo, los administradores pueden utilizar la interfaz de administración de usuarios y funciones para definir las políticas de acceso que rodean los campos de esquema XDM y administrar mejor el acceso dado a los usuarios o grupos de usuarios (usuarios internos, externos o de terceros). Además, el control de acceso basado en atributos permite a los administradores administrar el acceso a segmentos específicos.

Mediante el control de acceso basado en atributos, los administradores de su organización pueden controlar el acceso de los usuarios a los datos personales confidenciales (SPD) y a la información de identificación personal (PII) en todos los flujos de trabajo y recursos de Platform. Los administradores pueden definir funciones de usuario que solo tengan acceso a campos y datos específicos que se correspondan con esos campos.

Debido al control de acceso basado en atributos, algunos campos y funcionalidades tendrían acceso restringido y no estarían disponibles para algunos modelos de servicio de Customer AI. Algunos ejemplos son &quot;Identidad&quot;, &quot;Definición de puntuación&quot; y &quot;Clonar&quot;.

![El espacio de trabajo de Customer AI con los campos restringidos del modelo de servicio resaltados.](../images/user-guide/unavailable-functionalities.png)

En la parte superior del espacio de trabajo de Customer AI **página perspectivas**, observe que los detalles en la barra lateral, la definición de puntuación, la identidad y los atributos de perfil muestran &quot;Acceso restringido&quot;.

![Espacio de trabajo de Customer AI con los campos restringidos del esquema resaltados.](../images/user-guide/access-restricted.png)

Cuando se obtienen vistas previas de conjuntos de datos con esquema restringido en la variable **[!UICONTROL Creación del flujo de trabajo del modelo]** , aparece una advertencia que indica que [!UICONTROL Debido a las restricciones de acceso, cierta información no se muestra en la vista previa del conjunto de datos.]

![Espacio de trabajo de Customer AI con los campos restringidos de los conjuntos de datos de vista previa con resultados de esquema restringidos resaltados.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Después de crear un modelo con información restringida y continuar con el **[!UICONTROL Definir objetivo]** , aparece una advertencia en la parte superior: [!UICONTROL Debido a restricciones de acceso, cierta información no se muestra en la configuración.]

![El espacio de trabajo de Customer AI con los campos restringidos del modelo de servicio resaltados.](../images/user-guide/information-not-displayed-save-and-exit.png)

Cuando se utiliza el control de acceso, la variable **Ver Customer AI** y **Administrar la IA del cliente** los privilegios otorgan acceso a diferentes funcionalidades de Customer AI. La variable **Administrar la IA del cliente** permiso le permite **crear**,**actualizar**, **delete**, **enable** o **disable** un modelo while **Ver Customer AI** permite leerlo o verlo. La variable **crear**, **actualizar** y **delete** las acciones se registran mediante registros de auditoría.

Consulte la documentación para aprender [asignación de permisos para control de acceso](../../../help/access-control/home.md) o cómo [usar registros de auditoría para supervisar el acceso y la actividad](../../../help/landing/governance-privacy-security/audit-logs/overview.md).

## Pasos siguientes

Al leer esta guía, se le han introducido los principios principales del control de acceso en [!DNL Experience Platform]. Ahora puede continuar con el [guía del usuario de control de acceso](./ui/overview.md) para ver los pasos detallados sobre cómo usar la variable [!DNL Admin Console] para crear perfiles de producto y asignar permisos para [!DNL Platform].