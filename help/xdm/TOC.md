---
product: experience-platform
audience: user
user-guide-title: Ayuda del sistema del Modelo de datos de experiencia (XDM)
breadcrumb-title: Guía del modelo de datos (XDM)
user-guide-description: Utilice clases y mezclas del Modelo de datos de experiencia (XDM) para estandarizar los datos de experiencia.
translation-type: tm+mt
source-git-commit: a091acf1cfc572df7b300a7be6a673b1e7469be5
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 19%

---


# Experience Data Model (XDM) System {#xdm}

* [Descripción general del sistema XDM](home.md)
* Esquemas {#schema}
   * [Conceptos básicos de la composición de esquemas](schema/composition.md)
   * [Restricciones de tipo de campo XDM](schema/field-constraints.md)
   * [Diccionario de campo XDM](schema/field-dictionary.md)
   * Casos de uso de esquema {#use-cases}
      * [Mezcla de consentimiento de privacidad](schema/privacy-consent.md)
* Clases {#classes}
   * [Perfil individual XDM](./classes/individual-profile.md)
   * [XDM ExperienceEvent](./classes/experienceevent.md)
* Mezclas {#mixins}
   * Mezclas de perfil {#profile}
      * [IdentityMap](./mixins/profile/identitymap.md)
      * [Detalles de la persona de perfil](./mixins/profile/person-details.md)
      * [Datos personales del perfil](./mixins/profile/personal-details.md)
      * [Segmentación de perfiles](./mixins/profile/segmentation.md)
      * [Detalles de trabajo de perfil](./mixins/profile/work-details.md)
   * Mezclas de evento {#event}
      * [ID de usuario final de ExperienceEvent](./mixins/event/enduserids.md)
      * [Detalles del entorno de ExperienceEvent](./mixins/event/environment-details.md)
   * [Actualizaciones de nombres de mezcla](./mixins/name-updates.md)
* Tipos de datos {#data-types}
   * [Señalización](./data-types/beacon.md)
   * [Detalles del explorador](./data-types/browser-details.md)
   * [Device](./data-types/device.md)
   * [Dirección de correo electrónico](./data-types/email-address.md)
   * [Entorno](./data-types/environment.md)
   * [Ubicación geográfica](./data-types/geo.md)
   * [Círculo geográfico](./data-types/geo-circle.md)
   * [Coordenadas geográficas](./data-types/geo-coordinates.md)
   * [Detalles de interacción geográfica](./data-types/geo-interaction-details.md)
   * [Forma geográfica](./data-types/geo-shape.md)
   * [Identidad](./data-types/identity.md)
   * [Nombre de la persona](./data-types/person-name.md)
   * [Número de teléfono](./data-types/phone-number.md)
   * [Colocar contexto](./data-types/place-context.md)
   * [Detalles de puntos de interés](./data-types/poi-details.md)
   * [Interacción con POI](./data-types/poi-interaction.md)
   * [Dirección postal](./data-types/postal-address.md)
* API del Registro de esquemas {#api}
   * [Primeros pasos](api/getting-started.md)
   * [Recursos de lista](api/list-resources.md)
   * [Buscar un recurso](api/look-up-resource.md)
   * [Actualizar un recurso](api/update-resource.md)
   * [Reemplazar un recurso](api/replace-resource.md)
   * [Elimine un recurso](api/delete-resource.md)
   * [Crear una clase](api/create-class.md)
   * [Crear una mezcla](api/create-mixin.md)
   * [Crear un tipo de datos](api/create-data-type.md)
   * [Crear un esquema](api/create-schema.md)
   * [Uniones](api/unions.md)
   * [Descriptores](api/descriptors.md)
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