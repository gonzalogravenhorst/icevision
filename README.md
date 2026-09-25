# Hockey — planillero local + estadísticas públicas

La aplicación queda separada en dos partes:

- `planillero/`: aplicación privada/local. Se ejecuta en la computadora del planillero y guarda equipos, jugadores, fixture y estado en `localStorage` del navegador.
- `docs/`: página pública estática para GitHub Pages. Solo muestra los datos publicados en `docs/data.json`.

El `.gitignore` evita subir `planillero/` al repositorio. De esa forma, la URL pública de GitHub Pages no expone la aplicación del planillero.

## 1. Publicar la página pública en GitHub

1. Creá un repositorio en GitHub.
2. Copiá/subí `docs/`, `.gitignore` y este `README.md`.
3. En **Settings → Pages**, elegí desplegar desde la rama `main` y la carpeta `/docs`.
4. GitHub te dará la URL de la página pública.

La página pública contiene:

- Fixture en vista calendario.
- Partidos programados.
- Resultado de partidos finalizados.
- Equipos y categorías.
- Planteles.
- Goles y asistencias por jugador.
- Tabla de equipos con PJ, ganados, empatados, perdidos, GF, GC y puntos.

## 2. Usar el planillero

El planillero **no necesita GitHub Pages**. En la PC donde se lleva la planilla:

- Abrí `planillero/planilla.bat`, o
- ejecutá `python -m http.server 8000` dentro de `planillero/` y abrí `http://localhost:8000`.

Los equipos, jugadores y partidos quedan guardados en el navegador de esa PC mediante `localStorage`, por lo que no hay que recrearlos cada vez.

### Importante

El `localStorage` está asociado al navegador/perfil de esa PC. No borres los datos del sitio ni uses modo incógnito si querés conservarlos.

## 3. Publicar los datos en GitHub

En el planillero, abrí **Publicación** y completá:

- Usuario/organización de GitHub.
- Repositorio.
- Rama, normalmente `main`.
- Ruta pública: `docs/data.json`.
- Un token Fine-grained de GitHub con acceso **Contents: Read and write** únicamente al repositorio correspondiente.

El token se guarda solamente en `localStorage` de la computadora del planillero y no se escribe en `docs/data.json`.

Después de crear/modificar equipos, jugadores o partidos, usá **Publicar stats**. El planillero actualiza `docs/data.json` mediante la API de GitHub.

### Flujo recomendado

1. Crear equipos.
2. Cargar jugadores.
3. Crear el fixture.
4. Publicar.
5. Durante cada partido, registrar goles, asistencias y penalidades normalmente.
6. Finalizar el partido.
7. Volver a **Publicar stats**.
8. La página pública mostrará el resultado y actualizará las estadísticas.

## 4. Qué se publica

La publicación contiene únicamente información destinada a la página pública: equipos, jugadores, fixture, resultados y eventos deportivos necesarios para calcular las estadísticas.

Los oficiales del partido y otros datos internos del planillero no se incluyen en `docs/data.json`.
