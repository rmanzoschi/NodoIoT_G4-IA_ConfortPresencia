# Dashboard G4

Dashboard web en HTML, CSS y JavaScript. Incluye modo de demostración con datos simulados y modo MQTT para administración.

Abrir `index.html` en un navegador moderno. Para recibir datos reales, el navegador debe alcanzar el broker mediante WebSockets.

La dirección actual del broker es local (`ws://192.168.101.94:9001/mqtt`). Para una web pública se necesita un endpoint accesible y normalmente WSS. No inventar ni reemplazar la dirección sin confirmar la configuración real.

Se corrigió la inconsistencia entre `TOPICOS` y `TOPICS`: la configuración y las lecturas ahora usan `TOPICS`.
