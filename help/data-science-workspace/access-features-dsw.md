---
keywords: Experience Platform;inicio;Área de trabajo de ciencias de datos;temas populares;control de acceso;zona de pruebas;paquete de inteligencia;características de dsw;acceso dsw;Adobe Experience Platform Intelligence;inteligencia;paquete de inteligencia de aplicaciones
solution: Experience Platform
title: Acceso y características del área de trabajo de Data Science
topic: Access and features for data science workspace
description: 'El siguiente documento describe los permisos y el acceso a las funciones de Área de trabajo de ciencia de datos. '
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 3%

---


# Acceso y características de Área de trabajo de Data Science

El siguiente documento describe los permisos y el acceso a las funciones de Área de trabajo de ciencia de datos.

![Fichas DSW](./images/access/platform-tabs.png)

- **Equipos portátiles:** Proporciona un entorno de desarrollo interactivo ([JupyterLab](./jupyterlab/overview.md)) para explorar, analizar y modelar sus datos en Experience Platform.
- **Modelos:** Proporciona herramientas utilizadas para crear, publicar y almacenar fórmulas y modelos avanzados de aprendizaje automático. Para obtener más información, visite el tutorial [crear y publicar un modelo de aprendizaje automático](./models-recipes/create-publish-model.md).
- **Servicios:** Contiene servicios proporcionados por Adobes como  [Intelligent ](../intelligent-services/home.md) Services y cualquier servicio personalizado que haya creado con Data Science Workspace.

¿Por qué solo veo la ficha Servicios?

- Es posible que su organización solo tenga derecho a la plataforma de datos del cliente en tiempo real (RTCDP), que incluye la API del cliente de servicio inteligente.

Si no puede ver ninguna de las fichas **Data Science** y desea utilizar las funciones de Data Science Workspace, póngase en contacto con el administrador de compañías para comprobar si dispone de una licencia de Adobe Experience Platform Intelligence.

## Addon del paquete de Adobe Experience Platform Intelligence

La siguiente tabla describe algunas de las diferencias clave para el espacio de trabajo de ciencias de datos con y sin el complemento del paquete de inteligencia de Adobe Experience Platform:

>[!NOTE]
>
>Puede obtener licencias para más de un complemento del paquete de inteligencia y se agrega el aumento de la capacidad a la asignación general. Por ejemplo, si ha adquirido una licencia para dos complementos de paquete de Adobe Experience Platform Intelligence, tiene derecho a un total de 20 usuarios simultáneos de equipos portátiles.

|  | [!DNL Data Science Workspace] | [!DNL Data Science Workspace] with Intelligence package addon |
| --- | :---: | :---: |
| Número de usuarios de equipos portátiles admitidos. | 5 usuarios simultáneos | El primer paquete agrega 5 usuarios simultáneos y las compras adicionales agregan 10 usuarios simultáneos por paquete. |
| Permite la análisis de datos exploratorios y la creación de modelos con portátiles Jupyter integrados (R, Python, Scala, PySpark) | X | X |
| Integración nativa con el servicio de Consulta. Capacidad para explorar y dar forma a conjuntos de datos mediante SQL en portátiles. | X | X |
| Acceso a las plantillas de bloc de notas prediseñadas para análisis predictivos. | X | X |
| Capacite y puntee manualmente los modelos con equipos portátiles Jupyter. | X | X |
| Implemente y operacionalice modelos con la capacidad de programar trabajos de formación e inferencias. |  | X |
| Marco de fórmulas para configurar, evaluar, entrenar, marcar y publicar fácilmente modelos en producción. |  | X |
| Experimentación y evaluación de modelos impulsados por la interfaz de usuario. |  | X |
| Soporte de aprendizaje profundo para modelos de Tensorflow (GPU Compute). |  | X |
| Computación distribuida basada en chispas para entrenar y puntuar con conjuntos de datos grandes (10 MM + filas). |  | X |

## Control de acceso

Control de acceso para Experience Platform se administra a través de [Adobe Admin Console](https://adminconsole.adobe.com). Esta funcionalidad aprovecha los perfiles del producto en el Admin Console, que vinculan a los usuarios con permisos y entornos limitados. Consulte la [información general del control de acceso](../access-control/home.md) para obtener más información.

Para utilizar el área de trabajo de ciencias de datos, debe habilitarse el permiso &quot;Administrar área de trabajo de ciencias de datos&quot;. La siguiente tabla describe los efectos de habilitar o deshabilitar este permiso:

| Permiso | Habilitado | Desactivado |
|---|---|---|
| Administrar área de trabajo de ciencias de datos | Proporciona acceso a todos los servicios de Data Science Workspace. | El acceso a la API y a la interfaz de usuario para todos los servicios dentro de Área de trabajo de ciencias de datos está deshabilitado. Mientras está deshabilitado, se evita la selección de las páginas **Equipos portátiles**, **Modelos** y **Servicios**. <li>Es posible que el acceso a **Servicios** siga estando disponible a través de la Plataforma de datos del cliente en tiempo real (RTCDP).</li> |

## Compatibilidad con Simulador para pruebas

Los Simuladores de pruebas son particiones virtuales dentro de una sola instancia de Experience Platform. Cada instancia de Plataforma admite un entorno limitado de producción y varios entornos limitados que no sean de producción, cada uno de los cuales mantiene su propia biblioteca de recursos de la Plataforma. Los entornos limitados que no son de producción le permiten probar características, ejecutar experimentos y realizar configuraciones personalizadas sin afectar al entorno limitado de producción. Para obtener más información sobre los entornos limitados, consulte la [información general de los entornos limitados](../sandboxes/home.md).

Actualmente, el espacio de trabajo de ciencias de datos tiene la siguiente limitación de simulación de pruebas:

- Los recursos de cómputo se comparten en el entorno limitado de producción y en los entornos limitados que no son de producción.

## Pasos siguientes

Este documento describía los diferentes tipos de acceso y características disponibles en el área de trabajo de ciencias de datos.

Para obtener más información sobre el área de trabajo de ciencias de datos, como un flujo de trabajo diario completo, lea la [documentación del área de trabajo de ciencias de datos](./walkthrough.md). Para obtener más información general, visite la [información general de Área de trabajo de ciencia de datos](./home.md).