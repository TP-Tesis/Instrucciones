# Simulador de Riego Presurizado — Documento de trabajo

Referencia compartida del equipo. Aquí está **cómo funciona la app paso a paso** y **qué se decidió y por qué**, para que los dos trabajemos sobre lo mismo.

**Equipo:** Sosa Colca, Angello Rodolfo · Tongo Alejandro, Milagros Salet
**Programa:** Ingeniería de Software — UPC
**Última actualización:** revisión de reformulación del alcance

---

## Índice

1. [Qué cambió en esta revisión](#1-qué-cambió-en-esta-revisión)
2. [El encuadre: qué es la tesis](#2-el-encuadre-qué-es-la-tesis)
3. [Las siete concepciones erróneas](#3-las-siete-concepciones-erróneas)
4. [Paso a paso de la app](#4-paso-a-paso-de-la-app)
5. [Reglas del sistema](#5-reglas-del-sistema)
6. [Estado de los módulos](#6-estado-de-los-módulos)
7. [Decisiones de ingeniería de software](#7-decisiones-de-ingeniería-de-software)
8. [Verificación del motor](#8-verificación-del-motor)
9. [Evaluación en dos niveles](#9-evaluación-en-dos-niveles)
10. [Bitácora de decisiones](#10-bitácora-de-decisiones)
11. [Pendientes](#11-pendientes)

---

## 1. Qué cambió en esta revisión

El profesor especializado pidió **robustecer la idea base**, que era básicamente llevar el Excel a la web. Esto es lo que se agregó:

| Cambio | Por qué |
|---|---|
| **Capa agronómica (M9)** | El caudal deja de escribirse a mano: se deriva de la necesidad del cultivo. Antes no había ni una variable agronómica en una app dirigida a agrónomos. |
| **Predicción guiada (M10)** | El estudiante predice antes de ver el resultado. Impide avanzar por tanteo y genera la métrica de comprensión causal. |
| **Diagnóstico escalonado en 3 niveles** | Antes la app diagnosticaba por el estudiante. Diagnosticar es la habilidad que queremos medir; no podemos automatizarla y después evaluarla. |
| **Inventario de 7 concepciones erróneas** | Es lo que hace que el pretest/postest mida comprensión y no destreza de cálculo. |
| **Falla productiva** | El primer escenario no tiene alertas: el error precede a la explicación. |
| **Complejidad graduada** | La pantalla se desbloquea por escenarios. Antes el instrumento completo aparecía desde el minuto uno y ahogaba al novato. |
| **El 3D con dos tareas propias** | Deja de ser una vista más. Es el único lugar donde se pueden confrontar C5 y C6. |
| **La IA devuelve un frente de opciones** | No un óptimo único, y optimiza el diseño del alumno, no uno nuevo. Confronta C7. |
| **Transferencia fuera de la app** | Un ejercicio final en papel. Es la respuesta a «¿aprendieron hidráulica o aprendieron a usar su software?». |
| **Criterios del libro incorporados** | Longitud inclinada, pérdidas locales Kr, velocidad 0.60–3.00 m/s, límite de 50 m de desnivel sin CRP, C = 140 para PVC. |

**Se recortó:** la ingesta de terreno DEM (M7) pasa a perfiles pre-extraídos como archivos fijos. Era un proyecto de geomática completo y no aportaba comprensión hidráulica.

---

## 2. El encuadre: qué es la tesis

> No es «una app de riego». Es **un motor de simulación verificado** y **un proceso de aprendizaje instrumentado**, cuya eficacia se mide con un experimento de tres grupos.

Ese cambio de sujeto es el argumento central ante el jurado de Software.

### Entrega tres cosas, no una

1. **Una biblioteca** — el núcleo de cálculo hidráulico, independiente de la interfaz, versionado, con su suite de pruebas y verificado contra tres referencias.
2. **Una aplicación instrumentada** — no solo simula: mide. La telemetría es un subsistema diseñado, no un accesorio.
3. **Un conjunto de datos** — el registro anonimizado de un experimento real de tres grupos. Reutilizable y publicable, y sale del mismo experimento.

### Título propuesto

> Aplicación web de simulación interactiva con **núcleo de cálculo verificado** para la **comprensión conceptual** del diseño hidráulico de tuberías en riego **presurizado**, en estudiantes de Ingeniería Agrónoma

El título vigente dice «simulaciones 2D» y «riego por gravedad»; ninguna de las dos cosas describe ya el proyecto.

---

## 3. Las siete concepciones erróneas

**Esta tabla es la columna vertebral.** Cada escenario existe para provocar una y desmentirla. Cada ítem del pretest y postest mide una.

| | Lo que el estudiante cree | Lo que es | Dónde se desmiente |
|---|---|---|---|
| **C1** | Presión y caudal son lo mismo | Variables acopladas pero distintas | Etapa 2 · tabla y perfil |
| **C2** | Más diámetro da más presión | Da menos pérdida, que no es lo mismo | Etapa 2 · edición en vivo |
| **C3** | Subir en cota cuesta caudal | Cuesta presión; el caudal lo fija la demanda | Etapa 2 · cadena agronómica |
| **C4** | La velocidad la fija la fuente | La fija el diámetro para un caudal dado | Etapa 2 · tabla |
| **C5** | Si funciona regando, funciona siempre | Al cerrar válvulas la presión estática sube y revienta | **Solo en 3D · tarea A** |
| **C6** | La uniformidad depende del emisor | Depende de la distribución de presiones | **Solo en 3D · tarea B** |
| **C7** | Existe un diseño óptimo único | Es multicriterio, con restricciones fuera del modelo | **Solo en el contraste con la IA** |

### La hipótesis que habilita

Con C5, C6 y C7 ancladas a partes concretas del sistema, la comparación entre grupos deja de ser «¿el 3D ayuda?» y pasa a ser falsable:

> El grupo con vista 3D debería superar al grupo sin ella **en los ítems que miden C5 y C6, y no necesariamente en los demás.**

---

## 4. Paso a paso de la app

Tres etapas con propósito distinto. **Sin tiempos asignados todavía.**

### ETAPA 1 — Romper antes de construir

**Paso 1 · Pretest.** Ítems mapeados uno a uno contra C1–C7. Sin responderlo, el simulador no abre. Es condición del diseño experimental: sin línea base no hay ganancia de Hake.

**Paso 2 · Una red que ya funciona.** No abre con formulario. Abre con una red andina resuelta, en verde, y **una sola representación: el perfil**. Consigna: *«bájale el diámetro al último tramo hasta que algo se rompa»*.

**Paso 3 · Falla productiva.** Este escenario **no tiene alertas**. Ve caer la línea piezométrica y ponerse rojos los nodos, pero nadie le dice por qué.

**Paso 4 · El diagnóstico llega después del intento.** Recién cuando lo intentó y no le salió, la app revela qué pasaba. El contraste entre lo que creía y lo que era es lo que enseña.

**Paso 5 · Teoría situada.** Los fundamentos se abren desde el problema que acaba de tener, con sus propios números. No es un anexo: cada columna de la tabla y cada alerta enlazan al párrafo que las explica.

---

### ETAPA 2 — El bucle de diseño

**Paso 6 · Ingreso de datos.** Ahora sí el formulario. Dos bloques separados a propósito.

**Bloque agronómico:** cultivo (arrastra Kc, profundidad radicular, fracción de agotamiento), ET₀, área, eficiencia de aplicación, textura del suelo (arrastra infiltración básica y capacidad de campo), jornada de riego, número de sectores.

**Bloque hidráulico:** fuente (reservorio con cota, o bomba con altura dinámica), nodos con progresiva y cota, tramos con longitud, material y coeficiente C, diámetro y clase, accesorios con sus Kr.

De ahí sale la cadena:

```
ET₀ × Kc              →  lámina neta        mm/día
÷ eficiencia          →  lámina bruta       mm/día
× área × 10           →  volumen del turno  m³/día
÷ horas de jornada    →  CAUDAL DE DISEÑO   m³/h
÷ número de salidas   →  caudal por emisor  L/h
```

**El caudal nunca se escribe.** Cambiar papa por alfalfa mueve el Kc y ese movimiento se propaga hasta la velocidad en la tubería.

**Paso 7 · La pantalla se desbloquea por etapas.**

| Escenario | Qué se muestra |
|---|---|
| 2 | Perfil + tabla de 5 columnas (Ø, v, hf, Pr, veredicto) |
| 3 | Se suma la planta; tabla a 12 columnas |
| 4 | Tabla completa del libro, triángulo de decisión, costos |
| 5 | Se habilita el 3D |

La riqueza se gana. Lo que ayuda a un experto ahoga a un novato.

**Paso 8 · Modifica un parámetro.** Diámetro, clase, cota, elemento de control, accesorios.

**Paso 9 · La app pide una predicción antes de recalcular.** Solo en cambios consecuentes, y rotando tres formatos:

- **Dirección** — ¿sube o baja?
- **Magnitud** — ¿menos de 2 m, entre 2 y 10, más de 10?
- **Causa** — pasó esto, ¿por qué? Tres opciones, una correcta

La tasa de acierto se reporta **contra el azar** de cada formato, no en bruto.

**Paso 10 · Recálculo y revelación.** El núcleo resuelve y aparece el número junto al veredicto de la predicción.

**Paso 11 · Diagnóstico escalonado.** Tres niveles, y **cada uno hay que pedirlo**:

| Nivel | Qué muestra | Ejemplo |
|---|---|---|
| 1 | El síntoma | «Algo falla en el sector A» |
| 2 | La causa | «Sub-presión en A1, −20.3 m.c.a.» |
| 3 | Las salidas en orden | «1 · Ampliar Ø del lateral · 2 · Acortar el recorrido» |

**Queda registrado qué nivel necesitó.** Su descenso a lo largo de los escenarios es la medida directa de competencia diagnóstica — mejor que contar iteraciones, que no distingue destreza de tanteo.

**Paso 12 · Corrige.**

**Paso 13 · Autoexplicación.** Al cerrar el problema: *«¿por qué funcionó?»*, tres opciones, una correcta. **Solo se pregunta cuando hubo éxito**: explicar un fracaso refuerza el error.

**Paso 14 · Vuelve al paso 8.** Cada vuelta cierra una alerta y destapa la siguiente. Este bucle es el mecanismo de aprendizaje.

---

### ETAPA 3 — Lo espacial, la IA y la transferencia

#### La vista 3D, con dos tareas propias

**Paso 15 · Tarea A — La envolvente estática.** Conmutador **regando / cerrado**.

Con el sistema regando, la fricción se come parte de la carga y el diseño cumple. Al cerrar las válvulas **desaparece la fricción, la presión estática sube a todo el desnivel disponible, y la cortina atraviesa la malla de la clase** en los tramos bajos.

El diseño que funcionaba regando revienta al cerrar. Coloca las CRP donde corresponde y repite hasta que no haya rotura estática.

→ Confronta **C5**. Un perfil de un ramal no lo muestra: la envolvente estática es una superficie sobre todo el terreno.

**Paso 16 · Tarea B — Sectorizar por bandas de presión.** El terreno se pinta por la presión disponible en bandas discretas, como carta topográfica.

Consigna: **agrupar las salidas en sectores de modo que dentro de cada uno la presión no varíe más del 20 %.** Repite hasta cumplirlo en todos.

→ Confronta **C6**. Es agrupar por curvas de nivel sobre una superficie; el perfil muestra un ramal a la vez.

**Degradación:** si el navegador no soporta WebGL, la vista se desactiva sola y avisa que el perfil da la misma lectura en 2D. Mitigación del riesgo R08, modelada en el proceso.

#### La compuerta

**Paso 17 · Entrega el diseño.** Queda congelado y firmado con todos sus indicadores. **Esa versión —y no la última— es contra la que se compara todo después.**

**Hasta aquí la IA está bloqueada.** No es traba de interfaz: si estuviera disponible antes, parte de los participantes copiaría y el grupo quedaría contaminado justo en la variable que medimos. Es condición de validez interna del cuasi-experimento.

#### El contraste con la IA

**Paso 18 · Fija sus restricciones.** Antes de optimizar puede bloquear decisiones: *«esta CRP no la muevas, hay una quebrada ahí»*, *«este tramo va enterrado»*.

**Paso 19 · La IA optimiza SU diseño.** El recocido simulado **arranca desde la configuración que él entregó**, no desde cero. Muestra la curva de convergencia mientras trabaja — el estudiante ve que la búsqueda acepta empeorar a veces para escapar de óptimos locales.

**Respaldo (riesgo R07):** si la metaheurística no converge de forma confiable, un temporizador conmuta a una heurística por reglas de ingeniería que produce el mismo resultado pedagógico.

**Paso 20 · Devuelve un frente de opciones, no un óptimo.**

```
la más barata que cumple    11 200 S/.   DU 90 %   margen  4 m
la más uniforme             14 800 S/.   DU 96 %   margen  4 m
la de mayor margen          13 100 S/.   DU 92 %   margen 18 m
la tuya                     13 900 S/.   DU 87 %   margen  2 m
```

**Paso 21 · Explica la razón de cada cambio.** No «costo 2 400 menos», sino:

> *«Subí el tramo 3 a clase C-7.5 porque tu presión estática ahí llega a 62 m y la C-5 aguanta 50. Con eso te sobra la CRP del nodo D, que costaba 1 800.»*

Legible, discutible, rebatible.

**Paso 22 · Puede volver a correr la IA con otras restricciones.** Ahí aprende la lección del módulo: **la IA optimiza lo que modelaste, no la realidad.**

**Paso 23 · Elige una opción y la defiende por escrito.** Por qué esa y no la de la IA, sabiendo que el agricultor tiene un presupuesto y un terreno que el modelo no conoce.

→ Confronta **C7**. Es nivel Evaluar de Bloom.

#### El cierre

**Paso 24 · Transferencia fuera de la aplicación.** Una línea nueva resuelta **en papel o en la hoja de cálculo de referencia**, sin simulador. Si puede hacerlo sin la app, aprendió diseño hidráulico. Si no, aprendió a usar el software.

**Paso 25 · Postest.** Ítems mapeados contra C1–C7.

**Paso 26 · Reporte y exportación.** Red, tabla completa por tramo, indicadores, alertas resueltas y pendientes, y **el origen de cada decisión: suya o adoptada de la IA**.

---

### Lo que corre por debajo todo el tiempo

Registro de eventos **en solo-anexado**:

- cada edición, con su valor antes y después
- cada predicción: formato, respuesta, resultado real, error en metros
- **el nivel de ayuda pedido en cada alerta**
- cada autoexplicación
- encuadres del 3D y ajustes de cota por arrastre
- la sectorización propuesta
- distancia entre su diseño y el frente de la IA
- su justificación escrita

**Las métricas no se calculan al vuelo: se derivan después.** El experimento se corre una sola vez, con estudiantes reales. Si en el análisis cambia la definición de una métrica, con el registro crudo se recalcula; sin él, el dato se perdió.

### El docente, en paralelo

Prepara y publica escenarios, ve el historial de cada estudiante y su trayectoria de versiones, y exporta todo para el análisis de los tres grupos.

---

## 5. Reglas del sistema

### Estado de cada nodo (los colores)

| Elemento | Condición | Estado |
|---|---|---|
| Emisor | `P < presión mínima` | 🟡 Alerta — sub-presión |
| Emisor | `P > 3 × presión nominal` | 🔴 Crítico — sobrepresión |
| Emisor | dentro de rango | 🟢 Correcto |
| Nodo de conducción | `P > presión máxima de la clase` | 🔴 Crítico — rotura |
| Nodo de conducción | dentro de la clase | 🟢 Correcto |

**El mismo color en planta, perfil y 3D.** El estudiante salta entre representaciones sin reaprender el código visual.

### Catálogo de alertas

| Alerta | Dominio | Se dispara cuando | Salidas en orden |
|---|---|---|---|
| Sub-presión en el emisor | Hidráulica | `P < P mínima` | 1 · Ampliar Ø del lateral · 2 · Acortar el recorrido |
| Variación de presión sobre el 20 % | Hidráulica | `Δp sector > 20 % de P nominal` | 1 · Ampliar Ø del lateral · 2 · Emisor autocompensante · 3 · Regulador en cabecera |
| Rotura por sobre la clase | Hidráulica | `P > P máx de la clase` | 1 · Subir la clase · 2 · CRP aguas arriba |
| Velocidad fuera de rango | Hidráulica | `v > 3.0` vibración · `v < 0.6` sedimentación | 1 · Ajustar el Ø del tramo |
| Desnivel acumulado sobre 50 m | Topográfica | `Σ desnivel sin CRP > 50 m` | 1 · Colocar CRP · 2 · Partir el tramo |
| La carga no alcanza | Topográfica | línea piezométrica bajo la tubería | 1 · Más carga en la fuente · 2 · Reducir pérdidas · 3 · Acortar el sector |
| Escorrentía | Agronómica | `precipitación del sistema > infiltración` | 1 · Alargar la jornada · 2 · Repartir en más sectores |
| Uniformidad bajo el objetivo | Agronómica | `DU < 90 %` | 1 · Uniformar presiones · 2 · Emisor autocompensante |
| El suelo no retiene un día | Agronómica | `agua aprovechable < consumo diario` | 1 · Regar más de una vez al día |

**Cada alerta declara su dominio** — hidráulica, topográfica o agronómica. Saber en qué disciplina está la causa es la mitad de la corrección, y es evaluable en el postest.

### Criterios del método de referencia

Incorporados del libro *EXCEL TUBERÍAS · Aplicativo de Diseño de Tuberías de Riego*, del Ing. Tongo Pizarro, Moisés:

- **Unidades:** Q en l/s · Ø en pulgadas · L en km · hf en m/km · cotas en m.s.n.m.
- **Longitud inclinada:** `L = √(H² + Dt²)` — no la distancia horizontal
- **Pérdida disponible:** `(H + Pr_anterior) / L`
- **Diámetro preliminar:** `D = (Q / (0.0004264 · C · S^0.54))^(1/2.63)`
- **Pérdida unitaria:** `hf = (1/0.0004264)^1.85 · Q^1.85 / C^1.85 / D^4.87`
- **Pérdidas locales:** `Hr = (v²/2g) · Kr` — entrada 0.5 · codo 45° 0.2 · codo 25° 0.1 · ampliación 0.1 · reducción 0.37
- **Velocidad:** > 3.0 vibración · 0.6–3.0 OK · < 0.6 sedimentación
- **π** se escribe `3.1416`, como en la hoja
- **Guardas:** desnivel > 50 m sin CRP → rechaza · tramo > 500 m → rechaza
- **C = 140 para PVC** (criterio del libro; el documento de tesis decía 150)

### Clases de tubería

| Clase | Presión máxima de trabajo |
|---|---|
| C-5 | 50 m.c.a. |
| C-7.5 | 75 m.c.a. |
| C-10 | 100 m.c.a. |
| C-15 | 150 m.c.a. |

---

## 6. Estado de los módulos

La idea se enriquece por completo; **la implementación se acota y se declara**. Un diseño completo con implementación acotada vale más que una implementación completa de algo poco pensado.

| Módulo | Estado | Alcance |
|---|---|---|
| M1 · Simulador base y gestión | ✅ Implementado | Acotado: red predefinida, editable en parámetros |
| M2 · Motor hidráulico topográfico | ✅ Implementado | Completo y verificado contra tres referencias |
| M4 · Eficiencia y uniformidad | ✅ Implementado | Completo |
| M5 · Control de presión y costos | ✅ Implementado | Completo |
| M9 · Base agronómica | ✅ Implementado | Completo |
| M10 · Predicción guiada y teoría situada | ✅ Implementado | Completo |
| M3 · Visualización 3D | 🟡 Reducido | Solo las dos tareas con objetivo de aprendizaje propio |
| M6 · Optimización con IA | 🟡 Reducido | Con respaldo por reglas si no converge |
| M7 · Terreno | 🟡 Reducido | Perfiles reales pre-extraídos, sin canalización DEM |
| M8 · Validación y panel docente | 🟡 Reducido | Pretest, postest y panel mínimo |
| Edición estructural libre de la red | ⚪ Especificado | Documentado en el plan de continuidad |
| Redes malladas · panel docente extendido | ⚪ Especificado | Documentado en el plan de continuidad |

---

## 7. Decisiones de ingeniería de software

Ninguna es novedosa en el estado del arte. Todas son verificables y están al alcance de dos personas.

**1 · Núcleo de cálculo puro, sin dependencia del framework.**
Obligado por una contradicción real: el navegador exige respuesta interactiva inmediata (< 200 ms) y el optimizador llama al mismo evaluador miles de veces. Un motor acoplado a la interfaz no puede cumplir las dos cosas.

```
              NÚCLEO DE CÁLCULO (TypeScript puro, sin framework)
                    red → presiones · DU · costo
                              │
        ┌─────────────────────┼─────────────────────┐
   1× por edición      ~10 000× por corrida     1× por caso
        │                     │                     │
   Navegador             Web Worker           Banco de pruebas
   D3 · R3F              recocido             EPANET · libro
   < 200 ms              no bloquea UI        error < 5 %
```

**2 · Verificación contra tres referencias independientes.**
La hoja profesional en uso, problemas resueltos de bibliografía, y un simulador hidráulico estándar. Con error documentado por caso, no una afirmación general.

**3 · Pruebas basadas en propiedades sobre invariantes físicas.**
Con `fast-check`, afirmando invariantes que deben cumplirse para *cualquier* red generada al azar:
- la presión nunca aumenta aguas abajo en un tramo horizontal
- insertar una CRP nunca sube la presión aguas abajo
- el DU siempre cae entre 0 y 1
- la suma de caudales de los emisores iguala el caudal de la fuente

Más pruebas de referencia fija contra salidas de EPANET guardadas como archivos de caso.

**4 · Telemetría por eventos, con métricas derivadas después.**
Ver sección 4, «lo que corre por debajo».

**5 · Reproducibilidad como entregable.**
Semilla fija en el recocido, dependencias fijadas, y una tubería que va del registro crudo a las tablas del documento.

### Stack

- **Frontend:** React 18 + TypeScript · D3.js (2D) · Three.js / React Three Fiber (3D)
- **Backend:** Node.js + Express · Prisma · JWT
- **Base de datos:** PostgreSQL con JSONB
- **Despliegue:** Vercel (frontend) + Railway (backend y BD)
- **Pruebas:** Jest · fast-check · Postman · JMeter
- **Verificación del motor:** EPANET

---

## 8. Verificación del motor

El núcleo reproduce el método de referencia **al décimo decimal**, contra los valores que la propia hoja tiene guardados en sus celdas:

| Magnitud | Valor del libro | Valor de la app | Error |
|---|---|---|---|
| Velocidad media v | `0.9867603132201427` | `0.9867603132201427` | **0.000000 %** |
| Pérdida de carga Hf | `0.5068456652968484` | `0.5068456652968484` | **0.000000 %** |
| Presión residual Pr | `11.993154334703151` | `11.993154334703151` | **0.000000 %** |
| Cota piezométrica final | `3001.9931543347034` | `3001.9931543347034` | **0.000000 %** |

*Caso: tramo RESERVORIO → CRP-1. Q = 2 l/s, C = 140, Ø = 2", cotas 3000 → 2990, progresivas 0+000 → 0+020, Pr anterior = 2.5 m.*

### Dos hallazgos sobre la hoja de referencia

**Uno que confirma el método.** La constante `0.0004264` no es arbitraria: es la de Hazen-Williams del Sistema Internacional (`0.2785`) convertida a l/s, pulgadas y m/km. La conversión exacta da `0.00042613` — la hoja redondea con 0.06 % de diferencia. Derivación correcta.

**Uno que hay que resolver.** Las dos hojas del libro usan constantes distintas para lo mismo:

| Hoja | Constante | Origen |
|---|---|---|
| `HTubería` | `1 717 268` | `(1/0.0004264)^1.85` |
| `TEORÍA y DEDUCCIONES` | `1 742 143` | exponente exacto `1/0.54 = 1.8519` |

**Difieren 1.43 %**, y esa diferencia va entera a la pérdida de carga. Ninguna está mal — 1.85 y 4.87 son el redondeo habitual — pero **hay que elegir una y dejarla escrita en el documento.** Por ahora el motor usa la de `HTubería`, que es la que reproduce los valores guardados con error cero.

---

## 9. Evaluación en dos niveles

Separarlos evita la confusión más común: tomar una validación de usabilidad por una validación de aprendizaje.

### Nivel de software — ¿el sistema hace bien lo que dice?

- Verificación del motor contra las tres referencias, con error documentado
- Estudio de rendimiento: recálculo incremental frente a completo, en ms contra número de nodos
- Pruebas por propiedades y de referencia fija
- Pruebas de carga con 30 usuarios concurrentes

### Nivel educativo — ¿sirve para lo que fue construido?

**Diseño de tres grupos:**

| Grupo | Condición | Qué responde |
|---|---|---|
| A | Método tradicional, sin app | Línea base |
| B | App sin vista 3D | ¿La app supera al método tradicional? |
| C | App completa con 3D | ¿El 3D aporta sobre el 2D? |

**Análisis:** ganancia normalizada de Hake por estudiante, ANOVA de una vía con post-hoc de Tukey, y tamaño de efecto (d de Cohen) por comparación.

**Condiciones de validez, sin las cuales se cae el experimento:**

1. Instrumento validado por juicio de experto + prueba piloto
2. Motor verificado antes de tocar estudiantes
3. Equivalencia inicial de grupos confirmada por el pretest
4. Hardware estandarizado para el grupo C (riesgo R08)

**Tercer nivel — métricas de proceso.** Derivadas del registro de eventos, y ninguna hoja de cálculo ni EPANET las captura:

- descenso del nivel de ayuda necesario para diagnosticar
- evolución de la tasa de acierto en las predicciones, contra el azar
- alertas corregidas por sesión y tiempo entre apertura y cierre
- acortamiento de la distancia entre su diseño y el frente de la IA

---

## 10. Bitácora de decisiones

| # | Decisión | Razón |
|---|---|---|
| D01 | El caudal se deriva, no se escribe | Sin origen agronómico, una app para agrónomos no tiene ni una variable de su disciplina |
| D02 | El cabezal de filtrado descuenta ~10 m.c.a. | Un sistema presurizado real lleva filtro de arena y anillos; omitirlo sobrestima la presión de todo el sector |
| D03 | El DU se expresa en mm que le faltan al cultivo | «DU 86 %» no describe ningún hecho agronómico |
| D04 | Longitud inclinada en lugar de horizontal | Criterio del método de referencia; es además lo físicamente correcto |
| D05 | Velocidad 0.60–3.00 m/s | Criterio del libro y rango de validez de Hazen-Williams. Antes se usaba 0.3–2.0, que era incorrecto |
| D06 | C = 140 para PVC | Criterio del libro (tubería con envejecimiento). El documento de tesis decía 150 (tubería nueva). **Pendiente de decidir y justificar** |
| D07 | El primer escenario no tiene alertas | Falla productiva: el error debe preceder a la explicación |
| D08 | Diagnóstico en tres niveles a pedido | Diagnosticar es la habilidad que medimos; no se puede automatizar y luego evaluar |
| D09 | La IA se bloquea hasta la entrega | Validez interna del cuasi-experimento |
| D10 | La IA optimiza el diseño del alumno | Un óptimo desde cero es un diseño ajeno, incomparable |
| D11 | La IA devuelve un frente, no un óptimo | Confronta C7 y enseña que el diseño es multicriterio |
| D12 | El 3D solo con dos tareas exclusivas | Si es una vista más, la comparación B vs C sale nula |
| D13 | Registro de eventos en solo-anexado | El experimento se corre una sola vez |
| D14 | Recorte de la ingesta DEM (M7) | Proyecto de geomática completo, sin aporte a la comprensión hidráulica |
| D15 | Complejidad graduada por escenario | Efecto de reversión por experiencia: lo que ayuda al experto ahoga al novato |

---

## 11. Pendientes

### Bloqueantes — no dependen del código y van primero

- [ ] **Redactar los ítems del pretest/postest** mapeados contra C1–C7
- [ ] **Juicio de experto** sobre el instrumento (docente de hidráulica)
- [ ] **Prueba piloto** del instrumento antes del experimento
- [ ] **Negociar el acceso a estudiantes** de Ingeniería Agrónoma — riesgo R01, es el cuello de botella real

### Documentales

- [ ] Decidir y justificar **C = 140 vs 150** para PVC
- [ ] Actualizar el **título** (dice «2D» y «por gravedad»)
- [ ] Enriquecer los **objetivos específicos** sin renumerar, para que el aporte de software sea explícito
- [ ] Definir el **umbral numérico de éxito** del proyecto

### Técnicos

- [ ] Extraer los 3–5 perfiles reales peruanos y guardarlos como archivos fijos
- [ ] Núcleo de cálculo como paquete independiente, con su suite de pruebas
- [ ] Prueba de rendimiento del 3D en el hardware del laboratorio — riesgo R08
- [ ] Corregir el registro lingüístico de los prototipos: hay **voseo** («arrastrá», «cambiá», «movés») y los usuarios son peruanos

---

## Referencias

- *EXCEL TUBERÍAS · Aplicativo de Diseño de Tuberías de Riego* — Ing. Tongo Pizarro, Moisés. Método de cálculo de referencia.
- EPANET — verificación cruzada del motor hidráulico.
- FAO-56 — coeficientes de cultivo, profundidad radicular y fracción de agotamiento.
