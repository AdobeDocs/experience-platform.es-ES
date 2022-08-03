---
description: Utilice la variable [!UICONTROL Enriquecimiento de perfiles] tablero para comprender si los trabajos de enriquecimiento de perfiles se ejecutaron y completaron correctamente, y para ver las métricas básicas para medir la eficacia de los enriquecimientos.
solution: Experience Platform
title: Monitorización de trabajos de enriquecimiento de perfiles
type: Tutorial
exl-id: 096a2212-ed7f-4419-8ead-fa1ca01c2804
source-git-commit: 6811e3032abe569b1f00d757553eb6862e4e3354
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Supervisar los trabajos de enriquecimiento de perfiles en la interfaz de usuario (#monitor-profile-enrich)

Utilice la variable [!UICONTROL Enriquecimiento de perfiles] tablero para comprender si los trabajos de enriquecimiento de perfiles se ejecutaron y completaron correctamente, y para ver las métricas básicas para medir la eficacia de los enriquecimientos.

En el [Interfaz de usuario de Platform](https://platform.adobe.com), seleccione **[!UICONTROL Monitorización]** desde el panel de navegación izquierdo para acceder a la [!UICONTROL Monitorización] tablero. En el selector de vista, seleccione **Flujo B2B** para ver los elementos de tablero específicos de [Real-Time CDP B2B](/help/rtcdp/b2b-overview.md).  La variable [!UICONTROL Monitorización] tablero incluye las métricas básicas de la última ejecución correcta y el estado diario del trabajo de hasta 90 días en el pasado.

## Enriquecimiento de perfiles de cuentas relacionadas (#related-accounts)

La variable [!UICONTROL Cuentas relacionadas] tablero muestra las métricas básicas y el estado del trabajo diario específico del [Cuentas relacionadas](/help/rtcdp/b2b-ai-ml-services/related-accounts.md) enriquecimiento de perfiles.

![Indicación visual de cómo llegar a la pantalla de monitorización de trabajos de enriquecimiento de perfil en la interfaz de usuario del Experience Platform.](/help/dataflows/assets/ui/b2b/monitoring-profile-enrichment-jobs.png)

Los datos de la variable **[!UICONTROL Métricas]** incluye las métricas básicas de la última ejecución exitosa del trabajo Cuentas relacionadas .

Las siguientes métricas están disponibles para trabajos de enriquecimiento de perfiles de cuentas relacionadas:

| Métrica | Descripción |
| --------- | ---------- |
| **[!UICONTROL Perfiles totales de la cuenta]** | Indica el total de perfiles de cuenta a los que tiene acceso su organización. |
| **[!UICONTROL Grupos de cuentas]** | Indica el número de grupos de cuentas agrupados por el trabajo de aprendizaje automático de cuentas relacionadas. |
| **[!UICONTROL Grupos de una sola cuenta]** | Indica el número de cuentas que no se agrupan con otras cuentas. |
| **[!UICONTROL Tamaño de grupo más grande]** | Indica el tamaño del grupo de cuentas relacionadas más grande. El tamaño máximo permitido del grupo es 30. |
| **[!UICONTROL Tamaño medio del grupo]** | Indica la mediana del tamaño de los grupos de cuentas relacionadas en su organización. |
| **[!UICONTROL Última ejecución correcta]** | Indica la fecha y la hora de la última ejecución correcta del trabajo de cuentas relacionadas. |
| **[!UICONTROL Estado]** | Indica el estado (correcto, fallido o procesado) del trabajo de cuentas relacionado. |
| **[!UICONTROL Mensaje]** | Indica un mensaje de error o advertencia para un trabajo en particular ejecutado. |

## Enriquecimiento de perfil coincidente de cuentas (#lead-to-account-match)

La variable [!UICONTROL Confrontación de posibles clientes con cuentas] tablero muestra las métricas básicas y el estado diario de ejecución del trabajo específico del [Confrontación de posibles clientes con cuentas](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md) enriquecimiento de perfiles.

![Enriquecimiento de perfil coincidente entre cuentas](/help/dataflows/assets/ui/b2b/mpc-lead-to-account-matching.png)

Las siguientes métricas están disponibles para trabajos de enriquecimiento de perfiles que coinciden con las cuentas:

| Métrica | Descripción |
| --------- | ---------- |
| **[!UICONTROL Total de personas con cuentas]** | Indica el número total de personas asociadas a una cuenta. |
| **[!UICONTROL Total de cuentas]** | Indica el número total de cuentas. |
| **[!UICONTROL Personas existentes con cuentas]** | Indica el número de personas que ya están asociadas a una cuenta de las fuentes de datos. |
| **[!UICONTROL Personas coincidentes]** | Indica el número de personas que coincidieron con una cuenta. |
| **[!UICONTROL Personas sin correspondencia]** | Indica el número de personas que no coinciden con una cuenta. |
| **[!UICONTROL Última ejecución correcta]** | Indica la fecha y la hora del último posible cliente correcto en la ejecución del trabajo coincidente de la cuenta. |
| **[!UICONTROL Estado]** | Indica el estado (correcto, fallido o procesado) del trabajo de coincidencia de cuentas del posible cliente. |

## Controles de IU {#ui-controls}

En esta sección se describen varias opciones de la interfaz de usuario (IU) de la interfaz de monitorización, que permiten filtrar las métricas que se muestran en la página.

Utilice el icono de flecha (![icono de flecha](/help/dataflows/assets/ui/monitor-destinations/chevron-up.png)) para expandir o descartar la tarjeta en la parte superior de la pantalla, que muestra información rápida sobre los trabajos de enriquecimiento de perfiles.

![Grabación de pantalla que muestra el control de la IU con el icono de flecha.](/help/dataflows/assets/ui/b2b/use-arrow-control.gif)

Utilice la variable **[!UICONTROL Métricas y gráficos]** para rechazar la vista que muestra las métricas más recientes.

![Grabación de pantalla que muestra la opción de alternancia de métricas y gráficos.](/help/dataflows/assets/ui/b2b/metrics-and-graphs-toggle.gif)

Utilice la variable **[!UICONTROL Mostrar solo errores]** alterne para mostrar solo los trabajos de enriquecimiento de perfiles fallidos.

![La grabación de pantalla muestra la opción Mostrar errores solo .](/help/dataflows/assets/ui/b2b/show-failures-only.gif)

## Pasos siguientes {#next-steps}

Al seguir este tutorial, ahora puede supervisar y comprender correctamente las métricas de trabajos de enriquecimiento de perfiles. Consulte los siguientes documentos para obtener más información:

* [Cuentas relacionadas en tiempo real CDP B2B](/help/rtcdp/b2b-ai-ml-services/related-accounts.md)
* [Ficha Cuentas relacionadas en la guía de la interfaz de usuario del perfil de la cuenta](/help/rtcdp/accounts/account-profile-ui-guide.md)
* [Concordancia de posibles clientes con cuentas en tiempo real CDP B2B](/help/rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)
