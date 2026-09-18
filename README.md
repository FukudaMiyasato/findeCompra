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
- El total siempre es coherente: `(190 × cantidad + Σ complementos activos (−10 %)) × (1 − % premio)`.

## Complementos: distancia y horario

Cada complemento muestra su **distancia al evento principal** (valores de ejemplo, todos a menos de 1 km: 300–900 m; complementos: Bembos, Pizza Hut, Popeyes,
Museo contemporáneo, Playland Park y Teatro)
y **hasta cuándo o en qué horario reclamarlo**. Ambos datos también salen en su boleto:

| Complemento | Reclamar |
|---|---|
| Bembos, Pizza Hut, Popeyes (comida) | hasta 15 de dic |
| Museo contemporáneo | de 1 pm a 6 pm |
| Playland Park | hasta 15 de dic |
| Teatro | de 6 am a 8 am |

**Teatro** es el complemento *Recomendado*: borde dorado redondeado, un descuento extra
(~~S/ 30~~ → ~~S/ 27~~ → **S/ 25** en dorado, que es lo que se cobra), etiquetas *Recomendado* (amarilla) y *Merlin* junto a *Experiencia*, y el
personaje recomendador (`assets/recomendador.webp`) por encima de su foto, anclado a la esquina
inferior izquierda y recortado por el borde de la tarjeta, para que se vea apoyado y no flotando.

En la cabecera de *Completa tu experiencia* hay un botón de radio (**3 km** por defecto) que
abre un menú para elegir 1, 3, 5 o 10 km. Por ahora es solo visual: no filtra nada.

## Mapa de ruta del plan

Debajo de los complementos hay un mapa (Leaflet + OpenStreetMap). Cada vez que se activa o
desactiva un complemento se recalcula y dibuja con animación la **Mejor ruta generada**
desde el Circo (Jockey Plaza) pasando por los complementos activos: prueba todos los
órdenes posibles y elige el de menor distancia. Muestra paradas, distancia por tramo y tiempo estimado a pie.

- **Editar**: permite reordenar las paradas (↑ ↓); el título cambia a *Ruta personalizada*.
- **Compartir plan**: WhatsApp, Copiar (portapapeles) y Más (menú de compartir del sistema).

Las ubicaciones de los complementos son de ejemplo (distancia + rumbo desde el evento).

## Premios por cantidad de ítems

El conteo incluye las entradas de El Circo (hasta 10). La barra empieza con un círculo
inicial y termina en el último premio (7 ítems); solo muestra la cantidad de ítems (3, 5, 7).
El porcentaje ganado se ve en naranja sobre la silueta de un ticket. El premio es un descuento sobre el
total y se suma al *Ahorro aplicado*.

| Ítems | Premio |
|---|---|
| < 3 | Sin premio |
| 3 | 1 % de descuento en el total |
| 5 | 2 % de descuento en el total |
| 7 | 3 % de descuento en el total |

La sección de premios vive en la barra fija inferior del paquete: se muestra al hacer
scroll hacia abajo y se minimiza a una rayita al hacer scroll hacia arriba
(p. ej. *Premio ganado (falta 1 ítem para el siguiente premio)*); tocarla la vuelve a abrir.
Al ganar un premio sale confeti y suena una fanfarria.

## Uso

Abrir `index.html` en el navegador. Sin dependencias ni build.
