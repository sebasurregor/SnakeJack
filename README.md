# Snake en Jack — Nand2Tetris

Videojuego retro **Snake (la culebrita)** desarrollado en el lenguaje **Jack** para la plataforma Hack de Nand2Tetris.
Entrega del **Tercer Parcial (Hito 1)** con opción de **entrega anticipada**: la versión incluida ya es el juego 100 % finalizado (Hito 2).

Curso: Organización de Computadores — Universidad EAFIT
Autor: **Sebastián Urrego Ramírez**

---

## 1. Reglas del juego

| Regla | Comportamiento |
|---|---|
| Movimiento | La culebrita avanza sola una casilla por cuadro; las flechas cambian su dirección. |
| Giro de 180° | Prohibido: si va a la derecha no puede girar directo a la izquierda. |
| Comida | Aparece en una casilla aleatoria libre. Al comerla crece 1 segmento y suma **+10 puntos**. |
| **Longitud máxima = 20** | Al llegar a 20 segmentos el jugador **GANA**. |
| **Las paredes matan** | Si la cabeza sale del tablero es **Game Over** (no hay teletransporte). |
| Autochoque | Chocar con el propio cuerpo también es Game Over. |
| Velocidad | Aumenta ligeramente a medida que la culebrita crece. |

## 2. Controles

| Tecla | Acción |
|---|---|
| `ESPACIO` | Iniciar partida (pantalla de inicio) |
| `↑ ↓ ← →` | Mover la culebrita |
| `R` | Reiniciar (en Game Over o Victoria) |
| `ESC` | Salir del juego (en cualquier momento) |

## 3. Compilar y ejecutar

**Con la suite de escritorio (JackCompiler + VMEmulator):**

```bash
# Desde la carpeta nand2tetris/tools
JackCompiler.bat  ruta/a/SnakeJack        # Windows
sh JackCompiler.sh ruta/a/SnakeJack       # macOS / Linux
```

1. Abrir `VMEmulator` y elegir **File → Load Program** sobre la carpeta `SnakeJack` (la carpeta completa, no un solo archivo).
2. En *Animate* elegir **No animation** y subir el control de velocidad al máximo.
3. Presionar **Run** (▶▶) y hacer clic sobre la pantalla del emulador para que reciba el teclado.

**Con el IDE web oficial (nand2tetris.org):** abrir el *Jack Compiler*, cargar la carpeta y compilar; después abrir el *VM Emulator*, cargar la misma carpeta y ejecutar.

> Los archivos `.vm` ya vienen compilados dentro de la carpeta, por lo que se puede ejecutar directamente en el VM Emulator.

## 4. Estructura del proyecto

```
SnakeJack/
├── Main.jack        Punto de entrada: ciclo crear partida → jugar → dispose()
├── SnakeGame.jack   Game loop, estados (inicio, jugando, game over, victoria), colisiones
├── Board.jack       Cuadrícula 60 × 28, paredes y conversión casilla → píxel
├── Snake.jack       Cuerpo (arreglos de 20), movimiento, giros y autochoque
├── Food.jack        Comida: dibujo y reubicación aleatoria
├── Hud.jack         Puntaje, longitud y pantallas de texto
├── Random.jack      Generador pseudoaleatorio (congruencial lineal)
├── *.vm             Archivos compilados
└── README.md
```

## 5. Decisiones técnicas importantes

- **Cuadrícula lógica:** el juego trabaja en casillas de 8 × 8 px; solo `Board` convierte a píxeles.
- **Redibujo mínimo:** en cada cuadro se redibujan solo 3 casillas (cola, cuello y cabeza), lo que evita el parpadeo.
- **Memoria sin fugas:** cada objeto tiene `dispose()`; `Snake` libera sus dos arreglos antes de sí misma; los textos se crean una sola vez (`Hud.init`) porque en Jack cada literal de texto crea un `String` nuevo.
- **Sin recursión:** todos los recorridos son ciclos `while`, por lo que la pila no crece durante el juego.

## 6. Enlaces

- Repositorio: `https://github.com/<usuario>/SnakeJack` *(reemplazar)*
- Video de sustentación: `https://youtu.be/M-IByA579k4` *(reemplazar)*

## 7. Créditos

Desarrollado por **Sebastián Urrego Ramírez** para Organización de Computadores (EAFIT).
Plataforma, lenguaje Jack y sistema operativo: Nisan & Schocken, *The Elements of Computing Systems*, 2.ª ed., MIT Press, 2021.
Se usó asistencia de inteligencia artificial (Claude) durante el desarrollo, tal como lo permite el enunciado.
