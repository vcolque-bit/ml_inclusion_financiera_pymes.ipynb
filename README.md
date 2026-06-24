# Machine Learning e inclusión financiera PYME

Este repositorio contiene un ejercicio exploratorio de Machine Learning aplicado a evaluación crediticia de pequeñas empresas.

La idea central es comparar un modelo lineal, como una regresión logística, con un modelo no lineal, en este caso Random Forest, para analizar si este último puede identificar empresas de bajo riesgo que podrían quedar fuera de una evaluación más tradicional.

El foco del análisis está en empresas jóvenes, ya que suelen tener menos historial financiero, menor disponibilidad de garantías y más dificultad para ser evaluadas por modelos tradicionales de scoring.

## Motivación

Las PyMEs cumplen un rol importante en la economía, pero muchas veces son un segmento difícil de evaluar crediticiamente. Esto es especialmente relevante en empresas nuevas o con poco historial, donde la falta de información puede terminar limitando el acceso a financiamiento.

Este ejercicio busca mostrar, de forma simple y aplicada, cómo modelos de Machine Learning pueden complementar enfoques tradicionales de riesgo, no para reemplazar el criterio financiero, sino para ampliar la capacidad de análisis.

## Datos y metodología

El análisis utiliza datos públicos del programa SBA 7(a) de Estados Unidos.

El target se define como:

* `default = 1`: préstamo dado de baja por pérdida (`CHGOFF`)
* `default = 0`: préstamo pagado completamente (`P I F`)

Se utiliza una separación temporal entre entrenamiento y test para reducir riesgo de data leakage:

* Entrenamiento: operaciones hasta 2017
* Test: operaciones desde 2018

Modelos comparados:

* Regresión logística
* Random Forest

Métrica principal:

* AUC-ROC

Además, se analiza un grupo de empresas jóvenes para observar diferencias entre ambos modelos al seleccionar clientes de menor riesgo.

## Resultados principales

| Modelo              | AUC    |
| ------------------- | ------ |
| Regresión logística | 0.8389 |
| Random Forest       | 0.8863 |

En el ejercicio, Random Forest obtiene una mayor capacidad de discriminación que la regresión logística.

Además, al comparar empresas jóvenes seleccionadas bajo un mismo volumen, el modelo no lineal logra identificar un grupo con menor default observado que el modelo lineal.

Esto sugiere que, al menos en este experimento, existen casos donde un modelo más flexible puede reconocer patrones de bajo riesgo que un enfoque lineal no captura con la misma precisión.

## Gráfico principal

El gráfico muestra las diferencias de selección entre ambos modelos para empresas jóvenes.

* Eje X: score de riesgo de la regresión logística
* Eje Y: score de riesgo de Random Forest
* Grupo “Solo Random Forest”: empresas que el modelo no lineal considera de bajo riesgo, pero que el modelo lineal no selecciona
* Grupo “Solo Logit”: empresas seleccionadas por la regresión logística, pero no por Random Forest

## Cómo ejecutar el notebook

```bash
git clone https://github.com/vcolque-bit/ml_inclusion_financiera_pymes.ipynb.git
cd ml_inclusion_financiera_pymes.ipynb
pip install -r requirements.txt
jupyter notebook ml_inclusion_financiera_pymes.ipynb
```

El dataset no se incluye en el repositorio por tamaño. Debe descargarse desde la fuente pública de SBA 7(a) y guardarse en la carpeta `data/`.

## Estructura sugerida

```text
ml_inclusion_financiera_pymes.ipynb/
├── README.md
├── ml_inclusion_financiera_pymes.ipynb
├── requirements.txt
├── figures/
│   └── desacuerdo_modelos_empresas_jovenes.png
└── data/
    └── .gitkeep
```

## Limitaciones

Este análisis es exploratorio y tiene varias limitaciones:

* Los datos corresponden al mercado de Estados Unidos, por lo que no son directamente extrapolables a Chile u otros países.
* El score del modelo se interpreta como ranking de riesgo, no como una probabilidad de default calibrada.
* El modelo no considera todos los factores que serían necesarios en una evaluación crediticia real.
* Los resultados no representan una política de crédito ni un modelo listo para producción.

## Disclaimer

Este repositorio tiene fines educativos y exploratorios. No constituye una recomendación crediticia, una evaluación formal de riesgo ni una propuesta de implementación productiva.

## Autor

Víctor Colque Shields
LinkedIn: https://www.linkedin.com/in/victorcolqueshields
GitHub: https://github.com/vcolque-bit
