# Smart Campus IoT — Grupo G4

Proyecto final de 6.º año · Informática A · Instituto Leonardo Murialdo · 2026.

## Accesos rápidos

<p align="center">
  <a href="https://rmanzoschi.github.io/NodoloT_G4-IA_ConfortPresencia/" target="_blank" rel="noopener noreferrer"><strong>📘 ABRIR DOCUMENTACIÓN</strong></a>
  &nbsp;&nbsp; | &nbsp;&nbsp;
  <a href="https://rmanzoschi.github.io/NodoloT_G4-IA_ConfortPresencia/dashboard/" target="_blank" rel="noopener noreferrer"><strong>📊 ABRIR DASHBOARD</strong></a>
</p>

> Si GitHub Pages todavía no publicó el sitio, activalo en **Settings → Pages**: Deploy from a branch → `main` → `/ (root)` → Save. Esperá a que termine el deploy de GitHub Actions.

## Estructura

- `index.html`: documentación web del proyecto.
- `dashboard/index.html`: dashboard de monitoreo.
- `assets/`: estilos y recursos de la documentación.
- `firmware/`: documentación del firmware.
- `hardware/`: documentación del hardware.
- `docs/`: material complementario.
- `evidencias/`: espacios para fotos y pruebas.

## Estado del proyecto

- Hardware: integrado y funcionando.
- Comunicación MQTT: conectada y funcionando en la red configurada.
- Presupuesto, pruebas ampliadas y detalles del indicador de confort: pendientes de completar en la documentación.

## Nota sobre MQTT

El dashboard está configurado con el broker indicado en su archivo. Para acceder a datos reales desde fuera de esa red, el broker debe ser accesible desde Internet y ofrecer WebSockets seguros (WSS); publicar GitHub Pages por sí solo no expone el broker local.
