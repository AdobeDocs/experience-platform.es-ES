---
description: Use el panel [!UICONTROL Enriquecimiento de perfil] para saber si los trabajos de enriquecimiento de perfil se ejecutaron y completaron correctamente, y para ver las métricas básicas y medir la efectividad de los enriquecimientos.
solution: Experience Platform
title: Supervisión de trabajos de enriquecimiento de perfil
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 2%

---

# Supervisión de trabajos de enriquecimiento de perfiles en la IU de {#monitor-profile-enrichment}

Use el panel [!UICONTROL Enriquecimiento de perfil] para saber si los trabajos de enriquecimiento de perfil se ejecutaron y completaron correctamente, y para ver las métricas básicas y medir la efectividad de los enriquecimientos.

En la [interfaz de usuario de Experience Platform](https://platform.adobe.com), seleccione **[!UICONTROL Supervisión]** en el panel izquierdo para acceder al [!UICONTROL Control]. En el selector de vista, seleccione **Flujo B2B** para ver los elementos de tablero específicos de [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  El panel [!UICONTROL Monitorización] incluye las métricas básicas de la última ejecución correcta y el estado diario de los trabajos hasta 90 días antes.

## Enriquecimiento de perfil de cuentas relacionadas {#related-accounts}

El panel [!UICONTROL Cuentas relacionadas] muestra métricas básicas y el estado del trabajo diario específico del enriquecimiento del perfil [Cuentas relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md).

![Indicación visual de cómo llegar a la pantalla de supervisión de trabajos de enriquecimiento de perfil en la interfaz de usuario de Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Los datos de la tarjeta **[!UICONTROL Métricas]** incluyen las métricas básicas de la última ejecución correcta del trabajo Cuentas relacionadas.

Las siguientes métricas están disponibles para trabajos de enriquecimiento de perfil de cuentas relacionadas:

| Métrica | Descripción |
| --------- | ---------- |
| **[!UICONTROL Perfiles totales de la cuenta]** | Indica el total de perfiles de cuenta a los que tiene acceso su organización. |
| **[!UICONTROL Grupos de cuentas]** | Indica el número de grupos de cuentas agrupados por el trabajo de aprendizaje automático de cuentas relacionado. |
| **[!UICONTROL Grupos de una sola cuenta]** | Indica el número de cuentas que no están agrupadas con otras cuentas. |
| **[!UICONTROL Tamaño de grupo más grande]** | Indica el tamaño del grupo de cuentas relacionadas más grande. El tamaño máximo de grupo permitido es 30. |
| **[!UICONTROL Mediana del tamaño del grupo]** | Indica la mediana del tamaño de los grupos de cuentas relacionadas de su organización. |
| **[!UICONTROL Última ejecución correcta]** | Indica la fecha y la hora de la última ejecución correcta del trabajo de cuentas relacionadas. |
| **[!UICONTROL Estado]** | Indica el estado (correcto, fallido o procesando) del trabajo de cuentas relacionado. |
| **[!UICONTROL Mensaje]** | Indica un mensaje de error o advertencia para una ejecución de trabajo determinada. |

## Enriquecimiento del perfil de coincidencia de cliente potencial con cuenta {#lead-to-account-matching}

El panel [!UICONTROL Coincidencia de cliente potencial con cuenta] muestra las métricas básicas y el estado diario de ejecución del trabajo específico del enriquecimiento de perfil [Coincidencia de cliente potencial con cuenta](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![Enriquecimiento del perfil coincidente del posible cliente con la cuenta](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Las siguientes métricas están disponibles para los trabajos de enriquecimiento de perfil de coincidencia de cuenta de posibles clientes:

| Métrica | Descripción |
| --------- | ---------- |
| **[!UICONTROL Total de personas con cuentas]** | Indica el número total de personas asociadas a una cuenta. |
| **[!UICONTROL Cuentas totales]** | Indica el número total de cuentas. |
| **[!UICONTROL Personas existentes con cuentas]** | Indica el número de personas que ya están asociadas a una cuenta desde las fuentes de datos. |
| **[!UICONTROL Personas coincidentes]** | Indica el número de personas que coincidieron con una cuenta. |
| **[!UICONTROL Personas sin coincidencias]** | Indica el número de personas que no coinciden con una cuenta. |
| **[!UICONTROL Última ejecución correcta]** | Indica la fecha y la hora de la última ejecución correcta del trabajo de conciliación de cuentas. |
| **[!UICONTROL Estado]** | Indica el estado (correcto, fallido o de procesamiento) del trabajo de coincidencia de cliente potencial con cuenta. |

## Enriquecimiento predictivo del perfil de puntuación de clientes potenciales y cuentas {#predictive-lead-to-account-scoring}

El panel [!UICONTROL Puntuación predictiva de posibles clientes y cuentas] muestra las métricas básicas y el estado diario de ejecución del trabajo específico para el enriquecimiento del perfil [Puntuación predictiva de posibles clientes y cuentas](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md).

![Enriquecimiento predictivo del perfil de puntuación de clientes potenciales y cuentas](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Las siguientes métricas están disponibles para trabajos predictivos de enriquecimiento de perfil de puntuación de cuenta y posible cliente:

| Métrica | Descripción |
| --------- | ---------- |
| **[!UICONTROL Inicio del trabajo]** | Indica la fecha y hora de inicio de la ejecución predictiva del trabajo de puntuación de clientes potenciales y cuentas. |
| **[!UICONTROL Tiempo de procesamiento]** | Tiempo total que tarda el trabajo en completarse. |
| **[!UICONTROL Nombre de puntuación]** | El nombre de puntuación del trabajo. |
| **[!UICONTROL Tipo de perfil]** | El tipo de puntuación: <ul><li>Persona</li><li>Cuenta</li></ul>. |
| **[!UICONTROL Tipo de trabajo]** | El tipo de trabajo:<ul><li>Puntuación</li><li>Aprendizaje</li>. |
| **[!UICONTROL Estado]** | Indica el estado (correcto, fallido o de procesamiento) del trabajo predictivo de puntuación de cuenta y posible cliente. |

## Controles de IU {#ui-controls}

En esta sección se describen varias opciones de la interfaz de usuario (IU) de la interfaz de monitorización, que le permiten filtrar las métricas que se muestran en la página.

Utilice el icono de flecha (![icono de flecha](/help/images/icons/chevron-up.png)) para expandir o descartar la tarjeta en la parte superior de la pantalla, que muestra información rápida sobre los trabajos de enriquecimiento de perfiles.

![Grabación de pantalla que muestra el icono de flecha del control de IU.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Use la opción **[!UICONTROL Métricas y gráficos]** para descartar la vista que muestra las métricas más recientes.

![Grabación de pantalla que muestra la alternancia de métricas y gráficos.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilice la opción **[!UICONTROL Mostrar solo errores]** para mostrar únicamente los trabajos de enriquecimiento de perfiles con errores.

![Grabación de pantalla que muestra la opción Mostrar solo errores.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ahora puede monitorizar y comprender correctamente las métricas de los trabajos de enriquecimiento de perfiles. Consulte los siguientes documentos para obtener más información:

* [Cuentas relacionadas en Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Pestaña Cuentas relacionadas en la guía de la IU del perfil de cuenta](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Coincidencia de clientes potenciales con cuentas en Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Puntuación predictiva de clientes potenciales y cuentas en Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
