# Modelos multimodales

**Supuestos de trabajo.** Público universitario y autodidacta, nivel introductorio-intermedio; conocimientos básicos de informática y alfabetización digital. Disciplina: inteligencia artificial y sistemas computacionales. Contexto académico y aplicado. Unidad modular de extensión media.

## Fundamentación conceptual

Una modalidad es una forma de representación de información, como texto, imagen, audio o series temporales. Un sistema multimodal procesa o relaciona más de una modalidad; puede aceptar imágenes y producir texto sin ser capaz de generar imágenes. Conviene distinguir modalidades de entrada, salida y tareas admitidas.

Las modalidades poseen estructuras distintas. Una imagen contiene relaciones espaciales, el audio relaciones temporales y el texto secuencias de símbolos. Los codificadores transforman estas señales en representaciones que pueden relacionarse mediante espacios vectoriales compartidos, atención cruzada u otras formas de fusión. Un modelo contrastivo puede aprender a aproximar imágenes y textos correspondientes; uno generativo puede producir una descripción condicionada por una imagen. Estas capacidades no son equivalentes.

El alineamiento entre modalidades es imperfecto. Una descripción plausible puede omitir objetos o inventar atributos; una imagen no establece por sí sola causa, identidad o intención. La resolución, el ruido, la distribución de entrenamiento y la accesibilidad de las señales afectan el desempeño.

## Formalización del conocimiento

Para modalidades A y B, sean $f_A(a)$ y $f_B(b)$ codificadores. Si producen vectores no nulos de igual dimensión, se puede calcular similitud coseno:

$$s(a,b)=\frac{f_A(a)\cdot f_B(b)}{\|f_A(a)\|\|f_B(b)\|}.$$

La recuperación selecciona candidatos con mayor similitud; la generación condicional modela $P(y\mid a,b)$. La similitud no es una probabilidad de verdad. En fusión temprana se combinan representaciones antes de la decisión; en fusión tardía se combinan predicciones. Ambas requieren una política para señales ausentes o contradictorias.

## Ejemplos e instancias

Ejemplo sintético en Python 3, sin dependencias. Se representan color rojo y forma circular mediante dos dimensiones inventadas, no embeddings reales.

```python
from math import sqrt

def cosine(a, b):
    na = sqrt(sum(x*x for x in a))
    nb = sqrt(sum(x*x for x in b))
    assert len(a) == len(b) and na and nb
    return sum(x*y for x,y in zip(a,b))/(na*nb)

image = [1, 1]
captions = {"rojo circular": [1,1], "rojo": [1,0],
            "sin rasgos coincidentes": [-1,-1]}
print(sorted(captions, key=lambda k: cosine(image,captions[k]),
             reverse=True))
```

Resultado esperado: rojo circular primero, rojo segundo y sin rasgos coincidentes al final. En un experimento real, utilizar fotografías de objetos propios, descripciones verificadas y distractores con atributos intercambiados. Separar ejemplos de ajuste y evaluación.

## Espacio de posibilidades

| Elemento | Modificación | Restricción | Consecuencia |
|---|---|---|---|
| Modalidad | Agregar audio o sensores | Sincronización y consentimiento | Evidencia complementaria |
| Fusión | Temprana o tardía | Representaciones compatibles | Diferente robustez |
| Datos | Introducir ruido u oclusiones | Conservar referencia original | Medición de sensibilidad |
| Salida | Texto, clasificación o recuperación | Capacidad real del sistema | Artefactos distintos |

## Activadores generativos

- Construir un buscador de imágenes de objetos mediante descripciones textuales. Explorar distractores, similitud y umbrales; usar imágenes autorizadas y registrar los fallos. ¿Qué atributos son difíciles de recuperar?
- Diseñar un asistente para interpretar fotografías de un circuito junto con lecturas de sensores. Construir una interfaz que marque discrepancias y solicite datos faltantes; no controlar dispositivos sin validación. ¿Qué modalidad aporta evidencia decisiva?
- Crear una evaluación de accesibilidad de descripciones de imágenes con usuarios voluntarios y criterios explícitos, sin inferir atributos personales. ¿Qué detalles son necesarios para distintos propósitos?

## Validación de las construcciones

Comprobar dimensiones, normas no nulas y simetría del coseno. En recuperación medir aciertos entre los primeros k candidatos sobre un conjunto etiquetado. En descripción evaluar atributos correctos, omitidos e inventados. Probar señales ausentes y contradictorias; no asumir que más modalidades siempre mejoran resultados.

## Reflexión sobre el aprendizaje

¿Qué información se perdió al codificar? ¿Cómo se resolvió una contradicción? ¿Qué resultados dependen de la calidad de los datos?

## Conexiones con otros conocimientos

- [Tokens, contexto y generación de respuestas](../05.%20%20Agentes%20y%20sistemas%20inteligentes/tokens-contexto-generacion.md)
- [Generación, búsqueda y razonamiento](../05.%20%20Agentes%20y%20sistemas%20inteligentes/generacion-busqueda-razonamiento.md)
- [Alucinaciones, verificación y evaluación de respuestas](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/alucinaciones-verificacion-evaluacion.md)
- [La IA como herramienta cognitiva](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/ia-herramienta-cognitiva.md)
- [Apropiación comunitaria, autonomía y construcción colectiva de conocimiento](../07.%20Filosof%C3%ADa%20y%20sociedad%20de%20la%20IA/apropiacion-comunitaria-conocimiento.md)

## Referencias

[Learning Transferable Visual Models From Natural Language Supervision](https://arxiv.org/abs/2103.00020); [Flamingo: a Visual Language Model for Few-Shot Learning](https://arxiv.org/abs/2204.14198).

Este contenido puede ampliarse mediante contribuciones que incluyan procedencia, condiciones de reproducción, evidencia de validación y registro de cambios.
