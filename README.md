# Simulador de un receptor digital de rayos X

[![Licencia: CC BY-NC-SA 4.0](https://img.shields.io/badge/Licencia-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es)

Web interactiva para entender cómo un receptor digital transforma los fotones de rayos X que recibe en información numérica y en una imagen visible, y cómo se procesa después esa imagen.

**CFGS Imagen para el diagnóstico y medicina nuclear** · Módulo 1346 - Fundamentos físicos y equipos

🔗 **Acceso a la web:** `https://sendroski22.github.io/<repositorio>/`

---

## ¿Para qué sirve?

En radiología digital, el receptor no «se ennegrece» como una película: registra un valor numérico en cada píxel. Con este simulador el alumnado construye una imagen píxel a píxel, ve el mismo dato en decimal, en binario y en escala de grises, y comprueba que el procesado cambia cómo se ve la imagen, pero no los datos registrados. Sirve para trabajar conceptos como matriz, píxel, profundidad de bits, imagen primaria, imagen final y ventaneo.

## Relación curricular

| | |
|---|---|
| **Ciclo** | CFGS Imagen para el diagnóstico y medicina nuclear |
| **Módulo** | 1346 - Fundamentos físicos y equipos |
| **Resultado de aprendizaje** | RA3. Procesa y trata imágenes radiográficas, describiendo las características de los receptores y sus aplicaciones. |
| **Criterio(s) de evaluación** | 3.e) Se ha descrito el procedimiento de captura de imagen en formato digital directo o indirecto.<br>3.f) Se ha procesado la imagen primaria digital para obtener una imagen final de calidad. |

## Contenido

El receptor tiene **10 × 10 píxeles** y **2 bits por píxel**, es decir, 4 valores posibles:

| Valor | Binario | Se ve | Significado |
|---|---|---|---|
| 0 | `00` | Blanco | Casi no llega radiación (hueso u objeto muy denso) |
| 1 | `01` | Gris claro | Llega poca radiación |
| 2 | `10` | Gris oscuro | Llega bastante radiación |
| 3 | `11` | Negro | Llega mucha radiación (aire, radiación directa) |

1. **Ejercicios:** hay cuatro. En cada uno se da una tabla con el valor de cada píxel («Datos del receptor»). El alumnado la reproduce clic a clic en la matriz: cada clic suma 1 y, después del 3, el píxel vuelve a 0. Al completarla aparece una figura sencilla.
2. **Comprobar:** marca en rojo los píxeles incorrectos. Si todo está bien, muestra el nombre de la figura y una breve explicación relacionada con la atenuación.
3. **Vistas del receptor:** el botón «Ver números» alterna entre colores, números y bits. En la vista de bits también pasan a binario la tabla de datos y la leyenda.
4. **Procesado de la imagen (ventaneo):** se desbloquea al comprobar la imagen. Los controles de **brillo** (nivel de ventana) y **contraste** (anchura de ventana) cambian cómo se ven los grises sin modificar los datos. Si se modifica un píxel, la imagen deja de estar comprobada y el procesado se desactiva. Al volver a comprobarla, se recuperan los ajustes que había.
5. **Apartados teóricos:** instrucciones; características de la imagen digital (resolución espacial y profundidad de bits); procesado de la imagen. Incluyen preguntas para el alumnado y una de ellas tiene respuesta desplegable.

### Modo profesor

Para mostrar la solución en clase sin tener que hacer todos los clics:

- Pulsa **5 veces seguidas** el botón **«Comprobar»**, con menos de 1 segundo entre un clic y el siguiente. La matriz muestra la solución y aparece el botón **«Volver a estado anterior»**.
- **«Volver a estado anterior»** devuelve la matriz tal como estaba justo antes de mostrar la solución, y después desaparece.
- Si se repite el gesto mientras se ve la solución, se guarda como «estado anterior» lo que haya en ese momento.
- Cada ejercicio guarda su propio estado anterior. «Reiniciar» lo borra.

Los cuatro primeros clics hacen una comprobación normal, así que durante un momento puede aparecer el mensaje de píxeles incorrectos.

## Uso

- **En línea:** abre el enlace de GitHub Pages.
- **Sin conexión:** descarga `index.html` y ábrelo con cualquier navegador. Funciona en ordenador, tablet y móvil. Sin conexión se ven las fuentes del sistema en lugar de las tipográficas de la web, pero todo funciona igual.

### Publicar en GitHub Pages

1. Sube `index.html` a la raíz del repositorio.
2. Ve a **Settings → Pages**.
3. En *Source*, elige **Deploy from a branch**, rama `main` y carpeta `/ (root)`.
4. Guarda: en uno o dos minutos la web estará disponible en `https://<usuario>.github.io/<repositorio>/`.

## Estructura del repositorio

```
├── index.html   # La web completa (HTML, CSS y JavaScript en un solo archivo)
├── README.md
└── LICENSE
```

No necesita instalación, ni dependencias, ni servidor.

## Personalización

Todo está al principio del bloque `<script>` de `index.html`:

- **`EXERCISES`:** los cuatro ejercicios. Cada uno tiene un nombre (`name`), la explicación que aparece al resolverlo (`note`) y la matriz (`data`), escrita como 10 filas de 10 dígitos entre 0 y 3. Se pueden cambiar las figuras o añadir ejercicios nuevos; el tamaño de la matriz se calcula a partir del número de filas, así que todos los ejercicios deben tener el mismo tamaño y ser cuadrados.
- **`SECRET_CLICKS`** y **`SECRET_WINDOW_MS`:** número de clics y tiempo máximo entre clics del modo profesor.
- **`WL_DEFAULT`:** valores iniciales de brillo y contraste.

## Modelo y limitaciones

**Es un modelo simplificado y de carácter didáctico.** Principales simplificaciones:

- **Matriz y profundidad de bits:** 10 × 10 píxeles y 2 bits por píxel, muy por debajo de los equipos reales (matrices de 2048 × 2048 píxeles o más y entre 12 y 16 bits por píxel).
- **Clics y fotones:** un clic no representa un solo fotón, sino una cantidad de radiación formada por muchísimos fotones.
- **Saturación:** en un receptor real, un píxel que recibe más radiación no vuelve a 0, sino que se satura en el valor máximo. En el simulador vuelve a 0 solo para poder corregir errores.
- **Convenio de visualización:** más señal se muestra más oscura, imitando el aspecto de la película radiográfica.
- **Figuras:** son siluetas esquemáticas pensadas para que se reconozcan con 10 × 10 píxeles, no representaciones anatómicas exactas.
- **Captura:** no se distingue entre captura directa e indirecta, y no se modelan el ruido ni la radiación dispersa.
- **Procesado:** solo se incluye el ventaneo, con una conversión lineal de valores a grises dentro de la ventana. Los valores por debajo de la ventana se ven blancos y los de encima, negros.

## Autoría y licencia

“Web interactiva Simulador de un receptor digital de rayos X” por **Pablo A. Sendra Lleó** (2026), disponible bajo licencia [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/deed.es).

Puedes compartir y adaptar este material siempre que cites la autoría, no lo uses con fines comerciales y compartas las obras derivadas con la misma licencia. El texto legal completo está en el archivo [`LICENSE`](LICENSE).

Este material fue desarrollado con la asistencia del modelo de inteligencia artificial [Claude (Anthropic)](https://claude.ai/).
