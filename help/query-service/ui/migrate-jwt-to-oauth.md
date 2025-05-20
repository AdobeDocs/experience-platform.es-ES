---
title: Migrar de JWT a credenciales de servidor a servidor OAuth
description: Obtenga información sobre cómo migrar credenciales de JWT que no caducan a credenciales de servidor a servidor OAuth en Adobe Experience Platform para mantener un acceso seguro e ininterrumpido al servicio de consultas antes de que la compatibilidad con JWT termine el 30 de junio de 2025. Esta guía proporciona instrucciones paso a paso, explica el comportamiento posterior a la migración y responde a preguntas comunes.
source-git-commit: 264d3b12d8fd3bd100018513af1576b3de1cbb33
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---

# Migrar de JWT a credenciales de servidor a servidor OAuth

>[!IMPORTANT]
>
>Adobe está desaprobando la compatibilidad con las credenciales de la cuenta de servicio (JWT) utilizadas por el servicio de consultas. A partir del 30 de junio de 2025, las credenciales que no caduquen basadas en JWT ya no actualizarán ni autenticarán solicitudes de API. Para evitar interrupciones en el servicio, debe migrar cada credencial elegible a la autenticación de servidor a servidor OAuth.

Esta guía muestra cómo migrar credenciales de JWT que no caducan a credenciales de servidor a servidor OAuth en Adobe Experience Platform. Completar este proceso garantiza el acceso ininterrumpido al servicio de consulta antes de que la compatibilidad con las credenciales de JWT finalice el 30 de junio de 2025.

Este documento proporciona instrucciones paso a paso para realizar la migración, comprender el impacto y verificar las credenciales actualizadas.

## Quién debe migrar {#who-needs-to-migrate}

Si utiliza credenciales que no caducan en el servicio de consultas, debe migrar cada una de ellas. Esto se aplica a las credenciales utilizadas en flujos de trabajo automatizados, consultas programadas o integraciones de API personalizadas.

Si ve las credenciales enumeradas en la sección **[!UICONTROL Credenciales que no caducan]** de la ficha **[!UICONTROL Credenciales]**, dichas credenciales se verán afectadas.

## Migración de credenciales {#how-to-migrate}

Puede migrar las credenciales directamente en la interfaz de usuario de Experience Platform. Para ello, vaya a **[!UICONTROL Consultas]** en el panel de navegación izquierdo y luego seleccione la pestaña **[!UICONTROL Credenciales]**. En la sección **[!UICONTROL Credenciales que no caducan]**, identifique una credencial marcada como elegible para la migración y seleccione **[!UICONTROL Migrar]** junto a ella.

>[!NOTE]
>
>La migración tarda de 8 a 10 segundos y no se puede cancelar una vez iniciada.

![Área de trabajo de credenciales del servicio de consulta con consultas, credenciales y migración resaltadas.](../images/ui/migrate-jwt-to-oauth/migrate.png)

Después de la migración, el sistema actualiza la credencial para utilizar la autenticación de servidor a servidor OAuth. El método basado en JWT se retira automáticamente y el estado se actualiza a **[!UICONTROL Migrado]**.

No se requiere ninguna reconfiguración. Los trabajos e integraciones existentes siguen funcionando sin interrupciones.

## Qué sucede después de la migración {#after-migration}

Una vez completada la migración:

- Sus credenciales siguen funcionando sin problemas, por lo que no es necesario realizar cambios en sus trabajos o integraciones.
- El servicio de consulta utiliza automáticamente la autenticación de servidor a servidor OAuth.
- El método de autenticación basado en JWT se ha retirado y ya no está en uso.

>[!IMPORTANT]
>
>No puede deshacer este cambio. Una vez migrada, la credencial no se puede revertir a JWT.

## Preguntas frecuentes {#faq}

Estas preguntas responden a preocupaciones comunes y le ayudan a garantizar una migración sin interrupciones y sin interrupciones.

### ¿Por qué Adobe está desaprobando las credenciales de JWT?

Servidor a servidor OAuth es un método de autenticación más seguro y estandarizado. Proporciona una mejor administración del ciclo de vida y admite una coherencia de plataforma más amplia.

### ¿Qué sucede si no migre antes del 30 de junio de 2025?

Las credenciales de JWT dejarán de actualizarse y las integraciones que dependen de ellas fallarán. Adobe no puede migrar credenciales en su nombre a menos que inicie el proceso.

### ¿Cómo sé si necesito migrar?

Si aparece una credencial en la sección **[!UICONTROL Credenciales que no caducan]** de la pestaña Credenciales, esas credenciales deben migrarse.

### ¿Necesito actualizar mis integraciones o volver a configurar algo?

No. Después de la migración, las credenciales de OAuth se hacen cargo automáticamente. No se requieren cambios manuales en sus trabajos o integraciones.

### ¿Puedo migrar todas las credenciales a la vez?

No. Debe migrar cada credencial de forma individual mediante el botón **[!UICONTROL Migrar]**.

### ¿Puedo seguir utilizando credenciales que caducan?

Sí. Las credenciales que caducan no se ven afectadas por este cambio. Solo se deben migrar las credenciales de JWT que no caduquen.

### Veo un mensaje que dice &quot;[!UICONTROL No se encontraron credenciales que no caduquen.]&quot; ¿Qué significa eso? ¿Debo tomar alguna acción?

Este mensaje significa que aún no ha creado ninguna credencial que no caduque, por lo que no tiene que hacer nada.

### Veo un mensaje que dice &quot;[!UICONTROL Error en la verificación del administrador de AEP]...&quot; ¿Qué significa eso? ¿Debo tomar alguna acción?

Este mensaje indica que no es administrador o que no tiene los permisos necesarios para crear credenciales que no caducan.

- Si los permisos no han cambiado recientemente, significa que nunca tuvo acceso para crear credenciales, por lo que no es necesario realizar ninguna acción.
- Si los permisos se han cambiado recientemente, póngase en contacto con el administrador de su organización y pídale que migre las credenciales.

### ¿Puedo migrar las credenciales que no caducan para otra persona?

Sí, pero solo si es administrador. Solo los administradores tienen los permisos necesarios para crear y migrar credenciales que no caducan para otros usuarios, de modo que puedan seguir trabajando sin interrupciones.

## Pasos siguientes {#next-steps}

Revise cada credencial que no caduque en la ficha [!UICONTROL Credenciales] y migre las credenciales individualmente antes del 30 de junio de 2025. Si tiene alguna pregunta o necesita asistencia, póngase en contacto con el representante de su cuenta de Adobe.
