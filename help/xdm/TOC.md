---
product: experience-platform
audience: user
user-guide-title: Ayuda del sistema del Modelo de datos de experiencia (XDM)
breadcrumb-title: Guía del modelo de datos (XDM) de Experience
user-guide-description: Utilice clases y mezclas del Modelo de datos de experiencia (XDM) para estandarizar los datos de experiencia.
translation-type: tm+mt
source-git-commit: c82ad393ecaa46d01596dbba06f5fc756711bc31
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 23%

---


# Sistema de modelo de datos de experiencia (XDM) {#xdm}

* [Descripción general del sistema XDM](home.md)
* Esquemas {#schema}
   * [Conceptos básicos de la composición de esquemas](schema/composition.md)
   * [Prácticas recomendadas para el modelado de datos](schema/best-practices.md)
   * [Restricciones de tipo de campo XDM](schema/field-constraints.md)
   * [Diccionario de campo XDM](schema/field-dictionary.md)
* Clases {#classes}
   * [Perfil individual XDM](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mezclas {#mixins}
   * Mezclas de perfil {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Detalles demográficos](./mixins/profile/person-details.md)
      * [Detalles de contacto personal](./mixins/profile/personal-details.md)
      * [Detalles de pertenencia a segmentos](./mixins/profile/segmentation.md)
      * [Detalles de contacto de trabajo](./mixins/profile/work-details.md)
   * Mezclas de evento {#event}
      * [Detalles del ID de usuario final](./mixins/event/enduserids.md)
      * [Detalles del entorno](./mixins/event/environment-details.md)
   * [Actualizaciones de nombres de mezcla](./mixins/name-updates.md)
* Tipos de datos {#data-types}
   * [de asistencia al cliente](./data-types/application.md)
   * [Señalización](./data-types/beacon.md)
   * [Detalles del explorador](./data-types/browser-details.md)
   * [Contenido y preferencias](./data-types/consents.md)
   * [Dispositivo](./data-types/device.md)
   * [Dirección de correo electrónico](./data-types/email-address.md)
   * [Entorno](./data-types/environment.md)
   * [Ubicación geográfica](./data-types/geo.md)
   * [Círculo geográfico](./data-types/geo-circle.md)
   * [Coordenadas geográficas](./data-types/geo-coordinates.md)
   * [Detalles de interacción geográfica](./data-types/geo-interaction-details.md)
   * [Forma geográfica](./data-types/geo-shape.md)
   * [Identidad](./data-types/identity.md)
   * [Medida](./data-types/measure.md)
   * [Persona](./data-types/person.md)
   * [Nombre de la persona](./data-types/person-name.md)
   * [Número de teléfono](./data-types/phone-number.md)
   * [Colocar contexto](./data-types/place-context.md)
   * [Detalles de puntos de interés](./data-types/poi-details.md)
   * [Interacción con POI](./data-types/poi-interaction.md)
   * [Dirección postal](./data-types/postal-address.md)
   * [Buscar](./data-types/search.md)
   * [Suscripción](./data-types/subscription.md)
   * [Interacción con Web](./data-types/web-interactions.md)
   * [Detalles de la página Web](./data-types/webpage-details.md)
*  EsquemasUI  {#ui}
   * [Información general](./ui/overview.md)
   * [Explorar recursos XDM](./ui/explore.md)
   * Crear y editar recursos {#resources}
      * [Esquemas](./ui/resources/schemas.md)
      * [Clases](./ui/resources/classes.md)
      * [Mezclas](./ui/resources/mixins.md)
      * [Tipos de datos](./ui/resources/data-types.md)
   * Definir campos {#fields}
      * [Información general](./ui/fields/overview.md)
      * [Campos requeridos](./ui/fields/required.md)
      * [Campos de objeto](./ui/fields/object.md)
      * [Campos de matriz](./ui/fields/array.md)
      * [Campos Enum](./ui/fields/enum.md)
      * [Campos de identidad](./ui/fields/identity.md)
      * [Campos de relación](./ui/fields/relationship.md)
   * [Generar datos XDM de muestra](./ui/sample.md)
   * [Exportar esquemas XDM](./ui/export.md)
* API del Registro de esquemas {#api}
   * [Información general](api/overview.md)
   * [Primeros pasos](api/getting-started.md)
   * [Esquemas](api/schemas.md)
   * [Comportamientos](api/behaviors.md)
   * [Clases](api/classes.md)
   * [Mezclas](api/mixins.md)
   * [Tipos de datos](api/data-types.md)
   * [Descriptores](api/descriptors.md)
   * [Uniones](api/unions.md)
   * [Exportar/Importar](api/export-import.md)
   * [Datos de muestra](api/sample-data.md)
   * [Registro de auditoría](api/audit-log.md)
   * [Esquemas específicos](api/ad-hoc.md)
   * [Apéndice](api/appendix.md)
* Tutoriales {#tutorials}
   * [Creación de un esquema (API)](tutorials/create-schema-api.md)
   * [Creación de un esquema (IU)](tutorials/create-schema-ui.md)
   * [Definir una relación entre dos esquemas (API)](tutorials/relationship-api.md)
   * [Definir una relación entre dos esquemas (IU)](tutorials/relationship-ui.md)
   * [Creación de un esquema ad-hoc (API)](tutorials/ad-hoc.md)
* [Guía de resolución de problemas](troubleshooting-guide.md)
* [Referencia de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)
* [Notas de la versión de la plataforma](https://www.adobe.com/go/platform-release-notes-en)