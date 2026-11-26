# Tokens, contexto y generación de respuestas

**Supuestos de trabajo.** Público universitario y autodidacta, nivel introductorio-intermedio; conocimientos básicos de informática y alfabetización digital. Disciplina: inteligencia artificial y sistemas computacionales. Contexto académico y aplicado. Unidad modular de extensión media.

## Fundamentación conceptual

Un modelo de lenguaje autorregresivo aprende regularidades de secuencias de símbolos. Un token es una unidad discreta de su vocabulario, que puede representar una palabra, una parte de ella, un signo o bytes. La tokenización no equivale a separar palabras: depende del vocabulario y del algoritmo empleado. El identificador de un token se transforma en una representación vectorial, no en una definición semántica fija.

El contexto es la secuencia disponible para condicionar la generación. Puede incluir instrucciones, conversación, documentos recuperados y resultados de herramientas. La ventana de contexto limita la cantidad de información procesable en una llamada; no equivale a memoria persistente ni garantiza que toda la información sea utilizada correctamente. Los parámetros aprendidos son distintos del contexto suministrado durante la inferencia. Incorporar un documento al contexto normalmente no modifica los parámetros.

En un modelo autorregresivo, cada nuevo token se condiciona en los anteriores. Un mecanismo de atención permite relacionar posiciones de la secuencia; no implica atención consciente. El proceso termina por una condición de parada, un token especial o un límite. La salida puede variar aunque la entrada sea idéntica.

## Formalización del conocimiento

Sea T un tokenizador, x=T(texto) una secuencia y V el vocabulario. El modelo asigna probabilidades:

$$P(y\mid x)=\prod_{i=1}^{m}P(y_i\mid x,y_{<i}).$$

Dados logits $z_j$, la distribución con temperatura $\tau>0$ es $p_j=\exp(z_j/\tau)/\sum_k\exp(z_k/\tau)$. Una temperatura menor concentra la distribución; no garantiza veracidad. La selección voraz elige el máximo; el muestreo selecciona según probabilidades. En un modelo simplificado con ventana compartida de tamaño C, debe cumplirse $|x|+m\le C$. Los límites reales dependen de la implementación.

## Ejemplos e instancias

El siguiente programa de Python 3 simula la selección del próximo token mediante logits ficticios. No es un modelo entrenado. Entrada: temperatura y semilla. Salida: frecuencias en 1000 muestras.

```python
import math
import random

def sample_counts(tau, seed=7, n=1000):
    assert tau > 0 and n > 0
    tokens = ["agua", "luz", "suelo"]
    logits = [2.0, 1.0, 0.0]
    weights = [math.exp((z-max(logits))/tau) for z in logits]
    draws = random.Random(seed).choices(tokens, weights=weights, k=n)
    return {t: draws.count(t) for t in tokens}

for t in (0.2, 1.0, 3.0):
    print(t, sample_counts(t))
```

Se espera que a temperatura 0.2 predomine agua y que a 3.0 las frecuencias sean más equilibradas. Otro experimento consiste en presentar a un modelo una pregunta sobre un código ficticio, primero sin su definición y luego con ella; registrar las diferencias sin confundir una coincidencia con aprendizaje permanente.

## Espacio de posibilidades

| Elemento | Modificación | Restricción | Consecuencia potencial |
|---|---|---|---|
| Tokenizador | Comparar idiomas y vocabularios | Registrar el algoritmo | Diferente longitud y segmentación |
| Temperatura | Variar la concentración | Positiva en la fórmula | Diversidad variable |
| Contexto | Cambiar orden y evidencia | Respetar ventana y privacidad | Respuestas distintas |
| Parada | Cambiar presupuesto de salida | Límite del sistema | Mayor o menor completitud |

## Activadores generativos

- Construir un explorador de tokenización y presupuesto de contexto con textos propios en varios idiomas. Usar secuencias, vocabulario y límites; comparar segmentaciones y visualizar costos relativos sin asumir equivalencia palabra-token. ¿Qué textos son más costosos de representar?
- Diseñar un simulador de generación con distribuciones configurables y comparar estrategias de selección. El artefacto debe distinguir logits ficticios de un modelo entrenado. ¿Cuándo sacrificar diversidad por estabilidad?
- Investigar cómo cambia la respuesta al mover evidencia relevante dentro de documentos sintéticos. Mantener pregunta y modelo constantes, registrar condiciones y formular hipótesis sobre uso del contexto.

## Validación de las construcciones

Verificar que las frecuencias sumen n, que las probabilidades normalizadas sumen uno y que la misma semilla reproduzca el ejemplo. Comparar varias semillas. Para pruebas con modelos reales, registrar versión, configuración y entrada; no inferir comprensión a partir de fluidez. Casos límite: contexto vacío, evidencia contradictoria y presupuesto insuficiente.

## Reflexión sobre el aprendizaje

¿Qué información estaba en los parámetros y cuál fue aportada? ¿Qué decisión delegué al modelo? ¿Cómo distinguiría diversidad de error factual?

## Conexiones con otros conocimientos

- [Modelos multimodales](../05.%20%20Agentes%20y%20sistemas%20inteligentes/modelos-multimodales.md)
- [Generación, búsqueda y razonamiento](../05.%20%20Agentes%20y%20sistemas%20inteligentes/generacion-busqueda-razonamiento.md)
- [Alucinaciones, verificación y evaluación de respuestas](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/alucinaciones-verificacion-evaluacion.md)
- [La IA como herramienta cognitiva](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/ia-herramienta-cognitiva.md)
- [Apropiación comunitaria, autonomía y construcción colectiva de conocimiento](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/apropiacion-comunitaria-conocimiento.md)

## Referencias

[Attention Is All You Need](https://arxiv.org/abs/1706.03762); [Neural Machine Translation of Rare Words with Subword Units](https://arxiv.org/abs/1508.07909).

Este contenido puede ampliarse mediante contribuciones que incluyan procedencia, condiciones de reproducción, evidencia de validación y registro de cambios.
