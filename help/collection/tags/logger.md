---
title: logger
description: Enviar información a la consola del explorador durante la depuración.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 1%

---

# `logger`

El objeto `_satellite.logger` contiene métodos que permiten enviar mensajes de diagnóstico o información a la consola del explorador cuando la [depuración](../use-cases/debugging.md) está habilitada. Si la depuración no está habilitada, ninguna de las llamadas al método `logger` hará nada.

Estos métodos permiten a los desarrolladores, expertos en marketing técnico y probadores ver fácilmente qué déclencheur hay dentro de una propiedad de etiquetas y cuándo. Dado que estos mensajes de la consola solo aparecen cuando la depuración está habilitada, puede dejar `logger` mensajes en implementaciones en producción sin que ello afecte a la consola del explorador de los visitantes del sitio.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>Las versiones anteriores del objeto de etiqueta usaban `_satellite.notify()`. La función `notify()` está obsoleta en favor de `_satellite.logger`.

## Métodos

Todos los métodos `_satellite.logger` pasan a su método `console.*` de JavaScript correspondiente cuando la depuración está habilitada. La mayoría de los objetos o argumentos `console` son compatibles con `_satellite.logger`:

| Método | Reenvía a | Usos recomendados |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Diagnósticos detallados; algunos exploradores pueden requerir un registro detallado para verlo. |
| `_satellite.logger.log()` | `console.log()` | Mensajes generales. |
| `_satellite.logger.info()` | `console.info()` | Eventos informativos de alto nivel. |
| `_satellite.logger.warn()` | `console.warn()` | Problemas recuperables. La entrada de la consola aparece resaltada en amarillo. |
| `_satellite.logger.error()` | `console.error()` | Errores. La entrada de la consola aparece resaltada en rojo. Adobe recomienda usar `error` objetos para las pilas. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Salida de consola

La biblioteca antepone lo siguiente en todos los mensajes de salida de la consola:

* **🚀**: ayuda a detectar fácilmente qué mensajes de la consola se originan en la implementación de etiquetas.
* **\[Origin\]**: El nombre de la regla, acción, extensión o elemento de datos desde el que se originó el registro. Si llama a un método de registrador fuera de la implementación (por ejemplo, a través de la consola del explorador), se utilizará `[Custom Script]`.
* **Salida de mensaje**: La salida de mensaje incluida al invocar el método.

>[!NOTE]
>
>Los tokens de formato de explorador como `%c`, `%s` y `%d` no se aplican debido a que el registrador aplica el prefijo `🚀 [Origin]`.
