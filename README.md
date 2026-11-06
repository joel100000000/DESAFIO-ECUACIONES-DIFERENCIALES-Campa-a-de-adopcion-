# Campaña de adopción de mascotas rescatadas: Heun y RK4

**Materia:** 
Métodos Numéricos · **Autor:** JOEL CHOQUE YUJRA
**Simulación web:** https://joel100000000.github.io/DESAFIO-ECUACIONES-DIFERENCIALES-Campa-a-de-adopcion-/

## Problema
Un refugio municipal quiere saber **¿en cuántas semanas puede lograr que el 90 % de sus mascotas rescatadas sea adoptado?** La comunidad beneficiaria son los animales del refugio y las familias que pueden adoptarlos.
> Los parámetros son **hipotéticos**. Los resultados son una simulación, no una predicción comprobada con datos reales.

## Modelo matemático
| Símbolo | Significado | Unidad |
|---|---|---|
| t | Tiempo (variable independiente) | semanas |
| y(t) | Mascotas adoptadas acumuladas (variable dependiente) | mascotas |
| M | Mascotas disponibles en total | mascotas |
| k | Tasa de adopción | 1/semana |
| y₀ | Mascotas adoptadas al inicio | mascotas |

**EDO con condición inicial:**
```
dy/dt = k (M − y),    y(0) = y₀
```
**Supuestos:** 
el ritmo de adopción es proporcional a las mascotas que aún esperan (M − y); k es constante; no ingresan mascotas nuevas durante la campaña.

**Valores por defecto:** 
M = 120, k = 0.15, y₀ = 10, h = 1, T = 30 semanas.

## Solución analítica
Por separación de variables: dy/(M − y) = k dt, luego M − y = C e^(−kt), y con y(0) = y₀ se tiene C = M − y₀.
```
y(t) = M − (M − y₀) e^(−kt)
```
**Verificación:** 
y′(t) = k(M − y₀)e^(−kt) = k(M − y(t)) ✓ y y(0) = y₀ ✓.

**Tiempo para llegar al 90 %:**
`t* = (1/k) · ln[(M − y₀) / (0.1 M)]`. Con los valores por defecto, t* ≈ 14.8 semanas.

## Métodos numéricos
Ambos usan los mismos parámetros, y₀, intervalo y tamaño de paso h.
- **Heun (Runge-Kutta de orden 2):**
  `k₁ = f(tₙ, yₙ)`, `k₂ = f(tₙ + h, yₙ + h·k₁)`, `yₙ₊₁ = yₙ + (h/2)(k₁ + k₂)`
- **Runge-Kutta de orden 4 (RK4):**
  `k₁ = f(tₙ, yₙ)`, `k₂ = f(tₙ + h/2, yₙ + h/2·k₁)`, `k₃ = f(tₙ + h/2, yₙ + h/2·k₂)`, `k₄ = f(tₙ + h, yₙ + h·k₃)`,
  `yₙ₊₁ = yₙ + (h/6)(k₁ + 2k₂ + 2k₃ + k₄)`
## Análisis de errores
La aplicación calcula, frente a la solución analítica:
- error absoluto: `|y exacta − y aproximada|`
- error relativo porcentual: `|error| / |y exacta| · 100`
- comparación automática con tamaños de paso 2h, h y h/2
Al reducir h a la mitad, el error de Heun baja unas 4 veces (orden 2) y el de RK4 unas 16 veces (orden 4). En los ensayos, **RK4 produjo menor error que Heun**.

## Cómo ejecutar
No requiere instalación.
1. Abre la URL de la simulación web en cualquier navegador, o descarga `index.html` y ábrelo con el navegador.
2. Ajusta M, k, y₀, h y T, y pulsa **Ejecutar Heun y RK4**.

Validaciones: M > 0, k > 0, 0 ≤ y₀ < M, h > 0, T > 0, h ≤ T, T múltiplo de h, máximo 1000 pasos y k·h < 2 (condición de estabilidad de Heun).

## Limitaciones

Parámetros hipotéticos; k constante; sin ingreso de mascotas nuevas. En la realidad la tasa de adopción cambia con la difusión de la campaña, la época del año y el perfil de cada animal.
