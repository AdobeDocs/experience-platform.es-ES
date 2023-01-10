---
keywords: Experience Platform;inicio;Data Science Workspace;temas populares;control de acceso;simulador de pruebas;paquete de inteligencia;funciones dsw;acceso dsw;Adobe Experience Platform Intelligence;inteligencia;paquete de inteligencia aep
solution: Experience Platform
title: Acceso y funciones de Data Science Workspace
description: El siguiente documento describe los permisos de Data Science Workspace y el acceso a las funciones.
exl-id: 6759fea4-adb9-4e4e-9f3d-e0e8c885b1dd
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 2%

---

# Acceso y funciones de Data Science Workspace

El siguiente documento describe los permisos de Data Science Workspace y el acceso a las funciones.

![Fichas DSW](./images/access/platform-tabs.png)

- **Portátiles:** Proporciona un entorno de desarrollo interactivo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analizar y modelar sus datos en Experience Platform.
- **Modelos:** Proporciona herramientas que se utilizan para crear, publicar y almacenar fórmulas y modelos de aprendizaje automático avanzados. Para obtener más información, consulte la [crear y publicar un modelo de aprendizaje automático](./models-recipes/create-publish-model.md) tutorial.
- **Servicios:** Contiene ambos servicios proporcionados por el Adobe, como [Servicios AI/ML](../intelligent-services/home.md) y cualquier servicio personalizado que haya creado con Data Science Workspace.

¿Por qué solo veo la pestaña Servicios?

- Es posible que su organización solo tenga derecho a Adobe Real-time Customer Data Platform (Real-Time CDP), que incluye el servicio AI/ML del cliente.

Si no puede ver ninguno de los **Ciencia de datos** y desee utilizar las funciones de Data Science Workspace, póngase en contacto con el administrador de su empresa para comprobar si dispone de una licencia de Adobe Experience Platform Intelligence.

## Empaquetado de Data Science Workspace

Las funcionalidades de Data Science Workspace están disponibles en el paquete de Adobe Experience Platform Intelligence y en el complemento de Advanced Intelligence Pack

La siguiente tabla describe algunas de las diferencias clave entre las autorizaciones de Data Science Workspace con y sin el complemento de Advanced Intelligence Pack:

>[!NOTE]
>
>Puede obtener una licencia de más de un Advanced Intelligence Pack Addon y el aumento de la capacidad se agrega a su asignación general. Por ejemplo, si tiene licencia de dos complementos de Adobe Experience Platform Advanced Intelligence Pack, tiene derecho a un total de 20 usuarios de Notebook simultáneos.

| Derechos de Data Science Workspace | Solo paquete de inteligencia de Adobe Experience Platform | Adobe Experience Platform Intelligence más el complemento Advanced Intelligence Pack |
| --- | :---: | :---: |
| Número de usuarios de portátiles admitidos. | 5 usuarios simultáneos | El primer paquete agrega 5 usuarios simultáneos y las compras adicionales agregan 10 usuarios simultáneos por paquete. |
| Permite Jupyter Notebooks integrados para análisis de datos exploratorios y creación de modelos. | X (admite bibliotecas R, Python y Scala) | X (añade bibliotecas PySpark y Spark ML) |
| Integración nativa con Query Service. Capacidad para explorar y dar forma a conjuntos de datos mediante SQL en portátiles. | X | X |
| Acceso a plantillas de portátiles creadas previamente para análisis predictivos. | X | X |
| Capacite y puntee manualmente los modelos con Jupyter Notebooks. | X | X |
| Implemente y operacionalice modelos con la capacidad de programar trabajos de formación e inferencias. |  | X |
| Marco de fórmula para configurar, evaluar, entrenar, puntuar y publicar fácilmente modelos en producción. |  | X |
| Experimentación y evaluación del modelo impulsado por la interfaz de usuario. |  | X |
| Compatibilidad de aprendizaje profundo para los modelos Tensorflow (GPU Compute). |  | X |
| Cálculo distribuido basado en chispas para entrenar y puntuar con conjuntos de datos grandes (10MM + filas). |  | X |

## Control de acceso

El control de acceso para el Experience Platform se administra a través de la variable [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles de producto del Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [información general sobre el control de acceso](../access-control/home.md) para obtener más información.

Para utilizar Data Science Workspace, el permiso &quot;Administrar Data Science Workspace&quot; debe estar habilitado. La siguiente tabla describe los efectos de habilitar o deshabilitar este permiso:

| Permiso | Habilitado | Desactivado |
|---|---|---|
| Administrar Data Science Workspace | Proporciona acceso a todos los servicios de Data Science Workspace. | El acceso a la API y la interfaz de usuario de todos los servicios de Data Science Workspace está desactivado. Aunque está desactivado, al seleccionar la opción **Portátiles**, **Modelos** y **Servicios** no se puede usar. <li>Acceso a **Servicios** puede que siga estando disponible a través de Adobe Real-time Customer Data Platform (Real-Time CDP).</li> |

## Compatibilidad con Sandbox

Los entornos limitados son particiones virtuales dentro de una sola instancia de Experience Platform. Cada instancia de Platform admite varios entornos limitados de producción y sin producción, cada uno de los cuales mantiene su propia biblioteca de recursos de Platform. Los entornos limitados que no son de producción permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar a los entornos limitados de producción. Para obtener más información sobre los entornos limitados, consulte la [información general sobre los entornos limitados](../sandboxes/home.md).

Actualmente, Data Science Workspace tiene la siguiente limitación de entornos limitados:

- Los recursos de cómputo se comparten entre los entornos limitados de producción y sin producción.

## Pasos siguientes

Este documento describe los diferentes tipos de acceso y características disponibles en Data Science Workspace.

Para obtener más información sobre Data Science Workspace, como un flujo de trabajo diario completo, comience por leer la [Recorrido por Data Science Workspace](./walkthrough.md) documentación. Para obtener información más general, consulte la [Información general de Data Science Workspace](./home.md).
