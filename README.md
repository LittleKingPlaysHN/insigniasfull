# Discord-badge-spoofer

Infla las insignias de tu perfil de Discord: añade horas de juego y marca los juegos como jugados.

**Cómo funciona:** El endpoint de análisis de Discord (`/api/v9/science`) registra a qué juegos juegas y cuánto tiempo juegas. Esta herramienta publica los mismos eventos que el cliente real (`launch_game` y `running_game_heartbeat`), pero con horas y listas de juegos personalizadas. Discord acepta los eventos (`204`) y estos aparecen en tus insignias.

**Estado:** Verificado y funcionando, sin parches. Las insignias tardan de 1 a 2 días en actualizarse, así que no esperes resultados inmediatos. Tu token y cookie se almacenan solo localmente; nada sale de tu ordenador. Esto podría dejar de funcionar en cualquier momento si Discord actualiza el endpoint.

**Importante:** Esto infringe los Términos de Servicio de Discord. Úsalo en cuentas que no te importe perder.

## Configuración

Sin dependencias: biblioteca estándar de Python (requiere Python 3.10 o superior).

1. Ejecútalo:

```

python spoofer.py

```

2. La primera vez que lo ejecutes, te pedirá el token de tu cuenta de Discord. Pégalo y se guardará en `science_state.json` (se reutilizará después). El token de análisis se obtiene automáticamente de `GET /users/@me?with_analytics_token=true`.

3. También necesitas una cookie (`cf_clearance`). Al iniciar, te la pedirá, o puedes añadirla/actualizarla más tarde mediante la opción `3` (actualizar autenticación). Obtén el encabezado completo de la cookie de cualquier solicitud `/science` en las herramientas para desarrolladores (pestaña Red). Se guardará en `science_state.json`.

5. **Opcional: huella digital para el recuento de juegos jugados.** La huella digital no es estrictamente necesaria; algunos usuarios han informado haber obtenido la insignia de juegos jugados sin configurarla. Si deseas configurarla, obtén una `executable_fingerprint` real de una solicitud `launch_game` en las herramientas de desarrollo de tu cliente y agrégala a `science_state.json` como `"fingerprint": "..."`.

## Menú

- `1` Tiempo de juego: solicita las horas por juego y se aplica a todos.
- `2` Partidas jugadas: marca cada partida como jugada (1 minuto cada una).
- `3` Actualizar autenticación: obtiene un nuevo token de análisis y permite actualizar la cookie.
- `4` Salir

## Cómo funciona la autenticación

- `token`: token de tu cuenta, introducido la primera vez que lo ejecutas, guardado en `science_state.json`.
- `analytics_token`: se obtiene mediante `GET /users/@me?with_analytics_token=true`.
- `super_props` / heartbeat / launch ids: se generan automáticamente.
- `cookie` (cf_clearance): se pega manualmente mediante la opción `3`.
- `fingerprint`: opcional, solo necesario para el recuento de partidas jugadas (ver más abajo).

Las insignias se actualizan según el ciclo de análisis de Discord (1-2 días), así que no esperes ver los resultados de inmediato.

## Acerca de la huella digital

Funciona con solo tu token y cookie. El contador de partidas jugadas podría requerir una `huella digital ejecutable` real; aún no estamos completamente seguros. Algunos usuarios han reportado obtener insignias sin ella, así que inténtalo primero. Si no funciona después de unos días, obtén una `huella digital ejecutable` real de una solicitud `launch_game` en las herramientas de desarrollo de tu cliente y agrégala a `science_state.json`:

```json
{ "huella digital": "Ab5ekw..." }
```

En cualquier caso, la herramienta publicará los eventos. Solo necesitamos saber si las insignias se mueven con o sin la huella digital para poder determinar qué se requiere realmente.

## Aviso legal

Esto infringe los términos de servicio de Discord. Úsalo solo en cuentas que no te importe perder.

Se proporciona tal cual, sin garantía.

## Licencia

Publicado bajo la licencia MIT. ver [LICENCIA](LICENCIA).