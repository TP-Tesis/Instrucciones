# Planteamiento — el norte del proyecto

> **Léelo antes de cada sprint.** Si una historia, una pantalla o una decisión técnica no se puede conectar con alguna de las seis causas de este documento, no va. Esa es la única regla que protege el enfoque durante los ocho meses que vienen.

**Equipo:** Sosa Colca, Angello Rodolfo · Tongo Alejandro, Milagros Salet
**Programa:** Ingeniería de Software — Universidad Peruana de Ciencias Aplicadas

---

## Índice

1. [El problema](#1--el-problema)
2. [Las seis causas](#2--las-seis-causas)
3. [Las consecuencias](#3--las-consecuencias)
4. [Por qué lo que ya existe no lo resuelve](#4--por-qué-lo-que-ya-existe-no-lo-resuelve)
5. [La solución: 2D, 3D e IA](#5--la-solución-2d-3d-e-ia)
6. [Trazabilidad: cada pieza contra su causa](#6--trazabilidad-cada-pieza-contra-su-causa)
7. [Pregunta de investigación e hipótesis](#7--pregunta-de-investigación-e-hipótesis)
8. [Lo que NO es la solución](#8--lo-que-no-es-la-solución)
9. [La prueba de enfoque](#9--la-prueba-de-enfoque)

---

## 1 · El problema

> **Los estudiantes de Ingeniería Agrónoma terminan el curso de diseño hidráulico sabiendo aplicar las fórmulas, pero sin comprender el comportamiento del sistema que diseñan.**

Esa es la frase, y conviene cuidar lo que **no** dice:

| No decimos | Porque |
|---|---|
| «No tienen un simulador» | Sería confundir el problema con la ausencia de nuestra solución. Es el error más común de un planteamiento. |
| «No saben calcular» | Sí saben. Aprueban los exámenes calculando pérdida de carga. |
| «El curso está mal dado» | El problema no es el docente: es la naturaleza del medio con el que se enseña. |

**Saben calcular y no saben diseñar.** Obtienen la pérdida de carga de un tramo dado, pero puestos frente a una red que falla no identifican el tramo culpable, no anticipan qué ocurre si cambian un diámetro, y no relacionan lo que hacen con el agua que efectivamente le llega a la planta.

---

## 2 · Las seis causas

### C1 · Se enseña el procedimiento, no el comportamiento
El ejercicio típico entrega los datos y pide un número. El estudiante practica **ejecutar una fórmula**, nunca **anticipar una consecuencia**. Son dos habilidades distintas y solo se evalúa la primera.

### C2 · La retroalimentación llega tarde
Entre que resuelve un ejercicio y le dicen si está bien pasan días. Sin ciclo corto de error y corrección no se construye intuición: se memoriza el procedimiento.

### C3 · Equivocarse es caro
En papel o en hoja de cálculo, probar una alternativa obliga a rehacer todo. Entonces el estudiante **no explora**: calcula una vez y entrega. Sin exploración no hay descubrimiento.

### C4 · El dato llega sin origen
El caudal viene dado en el enunciado. El estudiante nunca ve que ese número sale de lo que el cultivo necesita —de **su propia disciplina**—, y el diseño hidráulico le queda como un ejercicio de física ajeno a su carrera.

### C5 · Lo invisible se queda invisible
La presión, la línea piezométrica, la uniformidad y la envolvente estática son campos que no se ven. Sin una representación, el estudiante los manipula como símbolos y no como fenómenos.

### C6 · No hay práctica sobre terreno real
Los ejercicios son abstractos y planos. La topografía —que en la sierra es la que gobierna el diseño— sencillamente no aparece.

---

## 3 · Las consecuencias

### En el aprendizaje

Las concepciones erróneas **sobreviven al curso**. Un estudiante aprobado sigue creyendo cosas como estas, que son las siete que el instrumento va a medir:

| | Lo que cree | Lo que es |
|---|---|---|
| **CE1** | Presión y caudal son lo mismo | Variables acopladas pero distintas |
| **CE2** | Más diámetro da más presión | Da menos pérdida, que no es lo mismo |
| **CE3** | Subir en cota cuesta caudal | Cuesta presión; el caudal lo fija la demanda del cultivo |
| **CE4** | La velocidad la fija la fuente | La fija el diámetro, para un caudal dado |
| **CE5** | Si funciona regando, funciona siempre | Al cerrar las válvulas la presión estática sube y revienta |
| **CE6** | La uniformidad depende del emisor | Depende de la distribución de presiones en el sector |
| **CE7** | Existe un diseño óptimo único | Es multicriterio, con restricciones que el modelo no captura |

### En el ejercicio profesional

- Diseños con uniformidad baja: agua de más en unas zonas y cultivo con sed en otras.
- Roturas por no verificar la presión estática, que es la condición crítica y la que casi nadie comprueba.
- Sobredimensionamiento por precaución o subdimensionamiento por descuido, ambos por falta de criterio.

### En el contexto

El riego agrícola es el mayor consumidor de agua dulce del país y la sierra trabaja con disponibilidad limitada. **La diferencia entre un diseño con 70 % de uniformidad y uno con 90 % es agua que se aplica y no se aprovecha.** La competencia de quien diseña tiene efecto directo sobre ese recurso.

| Cifra | Qué mide | Fuente |
|---|---|---|
| **80 %** | del agua disponible del país la consume la agricultura | Sector agrícola nacional |
| **35 %** | de eficiencia con la que opera el riego nacional | ANA, 2023 |
| **45 %** | del agua distribuida se pierde en el trayecto | ANA, 2023 |
| **13 %** | del PBI, y 30 % del empleo, dependen del sector | Sector agrícola nacional |
| **S/ 6 200 M** | en proyectos hídricos sin ejecutar, por falta de especialistas | ComexPerú, 2024 |

Y en la población concreta: solo el **47,1 %** alcanza un razonamiento cuantitativo satisfactorio en variables hidráulicas (Ricra, 2023), y apenas el **38 %** de universitarios peruanos usa simulación de forma efectiva (Núñez-Rojas et al., 2024).

> ⚠️ **Único dato sin verificar.** El 13 % del PBI y el 30 % del empleo necesitan su referencia exacta. Las otras tres cifras ya la tienen.

---

## 4 · Por qué lo que ya existe no lo resuelve

Un jurado lo va a preguntar, así que va escrito:

| Herramienta | ¿Calcula bien? | Por qué no enseña |
|---|---|---|
| **Hoja de cálculo profesional** | Sí — es nuestro método de referencia | Entrega el resultado sin el porqué. Explorar cuesta rehacer las celdas. |
| **EPANET y similares** | Sí — es el estándar de la industria | No diagnostica en lenguaje del estudiante, no pide anticipación, no mide aprendizaje, y su curva de entrada es alta. |
| **Clase magistral, video, PDF** | No aplica | Explican, pero no devuelven la consecuencia de *tu* decisión. |

Ninguna es mala. **Ninguna cierra el ciclo error → diagnóstico → corrección**, que es donde ocurre el aprendizaje.

---

## 5 · La solución: 2D, 3D e IA

> **Un motor de cálculo verificado, envuelto en un ciclo de retroalimentación instrumentado, con tres formas de ver y decidir: simulación 2D, simulación 3D y optimización con inteligencia artificial.**

No es «una app que simula riego». Son cuatro piezas, y cada una existe por una razón distinta.

### El motor de cálculo verificado

Lo que hay debajo de todo. Resuelve la red completa en menos de doscientos milisegundos, reproduce el método profesional de referencia con **error de cero por ciento**, y se verifica contra tres fuentes independientes antes de que ningún estudiante lo toque.

Es la base de las otras tres: sin un cálculo en el que se pueda confiar, todo lo demás enseña algo falso.

### Simulación 2D — donde se diseña

Tres representaciones del mismo estado, a la vista al mismo tiempo y sincronizadas:

- **Planta** — la red a escala real sobre el campo
- **Perfil** — terreno, tubería y línea de presión disponible; la franja entre las dos últimas *es* la presión
- **Tabla por tramo** — las mismas columnas y unidades del método profesional, con las celdas de entrada editables ahí mismo

Tocar un tramo lo resalta en las tres. **Comparar las tres lecturas de un mismo hecho es donde se construye el modelo mental.**

### Simulación 3D — donde se ve lo que un corte no puede mostrar

No es una vista más bonita de lo mismo. Es el **único lugar** donde se pueden confrontar dos de las siete concepciones erróneas:

- **Tarea A · la envolvente estática.** Se conmuta el sistema a válvulas cerradas: desaparece la fricción, la presión sube a todo el desnivel disponible, y el diseño que funcionaba regando revienta. → confronta **CE5**
- **Tarea B · sectorización por bandas de presión.** Agrupar las salidas en sectores donde la presión no varíe más del 20 %, leyendo el campo pintado por zonas. → confronta **CE6**

Un perfil muestra un ramal a la vez; el campo es bidimensional en planta. **Ninguna de las dos tareas es resoluble sin la tercera dimensión.**

### Optimización con IA — donde se aprende que no hay una sola respuesta

Un optimizador metaheurístico —recocido simulado— que **parte del diseño que el estudiante entregó**, no de cero, y devuelve un **frente de opciones** con su costo, su uniformidad y su margen de seguridad. Explica la razón física de cada cambio que propone, y acepta que el estudiante le fije restricciones y vuelva a correr.

→ confronta **CE7**, y enseña la lección de ingeniería del módulo: **la máquina optimiza lo que se modeló, no la realidad.**

Se habilita **solo después de que el estudiante entregue su diseño**. No es una traba de interfaz: si estuviera disponible antes, parte de los participantes copiaría la respuesta y el grupo experimental quedaría contaminado justo en la variable que la tesis mide.

### Y la instrumentación, que es lo que la vuelve tesis

**El sistema no solo enseña: mide.** Cada acción queda registrada sin sobrescribir nada, y de ese registro se derivan las evidencias de que hubo aprendizaje:

- cuánto bajó el nivel de ayuda que necesitó para diagnosticar
- cuánto mejoró su acierto al anticipar consecuencias
- cuánto se acortó la distancia entre su diseño y el frente de la optimización

Ninguna de las herramientas de la sección 4 tiene esto. Es lo que convierte una aplicación educativa en un **instrumento de investigación**.

---

## 6 · Trazabilidad: cada pieza contra su causa

**Esta es la tabla que hay que mirar cuando aparezca la tentación de agregar algo.**

| Pieza | Causa que ataca | Cómo |
|---|---|---|
| Respuesta en menos de un segundo | **C2, C3** | Equivocarse pasa a ser gratis y reversible; el ciclo se cierra al instante |
| Línea de presión en el perfil | **C5** | Vuelve visible el campo que el estudiante manejaba como símbolo |
| Campo de presión sobre el relieve (3D) | **C5, C6** | Muestra la distribución en planta, que una sección no alcanza |
| Cadena del cultivo al caudal | **C4** | El caudal deja de ser un dato del enunciado y pasa a ser un resultado de su disciplina |
| Predicción antes de revelar el resultado | **C1** | Obliga a anticipar la consecuencia en lugar de ejecutar el procedimiento |
| Diagnóstico escalonado en tres niveles | **C1** | Devuelve al estudiante la tarea de diagnosticar, que es la que se quiere medir |
| Alertas con su dominio y sus salidas ordenadas | **C1** | Enseña que hay varias soluciones válidas, no una respuesta única |
| Autoexplicación al cerrar un problema | **C1, C2** | Fija la explicación y no solo el resultado |
| Teoría alcanzable desde la duda | **C1, C2** | La explicación llega cuando ya hay pregunta |
| Escenarios sobre terreno real peruano | **C6** | La topografía pasa a gobernar el diseño, como en la práctica |
| Control de presión y costos | **C1** | Convierte el ejercicio en una decisión con compromisos |
| Contraste con la optimización | **C1** | Comparar y justificar frente a un referente |

### Y por módulo del backlog

| Módulo | Causa | Nota |
|---|---|---|
| M1 · Simulador base 2D | C3, C5 | |
| M2 · Motor hidráulico topográfico | C5, C6 | Base de todo lo demás |
| M3 · Visualización 3D | C5, C6 | Solo con sus dos tareas propias |
| M4 · Eficiencia y uniformidad | C5 | Hace visible el DU en milímetros |
| M5 · Control de presión y costos | C1 | |
| M6 · Optimización con IA | C1 | Confronta CE7 |
| M7 · Terreno | C6 | Perfiles reales pre-extraídos |
| M8 · Validación y panel docente | — | No ataca una causa: **es el instrumento de medida** |
| M9 · Base agronómica | C4 | |
| M10 · Predicción guiada y teoría situada | C1, C2 | |

---

## 7 · Pregunta de investigación e hipótesis

### Pregunta

> ¿En qué medida una aplicación web que devuelve el comportamiento hidráulico de forma inmediata, exige anticipar la consecuencia de cada decisión y escalona el diagnóstico, mejora la **comprensión conceptual** del diseño de tuberías en estudiantes de Ingeniería Agrónoma, frente a la enseñanza tradicional?

### Hipótesis

> Los estudiantes que trabajen con la aplicación obtendrán una ganancia de aprendizaje significativamente mayor que los del grupo de control, **y esa ganancia se concentrará en los niveles de Analizar y Evaluar** —diagnosticar y comparar— y no solamente en Aplicar.

**El segundo tramo es el que la hace interesante.** Si la mejora se concentrara solo en Aplicar, habríamos construido una calculadora rápida. Que se concentre en Analizar y Evaluar es lo que prueba comprensión.

### Hipótesis secundaria, sobre el 3D

> El grupo que use la vista tridimensional superará al que no la use **en los ítems que miden CE5 y CE6, y no necesariamente en los demás**, porque esas dos concepciones solo se pueden confrontar ahí.

Falsable, específica, y ambos resultados son publicables.

---

## 8 · Lo que NO es la solución

Escrito aquí para poder decir que no sin discutirlo dos veces:

- **No es un reemplazo de EPANET.** No competimos en potencia de cálculo: competimos en capacidad de enseñar.
- **No es un reemplazo del docente.** La aplicación diagnostica errores de diseño, no reemplaza la clase.
- **No es una calculadora más rápida.** Si el estudiante sale calculando más rápido pero entendiendo lo mismo, el proyecto falló.
- **No es un sistema de gestión de riego real.** No opera equipos, no monitorea en campo, no toma decisiones agronómicas por nadie.
- **No resuelve redes malladas.** Solo redes abiertas, y esa restricción es la que permite cumplir el tiempo de respuesta.
- **No usa aprendizaje automático.** La IA del proyecto es optimización metaheurística, con función objetivo definida. No hay modelo entrenado con datos, porque no hay dataset ni el problema lo requiere.

---

## 9 · La prueba de enfoque

Cuando aparezca la duda de si algo entra o no, estas cuatro preguntas la resuelven:

1. **¿Qué causa ataca?** Si no se puede señalar una de las seis, no va.
2. **¿Qué concepción errónea ayuda a desmentir?** Si ninguna, probablemente sea una funcionalidad bonita.
3. **¿Deja evidencia medible en el registro?** Si no deja rastro, no aporta a la afirmación de la tesis.
4. **¿Cabe en los sprints comprometidos?** Si no, va al backlog con su prioridad, no al sprint «apretando un poco».

---

## Decisiones abiertas

Ninguna se resuelve programando. La primera hay que tomarla antes del sprint 1.

- [ ] **Alcance contra sprints.** Con cuatro sprints de dos semanas, la vista 3D y la optimización quedan en backlog, y el experimento cae a dos grupos — con lo cual la hipótesis secundaria sobre el 3D no se puede probar y la sección 5 promete algo que no se entrega. Es una decisión de alcance, no un detalle de planificación.
- [ ] **¿Falta una séptima causa?** Buena parte del aula llega al curso sin el razonamiento cuantitativo que la asignatura exige desde el primer día: 43,8 % en nivel de proceso y 9,1 % en significado insuficiente (Ricra, 2023). No es ninguna de las seis —es un déficit previo, no algo que el curso provoque—, pero si entra justifica el diagnóstico escalonado y conecta con Lu y Hu (2025): el subgrupo de menor habilidad previa es el que más mejora con simulación interactiva (21,3 % frente a 8,7 %). Si entra, hay que añadir su fila a la trazabilidad de la sección 6.
- [ ] **Evidencia propia de que el problema existe en la población.** Notas del curso, una entrevista al docente de Hidráulica Aplicada, o un pretest piloto. Sin esto, el jurado puede decir que el problema está supuesto y no documentado.
- [ ] **Parámetros del método de cálculo.** Coeficiente de Hazen-Williams para PVC: `C = 140` o `150`. Y el umbral de éxito de la ganancia normalizada. Ambos se fijan una vez, porque cambiarlos después de ver resultados invalida el estudio.
- [ ] **Referencia exacta** del 13 % del PBI y el 30 % del empleo agrícola (sección 3).

**Lo que ya está cerrado y no se rediscute:** el problema de la sección 1, las seis causas, las siete concepciones erróneas, el método de cálculo de referencia y la regla de trazabilidad de la sección 6.

---

## Versión navegable

Este mismo planteamiento, explicado y con las secciones de antecedentes y estado del arte, está en **[`planteamiento.html`](planteamiento.html)** — ábrelo en el navegador.
