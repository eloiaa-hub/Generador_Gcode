# Herramientas de desarrollo de la Suite CNC

Esta carpeta no se usa en clase y no hace falta subirla a Aules. Sirve para mantener la suite sin perder trabajo.

## Construir el Corrector

El Corrector es el Calcador en modo visor. Después de cualquier cambio en `calcador.html`:

```
python3 construir_corrector.py ..
```

(el argumento es la carpeta de la suite). Para subir la versión del Corrector, cambia `VERSION_CORRECTOR` dentro del script.

## Fuentes de ⚙️ Mecanizar (`fuentes_mecanizar/`)

Copia de referencia de lo que se integró en el Calcador (v74 y v75). **El Calcador ya lo lleva dentro**: los cambios nuevos se hacen directamente en `calcador.html`.

- `motor_mecanizado.js`: motor de G-code (adaptación fiel del Generador v81 a mm reales).
- `adaptador_calcador.js`: convierte los contornos del Calcador en trazados para el motor.
- `mecanizar_ui.js`: ventana ⚙️ Mecanizar (campos, vista previa, descargar, simulador).
- `caj_bloque.js`, `offset_bloque.js`, `clipper_bloque.js`: cajeras, desbaste/acabado y Clipper 6.4.2 (licencia Boost), sacados del Generador.
- `integrar_mecanizar.py` + `calcador_v73_original.html`: rehacen el Calcador actual desde el v73 (la versión resultante está en `VERSION_CALCADOR`) (`cp calcador_v73_original.html ../../calcador.html && python3 integrar_mecanizar.py ../..`).

## Simuladores

`simulador3d.html` y `simulador3d_profesor.html` se editan directamente (no se generan). Comparten el intérprete ISO, la compensación G41/G42 y el material 3D: un cambio en uno se copia al otro.

## Pruebas automáticas (`pruebas/`)

Requieren Node.js y Playwright con Chromium. Variables opcionales: `SUITE` (carpeta de la suite, por defecto `../..`), `EJERCICIOS` (carpeta con JSON de ejercicios) y `CHROME` (ruta del navegador).

| Prueba | Qué comprueba |
|---|---|
| `arranque.js` | Todos los programas abren sin errores y muestran su versión |
| `regresion_basica.js` | Todos los ejercicios abren y se corrigen en Calcador y Corrector |
| `motor_vs_generador.js` | El motor de Mecanizar da el mismo G-code que el Generador (`referencia_generador.json`, 390 casos). Desde el Calcador v75 los 65 casos con G41/G42 (`comp_oposic`) salen distintos a propósito: entrada y salida de la compensación |
| `referencia_generador.js` | Regenera esa referencia con el Generador |
| `comp_simulador.js` | Programas con G41/G42 en el Simulador (`SIM=simulador3d_profesor.html` para el del profesor): la trayectoria compensada corta todo el contorno sin meterse en la pieza (con `Prueba01.json`) |
| `corpus_comp.js` | `comp_simulador.js` sobre todos los ejercicios (quedan avisos esperables: detalles más pequeños que la fresa y huecos que se solapan) |
| `mecanizar_ui.js` | La ventana ⚙️ Mecanizar: herramienta, opciones, guardado, descarga y simulador |
| `interp_corpus.js`, `interp_cmp.js` | Intérprete ISO de los simuladores frente al corpus de programas |
| `estres_mecanizar.js`, `perfil_*.js`, `mec_vista.js` | Casos extremos y medidas de tiempo |

Ejemplo: `cd pruebas && node arranque.js`
