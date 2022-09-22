---
title: Guía de inicio rápido
description: Aprenda a empezar rápidamente a usar etiquetas con Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 96%

---

# Guía de inicio rápido

>[!NOTE]
>
>Adobe Experience Platform Launch se ha convertido en un conjunto de tecnologías de recopilación de datos en Adobe Experience Platform. Como resultado, se han implementado varios cambios terminológicos en la documentación del producto. Consulte el siguiente [documento](../term-updates.md) para obtener una referencia consolidada de los cambios terminológicos.

Las etiquetas son la nueva generación de tecnología de administración de etiquetas de Adobe Experience Platform. Se desarrolla desde cero para ofrecer un ecosistema abierto y sostenible, donde cualquier persona puede crear sus propias integraciones que los clientes de Adobe pueden implementar en sus sitios. Es una aplicación API First, por lo que todo lo que se puede hacer a través de la IU también se puede hacer mediante una API.

Flujo de trabajo de etiquetas básico:

1. Configurar grupos y usuarios.
2. Iniciar sesión.
3. Crear una propiedad.
4. Instalar extensiones.
5. Crear elementos de datos y reglas.
6. Realizar pruebas en el entorno de desarrollo.
7. Enviar a producción.

## 1. Configurar grupos y usuarios

Las etiquetas están totalmente integradas con su Adobe ID. Los permisos de usuario se administran mediante la Admin Console con otros productos y soluciones de Adobe desde [!DNL Creative Cloud], [!DNL Document Cloud] y Experience Cloud.

Las etiquetas tienen un sistema de administración de usuarios basado en los derechos. Esto significa que los derechos individuales deben concederse explícitamente. Estos derechos se asignan a grupos, y los usuarios se añaden a los grupos correspondientes para obtener acceso. Incluso si su empresa tiene acceso a la interfaz de usuario de recopilación de datos, los usuarios individuales no pueden hacer nada hasta que un administrador de organización les conceda explícitamente algún derecho.

Para obtener instrucciones detalladas sobre cómo crear grupos y agregar usuarios para etiquetas, consulte el documento [permisos de usuario](../ui/administration/user-permissions.md).

## 2. Iniciar sesión

Una vez añadidos los derechos de etiqueta a su Adobe ID, debe iniciar sesión en la interfaz de usuario de recopilación de datos. Para ello, navegue directamente a la [pantalla de inicio de sesión del Experience Cloud](https://experiencecloud.adobe.com)y seleccionando la IU de recopilación de datos en la pestaña Acceso rápido .

>[!NOTE]
>
>Si tiene una sola cuenta con derechos para varias organizaciones, se puede cambiar la organización seleccionando el nombre de la organización en la barra de control de la parte superior de la pantalla y eligiendo una organización diferente de la lista desplegable.

## 3. Crear una propiedad

Una vez que haya iniciado sesión en la interfaz de usuario de recopilación de datos, lo primero que debe hacer es crear una propiedad. Una propiedad es básicamente un contenedor que se rellena con extensiones, reglas, elementos de datos y bibliotecas al implementar etiquetas en el sitio. Mucha gente crea una propiedad para cada sitio web (o grupo de sitios relacionados) donde desean implementar el mismo conjunto de etiquetas.

Para obtener más información acerca de la creación de propiedades, consulte [Crear una propiedad](../ui/administration/companies-and-properties.md).

## 4. Instalar extensiones

Una extensión es una integración desarrollada por Adobe o un socio de Adobe que añade nuevas e ilimitadas opciones para las etiquetas que usted puede implementar en sus sitios. Si piensa en una etiqueta como un sistema operativo, las extensiones son las aplicaciones que instala para que pueda hacer lo que necesite.

Todas las propiedades nuevas llevan instalada la [Extensión principal](../extensions/web/core/overview.md). Las propiedades móviles incluyen extensiones adicionales. El equipo de Adobe desarrolla la Extensión principal para ofrecer un conjunto de elementos de datos sólido y robusto para sus reglas de datos y tipos de eventos para sus reglas. La mayoría de las acciones que puede querer realizar (obtener un ECID, enviar señalizaciones [!DNL Adobe Analytics], cargar el mbox global de [!DNL Target], etc.) provienen de las extensiones que se instalan del catálogo.

Lo que hace que las etiquetas de Platform sean verdaderamente únicas es que cualquier persona puede crear estas extensiones. ¿Necesita soltar un píxel de remarketing de Facebook en el sitio? Compruebe la extensión desarrollada por Facebook. ¿Desea lo mismo para Twitter o Linked In? Use esas extensiones. ¿Necesita llevar a cabo una encuesta? Consulte Question Pro o Foresee. ¿Necesita administrar la privacidad y el consentimiento de los usuarios finales para ayudarles con [!DNL GDPR]? Eche un vistazo a Evidon y Trust Arc. ¿Desea ver una perspectiva granular del comportamiento de los usuarios individuales en el sitio? Puede probar con Clicktale. Para obtener más información, consulte la sección sobre [adición de una nueva extensión](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Crear elementos de datos y reglas

**Los elementos de datos** señalan la información que desea recopilar y enviar a diferentes lugares de la página:

* Una capa de datos definida en JSON
* Elementos DOM
* Cookies
* Almacenamiento local y de sesión
* Prácticamente todo lo demás

Una vez definido el elemento de datos, puede utilizarlo en cualquier lugar de la interfaz de usuario de recopilación de datos para cualquier extensión. Consulte la documentación sobre [Elementos de datos](../ui/managing-resources/data-elements.md) para obtener información más detallada.

**Las reglas** son el núcleo lógico de la implementación y controlan el qué, el cuándo, el dónde y el cómo de todas las etiquetas del sitio. Defina un evento, establezca condiciones y excepciones y defina las acciones y el orden. Por último, publique los cambios para ver los resultados. Para obtener más información, consulte [Rules](../ui/managing-resources/rules.md).

## 6. Realizar pruebas en el entorno de desarrollo

### Bibliotecas y compilaciones

Las compilaciones de etiquetas nunca se publican automáticamente. Cada conjunto de cambios que realice se encapsula en una [biblioteca](../ui/publishing/libraries.md). Cada biblioteca que cree hereda automáticamente todo el flujo ascendente (publicado, aprobado o enviado) como punto de referencia, por lo que lo único que debe hacer es definir los cambios que desee realizar. Esta biblioteca sirve como modelo para una [compilación](../ui/publishing/builds.md). Una compilación es el conjunto real de archivos JavaScript que se implementan y usan.

Es importante comprender la relación entre la página web, la ubicación de alojamiento y las etiquetas.

1. El servidor host proporciona una ubicación para publicar la compilación. La propia compilación contiene los archivos de JavaScript necesarios para la biblioteca.

   Cada entorno tiene una relación con un host y este proporciona un extremo que indica dónde enviar la compilación. El host solo puede pertenecer a una propiedad, aunque una propiedad puede tener muchos hosts.

2. Se proporciona un código incrustado en la etiqueta de formulario `<script>` que va a las secciones `<head>` del HTML del sitio web.

   Cuando crea un entorno y adjunta un host, el entorno genera automáticamente un código incrustado único que le permite integrar su compilación asignada en el sitio. El código `<script>` se utiliza para implementar la compilación de biblioteca durante la ejecución.

3. Cuando un usuario explora el sitio, la etiqueta de código incrustado `<script>` recupera la compilación desde el servidor host y realiza las acciones definidas dentro del explorador.

### Hosts

Un host es una conexión entre una propiedad de etiqueta y su ubicación de alojamiento. Actualmente, las etiquetas admiten el alojamiento administrado por Adobe a través de un host [!DNL Akamai] o alojamiento propio a través de un host SFTP. Siempre que crea una compilación, las etiquetas se conectan al servidor definido por el host y presenta la compilación.

Si desea alojarlo por su cuenta, puede redirigir una compilación de etiquetas directamente a sus servidores a través de SFTP o puede enviarla a [!DNL Akamai] y descargarla mediante la opción Archivar del entorno.

Para obtener más información, consulte [Hosts](../ui/publishing/hosts/hosts-overview.md).

### Entornos

Cada biblioteca se crea dentro de un entorno. Un entorno define el aspecto que desea que tenga la compilación cuando se publique. Puede especificar:

* **Host:** Cada entorno necesita un host que determine el punto final al que se insertarán las compilaciones creadas en este entorno.
* **Archivo:** La configuración predeterminada es implementar la compilación como archivo reducido .js. Si utiliza código personalizado, puede tener varios archivos que se hagan referencia entre sí. Pueden combinarse en un solo archivo zip y cifrarse.

Después de guardar el entorno, genera el código incrustado que se puede copiar y pegar en el sitio web. Tenga en cuenta que el código incrustado no funciona hasta que cree una biblioteca y produzca una compilación. Para obtener más información, consulte [Environments](../ui/publishing/environments.md).

### Publicación de una compilación en Desarrollo

El proceso de publicación se describe en los pasos siguientes.

1. Cree un host.
1. Crear un entorno de desarrollo utilizando el host que ha creado.
1. Implementar el código incrustado desde su entorno de desarrollo en el sitio de prueba de desarrollo.
1. Crear una biblioteca y asignarla al entorno de desarrollo que ha creado.
1. Crear su biblioteca.

## 7. Enviar a producción

Después de probar la compilación en el entorno de desarrollo, asegúrese de crear los entornos de ensayo y producción, y colocar los códigos incrustados en los lugares necesarios. Para ello, puede reutilizar los hosts existentes.

El envío de una biblioteca hasta la producción suele requerir la coordinación entre distintas personas con los derechos apropiados.

* Un desarrollador (alguien con derecho de Desarrollo) envía la biblioteca, lo que hace que la biblioteca pase al estado Enviada.
* Un aprobador (alguien con derecho de Aprobación) puede llevar la biblioteca al entorno de ensayo y aprobarla después de ponerla a prueba. Esto mueve la biblioteca al estado aprobado. Solo se puede enviar y aprobar una biblioteca a la vez.
* Un publicador (alguien con derecho de Publicación) puede llevar la biblioteca al entorno de producción.

Puede asignar todos estos derechos a una sola persona.

Para obtener más información sobre los distintos estados y opciones disponibles durante el proceso de publicación, consulte [Approval Workflow](../ui/publishing/publishing-flow.md).

## Recursos adicionales

Para obtener más información sobre las etiquetas, consulte los siguientes recursos:

* **[La comunidad de recopilación de datos](https://forums.adobe.com/community/experience-cloud/platform/launch)**: Formule y responda preguntas, aporte ideas, y vote las ideas de otros. Inicie sesión con su ID de Adobe.
* **[Documentos de desarrolladores](https://developer.adobelaunch.com/)**: Participe en la comunidad de desarrolladores de etiquetas para desarrollar extensiones o utilizar las API de etiquetas.
* **[Información general sobre tutoriales](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=es)**: Estos documentos le presentan conceptos de etiquetas, incluidos el reenvío de eventos y SDK móvil en aplicaciones Android.
