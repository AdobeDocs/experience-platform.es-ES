---
title: Ver Insight SQL
description: Vea el SQL subyacente a sus perspectivas de perfil, audiencia, destino y personalizadas, y ejecute la consulta bajo demanda mediante el Editor de consultas.
exl-id: fd728926-c113-4593-92b1-916a02d09d41
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Ver insight SQL

Utilice la característica [!UICONTROL Ver SQL] para ver el SQL subyacente a sus perspectivas de perfil, audiencia, destino y personalizadas, y ejecutar la consulta bajo demanda mediante el Editor de consultas. Inspírese con el SQL de más de 40 perspectivas existentes para crear nuevas consultas que obtengan perspectivas únicas de los datos de Experience Platform en función de sus necesidades comerciales.

## Vaya a la información general del panel {#navigate-to-overview}

Para abrir el panel que has elegido, selecciona **[!UICONTROL Perfiles]**, **[!UICONTROL Audiencias]** o **[!UICONTROL Destinos]** en el panel de navegación izquierdo. A continuación, seleccione **[!UICONTROL Información general]** de las opciones de la ficha si el área de trabajo no aparece automáticamente.

Como alternativa, seleccione **[!UICONTROL Paneles]** en el panel de navegación izquierdo seguido del nombre de su panel personalizado. Aparecerá la descripción general del tablero definido por el usuario.

![Se ha resaltado la interfaz de usuario de Experience Platform con [!UICONTROL Perfiles], [!UICONTROL Audiencias], [!UICONTROL Destinos] y [!UICONTROL Paneles].](./images/view-sql/dashboard-navigation.png)

## Alternar Ver SQL {#toggle}

Hay disponible un conmutador en la descripción general de los paneles de Perfil, Audiencia, Destino y definidos por el usuario para habilitar o deshabilitar la función.

>[!NOTE]
>
>Si habilita la opción [!UICONTROL Ver SQL], no podrá cambiar los filtros globales y de nivel de widget hasta que deshabilite la característica.

![Se resaltó la opción de [!UICONTROL Ver SQL].](./images/view-sql/view-sql-toggle.png)

Habilite la opción para mostrar el texto [!UICONTROL Ver SQL] en cada insight individual.

![Se ha resaltado un insight con [!UICONTROL Ver SQL].](./images/view-sql/insight-view-sql.png)

Seleccione **[!UICONTROL Ver SQL]** para abrir un cuadro de diálogo que contenga el SQL del widget.

## Cuadro de diálogo SQL {#sql-dialog}

Aparecerá un cuadro de diálogo que contiene el título de la insight y el SQL que la genera.

>[!TIP]
>
>Puede copiar toda la instrucción SQL en el portapapeles seleccionando el icono de copia (![El icono de copia.](/help/images/icons/copy.png)) en la parte superior derecha del cuadro de diálogo.

![Cuadro de diálogo de insight con la instrucción SQL resaltada.](./images/view-sql/sql-dialog.png)

Seleccione **[!UICONTROL Ejecutar SQL]** para abrir el Editor de consultas con la consulta ya completada.

![Se ha resaltado un cuadro de diálogo de insight con [!UICONTROL Ejecutar SQL].](./images/view-sql/run-sql.png)

## Editar SQL existente {#edit-sql}

Aparecerá el Editor de consultas. Ahora puede editar la instrucción y consultar los datos de la plataforma para adaptarlos mejor a sus necesidades de creación de informes. Guarde la nueva plantilla de consulta con un nombre adecuado.

![El editor de consultas con el SQL de insight seleccionado ya se ha completado.](./images/view-sql/edit-sql.png)

## Pasos siguientes

Después de leer este documento, ahora sabe cómo acceder a SQL para cualquier insight dentro de los paneles estándar o de un panel definido por el usuario. Si aún no lo ha hecho, se recomienda leer el [documento Modelo de datos de Real-Time Customer Data Platform Insights](./data-models/cdp-insights-data-model-b2c.md). Ese documento contiene información sobre la personalización de plantillas SQL para informes de Real-Time CDP adaptados a sus necesidades de marketing y KPI.
