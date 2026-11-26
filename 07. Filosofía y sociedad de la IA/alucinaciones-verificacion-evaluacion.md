# Alucinaciones, verificación y evaluación de respuestas

**Supuestos de trabajo.** Público universitario y autodidacta, nivel introductorio-intermedio; conocimientos básicos de informática y alfabetización digital. Disciplina: inteligencia artificial y estudios sociotécnicos y educación. Contexto académico y aplicado. Unidad modular de extensión media.

## Fundamentación conceptual

Una alucinación es una salida generada que presenta contenido no respaldado o incompatible con los hechos o la evidencia pertinente. La terminología varía: una respuesta puede ser fiel a un documento equivocado, correcta sin evidencia explícita, o falsa pese a citar una fuente. En una tarea creativa, inventar no constituye necesariamente un error; importa el contrato de la tarea.

Los modelos de lenguaje optimizan objetivos estadísticos que no equivalen a una garantía de verdad. La ambigüedad, los datos insuficientes, la recuperación defectuosa y la presión por completar una respuesta pueden producir afirmaciones injustificadas. La confianza verbal no es una medida calibrada de certeza. El problema es epistemológico y técnico: distinguir qué se afirma, cómo se conoce y con qué evidencia se sostiene.

Verificar consiste en contrastar afirmaciones con evidencia pertinente e independiente cuando sea posible. Evaluar implica definir criterios para comparar resultados según la tarea: exactitud, fidelidad, cobertura, utilidad, seguridad o reproducibilidad. La abstención explícita puede ser preferible a completar información sin respaldo.

## Formalización del conocimiento

Representemos una respuesta como un conjunto de afirmaciones verificables $C=\{c_1,\ldots,c_n\}$. Cada afirmación recibe una etiqueta de evidencia: respaldada (B), contradicha (X), insuficiente (I). Para n>0:

$$F_B=\frac{|B|}{n},\qquad F_X=\frac{|X|}{n},\qquad F_I=\frac{|I|}{n}.$$

Las categorías son mutuamente excluyentes bajo un protocolo definido. No son medidas universales de verdad; dependen de las fuentes y del criterio de anotación. La cobertura se calcula aparte respecto de los hechos requeridos por la tarea. Para respuestas sin afirmaciones verificables, las fracciones no se definen.

## Ejemplos e instancias

Caso hipotético. Un registro comunitario fechado indica que un taller tuvo 20 participantes y ocurrió el 5 de marzo. No indica presupuesto.

| Afirmación generada | Etiqueta | Motivo |
|---|---|---|
| Participaron 20 personas | B | Coincide con registro |
| Ocurrió el 6 de marzo | X | Fecha incompatible |
| Costó 500 dólares | I | No hay dato de costo |

Cada fracción vale 1/3. Si se corrige la fecha y se expresa que el costo no consta, las dos afirmaciones fácticas quedan respaldadas. Sin embargo, la evaluación debe comprobar también que se respondió a la pregunta original y que el registro es confiable.

Para reproducir el experimento, dos personas pueden etiquetar independientemente respuestas a partir de un corpus fijo, registrar desacuerdos y adjudicarlos con criterios publicados.

## Espacio de posibilidades

| Elemento | Modificación | Restricción | Consecuencia |
|---|---|---|---|
| Evidencia | Agregar fuentes primarias | Registrar fecha y procedencia | Puede resolver incertidumbre |
| Unidad | Afirmación atómica o compuesta | Protocolo consistente | Cambia denominador |
| Tarea | Resumen o pregunta abierta | Definir resultado esperado | Cambian criterios |
| Abstención | Ajustar política | No ocultar hechos conocidos | Cambia cobertura y riesgo |

## Activadores generativos

- Construir un tablero de auditoría de respuestas con citas y etiquetas de respaldo. Usar un corpus verificable y separar evaluación de generación. ¿Cuánto cambia la puntuación según el anotador?
- Diseñar un banco de preguntas contestables y no contestables sobre un documento, con distractores y versiones incompatibles. Comparar sistemas por exactitud, cobertura y abstención. ¿Cuál es el costo de un falso positivo?
- Crear un asistente que proponga comprobaciones de afirmaciones y registre evidencia sin asignarse autoridad final. ¿Cómo detectar una cita que no respalda el texto?

## Validación de las construcciones

Incluir casos sin evidencia, evidencia contradictoria, citas inexistentes y afirmaciones compuestas. Comprobar que las etiquetas sumen n, documentar desacuerdos y conservar ejemplos de error. No usar al mismo generador como único juez. En asuntos de alto impacto exigir revisión experta y fuentes apropiadas.

## Reflexión sobre el aprendizaje

¿Qué confundí con evidencia? ¿Qué errores pasaron inadvertidos por la fluidez? ¿Cómo cambiaría mi criterio de aceptación según las consecuencias?

## Conexiones con otros conocimientos

- [Tokens, contexto y generación de respuestas](../05.%20%20Agentes%20y%20sistemas%20inteligentes/tokens-contexto-generacion.md)
- [Modelos multimodales](../05.%20%20Agentes%20y%20sistemas%20inteligentes/modelos-multimodales.md)
- [Generación, búsqueda y razonamiento](../05.%20%20Agentes%20y%20sistemas%20inteligentes/generacion-busqueda-razonamiento.md)
- [La IA como herramienta cognitiva](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/ia-herramienta-cognitiva.md)
- [Apropiación comunitaria, autonomía y construcción colectiva de conocimiento](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/apropiacion-comunitaria-conocimiento.md)

## Referencias

[Survey of Hallucination in Natural Language Generation](https://doi.org/10.1145/3571730); [FActScore](https://arxiv.org/abs/2305.14251).

Este contenido puede ampliarse mediante contribuciones que incluyan procedencia, condiciones de reproducción, evidencia de validación y registro de cambios.
