# Smart Campus IoT · Grupo G4

Proyecto final de 6.º año Informática A del Instituto Leonardo Murialdo (2026).

Sistema de monitoreo ambiental para un aula mediante un ESP32-C3, sensores, comunicación Wi-Fi/MQTT y un dashboard web.

## 🌐 Ver el proyecto
- **Documentación:** [`index.html`](index.html).
- **Dashboard:** [`dashboard/index.html`](dashboard/index.html).

> El dashboard conserva la dirección MQTT local utilizada en el entorno de pruebas. Para recibir datos desde Internet/GitHub Pages se necesita un broker accesible desde el exterior y compatible con WebSockets seguro (WSS), además de configurar el endpoint correcto.

## 🧩 Tecnologías
- ESP32-C3 Super Mini y sensores ambientales.
- Arduino/C++ para el firmware.
- Wi-Fi y MQTT para la comunicación.
- HTML, CSS y JavaScript para la interfaz.
- MQTT.js y Chart.js en el dashboard.

## 📁 Estructura
```text
.
├── index.html              # Documentación del proyecto
├── assets/
│   ├── styles.css
│   ├── app.js
│   └── modelo-3d/          # Reservado para el modelo original
├── dashboard/
│   ├── index.html          # Dashboard del equipo
│   └── README.md
├── docs/                   # Documentación técnica complementaria
├── firmware/               # Código ESP32 (incorporar)
├── hardware/               # Planos y conexiones
└── evidencias/             # Fotos, pruebas y resultados
```

## 🚀 Publicar con GitHub Pages
1. Subir el contenido de esta carpeta a la rama `main` del repositorio.
2. Abrir **Settings → Pages**.
3. En **Build and deployment**, elegir **Deploy from a branch**.
4. Seleccionar la rama `main` y la carpeta `/(root)`.
5. Guardar y esperar la URL que entrega GitHub Pages.

## 👥 Equipo G4
- **Manzo Román:** Dirección del proyecto.
- **Gavazza Fidel:** Hardware y electrónica.
- **Alvarez Benjamín:** Gestión de documentación.
- **Tagliaferro Tiziano:** Programación de redes.
- **Surra Joaquín:** Diseño UI/UX y frontend.

## 📌 Estado de esta entrega
La documentación y el dashboard están organizados. El equipo reporta el hardware y la comunicación MQTT como funcionales. Quedan por incorporar evidencias ampliadas, presupuesto, carta Gantt definitiva, firmware, planos/fotos finales y el modelo 3D.

---
**Instituto Leonardo Murialdo · 6.º año Informática A · Grupo G4 · 2026**
