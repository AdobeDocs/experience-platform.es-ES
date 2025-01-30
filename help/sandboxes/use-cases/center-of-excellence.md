---
title: Activación de un centro de excelencia mediante herramientas de zona protegida
description: Habilite un centro de excelencia con las herramientas de zona protegida creando un paquete de "zona protegida dorada" para estandarizar las prácticas recomendadas en varias zonas protegidas.
exl-id: 6f242ad5-bb02-4a6d-b255-d196dd5fe4b8
source-git-commit: d4df5606228347b5fb69fdaa24c637c329099895
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 7%

---

# Activación de un centro de excelencia mediante herramientas de zona protegida

Habilite un centro de excelencia con las herramientas de zona protegida creando un paquete de &quot;zona protegida dorada&quot; para estandarizar las prácticas recomendadas en varias zonas protegidas.

![Información general sobre la exportación de paquetes entre distintas organizaciones](../images/use-cases/packages-across-orgs.png){zoomable="yes"}

## Por qué considerar este caso de uso {#why-this-use-case}

Muchas grandes empresas o empresas utilizan varios entornos limitados para diferentes organizaciones, equipos, regiones o entornos de desarrollo. Con la potencia de [herramientas para zonas protegidas](../ui/sandbox-tooling.md), puede crear un paquete de zona protegida dorada para garantizar la coherencia, el cumplimiento y la alineación de los estándares de su organización en varias zonas protegidas.

Este paquete de zona protegida dorada crea un centro de excelencia para compartir de forma eficaz las configuraciones clave. Con las herramientas de zona protegida, puede importar fácilmente el paquete en varias zonas protegidas. También puede compartir el paquete con organizaciones adicionales para garantizar una coherencia generalizada.

Siga los pasos descritos en este caso de uso para crear su propio paquete de zona protegida dorado.

## Ejemplo del sector {#industry-example}

Por ejemplo, piense en un banco que opera en diferentes regiones, como, por ejemplo, Norteamérica, Europa y África. Cada mercado o región tiene su propia instancia de Adobe Experience Platform. Este banco desea mantener un modelo de datos centralizado y gestionado por un equipo global de arquitectos en el que se pueda implantar una única versión del modelo de datos en todos los mercados.

Este banco elige aprovechar las herramientas de la zona protegida para crear y mantener un paquete de zona protegida dorado. Esto contribuye a la eficacia del desarrollo, permite modelos de datos coherentes y garantiza la coherencia en todas las regiones.

## Requisitos previos y planificación {#prerequisites-and-planning}

Cuando planee crear su propio centro de excelencia dentro de su organización, tenga en cuenta los siguientes requisitos previos en el proceso de planificación:

- Identifique las prácticas recomendadas y las configuraciones que se deben incluir en el paquete.
- Cree una zona protegida con todas las configuraciones relevantes y validadas que se establecerán como zona protegida principal.
- Si es necesario, obtenga la información y el acuerdo de las partes interesadas sobre sus estándares de línea de base.

### Funcionalidad de la IU, componentes de Platform y productos de Experience Cloud que utilizará {#ui-functionality-and-elements}

Para implementar correctamente este caso de uso, debe utilizar varias áreas de Adobe Experience Platform. Asegúrese de que tiene los [permisos de control de acceso basados en atributos](../../access-control/abac/overview.md) necesarios para todas estas áreas, o bien pídale al administrador del sistema que le conceda los permisos necesarios.

- [Herramientas de zona protegida](../ui/sandbox-tooling.md)
- [Administración de zona protegida](../ui/user-guide.md)
- [Conjuntos de datos](../../catalog/datasets/overview.md)
- [Esquemas](../../xdm//home.md)
- [Públicos](../../segmentation/home.md)
- [Recorridos de Adobe Journey Optimizer](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/orchestrate-journeys/journey)

## Cómo lograr el caso de uso: información general de alto nivel {#achieve-the-use-case-high-level}

1. Cree la configuración de línea de base que represente las prácticas recomendadas en una zona protegida dorada. Esto puede incluir objetos como conjuntos de datos, esquemas, audiencias o recorridos.
2. Con las herramientas de zona protegida, exporte la configuración a un paquete.
3. Importe este paquete en todas las zonas protegidas relevantes.
4. Si tiene varias organizaciones, comparta este paquete con otras.
5. Monitorice las importaciones y exportaciones y rastree los cambios a través de los registros de auditoría.
6. Actualice con regularidad su zona protegida de oro a medida que evolucionan los estándares para garantizar que todos los espacios aislados permanezcan alineados con las prácticas recomendadas.

## Cómo lograr el caso de uso: Instrucciones paso a paso {#step-by-step-instructions}

Lea las secciones siguientes, que incluyen vínculos a documentación adicional, para completar cada uno de los pasos de la información general de alto nivel anterior.

### Cree su zona protegida dorada

El primer paso para habilitar su centro de excelencia es crear su zona protegida dorada. Esta zona protegida debe contener las configuraciones de línea de base que representan las prácticas recomendadas. Para crear esta zona protegida dorada, sigue la guía de [creación de una nueva zona protegida](../ui/user-guide.md#create-a-new-sandbox) en el Experience Platform.

Una vez creada la zona protegida, empiece a crear las configuraciones del objeto de línea de base, como [esquemas](../../xdm/ui/resources/schemas.md#create-a-new-schema), [conjuntos de datos](../../catalog/datasets/user-guide.md#create-a-dataset) o [audiencias](../../segmentation/ui/segment-builder.md). Asegúrese de revisar las configuraciones antes de continuar.

### Exportación de la zona protegida en un paquete

Ahora que la zona protegida contiene las configuraciones de objeto de línea de base, está lista para exportarse en un paquete con las herramientas de zona protegida. Siga la guía de [exportación de una zona protegida completa](../ui/sandbox-tooling.md#export-an-entire-sandbox) para crear su paquete de zona protegida dorada.

### Importe el paquete en las zonas protegidas relevantes

Ahora que el paquete se ha creado, puede importarlo en sus zonas protegidas correspondientes. La práctica recomendada es importar un paquete que contenga una zona protegida completa en una vacía. Con las herramientas de zona protegida, puede [importar fácilmente un paquete de zona protegida completo](../../sandboxes/ui/sandbox-tooling.md#import-the-entire-sandbox-package) en una zona protegida directamente en Experience Platform.

### Uso compartido de paquetes entre organizaciones

Las herramientas de zona protegida le permiten compartir paquetes que ha creado en diferentes organizaciones. Siga la [guía para compartir paquetes](../../sandboxes/ui/sharing-packages-across-orgs.md) para compartir su paquete de zona protegida dorada.

### Monitorización de importaciones y exportaciones mediante registros de auditoría

Al importar o exportar el paquete, puede supervisar el estado de los trabajos mediante el panel **[!UICONTROL Jobs]** en Experience Platform. Para obtener más información acerca de la supervisión de trabajos, lea la guía de [supervisión de detalles de importación](../../sandboxes/ui/sandbox-tooling.md#monitor-import-details).

### Actualizar regularmente la zona protegida dorada

Ahora que el paquete de zona protegida dorada está listo, ha establecido un centro de excelencia estandarizado que puede seguir importando en zonas protegidas o compartiendo entre organizaciones. A medida que cambien y se desarrollen las prácticas recomendadas, es importante actualizar regularmente las configuraciones de objetos de línea de base en su zona protegida dorada. A medida que realiza actualizaciones en la zona protegida, puede crear nuevas iteraciones del paquete de zona protegida siguiendo este mismo proceso.

>[!NOTE]
>
> Los pasos anteriores siguen el proceso en la interfaz de usuario de Experience Platform. Es posible seguir los mismos pasos utilizando la API a través de varios extremos. Consulte `sandboxes` [guía de extremo](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/api/sandboxes#create) y `packages` [guía de extremo](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages) para obtener información sobre cómo realizar cada solicitud a través de la API.

## Otros casos de uso obtenidos mediante la compatibilidad con datos de socios {#other-use-cases}

Explore más casos de uso habilitados mediante las herramientas de zona protegida:

- [Copia de seguridad de configuraciones de objetos mediante herramientas de zona protegida](./backup-object-configuration.md)
