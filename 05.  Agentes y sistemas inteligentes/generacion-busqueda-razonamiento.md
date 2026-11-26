# Generación, búsqueda y razonamiento

**Supuestos de trabajo.** Público universitario y autodidacta, nivel introductorio-intermedio; conocimientos básicos de informática y alfabetización digital. Disciplina: inteligencia artificial y sistemas computacionales. Contexto académico y aplicado. Unidad modular de extensión media.

## Fundamentación conceptual

La generación construye una salida a partir de una representación y unas condiciones. La búsqueda explora candidatos en un espacio, por ejemplo documentos indexados o estados de un problema. El razonamiento establece relaciones inferenciales entre premisas y conclusiones, aplica restricciones o compara consecuencias. Son funciones distintas que pueden coexistir dentro de un sistema.

Un modelo de lenguaje puede producir una explicación sin consultar fuentes externas. Un buscador puede localizar un documento sin determinar si sus afirmaciones son verdaderas. Un algoritmo de deducción puede establecer una conclusión válida respecto de premisas dadas sin garantizar que estas sean verdaderas en el mundo. La generación de una cadena de explicaciones no demuestra que el mecanismo interno haya seguido ese razonamiento.

Un sistema de generación aumentada por recuperación (RAG) incorpora evidencia recuperada al contexto del generador. Un agente puede además invocar herramientas, verificar restricciones y revisar resultados. La calidad depende de las interfaces entre funciones, no solamente del modelo de lenguaje.

## Formalización del conocimiento

Sea q una consulta, D un conjunto de documentos y s una función de relevancia. La búsqueda recupera $R_k(q)=\operatorname{top}_k\{s(q,d):d\in D\}$. El generador produce $y\sim P_\theta(y\mid q,R_k(q))$. Una inferencia deductiva se representa como $\Gamma\vdash\phi$, donde $\Gamma$ es el conjunto de premisas y $\phi$ la conclusión derivable según reglas explícitas.

En búsqueda de estados se especifican estado inicial, acciones, transición, meta y costo. El razonamiento puede utilizar búsqueda para encontrar una demostración; las categorías son funciones, no compartimentos excluyentes.

## Ejemplos e instancias

Ejemplo reproducible de cierre de reglas proposicionales simples en Python 3. Entrada: hechos y reglas con antecedentes conjuntivos. Salida: hechos derivables.

```python
def closure(facts, rules):
    facts = set(facts)
    while True:
        new = {head for body, head in rules if set(body) <= facts}
        if new <= facts:
            return facts
        facts |= new

rules = [(["lluvia"], "suelo_mojado"),
         (["suelo_mojado", "pendiente"], "riesgo")]
result = closure(["lluvia", "pendiente"], rules)
assert "riesgo" in result
assert "inundacion" not in result
print(sorted(result))
```

Las reglas son hipotéticas, no leyes hidrológicas. Un buscador podría recuperar observaciones de lluvia y un generador explicar la derivación. El cierre garantiza solamente lo derivable bajo las reglas suministradas.

## Espacio de posibilidades

| Elemento | Modificación | Restricción | Consecuencia |
|---|---|---|---|
| Índice | Léxico o vectorial | Corpus definido | Cambia relevancia |
| Reglas | Agregar antecedentes | Semántica explícita | Cambia derivabilidad |
| Generador | Cambiar contexto | Evidencia trazable | Variación de explicación |
| Verificador | Pruebas o restricciones | Criterios independientes | Detecta fallos |

## Activadores generativos

- Construir un sistema de preguntas sobre un pequeño repositorio de documentos con recuperación y citas. Comparar respuestas con y sin evidencia y medir recuperación. ¿Cuándo debe abstenerse?
- Diseñar un planificador de rutas en un grafo con costos y restricciones, integrando un generador para explicar rutas. Verificar costos por separado. ¿Qué cambia si se elimina una arista?
- Construir una interfaz que clasifique afirmaciones como recuperadas, inferidas o generadas y conserve sus dependencias. ¿Puede una afirmación pertenecer a varias categorías?

## Validación de las construcciones

Probar reglas cíclicas, ausencia de hechos y antecedentes incompletos; el cierre debe terminar con un conjunto finito. Evaluar recuperación, fidelidad de citas y validez inferencial por separado. Un texto convincente no sustituye una prueba, y una cita no garantiza que la fuente respalde la afirmación.

## Reflexión sobre el aprendizaje

¿Qué parte de mi construcción recuperó, generó o infirió información? ¿Qué evidencia cambiaría la conclusión? ¿Qué decisiones requieren revisión humana?

## Conexiones con otros conocimientos

- [Tokens, contexto y generación de respuestas](../05.%20%20Agentes%20y%20sistemas%20inteligentes/tokens-contexto-generacion.md)
- [Modelos multimodales](../05.%20%20Agentes%20y%20sistemas%20inteligentes/modelos-multimodales.md)
- [Alucinaciones, verificación y evaluación de respuestas](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/alucinaciones-verificacion-evaluacion.md)
- [La IA como herramienta cognitiva](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/ia-herramienta-cognitiva.md)
- [Apropiación comunitaria, autonomía y construcción colectiva de conocimiento](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/apropiacion-comunitaria-conocimiento.md)

## Referencias

[Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401); [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629).

Este contenido puede ampliarse mediante contribuciones que incluyan procedencia, condiciones de reproducción, evidencia de validación y registro de cambios.
