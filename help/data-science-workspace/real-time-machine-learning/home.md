---
keywords: Experience Platform;developer guide;Data Science Workspace;popular topics;Real time machine learning;
solution: Experience Platform
title: Información general sobre aprendizaje automático en tiempo real
topic: Overview
translation-type: tm+mt
source-git-commit: ab8b000bec0ae30c695582f57c40105b7ca1f22f
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 2%

---


# Información general sobre aprendizaje automático en tiempo real

>[!IMPORTANT]
>El aprendizaje automático en tiempo real todavía no está disponible para todos los usuarios. Esta función está en alfa y aún se está probando. Este documento está sujeto a cambios.

El módulo de aprendizaje automático en tiempo real de Adobe Experience Platform le permite utilizar el aprendizaje automático para ofrecer las experiencias correctas a los usuarios finales adecuados en el momento adecuado en los canales adecuados con un intervalo de tiempo de subsegundo.

## Ventajas

El aprendizaje automático en tiempo real puede aumentar considerablemente la relevancia del contenido de su experiencia digital para los usuarios finales. Esto es posible gracias a la inferenciación en tiempo real y al aprendizaje continuo en Experience Edge.

Una combinación de computación sin fisuras tanto en el concentrador como en el borde reduce considerablemente la latencia que tradicionalmente está involucrada en la generación de experiencias hiperpersonalizadas que son relevantes y responden. Por lo tanto, el aprendizaje automático en tiempo real proporciona inferencias con una latencia increíblemente baja para la toma de decisiones sincrónica. Algunos ejemplos son el procesamiento de contenido personalizado de una página web o la aparición de una oferta o descuento para reducir la generación y aumentar las conversiones en una tienda web.

## Arquitectura de aprendizaje automático en tiempo real

El siguiente diagrama proporciona una visión general de la arquitectura de aprendizaje automático en tiempo real.

![Visión general simplificada](../images/rtml/simple-overview.png)

## Flujo de trabajo de aprendizaje automático en tiempo real (Alpha)

El flujo de trabajo siguiente describe los pasos y resultados típicos que conlleva la creación y utilización de un modelo de aprendizaje automático en tiempo real.

### Introducción y preparación de datos

Los datos se ingieren y transforman con el modelo de datos de experiencia (XDM) en la plataforma Adobe Experience. Estos datos se utilizan para la formación de modelos. Para obtener más información sobre XDM, visite la descripción general [de](../../xdm/home.md)XDM.

### Creación  

Cree un modelo de aprendizaje automático en tiempo real creándolo desde cero o incluyéndolo como un modelo ONNX serializado previamente formalizado en equipos portátiles Jupyter de la plataforma Adobe Experience Platform.

### Implementación

Implemente el modelo en Experience Edge para crear un servicio de aprendizaje automático en tiempo real en la Galería de servicios mediante el punto final de la API de predicción.

### Inferencia

Utilice el punto final de la API de REST de predicción para generar perspectivas de aprendizaje automático en tiempo real.

### Entrega

Los especialistas en marketing pueden definir segmentos y reglas que asignen puntuaciones de aprendizaje automático en tiempo real a experiencias con Adobe Destinatario. Esto permite que visitantes del sitio web de su marca se muestren en tiempo real (menos de 100 ms) una experiencia hiperpersonalizada de la misma página o de la siguiente.

## Plan de desarrollo

El aprendizaje automático en tiempo real se encuentra actualmente en la fase alfa. La tabla siguiente describe algunas de las funciones y actualizaciones que se espera que se publiquen en la futura iteración beta.

<table>
    <th></th>
    <th>Alfa (mayo)</th>
    <th>Beta</th>
    <tr>
        <td>
            <strong>Funcionalidades</strong>
        </td>
        <td>
            <li>El espacio de trabajo de ciencias de datos ofrece su propio modelo y autor mediante la integración con el iniciador de portátiles.</li>
            <li>Conjunto inicial de operadores de creación.</li>
            <li>Implementar en concentrador</li>
            <li>Modelos basados en Scikit Learn.</li>
        </td>
        <td>
            <li>Integración de la interfaz de usuario de la galería de servicios de Data Science Workspace.</li>
            <li>Enriquecer automáticamente el Perfil del cliente en tiempo real con resultados de inferencia.</li>
            <li>Modelos de aprendizaje profundo.</li>
            <li>Conjunto ampliado de operadores de creación, incluidos los operadores personalizados.</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Disponibilidad</strong>
        </td>
        <td>
            América del Norte
        </td>
        <td>
            <li>América del Norte</li>
            <li>Europa y Oriente Medio (EMEA)</li>
            <li>Asia-Pacífico (APAC)</li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Creación  </strong>
        </td>
        <td>
            <li>Compatibilidad con Python</li>
            <li>SDK de aprendizaje automático en tiempo real</li>
            <li>Nodos de creación de Python: Pandas, ScikitLearn, ONNXNode, Split, ModelUpload, OneHotEncoder.</li>
        </td>
        <td>
            <li>Compatibilidad con Tensorflow.</li>
            <li>Nodos adicionales de creación de Python: Lector de Perfiles para clientes en tiempo real, Redactor de Perfiles para clientes en tiempo real, Matrices, XDM2Frame, Frame2XDM. </li>
        </td>
    </tr>
    <tr>
        <td>
            <strong>Tiempos de ejecución de puntuación</strong>
        </td>
        <td>
            ONNX
        </td>
        <td>
            ONNX
        </td>
    </tr>
</table>

## Pasos siguientes

Puede empezar por seguir la guía de [introducción](./getting-started.md) . Esta guía lo acompaña durante la configuración de todos los requisitos previos necesarios para crear un modelo de aprendizaje automático en tiempo real.

