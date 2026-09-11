# Simulador de Riego Presurizado

Documentación compartida del proyecto de tesis. Todo lo que hay que saber para trabajar sobre lo mismo, ordenado por para qué sirve cada cosa.

**Equipo:** Sosa Colca, Angello Rodolfo · Tongo Alejandro, Milagros Salet
**Programa:** Ingeniería de Software — Universidad Peruana de Ciencias Aplicadas

> Los archivos `.html` se abren en cualquier navegador. No hace falta instalar nada: descarga el archivo y ábrelo con doble clic, o usa la vista previa de GitHub.

---

## Cómo está organizado

| Carpeta | Qué contiene | Cuándo se usa |
|---|---|---|
| [`diagramas/`](diagramas) | Lo que se ve de un vistazo y se lleva a una diapositiva | Para presentar y explicar |
| [`documentos/`](documentos) | Lo que se lee de principio a fin | Para decidir y para sustentar |
| [`gestion/`](gestion) | Lo que se administra durante el desarrollo | Para planificar cada sprint |

---

## `diagramas/`

| Archivo | Qué muestra |
|---|---|
| **[diagrama-logico.html](diagramas/diagrama-logico.html)** | Las cinco capas de la aplicación, dónde se ejecuta cada una, la frontera de confianza, cómo se calcula y cómo se protege. Es el diagrama para la sustentación. |
| [diagrama-funcionalidad.json](diagramas/diagrama-funcionalidad.json) | La especificación del diagrama de funcionalidad: qué dice cada paso, su concepto pedagógico y cómo debe graficarse. |

## `documentos/`

| Archivo | De qué trata |
|---|---|
| **[planteamiento.html](documentos/planteamiento.html)** | El norte del proyecto: el problema, las seis causas, las consecuencias, la solución 2D/3D/IA, la trazabilidad, la pregunta y las hipótesis, y la evidencia que respalda cada parte. **Léelo antes de cada sprint.** |
| [planteamiento.md](documentos/planteamiento.md) | El mismo planteamiento en texto, para revisar rápido o citar. |
| [arquitectura.html](documentos/arquitectura.html) | La arquitectura explicada: las capas, el recorrido del estudiante y el del docente, y las once decisiones de diseño con lo que cuesta cada una. |
| [stack.html](documentos/stack.html) | Con qué se construye y dónde vive: el reparto entre Render y Railway, la estructura del repositorio, los riesgos del despliegue y el costo mensual. |
| [optimizacion-ia.html](documentos/optimizacion-ia.html) | Cómo funciona el módulo de optimización: qué se optimiza, con qué algoritmo, qué tecnología usa y de dónde sale la explicación de cada cambio. |
| [flujo-de-la-app.md](documentos/flujo-de-la-app.md) | El recorrido completo de la aplicación paso a paso, con las reglas del sistema y el registro de decisiones. |

## `gestion/`

| Archivo | Para qué |
|---|---|
| [product-backlog.xlsx](gestion/product-backlog.xlsx) | 30 historias de usuario repartidas en 4 sprints de dos semanas, cada una con sus criterios de aceptación. |

---

## La regla que ordena todo

Si una historia, una pantalla o una decisión técnica no se puede conectar con alguna de las **seis causas** del planteamiento, no entra al sprint. Es la única regla que protege el enfoque durante los meses que vienen.

## Lo que está decidido y lo que no

Lo cerrado —el problema, las seis causas, las siete concepciones erróneas, el método de cálculo y la regla de trazabilidad— no se rediscute.

Lo abierto está al final del planteamiento, en **Decisiones abiertas**. La primera hay que tomarla antes del sprint 1.
