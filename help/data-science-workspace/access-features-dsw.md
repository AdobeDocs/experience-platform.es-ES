---
keywords: Experience Platform;inicio;Workspace de ciencia de datos;temas populares;control de acceso;espacio aislado;paquete de inteligencia;funciones de dsw;acceso de dsw;Adobe Experience Platform Intelligence;intelligence;paquete de inteligencia de aep
solution: Experience Platform
title: Acceso y funciones de Data Science Workspace
description: El siguiente documento describe los permisos de Data Science Workspace y el acceso a las funciones de.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 2%

---

# Acceso y funciones de Data Science Workspace

El siguiente documento describe los permisos de Data Science Workspace y el acceso a las funciones de.

![fichas DSW](./images/access/platform-tabs.png)

- **Notebooks:** Proporciona un entorno de desarrollo interactivo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analizar y modelar sus datos en el Experience Platform.
- **Modelos:** Proporciona herramientas para crear, publicar y almacenar fórmulas y modelos avanzados de aprendizaje automático. Para obtener más información, visite el tutorial [crear y publicar un modelo de aprendizaje automático](./models-recipes/create-publish-model.md).
- **Servicios:** Contiene servicios proporcionados por el Adobe, como [servicios AI/ML](../intelligent-services/home.md) y cualquier servicio personalizado que haya creado con Data Science Workspace.

¿Por qué solo veo la pestaña Servicios?

- Es posible que su organización solo tenga derecho a Adobe Real-time Customer Data Platform (Real-Time CDP), que incluye el servicio AI/ML de inteligencia artificial aplicada al cliente.

Si no puede ver ninguna de las pestañas de **Data Science** y desea utilizar las funciones de Data Science Workspace, póngase en contacto con el administrador de su empresa para comprobar si tiene una licencia de Adobe Experience Platform Intelligence.

## Empaquetado de Data Science Workspace

Las funcionalidades de Data Science Workspace están disponibles en el paquete Adobe Experience Platform Intelligence y en el complemento Advanced Intelligence Pack

La siguiente tabla describe algunas de las diferencias clave para las autorizaciones de Data Science Workspace con y sin el complemento Advanced Intelligence Pack:

>[!NOTE]
>
>Puede autorizar más de un complemento del paquete de inteligencia avanzada y la mayor capacidad se añade a sus derechos generales. Por ejemplo, si tiene licencia para 2 complementos del paquete de inteligencia avanzada de Adobe Experience Platform, tiene derecho a un total de 20 usuarios simultáneos de Notebook.

| Derechos de Data Science Workspace | Solo paquete de Adobe Experience Platform Intelligence | Complemento de Adobe Experience Platform Intelligence plus Advanced Intelligence Pack |
| --- | :---: | :---: |
| Número de usuarios de Notebook admitidos. | 5 usuarios simultáneos | El primer paquete agrega 5 usuarios simultáneos y las compras adicionales agregan 10 usuarios simultáneos por paquete. |
| Permite el análisis de datos exploratorios y la creación de modelos con Jupyter Notebooks integrado. | X (admite bibliotecas R, Python y Scala) | X (Añade bibliotecas PySpark y Spark ML) |
| Integración nativa con el servicio de consultas. Capacidad para explorar y dar forma a conjuntos de datos utilizando SQL en blocs de notas. | X | X |
| Acceso a plantillas de bloc de notas creadas previamente para análisis predictivos. | X | X |
| Entrene y puntee manualmente modelos con Jupyter Notebooks. | X | X |
| Implemente y ponga en funcionamiento modelos con la capacidad de programar trabajos de formación e inferencias. | | X |
| Marco de fórmula para configurar, evaluar, entrenar, calificar y publicar fácilmente modelos en producción. |  | X |
| Experimentación y evaluación de modelos impulsados por la IU. | | X |
| Soporte de aprendizaje profundo para modelos Tensorflow (GPU Compute). | | X |
| Equipo distribuido basado en Spark para entrenar y puntuar con conjuntos de datos grandes (10 MM + filas). | | X |

## Control de acceso

El control de acceso del Experience Platform se administra mediante [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto en Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [descripción general del control de acceso](../access-control/home.md) para obtener más información.

Para utilizar Data Science Workspace, debe habilitarse el permiso &quot;Manage Data Science Workspace&quot;. En la tabla siguiente se describen los efectos de tener este permiso habilitado o deshabilitado:

| Permiso | Habilitado | Desactivado |
|---|---|---|
| Administrar Data Science Workspace | Proporciona acceso a todos los servicios de Data Science Workspace. | El acceso a la API y la IU a todos los servicios de Data Science Workspace está desactivado. Mientras está deshabilitada, se impide seleccionar las páginas **Notebooks**, **Models** y **Services**. <li>Es posible que el acceso a **Servicios** siga estando disponible a través de Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Compatibilidad con zona protegida

Las zonas protegidas son particiones virtuales en una sola instancia de Experience Platform. Cada instancia de Platform admite varios entornos limitados de producción y sin producción, cada uno con su propia biblioteca de recursos de Platform. Los entornos limitados que no son de producción le permiten probar funciones, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a los entornos limitados de producción. Para obtener más información sobre las zonas protegidas, consulte la [descripción general de las zonas protegidas](../sandboxes/home.md).

Actualmente, Data Science Workspace tiene la siguiente limitación de zona protegida:

- Los recursos de cómputo se comparten en los entornos limitados de producción y sin producción.

## Pasos siguientes

Este documento describe los diferentes tipos de acceso y funciones disponibles en Data Science Workspace.

Para obtener más información sobre Data Science Workspace, como un flujo de trabajo diario completo, lea la [documentación del tutorial de Data Science Workspace](./walkthrough.md). Para obtener información más general, visite la [Descripción general de Data Science Workspace](./home.md).
