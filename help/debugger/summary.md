---
title: Pestaña Resumen
description: Aprenda a utilizar la pestaña Resumen en el Adobe Experience Platform Debugger.
keywords: debugger;extensión de experience Platform Debugger;chrome;extensión;resumen;borrar;solicitudes;pantalla de resumen;solución;información;analytics;target;dtm;audience manager;launch;servicio de ID
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 82%

---

# Pestaña Resumen

Para ejecutar el Adobe Experience Platform Debugger, abra la página que desee examinar en el explorador y, a continuación, seleccione el icono (![](images/start-icon.jpg)) en la barra del explorador. La extensión se abrirá en la **Resumen** pestaña.

![](images/summary.jpg)

Esta pantalla muestra información sobre cada solución de Adobe Experience Cloud. La información mostrada varía según la solución, pero generalmente incluye información como la biblioteca y la versión de la solución (por ejemplo, “AppMeasurement v2.9”) e identificadores de cuenta (como el ID del grupo de informes de Analytics, el código de cliente de Target, el ID del socio de Audience Manager, etc.)

## Información que aparece en Experience Platform Debugger

Experience Platform Debugger muestra la siguiente información para cada solución:

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Grupo(s) de informes </p> </td> 
   <td colname="col2"> <p>Los <a href="https://experiencecloud.adobe.com/resources/help/es_ES/reference/report_suites_admin.html" format="html" scope="external">grupos de informes</a> definen los informes completos e independientes de un sitio web concreto, de un conjunto de sitios web o de un subconjunto de páginas web. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versión </p> </td> 
   <td colname="col2"> <p>Versión de <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=es" format="html" scope="external"> AppMeasurement</a> definida para la página. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versión del visitante </p> </td> 
   <td colname="col2"> <p>Versión de la biblioteca de <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=es" format="html" scope="external">ID de visitante</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nombre de la página </p> </td> 
   <td colname="col2"> <p>Variable <a href="https://experiencecloud.adobe.com/resources/help/es_ES/sc/implement/pageName.html" format="html" scope="external">pageName</a> enviada a Analytics que contiene un nombre descriptivo del sitio. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Módulos </p> </td> 
   <td colname="col2"> <p>Los módulos cargados por Adobe Analytics. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Socio </p> </td> 
   <td colname="col2"> <p>El <a href="https://experiencecloud.adobe.com/resources/help/es_ES/aam/r_dil_get_partner.html" format="html" scope="external">nombre del socio</a> para la instancia DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versión </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/es_ES/aam/r_api_return_versions_dil.html" format="html" scope="external">Número de versión</a> de la instancia DIL. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Identificador único universal (UUID) </p> </td> 
   <td colname="col2"> <p><a href="https://experiencecloud.adobe.com/resources/help/es_ES/aam/ids-in-aam.html" format="html" scope="external">ID único de usuario</a> asociado a la instancia DIL. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Etiquetas de Adobe Experience Platform**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Nombre </p> </td> 
   <td colname="col2"> <p>Nombre de la etiqueta <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> propiedad</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versión </p> </td> 
   <td colname="col2"> <p>La versión de Turbine.</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Fecha de compilación </p> </td> 
   <td colname="col2"> <p>La etiqueta <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> biblioteca</a> fecha de compilación </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Entorno </p> </td> 
   <td colname="col2"> <p>El <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=es" format="https" scope="external"> entorno</a> lo utiliza la biblioteca de etiquetas </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Extensiones </p> </td> 
   <td colname="col2"> <p>Extensiones utilizadas en la página. </p> </td> 
  </tr> 
 </tbody> 
</table>

**SDK web de Adobe Experience Platform**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Versión de biblioteca </p> </td> 
   <td colname="col2"> <p>Número de versión <a href="https://experienceleague.adobe.com/docs/experience-platform/web-sdk/extension/web-sdk-ext-release-notes.html" format="html" scope="external">de la biblioteca</a> del SDK web de Adobe Experience Platform. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Área de nombres</p> </td> 
   <td colname="col2"> <p>El nombre identificado en la extensión.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID de propiedad </p> </td> 
   <td colname="col2"> <p>Nombre de la propiedad de etiqueta especificada en la extensión. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Dominio de Edge </p> </td> 
   <td colname="col2"> <p>El dominio desde el cual la extensión de Adobe Experience Platform envía y recibe datos. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID de organización de IMS </p> </td> 
   <td colname="col2"> <p>La organización a la que desea que se envíen los datos en Adobe, como se especifica en la extensión. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Registro habilitado </p> </td> 
   <td colname="col2"> <p>Especifica si el registro se ha habilitado para esta propiedad.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Servicio de Adobe Experience Cloud ID**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>ID de organización de Experience Cloud </p> </td> 
   <td colname="col2"> <p>Su <a href="https://experiencecloud.adobe.com/resources/help/es_ES/mcvid/" format="https" scope="external"> ID de organización</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versión </p> </td> 
   <td colname="col2"> <p>Versión de la biblioteca de <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=es" format="html" scope="external">ID de visitante</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Código de cliente </p> </td> 
   <td colname="col2"> <p>Su <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> código de cliente </a> de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Versión </p> </td> 
   <td colname="col2"> <p>Su versión actual de <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a> o mbox.js. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nombre de solicitud global </p> </td> 
   <td colname="col2"> <p>El <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external">mbox global</a> hace referencia a la llamada al servidor única que se realiza sobre cada página web de la implementación de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Evento de carga de página </p> </td> 
   <td colname="col2"> <p>El tipo de <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=es" format="html" scope="external">evento</a> que se activa cuando se carga la página. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nombre de la solicitud </p> </td> 
   <td colname="col2"> <p>El nombre de una solicitud alrededor de una <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> ubicación</a> en la página. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nombre de la actividad </p> </td> 
   <td colname="col2"> <p>El nombre de la <a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> campaña o actividad</a> de Target. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID de actividad </p> </td> 
   <td colname="col2"> <p>El ID de la actividad de Target. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nombre de la experiencia </p> </td> 
   <td colname="col2"> <p>Nombre de la <a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> experiencia</a> de Target. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID de la experiencia </p> </td> 
   <td colname="col2"> <p>El ID de la experiencia de Target. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Nombre de oferta</p> </td> 
   <td colname="col2"> <p>Nombre de la <a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> oferta</a> de Target. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>ID de oferta </p> </td> 
   <td colname="col2"> <p>El ID de la oferta de Target. Disponible sin autenticación solo si implementa el detector de eventos de depuración en el administrador de códigos o etiquetas y activa los <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> tokens de respuesta</a> necesarios en la interfaz de usuario de Target. </p> </td> 
  </tr> 
 </tbody> 
</table>
