# Centro Médico Galte Laime · Sistema de citas (HTML5 + CSS3, sin JavaScript)

Sitio construido a partir del **Card Sorting** y de los **mockups** de la tarea anterior, con el objetivo de cumplir **WCAG 2.2 nivel AA**.

## Cómo abrirlo
1. Descomprima la carpeta.
2. Abra `index.html` en cualquier navegador.

No necesita servidor ni instalación.

## Estructura
```
index.html          Inicio: hero + reserva rápida, datos clave, Atenciones, Antes de ir, Comunidad, Dónde estamos
pedir-turno.html    Paso 1 de 2: atención, día y hora (formulario GET → datos.html)
datos.html          Paso 2 de 2: nombre, cédula y celular (formulario → turno-listo.html)
turno-listo.html    Confirmación: ticket de turno (se imprime solo el ticket)
css/estilos.css     Un único archivo CSS organizado en @layer
fonts/              Atkinson Hyperlegible (texto) y Bricolage Grotesque (títulos), alojadas localmente
```

## Menú = categorías del Card Sorting
Pedir turno · Atenciones · Antes de ir · Comunidad · Dónde estamos

"Preguntas frecuentes" ya no es una sección: cada respuesta aparece donde surge la duda.

## Accesibilidad aplicada
| Requisito | Cómo se cumple |
|---|---|
| Semántica HTML5 | `header`, `nav` (menú principal y acciones rápidas), `main`, `section` con `aria-labelledby`, `article` (atenciones, eventos, video, ticket), `aside` (resumen), `footer`, `address`, `time`, `dl`, `fieldset` y `legend` |
| Objetivos táctiles ≥ 48 px | Variable `--tactil: 48px` en botones, enlaces, opciones, días, horas y campos (los campos miden 56 px) |
| Foco visible ≥ 3 px | `:focus-visible` con un anillo de 3 px más un halo de contraste en todos los `a`, `button` e `input`. Los campos de texto usan `:focus`. Sobre fondos verdes, el anillo pasa a blanco |
| Contraste ≥ 4,5:1 | Paleta verificada: texto 7,0:1 a 15,4:1; bordes de controles 4,4:1 |
| Tipografía legible | Base de 18 px, mínimo de 16 px y Atkinson Hyperlegible (diseñada para baja visión) |
| Teclado | Enlace "Saltar al contenido"; los radios son nativos (se eligen con las flechas) |
| Errores claros | `:user-invalid` muestra el mensaje solo después de interactuar; `pattern`, `inputmode` y `autocomplete` |
| Preferencias del usuario | `prefers-reduced-motion`, `forced-colors` (alto contraste de Windows) y `@media print` |

## CSS moderno usado (sin JavaScript)
- **`:has()`:** pinta las tarjetas seleccionadas y actualiza el resumen "Su turno" en vivo.
- **`:user-invalid` / `:user-valid`:** muestran los errores en el momento correcto.
- **Container queries, `clamp()`, propiedades lógicas, `text-wrap: balance` y `@layer`.**

## Verificación automática
- **axe-core 4.x** (WCAG 2.0/2.1/2.2 A y AA + buenas prácticas): **0 violaciones** en las 4 páginas, tanto a 360 px como a 1280 px.
- **html-validate** (perfil recomendado): **0 errores**. Se conserva `role="list"` a propósito, porque Safari/VoiceOver quita la semántica de lista cuando se usa `list-style: none`.
- **Medición propia:** 0 elementos interactivos de menos de 48 px de alto y 100 % de las paradas de tabulación con un contorno de 3 px o más.

## Limitaciones de un sitio sin JavaScript ni backend
- **Datos de ejemplo:** el resumen del paso 2 y el ticket muestran datos fijos. En producción, el servidor los rellena con lo que eligió la persona.
- **Envío por GET:** los formularios usan `method="get"` para que el prototipo funcione en un hosting estático. **En producción deben usar `method="post"`** hacia el backend, para que la cédula no viaje en la URL.
- **Horarios llenos fijos:** las horas "llenas" están escritas a mano. En producción deben venir de la agenda real del dispensario.
