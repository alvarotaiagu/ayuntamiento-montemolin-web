# Ayuntamiento de Montemolín · propuesta de web «Puerta abierta»

Maqueta de la web municipal del **Ayuntamiento de Montemolín** (Badajoz, 1.231 habitantes, INE 2025), hecha con la plantilla «Puerta abierta» v3 (`plantilla-ayuntamiento-puerta-abierta-web`) y con sus datos reales. Se le propone por correo.

- **No es la web oficial.** Lleva en todas las páginas la banda «Propuesta de diseño… no es la web oficial» y `noindex, nofollow`.
- **Sin publicar** (5-10-2026): vive solo en local. Con `?revision` sale el mando de versión y color.
- Las fuentes de cada dato, el inventario de su web actual y sus errores están **fuera de esta carpeta**, en `../ayuntamiento-montemolin-bocetos/`:
  - `DATOS.md`;
  - `INVENTARIO.md`;
  - `ERRORES.md`.

```bash
npm install                     # Playwright y axe-core (solo para los scripts)
node scripts/aplicar.mjs        # genera la web desde municipio.json, marca/, contenido/ y media/
node scripts/servir.mjs         # http://127.0.0.1:4192/  ·  con ?revision, el mando
node scripts/verificar.mjs      # todas las comprobaciones
```

`municipio.json` lo escribe `../ayuntamiento-montemolin-bocetos/_scripts/municipio.mjs` a partir de lo recogido. El tablón lo escribe `_scripts/tablon-web.mjs` (con los títulos claros de `_scripts/titulos-claros.json`).

---

## El concepto

**La puerta del Ayuntamiento, abierta todo el día.** El arco de medio punto encalado es el único motivo dibujado y enmarca el castillo, la parroquia o la ermita de la Granada en la portada (sale una al azar en cada visita). El panel «Hoy en Montemolín» dice tres cosas:
- si el Ayuntamiento está abierto, calculado con la hora real;
- qué es lo próximo de la agenda;
- cuál es el último aviso.

Por qué le encaja a Montemolín:
- **La web actual tiene la mitad del menú vacío.** Diecisiete entradas (Hacienda, Obras, Padrón, Registro, Urbanismo, Biblioteca, Piscina, Fiestas, Alojamientos…) llevan a una página sin nada, y las noticias están paradas desde julio de 2023. Aquí cada cosa que el vecino busca tiene su sitio: 20 trámites con un buscador en palabras normales, el listín con los consultorios, las farmacias y los teléfonos que la web no tenía, las instalaciones municipales y la normativa (69 documentos de 2014 a 2026).
- **El tablón vivo está en su web, no en la sede.** La sede tiene el tablón vacío; el que se usa está en `montemolin.es/tablon.php`, con 95 anuncios y el último de septiembre de 2026. Aquí entran los 30 más recientes, cada uno con su título en lenguaje claro y su plazo con cuenta atrás (IAE: hasta el 16 de noviembre). Lo que lleva datos personales se queda fuera.
- **Dos pueblos más.** Pallares y Santa María de Nava tienen concejal delegado, consultorio, farmacia (Pallares), agencias de lectura y fiestas propias: aparecen en «¿Quién se ocupa de qué?», en el listín, en «El pueblo» y en las fiestas.
- **Los avisos, donde ya se dan.** No hay Bandomóvil: el Ayuntamiento publica sus bandos en el Facebook de la Universidad Popular, y la web lo cuenta («Reciba los avisos en el móvil») sin sustituirlo.
- **Una historia con personajes.** Martín Álvarez (el granadero de San Vicente, que da nombre a un buque de la Armada) y Casiodoro de Reina (la «Biblia del Oso») salen de los PDF de su propia web, que nadie encontraba.

**Marca: el sinople del escudo.** El escudo es plata y gules (la cruz de Santiago y el campo) con dos anclas de oro. El gules es el color de las alertas y el azur y el sinople solo salen de las gemas de la corona; se eligió el sinople porque es el verde de la dehesa y el que ya usa su web actual (motivo escrito en `marca/marca.json`). La cortina de entrada es la del escudo.

**Escudo.** El de Commons (Erlenmeyer, CC BY-SA 4.0) sigue el blasón del BOE (RD 1624/1977). El de su sede electrónica tiene el primer cuartel azul y no coincide.

---

## Mapa de páginas

- **Inicio.** Hoy, plazos abiertos, trámites más pedidos, tablón, lo que viene y lo que pasó, «El año en Montemolín», cifras (padrón, superficie, altitud, 1248), «Conocer», ¿quién se ocupa de qué?, la sede y el pie con el plano de las calles.
- **El Ayuntamiento:** corporación (hemiciclo de 9: PP 5 y PSOE 4), delegaciones, contacto y normativa.
- **Trámites** (buscador global), **Avisos** y tablón, **Noticias**, **Agenda**, **Teléfonos y servicios** (con la hoja para imprimir en una A4), **El pueblo** (con el mapa del término), **Contacto**.
- **Trámites explicados fácil**, **Avisar de un problema**, **Escríbanos**, **Transparencia**, **Suscribirse** (feed y calendario).
- Aviso legal, privacidad, cookies, accesibilidad y 404.
- Solo en castellano: **«El pueblo» no se traduce** (decisión del 5-10-2026 para los pueblos nuevos).
- Fuera del menú: `propuesta.html` (la página para el alcalde) y `publicar.html` (para la secretaría).

---

## Qué se añadió a la plantilla para Montemolín (v3d)

La plantilla se amplió **una sola vez**, sin parches de este pueblo (commits `8413090` y `cea58fd` de la plantilla, 176 de 176 comprobaciones):
- **`sede.tablon_url`**: el tablón oficial está en la web y no en la sede. El pie, «Avisos» y la portada llevan a ese tablón; sus anuncios pueden enlazar a ese sitio (y a ningún otro); los avisos para lectores de pantalla dicen «se abre la web del Ayuntamiento»; `tablon.mjs` no pisa `tablon.json` con el tablón vacío de la sede. Documentado en `RESKIN.md` §4 y probado en `verificar.mjs` («v3d · sede.tablon_url»).
- **«Plan de empleo» en singular** no se reconocía como empleo (solo «planes de empleo»): era justo el último anuncio de su tablón.
- **El espejo `overpass.openstreetmap.fr`** en la lista de servidores de OSM: los otros tres fallaron el 5-10-2026.

Adaptado en esta copia (lo que depende de los datos del pueblo): en `verificar.mjs`, la muestra del mapa del término con lugares de Montemolín y los ids de OSM comprobados (F25).

---

## Pendientes para el Ayuntamiento

1. **Horario de atención.** El único que consta es el cartel de 2021 (lunes a viernes, de 8:00 a 14:00); el PDF del Punto de Información Catastral, de 2018, dice 9:00-15:00. Confirmarlo.
2. **Correo** para «Avisar de un problema» y «Escríbanos»: ahora, `ayuntamiento@montemolin.es`, por confirmar. Y cuál de los dos teléfonos es el de ventanilla (924 510 001 o 924 510 111).
3. **Perfil del pie** (el dibujo del pueblo): es el genérico. Dibujarlo desde fotos reales (el castillo y la torre de la parroquia) es un paso aparte.
4. **`hoja.id`**: la hoja de Google para publicar desde el móvil (`PUBLICAR.md`).
5. **Autorización para leer su tablón** cada día (`tablon_autorizado`): el lector automático solo está hecho para sedes; el tablón de su web se ha copiado a mano el 5-10-2026 y hace falta un lector para `tablon.php` o que lo publiquen en la hoja.
6. **Permiso para usar las fotos de su web** (galería y repositorio) o fotos propias de la plaza, las fiestas y el interior de la parroquia.
7. **Canal de avisos**: confirmar que «Univ Pop Montemolín» (Facebook) es el canal del Ayuntamiento, o crear uno propio (Bandomóvil).
8. Un alcalde que escriba el **saludo** (el de su web es del alcalde anterior).
9. Fecha del cambio de alcaldía y toma de posesión de Encarnación Valverde Luna (no constan).
10. Teléfonos de la Agente de Empleo, la Policía Local, el Juzgado de Paz y Protección Civil; la Guardia Civil que cubre el municipio; el teléfono del colegio.
11. Horario de la biblioteca y del punto limpio; calendario de recogida de basura; farmacia de guardia.
12. Nombre oficial del núcleo («Nava» o «Navas») y de la ermita de San Blas (OSM la llama «de Gracia»).
13. Dirección del perfil del contratante en la Plataforma de Contratación (la web enlaza la página general).
14. Fiestas locales de 2027 (aún no están en el DOE).

---

## Erratas de su web, corregidas al usar sus textos

- «Archivo **Muncipal**», «**Uuniversidad** Popular», «**Callejeroi** Santa María de Navas», «Pedanias», «**Tenitente**», «**Dº.**», «Andrés **Fabrique**» (Fadrique), «**comformidad**».
- «Información **pùblica**» y «**clàusulas**» (tildes graves), «**Escruitinio**», «**CANIDIDATAS**» y «**EXCLUSIVON**».
- «ELECCIONES A CORTES GENERALES 23 DE **JUNIO** 2023»: las generales fueron el 23 de julio (el anuncio es del 24-07-2023). En la web nueva se dice «Elecciones generales de 2023».
- Los títulos en mayúsculas pasan a frase normal («ORDENANZA TASA POR…» → «Ordenanza tasa por…») y se añade el espacio que faltaba tras alguna coma.
- La lista completa de errores de su web, con su URL, está en `ERRORES.md`.

## Datos que se contradicen

Lista completa en `ERRORES.md` §6. Los que cambian lo que se ve:
- **Superficie:** 202,7 km² (ficha municipal y polígono del término en OSM) frente a 208,90 (Cedeco): se enseña 202,7 con su fuente.
- **Altitud:** 615 m (ficha) y 619 m (IGN, en OSM): se enseña 615 m «según la ficha municipal».
- **Habitantes:** INE 1.231; la ficha de la Diputación aún dice 1.467 (de 2014).
- **Año de la recompra de la jurisdicción:** 1770 (web) y 1779 (Wikipedia): no se escribe.
- **Teléfonos y direcciones de los consultorios:** web actual del SES frente al catálogo de 2022: se usa la web actual.
- **Alcalde:** su web da a dos alcaldes distintos según la página; se usa el de los bandos de 2026 y el BOP.

## Fotos

- **De Wikimedia Commons**, con su licencia en `media/creditos.json`: la parroquia (Adolfobrigido, CC BY-SA 4.0) y el abrevadero de Pilar Redondo (Marbregal, CC BY 3.0).
- **De su web** (galería y repositorio), **solo para esta maqueta** y con la nota en `creditos.json`: vista general, castillo, ermita de la Granada, ermita de San Blas, iglesia de Pallares, Santa María de Nava y su torre. No se usa la segunda foto de la página del castillo: es un archivo cortado.
- `fotos.py` las recorta y las lleva a 1600 y 800 px; `fotos-igualar.py` les aplica a todas el mismo tratamiento de color (`media/_comparativa-igualado.jpg`). Los originales están en `media/originales/`.
- Ni banco de imágenes ni IA. Faltan: la Plaza de la Constitución, las fiestas y el interior de la parroquia (huecos diseñados).

## Antes de entregar

Ver `RESKIN.md` §9: pasar a `"propuesta": false` y `"indexar": true` solo cuando sea la web oficial en su dominio, quitar el mando con `scripts/quitar_mandos.py`, y volver a ejecutar `aplicar.mjs` y `verificar.mjs`. No se ha creado ningún repositorio ni se ha publicado nada para este municipio.

## v3 (5-10-2026)

Hecha con la plantilla v3 (v3, v3b, v3c y la v3d de arriba): hero con varias fotos al azar, panel «Hoy» con plazos y empleo, «en cifras», buscador global, mapa propio del término (7 lugares de OSM), plano de las calles del pie, lectura fácil (4 trámites y las incidencias), avisar de un problema, «Escríbanos», transparencia, feed y calendario, hoja para publicar desde el móvil y la tarea diaria de GitHub (que, mientras `tablon_autorizado` y `hoja.id` estén vacíos, solo rehace las fechas). `contenido/tablon.json` se escribe con `_scripts/tablon-web.mjs`.

**Resultado de `verificar.mjs --capturas` (5-10-2026): 174 de 174 comprobaciones en 818 s** (axe con las dos densidades y las tres paletas, 320 a 1440 px y zoom al 200 %, teclado, cortina, hoja de teléfonos en una A4, reskin a Segura de León, `sede.tablon_url`…). El registro está en `../ayuntamiento-montemolin-bocetos/_verificar-final.log`. Las pruebas que dependen de los datos del pueblo se adaptaron en `scripts/verificar.mjs` (lugares de OSM y muestra del mapa, A–Z, tira de «Hoy» a 375×480) y en `css/imprimir.css` (hoja de teléfonos).
