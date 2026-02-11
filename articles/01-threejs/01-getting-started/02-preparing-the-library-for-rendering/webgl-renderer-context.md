---
tags:
  - ref
  - deep-dive
status: draft
---

# Контекст рендеринга

> Начиная с версии `r163`, `Three.js` поддерживает только `WebGL2`. Передача в качестве параметра контекста `WebGLRenderingContext` приведёт к ошибке.

По умолчанию, конструктор `WebGLRenderer` создаст контекст за нас используя метод холста `getContext`. В этом случае у нас остаётся возможность задать большую часть (но не все) настроек через параметры конструктора, эти параметры являются отображением на атрибуты [`webgl2` контекста](https://registry.khronos.org/webgl/specs/latest/2.0/#3.7) (второй параметр метода [`getContext`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLCanvasElement/getContext), [объект атрибутов контекста](https://registry.khronos.org/webgl/specs/latest/1.0/index.html#WEBGLCONTEXTATTRIBUTES))

## Параметры конструктора

| Параметр                | Атрибут контекста       | По умолчанию | Описание                                              |
| ----------------------- | ----------------------- | ------------ | ----------------------------------------------------- |
| `alpha`                 | `alpha`                 | `true`       | Прозрачность холста                                   |
| `antialias`             | `antialias`             | `false`      | Сглаживание                                           |
| `depth`                 | `depth`                 | `true`       | Буфер глубины                                         |
| `stencil`               | `stencil`               | `false`      | Буфер трафарета                                       |
| `premultipliedAlpha`    | `premultipliedAlpha`    | `true`       | Предумноженная альфа                                  |
| `preserveDrawingBuffer` | `preserveDrawingBuffer` | `false`      | Сохранять буфер^[Необходимо для `canvas.toDataURL()`] |
| `powerPreference`       | `powerPreference`       | `"default"`  | `"high-performance"` / `"low-power"`                  |

## Передача своего контекста

```javascript
const canvas = document.createElement('canvas');
const context = canvas.getContext('webgl2', { antialias: true });
const renderer = new THREE.WebGLRenderer({ canvas, context });

> Конструктор устанавливает большое количество различных настроек, и самое главное, задаёт текущее состояние, и изолирует стек состояний, создаёт контекст рендеринга вызовом метода `getContext(type[, attrs])` элемента `canvas`, объект через который осуществляется доступ ко всем возможностям WebGL.
```
