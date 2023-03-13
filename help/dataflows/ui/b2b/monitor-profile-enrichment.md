---
description: Utilice el [!UICONTROL Enriquecimiento de perfil] panel para comprender si los trabajos de enriquecimiento de perfiles se ejecutaron y completaron correctamente, y para ver las métricas básicas y medir la eficacia de los enriquecimientos.
solution: Experience Platform
title: Supervisión de trabajos de enriquecimiento de perfil
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '768'
ht-degree: 2%

---

# Supervisión de trabajos de enriquecimiento de perfiles en la IU de {#monitor-profile-enrichment}

Utilice el [!UICONTROL Enriquecimiento de perfil] panel para comprender si los trabajos de enriquecimiento de perfiles se ejecutaron y completaron correctamente, y para ver las métricas básicas y medir la eficacia de los enriquecimientos.

En el [IU de Platform](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** desde la navegación izquierda para acceder a [!UICONTROL Monitorización] panel. En el selector de vistas, seleccione **Flujo B2B** para ver los elementos de panel específicos de [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  El [!UICONTROL Monitorización] el tablero incluye las métricas básicas de la última ejecución correcta y el estado diario del trabajo hasta 90 días antes.

## Enriquecimiento de perfil de cuentas relacionadas {#related-accounts}

El [!UICONTROL Cuentas relacionadas] el panel muestra las métricas básicas y el estado del trabajo diario específico del [Cuentas relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) enriquecimiento de perfiles.

![Indicación visual de cómo llegar a la pantalla de monitorización de trabajos de enriquecimiento de perfil en la interfaz de usuario de Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Los datos de la **[!UICONTROL Métricas]** incluye las métricas básicas de la última ejecución correcta del trabajo Cuentas relacionadas.

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

El [!UICONTROL Coincidencia de cliente potencial con cuenta] El panel muestra las métricas básicas y el estado diario de ejecución del trabajo específico de [Coincidencia de cliente potencial con cuenta](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) enriquecimiento de perfiles.

![Enriquecimiento del perfil de coincidencia de cliente potencial con cuenta](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

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

El [!UICONTROL Puntuación predictiva de posibles clientes y cuentas] El panel muestra las métricas básicas y el estado diario de ejecución del trabajo específico de [Puntuación predictiva de posibles clientes y cuentas](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md) enriquecimiento de perfiles.

![Enriquecimiento predictivo del perfil de puntuación de clientes potenciales y cuentas](/help/dataflows/assets/ui/b2b/predictive-lead-and-account-scoring.png)

Las siguientes métricas están disponibles para trabajos predictivos de enriquecimiento de perfil de puntuación de cuenta y posible cliente:

| Métrica | Descripción |
| --------- | ---------- |
| **[!UICONTROL Inicio del trabajo]** | Indica la fecha y hora de inicio de la ejecución predictiva del trabajo de puntuación de clientes potenciales y cuentas. |
| **[!UICONTROL Tiempo de procesamiento]** | Tiempo total que tarda el trabajo en completarse. |
| **[!UICONTROL Nombre de puntuación]** | El nombre de puntuación del trabajo. |
| **[!UICONTROL Tipo de perfil]** | El tipo de puntuación: <ul><li>Persona</li><li>Cuenta</li></ul>. |
| **[!UICONTROL Tipo de trabajo]** | El tipo de trabajo:<ul><li>Puntuación</li><li>Formación</li>. |
| **[!UICONTROL Estado]** | Indica el estado (correcto, fallido o de procesamiento) del trabajo predictivo de puntuación de cuenta y posible cliente. |

## Controles de IU {#ui-controls}

En esta sección se describen varias opciones de la interfaz de usuario (IU) de la interfaz de monitorización, que le permiten filtrar las métricas que se muestran en la página.

Utilice el icono de flecha (![icono de flecha](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) para expandir o descartar la tarjeta en la parte superior de la pantalla, que muestra información rápida sobre los trabajos de enriquecimiento de perfiles.

![Grabación de pantalla que muestra el icono de flecha del control de interfaz de usuario.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilice el **[!UICONTROL Métricas y gráficos]** cambie para descartar la vista que muestra las métricas más recientes.

![Grabación de pantalla que muestra la alternancia de métricas y gráficos.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilice el **[!UICONTROL Mostrar solo errores]** active esta opción para mostrar solo los trabajos de enriquecimiento de perfiles con errores.

![Grabación de pantalla que muestra la opción Mostrar solo errores.](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ahora puede monitorizar y comprender correctamente las métricas de los trabajos de enriquecimiento de perfiles. Consulte los siguientes documentos para obtener más información:

* [Cuentas relacionadas en Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Pestaña Cuentas relacionadas en la guía de la IU del perfil de cuenta](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Coincidencia de clientes potenciales con cuentas en Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
* [Puntuación predictiva de clientes potenciales y cuentas en Real-Time CDP B2B](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
