# Web Calendario (Cloudflare Pages)

## Deploy seguro (recomendado)
- Producción: solo desde `main`.
- Cambios: siempre vía PR pequeño (1 objetivo por PR).
- Validación: usar Preview Deployment de Cloudflare Pages en cada PR.

## Checklist smoke test (manual, 2–3 min)
1. Nuevo proyecto: seleccionar año y orientación.
2. Subir portada y algunas fotos diarias.
3. Cambiar mes, ajustar zoom/rotación, volver atrás/adelante.
4. Vista previa: generar y comprobar que no hay errores en consola.
5. Exportar: PDF mes y PDF año (si hay portada).
6. Exportar ZIP e importar ZIP.

## Rollback
- Opción 1: revert del commit en `main`.
- Opción 2: redeploy de un deployment anterior en Cloudflare Pages.

## Debug
- Activar modo debug: añadir `?debug=1` a la URL (se recuerda en el navegador).
- En debug se loguean errores no controlados con un snapshot mínimo del estado.


## Error monitoring (Sentry)

Este proyecto no tiene servidor. Para ver errores reales en usuarios se integra Sentry (Browser JS) via script loader en las páginas HTML.

- Release actual: `web-calendario@20260128210911` (se recomienda alinearlo con tags de git en futuros releases).
- Tracing y Session Replay están desactivados por defecto en el snippet (`tracesSampleRate: 0`, `replays*SampleRate: 0`) para minimizar impacto y evitar capturar contenido visual.
- Contexto extra enviado: `window.__WC_APP_STATE__` (build, path, lastAction).

Para probar que está activo, puedes forzar un error en consola o temporalmente llamar una función inexistente.
