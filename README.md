# 👾 Taller 5: Enemigo Patrullero Inteligente y Prefabs

Proyecto de Unity 6 (2D) donde se crea un enemigo que patrulla de forma autónoma usando sensores de física (`RaycastHit2D`). Detecta bordes y paredes, y se voltea solo. El enemigo se convirtió en un Prefab y se colocaron 4 copias en distintas plataformas del mapa.

## 🎯 Objetivo

Demostrar el dominio de:
- Sensores de física 2D con `Physics2D.Raycast`.
- Detección automática de bordes y paredes.
- Reutilización de elementos mediante Prefabs.

## 🎬 Video de demostración

El video `videoCreacionEnemigo` está en la raíz de este repositorio. Muestra a los enemigos patrullando de forma autónoma y volteándose al llegar a un borde o chocar con una pared.

## 🧩 Cómo está armado el enemigo

**Objeto `Enemigo_Patrulla`**
- `SpriteRenderer` con el sprite del enemigo.
- `Rigidbody2D` (Dynamic) con **Freeze Rotation Z**.
- `BoxCollider2D` ajustado al sprite.
- Script `EnemyPatrol`.

**Objeto hijo `GroundCheck`**
- Objeto vacío ubicado ligeramente al frente y abajo del cuerpo. Desde aquí sale el rayo que busca suelo.

**Capas (Layers)**
- Las plataformas y el Tilemap están en la capa `GroundLayer`.
- El enemigo **no** está en `GroundLayer`, para que sus rayos no lo detecten a él mismo.

## 📜 Script `EnemyPatrol.cs`

El enemigo camina en una dirección y lanza dos rayos invisibles en cada frame:

| Rayo | Origen | Dirección | Qué detecta |
|------|--------|-----------|-------------|
| Suelo | `puntoSuelo` (GroundCheck) | Hacia abajo | Si no hay piso, hay un borde o abismo |
| Pared | Centro del enemigo | Hacia adelante | Si hay algo, hay una pared |

Si **no hay piso** o **hay pared**, llama a `Voltear()`, que invierte la dirección y espeja el sprite con `localScale.x`.

### Parámetros ajustables (Inspector)

| Variable | Descripción |
|----------|-------------|
| `velocidad` | Qué tan rápido camina |
| `puntoSuelo` | Transform del hijo GroundCheck |
| `distanciaSuelo` | Largo del rayo hacia abajo |
| `distanciaPared` | Largo del rayo hacia adelante |
| `capaSueloLayer` | Capas que cuentan como suelo o pared (`GroundLayer`) |

Los rayos se dibujan en azul en la vista Scene con `OnDrawGizmos`, para ajustar las distancias fácilmente.

## 🧱 Prefab

- El enemigo se guardó como Prefab en `Assets/Prefabs/Enemigo_Patrulla`.
- Se colocaron 4 copias en distintas plataformas. Si se modifica el Prefab (por ejemplo la velocidad), las copias se actualizan.

## 📁 Estructura del repositorio

```
Assets/
├── Prefabs/        → Enemigo_Patrulla
├── Script/         → EnemyPatrol.cs, PlayerController.cs, CameraFlow.cs
├── Scenes/         → Nivel_1
├── Animations/
└── Sprites/
videoCreacionEnemigo   → video de demostración
```

## ▶️ Cómo probarlo

1. Clonar el repositorio y abrirlo con **Unity 6**.
2. Abrir la escena `Nivel_1` en `Assets/Scenes`.
3. Dar **Play** y observar a los enemigos patrullar.
4. Para ver los rayos, seleccionar un enemigo y mirar la pestaña **Scene**.

## 🛠️ Tecnologías

- Unity 6 (2D, Universal Render Pipeline)
- C#

## 🎬 Video de demostración

[▶️ Ver video completo](videoCreacionEnemigo.mp4)

Muestra a los enemigos patrullando de forma autónoma y volteándose al llegar a un borde o chocar con una pared.
