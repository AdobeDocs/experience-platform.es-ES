---
keywords: Experience Platform; hogar; Data Science Espacio de trabajo; temas populares; control de acceso; arenero; inteligencia paquete; características de DSW; Acceso DSW; Adobe Experience Platform Inteligencia; inteligencia; Paquete de inteligencia AEP
solution: Experience Platform
title: Acceso y características a Espacio de trabajo ciencia de datos
description: El siguiente documento describe los permisos de Espacio de trabajo de ciencia de datos y el acceso a las funciones.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 2%

---

# Acceso y funciones de Data Science Workspace

>[!NOTE]
>
>La Espacio de trabajo de ciencia de datos ya no está disponible para su compra.
>
>Esta documentación está destinada a clientes existentes con derechos previos a Data Science Espacio de trabajo.

El siguiente documento describe los permisos de Espacio de trabajo de ciencia de datos y el acceso a las funciones.

![Fichas DSW](./images/access/platform-tabs.png)

- **Blocs de notas:** proporciona un entorno de desarrollo interactivo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analizar y modelar sus datos en Experience Platform.
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

| Derechos de Data Science Workspace | Solo Adobe Experience Platform Intelligence Package | Adobe Experience Platform Intelligence plus Avanzadas Intelligence Pack añadir-on |
| --- | :---: | :---: |
| Número de usuarios de portátiles admitidos. | 5 usuarios simultáneos | El primer paquete agrega 5 usuarios simultáneos y las compras adicionales agregan 10 usuarios simultáneos por paquete. |
| Permite el análisis de datos exploratorios y la creación de modelos con Jupyter Notebooks integrado. | X (admite bibliotecas R, Python y Scala) | X (agrega PySpark y Spark ML bibliotecas) |
| Integración nativa con Query Service. Capacidad para explorar y dar forma a conjuntos de datos utilizando SQL en cuadernos. | X | X |
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
| Administrar Data Science Workspace | Proporciona acceso a todos los servicios de Data Science Workspace. | El acceso a la API y la IU a todos los servicios de Data Science Workspace está desactivado. Mientras está deshabilitada, se impide seleccionar las páginas **Notebooks**, **Models** y **Services**. <li>Es posible que el acceso a **los Servicios** siga estando disponible a través de Adobe Systems Platform de datos del cliente en tiempo real (CDP en tiempo real).</li> |

## Compatibilidad con Sandbox

Los entornos aislados son particiones virtuales dentro de un único instancia de Experience Platform. Cada Platform instancia admite múltiples entornos limitados de producción y no producción, y cada uno mantiene su propio biblioteca de recursos Platform. Los entornos limitados que no son de producción le permiten prueba características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a los entornos limitados de producción. Para obtener más información sobre los entornos limitados, consulte la información general](../sandboxes/home.md) sobre los [entornos limitados.

Actualmente, Data Science Workspace tiene la siguiente limitación de zona protegida:

- Los recursos informáticos se comparten entre los entornos de pruebas de producción y de no producción.

## Pasos siguientes

Este documento describe los diferentes tipos de acceso y características disponibles en Data Science Espacio de trabajo.

Para obtener más información sobre el Espacio de trabajo de ciencia de datos, como un flujo de trabajo diario completo, comience leyendo la [documentación del tutorial](./walkthrough.md) de Data Science Espacio de trabajo. Para obtener más información general, visita la información general](./home.md) de la [Espacio de trabajo Ciencia de datos.
