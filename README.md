# findeCompra · Prototipo iOS

Prototipo web (mobile first, estilo iOS) de cuatro pantallas:

1. **Detalle de experiencia** — Circo American: imagen del circo (`assets/american-circus.webp`)
   al 40 % del alto de pantalla con recorte centrado,
   datos, mapa de Google Maps del Jockey Plaza (al tocarlo abre la ruta desde tu ubicación actual),
   precio, botón *Comprar*, combo recomendado y barra de costo fija.
2. **Crea tu paquete** — se abre como *sheet* al presionar *Comprar* (con todos los complementos
   desactivados) o *Crear Paquete* del combo (con Bembos activado).
3. **Pago** — pantalla naranja "Completando pago con tarjeta guardada" con carga y confirmación.
4. **App tufinde** — cabecera con el logo (`assets/tufinde-logo.png`) y menú inferior con dos pestañas:
   - **Boletos**: pases estilo Apple Wallet que aparecen animados, uno por ítem comprado
     (más el premio ganado). Tocar un pase lo trae al frente; *Listo* reinicia el flujo.
   - **Explorar**: listado de experiencias familiares con filtro por categoría
     (Todo, Shows, Aire libre, Museos, Talleres). *Circo American* vuelve al detalle.

## Lógica de complementos

- Cada complemento tiene **10 % de descuento** al comprarse dentro del paquete.
- Al activar un switch se recalculan **con animación**: cantidad de ítems,
  ahorro aplicado (un solo valor) y total a pagar.
- Cada ítem agregado suena un "cling" de ahorro (Web Audio, sin archivos).
- El total siempre es coherente: `190 × cantidad + Σ complementos activos (−10 %)`.

## Premios por cantidad de ítems

El conteo incluye la experiencia base (El Circo).

| Ítems | Premio |
|---|---|
| < 2 | *No tienes premios, agrega más ítems para conseguir premios* |
| 2 | 🍟 Papas fritas |
| 3 | 🍟🥤 Papas fritas + gaseosa |
| 5 | 🍗 Pieza de pollo |

La sección de premios vive en la barra fija inferior del paquete: se muestra al hacer
scroll hacia abajo y se minimiza a una rayita al hacer scroll hacia arriba
(p. ej. *Premio ganado (falta 1 ítem para el siguiente premio)*); tocarla la vuelve a abrir.
Al ganar un premio sale confeti y suena una fanfarria.

## Uso

Abrir `index.html` en el navegador. Sin dependencias ni build.
