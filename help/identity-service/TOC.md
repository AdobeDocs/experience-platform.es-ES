---
audience: user
user-guide-title: Servicio de identidad de Adobe Experience Platform
breadcrumb-title: Guía del servicio de identidad de Experience Platform
user-guide-description: Una las identidades de los clientes entre dispositivos y sistemas para ofrecer experiencias digitales personalizadas.
feature: Identities
role: Admin,Developer
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 30%

---


# Servicio de identidad de Adobe Experience Platform {#identity}

- [Introducción al servicio de identidad](home.md)
- [Servicio de identidad y perfil del cliente en tiempo real](identity-and-profile.md)
- Funciones {#features}
   - [Área de nombres de identidad](./features/namespaces.md)
   - [Lógica de vinculación de identidad](./features/identity-linking-logic.md)
   - [Visualizador de gráficos de identidad](./features/identity-graph-viewer.md)
   - [Eliminaciones en el servicio de identidad](./features/deletion.md)
   - Reglas de vinculación de gráfico de identidad {#identity-graph-linking-rules}
      - [Resumen de funciones](./identity-graph-linking-rules/overview.md)
      - [Algoritmo de optimización de identidad](./identity-graph-linking-rules/identity-optimization-algorithm.md)
      - [Guía de implementación para reglas de vinculación de gráficos de identidad](./identity-graph-linking-rules/implementation-guide.md)
      - [Ejemplo de configuraciones de gráficos](./identity-graph-linking-rules/example-configurations.md)
      - [Solución de problemas de reglas de vinculación de gráficos de identidad](./identity-graph-linking-rules/troubleshooting.md)
      - [Prioridad del área de nombres](./identity-graph-linking-rules/namespace-priority.md)
      - [IU de simulación de gráficos](./identity-graph-linking-rules/graph-simulation.md)
      - [IU de configuración de identidad](./identity-graph-linking-rules/identity-settings-ui.md)
   - [Información general de ECID](./features/ecid.md)
- [Guía de implementación](implementation.md)
- [Protecciones para datos de identidad](guardrails.md)
- API del servicio de identidad {#api}
   - [Primeros pasos](api/getting-started.md)
   - [Etiquetado de un campo como identidad](api/label-identities.md)
   - [Enumerar identidades de clúster](api/list-cluster-identites.md)
   - [Enumerar el historial de clúster de una identidad](api/list-cluster-history.md)
   - [Enumerar asignaciones de identidad](api/list-identity-mappings.md)
   - [Enumerar áreas de nombres disponibles](api/list-namespaces.md)
   - [Crear un área de nombres personalizada](api/create-custom-namespace.md)
   - [Enumeración del ID nativo de una identidad](api/list-native-id.md)
   - [Referencia de API](https://www.adobe.io/experience-platform-apis/references/identity-service)
- [Definición de campos de identidad en la IU](label-identities.md)
- [Procesamiento de solicitud de privacidad](privacy.md)
- [Guía de resolución de problemas](troubleshooting-guide.md)
- [Notas de la versión de Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform/release-notes/latest)