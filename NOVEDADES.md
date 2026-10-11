# Novedades de la Suite CNC

La versión de la suite es **año.mes** (por ejemplo, 2026.10). Cada programa conserva además su propio número junto a su título.

## Suite CNC 2026.10 · actualización «Mecanizar»

Versiones: **Calcador v76 · Corrector v24 · Generador v81 (antiguo) · Simulador 3D V37 · Simulador del profesor V37**.

### Calcador y Corrector: ventana ⚙️ Mecanizar (G-code)
- El G-code de la máquina se genera dentro del Calcador, en mm reales, sin pasar por el Generador.
- Mismo motor que el Generador: cortes, grabados, cajeras con islas, puentes, pasadas en Z, desbaste y acabado, estrategia (plano, concordancia, oposición), G90/G91, G71/G70. Comprobado: produce el mismo programa que el Generador en 390 casos de prueba.
- Herramienta de la base compartida (T, F, S y paso se rellenan solos).
- Compensación **automática**: G41 o G42 en cada trazado según sea interior o exterior.
- Con G41/G42, cada contorno se mecaniza como en los ejemplos del Simulador: la fresa baja fuera del contorno (a Ø + 2 mm, por el lado de la fresa), activa la compensación en una recta de entrada perpendicular y la anula con **G40** en una recta de salida. El programa empieza y termina siempre en G40. (Antes la compensación se activaba en el G0 sobre el propio contorno y no se anulaba: en el Simulador el último trazado quedaba sin terminar).
- Si la entrada P1 es una esquina, con G41/G42 se entra por el centro de un lado (el contorno cortado es el mismo). La bajada de la fresa no toca ningún otro contorno de la pieza; si no hay sitio para la entrada, se avisa.
- Coordenadas **mixtas G90/G91**, como en la tabla de soluciones: G90 en la entrada y el cierre de cada contorno, G91 en el recorrido.
- Vista previa con la banda de la fresa y colores por profundidad, resumen (pasadas, longitud, tiempo) y avisos.
- Descargar .nc, copiar y «➜ Simulador» con un clic.
- Los ajustes de mecanizado se guardan en la sesión y en el JSON.
- Las ayudas emergentes de la profundidad (panel derecho, Mecanizado) hablan de la profundidad general de ⚙️ Mecanizar.

### Generador
- Marcado como **antiguo** en la portada. Se retirará cuando ⚙️ Mecanizar esté probado en la máquina.

### Simuladores
- **Corte más suave en 3D**: las paredes siguen el círculo de la fresa en lugar de ir en dientes de sierra, y el material tiene más resolución (400 puntos por lado). Con fresa plana, de bola y en V (en estas, el borde de arriba del corte y la parte vertical de la pared).
- El programa recibido conserva el nombre del archivo («… (mecanizado).nc»).

## Suite CNC 2026.10

Primera versión publicada. Versiones de los programas: **Calcador v73 · Corrector v21 · Generador v81 · Simulador 3D V34 · Simulador del profesor V34**.

### Calcador de contornos
- Dibujo y calco de piezas con cotas automáticas en cadena (sin números que se pisen), cotas manuales, tangencias (recta tangente y arco de radio R), corte y unión de contornos, cajeras con islas y puentes de sujeción.
- Entrada de coordenadas absolutas, incrementales, polares y en ISO (G1, G2 y G3 con I J o R).
- Ajuste de medidas con el centro de los arcos en la rejilla (I y J exactos).
- Hoja de ejercicio, tabla de soluciones (con el programa ISO y sus alturas de seguridad), variantes para examen y biblioteca de ejercicios con copia de seguridad.
- Corrección de programas, uno a uno o de toda la clase: geometría, seguridad (incluido el rápido sin subir la herramienta), lo pedido y la compensación de radio G40/G41/G42 según el tipo de cada trazado (interior o exterior).
- Simulación del programa del alumno bloque a bloque, con la trayectoria real de la fresa, y reproductor del programa de la pieza en la barra superior.
- «➜ Abrir en el Generador» y «➜ Abrir en el Simulador» con un clic.
- Aviso de cambios sin guardar en archivo.

### Corrector
- El Calcador sin herramientas de dibujo, solo para corregir, imprimir, exportar y enviar al Generador. Se genera a partir del Calcador.

### Generador de G-Code
- Cortes, grabados, cajeras y puentes; G-code con 3 decimales.
- **Desbaste y acabado**: las pasadas dejan un sobreespesor y una pasada final recorre el contorno exacto.

### Simulador 3D (alumnado y profesorado)
- Vista 3D y **vista 2D** en planta (arranca en 2D si el equipo no tiene 3D).
- **Plano del ejercicio**: abre el JSON del Calcador y colorea el recorrido del programa (autocorrección).
- Grosor del tablero para cortes no pasantes y vaciados.
- Compensación G41/G42 con las esquinas interiores bien resueltas; ejemplos de corte interior y exterior.
- Coordenadas polares (G16) y coma decimal interpretadas igual que en el Calcador.

### En toda la suite
- **Base de herramientas** compartida (T101…T999), con importación y exportación en JSON y CSV.
- Ventana «Créditos y licencias» en cada programa (EUPL-1.2 y licencias de terceros).

### Revisión de robustez
Pruebas de estrés con miles de programas, proyectos y archivos aleatorios, rotos y extremos en todos los programas. Corregido:
- **Simuladores**: un programa con coordenadas enormes (por ejemplo, un radio de un kilómetro por un cero de más) podía colgar el simulador al dibujar la cuadrícula; ahora la cuadrícula se adapta al tamaño de la escena. Mismo tope en la evaluación del plano.
- **Calcador y Corrector**: la corrección de un programa con un tramo de kilómetros podía tardar más de un minuto (ahora, milisegundos); al seleccionar el aviso de un arco imposible, o uno de «lo pedido», el dibujo de la corrección fallaba; un arco de radio nulo (I0 J0) con G41/G42 rompía la simulación.
- **Generador**: con desbaste y acabado, un trazado demasiado estrecho para el sobreespesor (por ejemplo, una media luna fina) generaba arcos imposibles; ahora se corta sin acabado y el G-code lo avisa. Mensaje más claro al abrir un archivo que no es un proyecto.

### Manuales y ayudas
- **Manual del Calcador** (82 páginas): el índice del PDF llevaba los dos últimos capítulos a la página 3; capturas al día (la pantalla con sus zonas, el Corrector y el reproductor); la barra superior descrita con la biblioteca, el reproductor y el aviso de cambios sin guardar; seis dudas nuevas en «Problemas frecuentes»; lo nuevo del Generador (base de herramientas, desbaste y acabado, 3 decimales); sin referencias a versiones antiguas.
- **Ayuda del Generador**: número de herramienta de tres cifras (T101), el desplegable «De la base», para qué sirve el radio de la herramienta y los 3 decimales del G-code.
- **Ayuda de los Simuladores**: el botón «📂 Cargar G-code / plano».
- **Guía del Simulador para el alumnado** (`guia_simulador.pdf`, 17 páginas): para qué sirve, la pantalla, cargar el programa, la simulación, 2D o 3D, la revisión y sus mensajes, la herramienta, el tablero, la compensación G41/G42, el plano del ejercicio (autocorrección), el vídeo para Aules, problemas frecuentes y una lista de comprobación antes de entregar. Enlazada desde la portada y desde la ayuda de los simuladores.
- **Simuladores**: la cabecera cabía mal en pantallas de menos de 1600 píxeles (desaparecían los ajustes ⚙️ y parte de la ayuda); ahora los botones se compactan y caben de 1024 a 1920 píxeles.
- **Manual del Corrector** (`manual_corrector.html` y `.pdf`, 16 páginas, para el profesorado): abrir un ejercicio, corregir un programa, qué se comprueba, la simulación, la corrección de toda la clase con la nota orientativa, demostrar los errores en clase, hojas, variantes y problemas frecuentes. El botón «📖 Manual» del Corrector abre ahora su propio manual.
- **Corrección masiva**: con la compensación del lado equivocado, el programa salía «no sale bien» pero con un 10; ahora los errores de compensación cuentan como cortes que dañan la pieza (el del lado, uno por cada corte afectado).

### Interfaz
- **Calcador**: si la pantalla es baja (portátil apaisado, pantalla táctil o zoom del navegador), la barra de herramientas se reparte sola en dos o más columnas y ya no queda cortada por abajo.
- **Calcador y Generador**: el panel izquierdo es un poco más ancho y el botón 🧰 de la base de herramientas se ve entero. En el Generador, el desplegable se llama «Base».
- **Calcador**: el botón «Guardar para el Generador (.json)» se llama ahora **«💾 Guardar (.json)»**: ese archivo lo abren todos los programas de la suite.
- **Generador**: el botón «EDITOR» (de un programa que ya no forma parte de la suite) es ahora **«➜ CALCADOR»**: devuelve el proyecto al Calcador si vino de él, o abre el Calcador con el proyecto del Generador.

### Compensación con fresas grandes
- **Calcador, Corrector y Simuladores**: con G41/G42 y una fresa más grande que un arco cóncavo o que un hueco de la pieza, el camino de la fresa formaba bucles que se metían en la pieza. Ahora esos bucles se quitan, como haría un CAM: la fresa pasa de largo y deja ese material sin cortar.
- **Corrección**: aviso en la línea del arco cóncavo donde la fresa no cabe («la máquina daría una alarma de interferencia o dejaría ese material sin cortar»), con el diámetro máximo que cabría. La revisión de los Simuladores ya lo marcaba como error.

