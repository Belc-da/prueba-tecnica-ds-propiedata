**Estado Actual**
A la fecha, se ha conseguido únicamente la  normalización de las Bases A y B e integración de fuentes. Se logró transformar estas dos bases de datos heterogéneas en un único ecosistema de datos de alquileres, estandarizando variables clave como dormitorios, baños, antigüedad y comodidades (dummies de pileta, cochera y balcón). Un paso fundamental aplicado fue la implementación de una lógica de conversión de ARS a USD, que utiliza las cotizaciones mensuales del BCRA para llevar los precios de las Bases A y B a USD según su fecha de publicación, permitiendo así la utilización de la base completa en una "moneda estable". Asimismo, se garantizó la integridad del set unificado mediante la creación de una Clave Primaria (PK) geoespacial, que permitió identificar y excluir registros duplicados entre ambas fuentes.

No obstante, en virtud de falta de tiempo, se ha decidido cerrar la etapa de limpieza. Esto significa que procesos complementarios como la depuración estadística exhaustiva de outliers en la Base B, la imputación algorítmica de registros nulos y la ingesta de la Base C se consideran tareas de refinamiento para futuras iteraciones, asumiendo el dataset actual como la línea base para el modelado.

**Hoja de Ruta Estratégica: De Datos a Predicción**
El plan de acción se estructura ahora sobre cuatro pilares técnicos diseñados para convertir este volumen de datos en una herramienta de estimación de precios de alquiler:

**Refinamiento de Matching y Consistencia**: Se profundizará en la alineación de las features para asegurar que las variables predictoras (como los metros cuadrados o ambientes) mantengan distribuciones coherentes tras la unión, resolviendo posibles sesgos geográficos entre las dos fuentes originales.

**Arquitectura y Feature Store**: El objetivo es automatizar el flujo de pre-procesamiento actual para que la ingesta de nuevos datos sea reproducible, en especial la toma de datos del tipo de cambio del BCRA. Se organizarán las variables en una estructura de entrenamiento-prueba

**Modelado Predictivo Avanzado**:  La fase de entrenamiento se iniciaría evaluando algoritmos de ensamble (XGBoost, CatBoost o LightGBM), que son robustos ante la presencia de los nulos que decidimos conservar. Se aplicará Hyperparameter Tuning y validación cruzada para minimizar el error medio absoluto (MAE), buscando que la predicción del precio del alquiler sea sensible tanto a las características del inmueble como a la temporalidad del mercado.

**Despliegue y MLOps**: Finalmente, se establecerá un marco de trabajo para el seguimiento de experimentos, permitiendo versionar cada modelo generado. El cierre del ciclo será la implementación de una API de inferencia capaz de recibir las coordenadas y dimensiones de una propiedad para devolver, en tiempo real, una valoración de mercado ajustada.
