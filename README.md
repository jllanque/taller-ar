# Tarjetas geométricas en realidad aumentada

Taller de laboratorio de **ETN 1024 – Tecnologías de Telecomunicaciones**
Carrera de Ingeniería Electrónica, Universidad Mayor de San Andrés (UMSA).

Aplicación web de realidad aumentada que usa la cámara trasera del teléfono para
reconocer dos tarjetas impresas y dibujar una figura 3D sobre cada una.

| Tarjeta | Marcador | Figura virtual |
| ------- | -------- | -------------- |
| A       | Hiro     | Cubo azul      |
| B       | Kanji    | Esfera roja    |

Un botón **Cambiar tamaño** alterna las figuras entre escala normal (1,0) y
ampliada (1,5), con una etiqueta que indica el estado actual ("Normal" o "Ampliado").

## Demostración

Enlace de la aplicación (HTTPS):
`https://jllanque.github.io/taller-ar/`

## Cómo usarla

1. Imprime las dos tarjetas (ver sección _Tarjetas_).
2. Abre el enlace **directamente en el navegador del teléfono** (por ejemplo Chrome),
   no dentro de una app de mensajería.
3. Acepta el permiso de cámara.
4. Enfoca una tarjeta a unos 30–60 cm, con buena luz y con el marcador completo a la vista.
5. Pulsa **Cambiar tamaño** para alternar entre Normal y Ampliado.

## Tarjetas

Se usan dos marcadores predefinidos de AR.js; no se inventó ni modificó ningún patrón.

- Hiro: `data/images/hiro.png` en el repositorio oficial AR-js-org/AR.js.
- Kanji: `three.js/examples/marker-training/examples/pattern-images/pattern-kanji.png`
  en el mismo repositorio.

Recomendaciones de impresión: tamaño real (6 × 6 cm), blanco y negro, dejando al
menos 1 cm de margen blanco alrededor del borde negro. Pegar sobre cartulina plana,
sin pliegues, brillo ni cinta sobre el patrón.

## Estructura del proyecto

```
taller-ar/
├── index.html   # Aplicación completa (HTML + JavaScript)
├── README.md    # Este documento
├── LICENSE      # Licencia MIT
└── .gitignore
```

## Cómo funciona

- **AR.js** detecta el patrón impreso en cada fotograma y calcula su posición y orientación.
- **A-Frame** crea y dibuja las figuras 3D (`a-box` y `a-sphere`).
- La relación marcador–figura se define en el código con `<a-marker preset="hiro">`
  (contiene el cubo) y `<a-marker preset="kanji">` (contiene la esfera). Al ser
  elementos hijos del marcador, las figuras reciben su transformación espacial.
- Cuando se pierde la detección de una tarjeta, su figura deja de mostrarse; al volver
  a detectarla, reaparece sin recargar la página.
- El botón cambia el atributo `scale` de los contenedores de ambas figuras
  (un solo estado compartido) y actualiza la etiqueta de texto.

### Dónde modificar

| Qué                            | Dónde en `index.html`                         |
| ------------------------------ | --------------------------------------------- |
| Color del cubo o la esfera     | atributo `color` de `a-box` / `a-sphere`      |
| Figura asociada a cada tarjeta | elemento hijo de cada `a-marker`              |
| Escala ampliada                | constante `s` en el manejador del botón (1,5) |
| Nombre mostrado en pantalla    | `<div id="nombre">`                           |

## Tecnologías y versiones

- A-Frame 1.3.0
- AR.js 3.4.5 (seguimiento de marcadores para A-Frame)
- HTML y JavaScript, sin proceso de compilación
- Alojamiento: GitHub Pages (HTTPS)

Las bibliotecas se cargan desde CDN, por lo que se necesita conexión a internet.

## Pruebas realizadas

Completar con tus resultados reales:

- [ ] Permiso de cámara y cámara trasera activa
- [ ] Hiro muestra cubo azul
- [ ] Kanji muestra esfera roja
- [ ] La figura sigue a la tarjeta al moverla y girarla
- [ ] La figura desaparece al retirar la tarjeta y reaparece sin recargar
- [ ] El botón alterna Normal → Ampliado → Normal con etiqueta coherente
- [ ] Probado más cerca, más lejos y con la tarjeta inclinada

## Limitaciones

- Se evalúa una tarjeta a la vez.
- No se garantiza el funcionamiento con poca luz, reflejos intensos o con el marcador casi de canto.
- La escala es relativa; no representa una medida física en centímetros.
- Compatibilidad dependiente del teléfono, el navegador y WebGL.

## Fuentes y ayudas

- Documentación de AR.js (marcadores): https://ar-js-org.github.io/AR.js-Docs/marker-based/
- Documentación de AR.js: https://ar-js-org.github.io/AR.js-Docs/
- MDN, `getUserMedia`: https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia
- Ejemplos oficiales de AR.js y A-Frame, adaptados para este taller.
- Se utilizó un asistente de IA (Claude, de Anthropic) como ayuda para estructurar el
  código base y la documentación; el código fue revisado y probado por el autor.

## Licencia

Distribuido bajo licencia MIT. Ver el archivo [LICENSE](LICENSE).
A-Frame y AR.js son proyectos independientes con sus propias licencias.
