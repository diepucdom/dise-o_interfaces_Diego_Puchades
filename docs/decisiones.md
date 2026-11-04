# Documento de decisiones de diseño

> Cada decisión: **qué** elegiste, **por qué**, y **qué alternativa descartaste**.
> Se evalúa la justificación, no la longitud. Máximo 2 páginas en la Fase 1.

## Ruta de trabajo

- [ ] Ruta A · Figma (enlace con permiso de lectura: …)
- [x] Ruta B · VS Code (diseño directamente en `guia.html`)

## 1. Color (RA1 · CE b)

- **Tono de acento de la ficha y cómo has obtenido la escala (50 … 950):**  
  Se ha seleccionado el tono corporativo $H = 22^\circ$ (Rojo cálido Los Pinos) bajo el espacio de color OKLCH. La escala se genera fijando el matiz ($H=22$) y ajustando la luminosidad ($L$) desde un 97% (`50`) hasta un 15% (`950`), asegurando una progresión perceptualmente uniforme.  
  *Alternativa descartada:* Utilizar valores RGB/HEX aleatorios sin base matemática en OKLCH, lo que rompería la consistencia cromática entre tonos claros y oscuros.

- **Por qué el acento de texto/fondo es el 700 en claro y el 400 en oscuro (o el que elijas):**  
  En tema claro se emplea `acento-700` (`#b82613`) sobre fondo blanco para garantizar una relación de contraste óptima segun normativa. En tema oscuro se utiliza un tono más claro (`acento-300`/`acento-400`) para que destaque correctamente sin perder legibilidad.

- **Tokens semánticos añadidos y para qué:**  
  Se han añadido `--color-superficie`, `--color-superficie-elevada`, `--color-texto`, `--color-texto-atenuado`, `--color-acento`, `--color-acento-tenue`, `--color-borde`, `--color-borde-control`, `--color-exito` y `--color-error`. Su propósito es abstraer los valores cromáticos y permitir la adaptación dinámica automática con la función nativa `light-dark()`.  
  *Alternativa descartada:* Escribir códigos de color fijos directamente en los selectores CSS de los componentes.

- **Pares de contraste añadidos a `$pares-contraste`:**  
  Se han añadido los pares: `--color-texto` con `--color-superficie`, `--color-acento` con `--color-superficie`, `--color-exito` con `--color-superficie`, y `--color-error` con `--color-superficie`.  
  *Por qué:* Permiten que el compilador de Sass compruebe automáticamente que las combinaciones críticas cumplen con el contraste mínimo legal.

## 2. Tipografía (RA1 · CE b)

- **Familia elegida y por qué (rendimiento, legibilidad, licencia):**  
  Se ha optado por una pila tipográfica nativa del sistema (`system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif`).  
  *Por qué:* Ofrece un rendimiento de carga sin latencia de red, se integra perfectamente con las convenciones visuales del sistema operativo del usuario y no tiene restricciones de licencia.

- **Base y razón en móvil y escritorio. Por qué esas:**  
  En móvil se establece una base de `1rem` ($16\text{ px}$) con una razón modular de $1.125$ (Second Major), optimizando el espacio en pantallas reducidas. En escritorio la base asciende a `1.125rem` ($18\text{ px}$) con una razón de $1.25$ (Third Major), mejorando la jerarquía visual a mayor distancia de lectura.  
  *Alternativa descartada:* Utilizar tamaños fijos en píxeles que ignoren las preferencias de accesibilidad y zoom del navegador.

- **Medida de línea (`max-inline-size` del párrafo en `ch`):**  
  Se ha limitado estrictamente a `65ch` en los bloques de texto continuo.  
  *Por qué:* El ancho ideal de lectura humana se sitúa entre 45 y 75 caracteres por línea; superar este límite dificulta el seguimiento visual del renglón.  
  *Alternativa descartada:* Permitir que los párrafos se expandan de lado a lado en pantallas ultrapanorámicas.

## 3. Espaciado y forma

- **Escala de espaciado y radios. Si cambias algo respecto a la plantilla, por qué:**  
  Se mantiene la escala modular basada en variables relativas (`--espacio-xs` a `--espacio-l`) y radios geométricos (`--radio-s: 4px`, `--radio-m: 8px`).  
  *Por qué:* Asegura una retícula consistente y garantiza que todos los elementos interactivos cumplan con el área de contacto táctil mínima de $44 \times 44\text{ px}$ (WCAG 2.5.5).  
  *Alternativa descartada:* Definir medidas arbitrarias a ojo en cada componente, rompiendo la armonía visual del sistema.

## 4. Componentes (RA1 · CE f)

| Componente | Estados | Cómo se resuelve cada estado en CSS |
| --- | --- | --- |
| **Botón** | normal, hover, foco, desactivado, secundario | `.btn` estructurado con variables de color. `:hover` ajusta la opacidad/sombra. `:focus-visible` aplica un contorno accesible (`outline: 2px solid var(--color-acento)`). `:disabled` reduce la opacidad al 50% y desactiva el cursor (`cursor: not-allowed`). Las variantes secundarias invierten los fondos y bordes mediante modificadores BEM. |
| **Turno** | disponible, seleccionado, ocupado, foco | `.turno` estructurado en contenedor flexible. `:has(.turno__input:checked)` eleva el grosor del borde a 3px y aplica un fondo tenue (`--color-acento-tenue`). `:has(.turno__input:disabled)` estiliza con borde discontinuo (`border-style: dashed`) y opacidad atenuada. `:has(.turno__input:focus-visible)` genera el anillo de enfoque del teclado. |
| **Contador de invitados** | normal, seleccionado, foco | `.invitados__opcion` como bloque de selección. `:has(input:checked)` invierte los tokens de color (`background: var(--color-acento); color: var(--color-superficie)`). `:has(input:focus-visible)` resalta el perímetro con el color de acento. |
| **Aviso de pago** | normal / destacado | `.aviso` contenedor con borde resaltado de grosor 2px y fondo semántico atenuado. El campo de concepto interno utiliza tipografía monoespaciada con superficie elevada diferenciada. |

## 5. Comparativa de tecnologías (RA1 · CE e · RA2 · CE i)

| Criterio | Figma | Penpot | Diseño en código |
| --- | --- | --- | --- |
| **Coste / licencia** | Privativo (modelo freemium de suscripción por usuario). | Código abierto (Open Source), totalmente gratuito. | Gratuito, integrado directamente en el flujo de desarrollo del módulo. |
| **Traslado a código (handoff)** | Requiere interpretación manual de inspectores de estilos y plugins. | Similar a Figma, requiere inspección de propiedades CSS o plugins. | Inmediato y directo; el código redactado es la interfaz final sin intermediarios. |
| **Mantenimiento del sistema** | Mediante librerías de componentes centralizadas en la nube. | Mediante componentes y librerías colaborativas en la plataforma. | Centralizado mediante clases BEM y variables de diseño en Sass. |

| Criterio | Sass + CSS propio | CSS nativo sin preprocesador | Bootstrap / Tailwind |
| --- | --- | --- | --- |
| **Tokens y temas** | Excelente: uso de mapas Sass avanzados, bucles y funciones `light-dark()`. | Moderado: limitado al soporte nativo de variables y funciones de color modernas. | Complejo: requiere sobreescritura profunda de configuraciones o capas de utilidad. |
| **Peso del CSS final** | Mínimo y altamente optimizado al compilar exclusivamente lo necesario. | Mínimo absoluto al no requerir ningún paso de compilación previa. | Elevado (salvo en Tailwind con purgado estricto) debido al volumen de clases utilitarias. |
| **Control de la cascada** | Absoluto y estructurado mediante directivas `@layer` y nomenclatura BEM. | Absoluto, pero recae totalmente en la disciplina manual del desarrollador. | Bajo/Medio: propenso a una alta especificidad o abuso de reglas `!important`. |

**Decisión y motivo:**  
Se ha seleccionado **Diseño en código con Sass + CSS propio** porque proporciona un control muy certero sobre la arquitectura CSS, facilita la validación de contrastes de color en tiempo de compilación mediante mapas semánticos y evita la sobrecarga innecesaria de frameworks de terceros pesados, cumpliendo de sobra con los requisitos técnicos exigidos en el ciclo formativo de 2.º DAW.