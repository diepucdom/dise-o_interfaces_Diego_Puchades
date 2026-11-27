## A1
1. En tokens: $tipo-pasos: (-1, 0, 1, 2, 3, 4, 5), el paso 0 es el texto plano base, los positivos son títulos y los negativos, el -1, se trata de tamaños inferiores.
El rem es necesario dentro de clamp para darle tamaño relativo a los elementos sin influir directamente en el tamaño cuantificable en px, sirve para generalizar tamaños ej: xs, s...
2. El color:var(color-acento) se usa para asignar a color el valor del color-acento se usa la forma semántica para generalizar en todo el proyecto el acento corporativo.
## A2
En otros proyectos utilizaria otras tecnologias de diseño como puedan ser tailwind o bootstrap ya que me facilitaria mucho la labor de crear estructuras automatizando tareas que antes demoraban mucho más en ser culminadas en las empresas como formularios nuevos, logins, páginas con flex interactivas...
## A3
1.color-acento pasa por decisiones.md, _elementos.scss hasta llegar al primer componente en orden natural que sería _aviso.scss
2. El motivo de usar forward e input yace tras de la filosofia de ir compilando en cascada, además de que en el proyecto nos encontramos que hay elementos que habitan en la web directamente y hay que hacer implementaciones que hagan que no tenga que recompilarse todo al hacer refrescos de página o al actualizar módulos independientes.
3. Es falso, si bien es cierto que la compilacion con forward en cascada hace más fácil la tarea de no tener que actualizar todos los modulos de la página no se puede negar el hecho de que el navegador compila el Sass, que sí que habita en el navegador, es decir está ahí pero si que lo compila (interpreta)
## A4
1. A incidencias.html se llegará desde index.html a través de un enlace en el footer.
2. Se vuelve atrás de incidencias  sin usar las flechas del navegador con el pie, en un enlace incrustado que redirige al inicio (desde dónde se accede a la página de incidencias).
3. Turnos · index.html -> Incidencias · incidecias.html
4. Creo que debería estar en las páginas más representativas de la aplicación web por lo que es una buena idea tenerlo en el menú principal donde se puede llegar de forma intuitiva.