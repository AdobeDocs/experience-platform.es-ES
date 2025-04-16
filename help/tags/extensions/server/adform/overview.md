---
keywords: integración de adform; adform;
title: Integración de Adform para retargeting no autenticado
description: Esta integración de Adobe Experience Platform le permite redireccionar a los usuarios en función de ECID.
last-substantial-update: 2025-03-26T00:00:00Z
source-git-commit: 23da6e12b1f5bdc37240d7aa11a44e040b29e3f7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# Información general sobre la extensión [!DNL Adform]

La extensión [[!DNL Adform]](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud) habilita el reenvío de eventos del lado del servidor en Adobe Experience Platform, lo que permite a los anunciantes, agencias de medios y editores sincronizar datos directamente con el sistema ID Fusion de Adobe. Esta integración permite a las empresas atraer audiencias en varios canales, mejorar el rendimiento de las campañas y proporcionar soluciones personalizadas para refinar las estrategias de publicidad digital y maximizar la eficacia del gasto en publicidad.

A diferencia del seguimiento tradicional del lado del cliente, esta extensión elimina la necesidad de cookies de terceros al aprovechar ID de origen, específicamente, el ECID (Experience Cloud ID) que se sincroniza con Adobe Forms. Esto permite un retargeting de audiencia sin problemas sin necesidad de implementar JavaScript en el lado del cliente.

Esta guía explica cómo instalar, configurar e implementar la extensión para reenviar eventos desde las propiedades digitales de una marca a través de Edge Network de Adobe a Adobe para permitir un redireccionamiento perfecto de los visitantes.

## Retargeting fuera del sitio

Mediante el redireccionamiento fuera del sitio, puede volver a atraer a los clientes potenciales que visitaron el sitio web pero no se convirtieron. Adform le ayuda a llegar a estas audiencias en varias plataformas, lo que refuerza la presencia de la marca y aumenta las oportunidades de conversión. Utilice esta integración para:

* Volver a atraer visitantes desconocidos sin el uso de cookies de terceros.
* Active audiencias directamente en los ECID sin utilizar identificadores de cookies alternativas de terceros ni etiquetas adicionales en sus propiedades digitales.

Adform le ayuda a lo siguiente:

* Convierta fácilmente las audiencias de origen indicadas en ECID en ID accesibles para campañas de publicidad digital.
* Vincule los ECID a más de 40 soluciones de ID facturables para optimizar su alcance, frecuencia y rendimiento frente a las audiencias de destino.

### Activación de audiencia del lado del servidor con [!DNL Adform] {#server-side-activation}

A diferencia de las implementaciones de ID tradicionales del lado del cliente, esta integración no requiere que implemente una solución del proveedor de ID en sus propiedades digitales. En su lugar, habilita la activación de audiencias del lado del servidor aprovechando los ECID que ya están sincronizados con Adobe Forms. Las ventajas principales incluyen:

* **Sin implementación de JavaScript en el lado del cliente**: no necesita administrar la lógica de reconocimiento de visitantes en el lado del cliente ni descifrar los ID del lado del cliente en versiones estables de mayor duración.
* **Sincronización perfecta de audiencias**: los ECID se asignan al gráfico de ID interno de Adobe, lo que permite un resegmentado eficiente en todas las plataformas.
* **Alcance y deduplicación mejorados**: El gráfico de ID Fusion conecta los ECID con varios identificadores, lo que garantiza una coincidencia de audiencia de alta calidad.

## Requisitos previos {#prerequisites}

Antes de integrar Adobe con Adobe, asegúrese de que se cumplen los siguientes requisitos previos:

1. **Configuración de Adobe Web SDK**: Adobe Web SDK debe implementarse para facilitar la recopilación de datos y el reenvío de eventos.

2. **CDP o SKU de conexión**: para habilitar una comunicación perfecta del lado del cliente y del servidor, debe tener el Prime de Adobe Customer Data Platform (CDP) o el SKU de Ultimate, o el SKU de conexión.

3. **Configuración de Adobe Experience Platform Edge Network**:
   * Asegúrese de que Edge Network esté configurado para admitir el reenvío de eventos en tiempo real para el redireccionamiento fuera del sitio. Consulte la [Guía de introducción al reenvío de eventos](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/getting-started) de Adobe para obtener más información.
   * Este paso es crucial para transmitir datos al extremo del lado del servidor de Adobe de forma eficaz.

Una vez cumplidos estos requisitos previos, puede seguir configurando e implementando la extensión [!DNL Adform].

## Configurar la extensión de [!DNL Adform] {#configure-adform-extension}

Para configurar la extensión [!DNL Adform], siga los pasos descritos en las secciones siguientes.

### Instalación y configuración de la extensión de

Vaya a [!DNL Adform extension] en la interfaz de usuario del reenvío de eventos e introduzca los valores necesarios:

| Entrada | Descripción |
| --- | --- |
| ID de configuración de seguimiento | El identificador único proporcionado por Adobe para el seguimiento de eventos. |
| Dominio global | Use `a1.adform.net` para optimizar el rendimiento y evitar problemas de latencia regional. |

Guarde la configuración después de introducir estos detalles.

<!-- ![Installing and configuring the Adform extension in Adobe Experience Platorm]() -->

### Definir parámetros de seguimiento

La acción &quot;rastrear&quot; es la regla de evento principal. Se basa en déclencheur de acciones predefinidas, generalmente `page load.`. Incluye los siguientes parámetros:

**Parámetros necesarios:**

| Parámetros | Descripción |
| --- | --- |
| `Page Name` | Identifica la página o la acción del usuario. |
| `User Agent` | Registra información para la coincidencia de audiencias. |
| `IP Address` | Crucial para un direccionamiento y redireccionamiento precisos. |

**Parámetros recomendados:**

| Parámetros | Descripción |
| --- | --- |
| `Page URL` | Identifica la página o la acción del usuario. |
| `Referral URL` | Registra información para la coincidencia de audiencias. |
| `ECID` | Crucial para un direccionamiento y redireccionamiento precisos. |
| `Source Domain` | Crucial para un direccionamiento y redireccionamiento precisos. |

<!-- ![Tracking parameters for Adform]() -->

### Adjuntar regla

La extensión debe estar adjunta a una regla para funcionar correctamente. Si no se establece ninguna condición, cree una regla global para asegurarse de que se ejecute siempre.

>[!NOTE]
>
>Si la extensión no se activa, compruebe que esté adjunta a una regla válida en la recopilación de datos de Adobe Experience Platform.

<!-- ![Attach a rule to the Adform extension]() -->

## Validación e implementación

Asegúrese de que la extensión esté instalada y configurada correctamente y de que todos los elementos de datos necesarios estén asignados, lo que incluye:
* [ECID](/help/identity-service/features/ecid.md)
* Nombre de página
* URL de referencia
* Agente de usuario
* Dirección IP

Una vez que ingrese todos los campos requeridos y termine la prueba, seleccione **build** para implementar la extensión.

## Pasos siguientes

Ahora debería saber cómo se integra Adobe con las capacidades del lado del servidor de Adobe y puede evaluar la viabilidad de la integración dentro de su infraestructura existente. Para obtener más información, consulte [Documentación oficial de Adobe](https://www.adformhelp.com/hc/en-us/articles/29635608709137-Use-the-Adform-S2S-Site-Tracking-Extension-With-Adobe-Experience-Cloud).