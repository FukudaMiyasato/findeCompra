# findeCompra · Prototipo iOS

Prototipo web (mobile first, estilo iOS) de dos pantallas:

1. **Detalle de experiencia** — Circo American: hero, datos, mapa de ruta, precio,
   botones *Comprar* / *Crear Paquete*, combo recomendado y barra de costo fija.
2. **Crea tu paquete** — se abre como *sheet* al presionar *Comprar* o *Crear Paquete*.

## Lógica de complementos

- Cada complemento tiene **10 % de descuento** al comprarse dentro del paquete.
- Al activar un switch se recalculan **con animación**: cantidad de ítems,
  ahorro aplicado y total a pagar.
- El total siempre es coherente: `190 × cantidad + Σ complementos activos (−10 %)`.

## Premios por cantidad de ítems

El conteo incluye la experiencia base (El Circo).

| Ítems | Premio |
|---|---|
| < 2 | *No tienes premios, agrega más ítems para conseguir premios* |
| 2 | 🍟 Papas fritas |
| 3 | 🍟🥤 Papas fritas + gaseosa |
| 5 | 🍗 Pieza de pollo |

La barra de progreso se llena hasta el hito alcanzado y el nodo correspondiente
se activa con animación.

## Uso

Abrir `index.html` en el navegador. Sin dependencias ni build.
