# Actividad 0. Equipos, ideas de producto y repositorio

**Estado del proyecto:** Exploración de ideas
**Repositorio:** [enlace al repositorio](https://github.com/lesliemosquera96-netizen/TFM_Evolve])

---

## 1. Composición del equipo

| Integrante | Usuario de GitHub |
|---|---|
| Leslie Mosquera | [@lesliemosquera96-netizen](https://github.com/lesliemosquera96-netizen) |
| Carlos | [@hijonario](https://github.com/hijonario) |
| Antonio | [@AntorioH](https://github.com/AntorioH) |

**Organización del equipo.** Todos los integrantes participarán en todas las fases del proyecto y conocerán el producto completo. Para cada actividad se asignará una persona responsable de coordinar la entrega y revisar que la documentación del repositorio esté actualizada.

---

## 2. Resumen de las propuestas

| | Idea 1. DermaVision | Idea 2. App para gestionar un viaje con IA | Idea 3. Optimización energética y mantenimiento predictivo |
|---|---|---|---|
| **Usuario** | Adultos que compran productos de cuidado facial sin saber qué necesita su piel | Personas que organizan un viaje individual o en grupo | Ingenieros de planta y personal de mantenimiento industrial |
| **Problema** | No saben interpretar las imperfecciones de su piel ni qué cuidado elegir | La información está repartida en muchas herramientas y combinar los gustos del grupo lleva mucho tiempo | Las lecturas de los sensores no se aprovechan y las ineficiencias y fallos se detectan tarde |
| **Producto** | Aplicación web que detecta imperfecciones faciales en una foto y da recomendaciones de cuidado | Aplicación en la que la IA genera y adapta un plan de viaje completo conversando con el usuario | Plataforma con predicción de consumo, detección de anomalías, asistente RAG y cuadros de mando |
| **Datos principales** | Imágenes faciales con imperfecciones anotadas (Roboflow, ACNE04) | Google Maps o Mapbox, Open-Meteo, APIs turísticas, guías de viaje | Steel Industry Energy Consumption (UCI) y manuales de mantenimiento |
| **Estado de los datos** | Parcialmente confirmado | Hipótesis (APIs sin probar) | Confirmado (dataset principal); manuales por seleccionar |
| **Principal riesgo** | Datos desbalanceados y de varias fuentes; fiabilidad de la detección | Acceso a precios y disponibilidad reales mediante APIs externas | Validar las anomalías sin registros de fallos reales |

---

## 3. Idea 1. DermaVision: análisis de imperfecciones faciales y recomendaciones de cuidado

### 3.1 Título y descripción

DermaVision es una aplicación web que analiza una fotografía del rostro y detecta imperfecciones visibles de la piel, como acné, manchas u ojeras. El sistema marca en la imagen dónde se encuentra cada imperfección y, a partir del resultado, genera recomendaciones orientativas de cuidado: qué tipo de producto o ingrediente puede ayudar y cuándo conviene consultar a un profesional. Además, guarda cada análisis en un historial para que el usuario pueda consultarlo más adelante.

### 3.2 Problema y usuario

**Usuario.** Adultos que compran productos de cuidado facial por su cuenta (en farmacia, parafarmacia, perfumería o tiendas online) y no tienen claro qué necesita su piel.

**Necesidad.** Identificar qué imperfecciones tienen y qué tipo de cuidado les conviene, para elegir productos con criterio.

**Solución actual.** Se miran al espejo y buscan información en internet, redes sociales o recomendaciones de conocidos. En algunos casos piden consejo en el mostrador de la farmacia, que depende del tiempo y la formación del personal. Algunas marcas cosméticas ofrecen herramientas de diagnóstico, pero están ligadas a su propio catálogo. La consulta dermatológica suele reservarse para problemas más serios y tiene coste o tiempos de espera.

**Dificultad.** El usuario no sabe interpretar los signos que ve en su piel ni relacionarlos con un tipo de cuidado. Como resultado, compra por prueba y error, gasta dinero en productos que no corresponden a su necesidad o recibe recomendaciones poco neutrales.

**Mejora propuesta.** Un análisis automático que identifica las imperfecciones visibles y las traduce en recomendaciones claras y neutrales, basadas en tipos de producto e ingredientes y no en marcas concretas.

**Usuario secundario.** Farmacias y tiendas cosméticas, que podrían usar la herramienta como apoyo en una primera consulta con el cliente. Este uso se plantea como ampliación y no forma parte del MVP.

**Job to be done.** *Cuando noto algo en mi piel que no me gusta y voy a comprar un producto, quiero entender qué tengo y qué tipo de cuidado me conviene, para no gastar dinero en productos que no me sirven.*

**Estado de la evidencia.** El problema y el usuario son, por ahora, hipótesis del equipo basadas en la observación de nuestro entorno. Todavía no los hemos contrastado con usuarios reales (ver apartado 3.6).

### 3.3 Uso y valor

**Situación de uso.** Marta tiene 28 años y quiere comprar un sérum, pero no sabe cuál elegir. Antes de ir a la farmacia se hace una foto con el móvil y la sube a la aplicación. En primer lugar, el sistema comprueba que la imagen es válida (rostro frontal, nitidez e iluminación suficientes). Después le muestra la foto con las imperfecciones marcadas: manchas en las mejillas, algunas lesiones de acné en el mentón y ojeras. Finalmente, para cada una recibe una explicación breve y una recomendación general, por ejemplo, el uso diario de protector solar para las manchas o un limpiador suave para el acné, junto con los casos en los que debería consultar a un dermatólogo.

**Valor.** Marta llega a la farmacia sabiendo qué necesita su piel y qué tipo de producto buscar. De esta forma, evita compras por prueba y error y puede hacer preguntas más concretas al personal de la farmacia.

**Hipótesis de valor.** Un análisis visual con recomendaciones explicadas ayuda al usuario a elegir productos de cuidado facial con más seguridad que buscando información por su cuenta.

La aplicación ofrece información orientativa y lo indica de forma explícita. No realiza diagnósticos ni sustituye la evaluación de un dermatólogo.

### 3.4 Datos

**Información necesaria.** En primer lugar, imágenes faciales con las imperfecciones anotadas (tipo y posición de cada una) para entrenar el modelo de detección. En segundo lugar, una base de recomendaciones de cuidado por tipo de imperfección, elaborada a partir de fuentes fiables.

| Fuente | Contenido | Estado del acceso | Condiciones de uso y restricciones |
|---|---|---|---|
| [Skin Problem Detection Multiple Clean v2](https://universe.roboflow.com/parin-kittipongdaja-vwmn3/skin-problem-detection-multiple-clean) (Roboflow Universe) | 4.717 imágenes faciales de 640×640 px con 9 clases anotadas: acné, ojeras, manchas, piel seca, piel normal, piel grasa, poros, rojeces y arrugas | **Confirmado.** Descarga y revisión inicial realizadas | Revisar la licencia del proyecto. Desbalance fuerte: el acné concentra la mayoría de anotaciones |
| [face_skin_condition](https://universe.roboflow.com/muhammad-rifqi-maruf/face_skin_condition) (Roboflow Universe) | Imágenes faciales anotadas con acné, piel seca, grasa, normal y arrugas | **Confirmado.** Descarga realizada mediante la API de Roboflow | Revisar la licencia del proyecto |
| [dark_circle](https://universe.roboflow.com/buyume-ahuro/dark_circle) (Roboflow Universe) | Imágenes con ojeras, bolsas, manchas y arrugas anotadas | **Confirmado.** Descarga realizada | Revisar la licencia del proyecto |
| [DarkSpot](https://universe.roboflow.com/skinanalysisv22025/darkspot-jpnki) (Roboflow Universe) | Imágenes con manchas oscuras anotadas | **Confirmado.** Descarga realizada | Revisar la licencia del proyecto |
| [ACNE04](https://github.com/xpwu95/ldl) (Wu et al., ICCV 2019) | 1.457 imágenes faciales con 18.983 lesiones de acné anotadas por especialistas | **Hipótesis.** Pendiente de descarga | Publicado para investigación; confirmar condiciones de uso |
| Guías de cuidado de la piel de sociedades dermatológicas | Recomendaciones generales por tipo de imperfección | **Hipótesis.** Fuentes por seleccionar | Revisar condiciones de reutilización del contenido |
| Fotografías de voluntarios | Pequeño conjunto de fotos para probar la aplicación en condiciones reales | **Hipótesis.** Pendiente de recoger | Solo con consentimiento explícito; no se publicarán en el repositorio |

**Calidad de los datos.** Los datasets de Roboflow proceden de autores distintos, por lo que cada uno puede usar criterios de anotación diferentes. Además, algunas clases tienen muy pocos ejemplos. Por este motivo, antes de combinarlos será necesario revisar una muestra de cada fuente y unificar la definición de cada clase.

**Privacidad.** Las fotografías del rostro son datos personales, y las que muestran una afección de la piel pueden considerarse datos de salud. Por este motivo, el MVP no almacenará las imágenes de los usuarios, solo los resultados del análisis. Los datos de voluntarios se guardarán fuera del repositorio.

### 3.5 Primera versión o MVP

**Usuario y tarea principal.** Una persona que quiere saber qué imperfecciones tiene su piel y qué tipo de cuidado le conviene antes de comprar un producto.

**Qué mostraríamos funcionando.** Una aplicación web en la que el usuario:

1. Sube una fotografía de su rostro o la toma con la cámara.
2. Recibe un aviso si la imagen no es válida (sin rostro, borrosa u oscura).
3. Ve la imagen con las imperfecciones detectadas marcadas. En el MVP se limitarán a tres tipos con suficientes ejemplos anotados: acné, manchas oscuras y ojeras.
4. Obtiene, para cada imperfección, una explicación breve, una recomendación general de cuidado (tipo de producto o ingrediente) y las señales que indican que debería consultar a un profesional.
5. Consulta el historial de sus análisis anteriores.

**Qué queda fuera por ahora.** El resto de condiciones (arrugas, poros, rojeces y tipo de piel seca, grasa o normal), la recomendación de productos comerciales concretos con precios, el modo de uso para farmacias y la versión móvil. Las recomendaciones personalizadas generadas con un LLM se incorporarían en la actividad 6.

**Criterio de éxito.** Lo evaluamos en tres niveles, porque un buen modelo no garantiza un buen producto:

| Nivel | Pregunta | Evidencia esperada |
|---|---|---|
| Producto | ¿Resuelve un problema relevante para el usuario? | Al menos 4 de 5 usuarios de prueba afirman que el análisis cambiaría o confirmaría lo que pensaban comprar |
| Experiencia | ¿Lo entiende y sabe cuándo confiar en él? | Los usuarios interpretan correctamente el resultado y entienden que es orientativo |
| IA/Data | ¿El modelo funciona lo suficiente para este uso? | El modelo supera a un modelo base y alcanza, para cada clase, un recall mínimo que fijaremos tras analizar los datos |

### 3.6 Viabilidad y dudas

**Principal incertidumbre.** Si los datos públicos disponibles permiten detectar cada imperfección con una fiabilidad suficiente. Los datasets son pequeños para algunas clases, están desbalanceados y combinan fuentes con criterios de anotación distintos.

**Qué necesitamos comprobar.**

- Las licencias de cada dataset de Roboflow y de ACNE04.
- El número de ejemplos y la calidad de las anotaciones por clase, revisando una muestra de cada fuente.
- El rendimiento de un primer modelo por clase, para confirmar qué imperfecciones pueden incluirse en el MVP.
- La disponibilidad de GPU (Kaggle o Google Colab), ya que el entrenamiento de modelos de detección no es viable en CPU.

**Cómo validaremos el problema y el valor.** Haremos entrevistas cortas a 5–8 personas que compran productos de cuidado facial, preguntando por su última compra: cómo eligieron el producto, qué información usaron y si quedaron satisfechas. De esta forma, comprobaremos si el problema existe y si es relevante para el usuario. Más adelante, cuando la aplicación esté disponible, haremos una prueba de usabilidad para comprobar si los usuarios entienden el resultado y si la recomendación les ayuda a decidir.

**Riesgos identificados.**

- **Desbalance de clases.** Las clases con pocos ejemplos pueden no aprenderse bien. Por este motivo, el MVP empieza con pocas clases y amplía solo cuando haya datos suficientes.
- **Imperfecciones pequeñas.** Muchas lesiones ocupan una parte muy pequeña de la imagen, lo que dificulta su detección.
- **Diferencias entre datos de entrenamiento y fotos reales.** Las imágenes públicas se suelen tomar con buena iluminación, mientras que las del usuario pueden ser de menor calidad.
- **Diversidad de tonos de piel.** Si los datos no cubren distintos tonos, el modelo puede funcionar peor para parte de los usuarios.
- **Confianza y uso indebido.** El usuario podría interpretar el resultado como un diagnóstico o confiar en una detección errónea. La interfaz debe mostrar el nivel de confianza de cada detección, dejar claro el carácter orientativo de la herramienta y permitir al usuario indicar si un resultado le parece incorrecto.
- **Problema no validado.** Es posible que el usuario prefiera el consejo de una persona en la farmacia. Las entrevistas nos permitirán comprobarlo.

**Encaje con el máster.** El proyecto permite trabajar la preparación de datos de imagen de varias fuentes (actividad 1), el almacenamiento del historial y de la base de recomendaciones en SQL (actividad 2), un análisis estadístico de los resultados (actividad 3), un experimento con modelo base y modelos de detección (actividad 4), la interfaz de usuario (actividad 5) y recomendaciones generadas con un LLM a partir de fuentes documentadas (actividad 6).

---

## 4. Idea 2. App para gestionar un viaje con IA

### 4.1 Título y descripción

Aplicación para organizar viajes individuales o en grupo. El usuario introduce sus preferencias en lenguaje natural y la IA genera una propuesta de viaje completa: ruta organizada por días, lugares y actividades, alojamientos, opciones de transporte, previsión meteorológica, estimación del presupuesto, restaurantes y alternativas si llueve o cambia algún plan. El usuario puede modificar toda la planificación conversando con la IA, y en los viajes en grupo cada participante dispone de un espacio compartido para proponer, votar y repartir gastos.

### 4.2 Problema y usuario

**Usuario.** Personas que organizan un viaje, de forma individual o para un grupo de amigos o familiares.

**Necesidad.** Planificar un viaje completo (ruta, actividades, alojamiento, transporte y presupuesto) que se ajuste a sus intereses y, en el caso de los grupos, a los gustos de todos los participantes.

**Solución actual.** El viajero busca información en blogs, buscadores de vuelos y hoteles, Google Maps y páginas de previsión meteorológica, y la reúne en notas o en una hoja de cálculo. En los viajes en grupo, las decisiones se toman en el chat, y los gastos se reparten a mano o con otra aplicación distinta.

**Dificultad.** La información está repartida en muchas herramientas, y organizar un viaje lleva muchas horas. Además, cuando cambia algo (el tiempo, un horario o el presupuesto), hay que rehacer parte de la planificación. En los grupos se añade otra dificultad: combinar los intereses de personas que quieren cosas distintas y llevar el control de lo que ha pagado cada uno.

**Mejora propuesta.** Una sola aplicación en la que la IA genera el plan completo a partir de las preferencias, lo adapta conversando sin empezar de cero y, en los viajes en grupo, busca un itinerario equilibrado entre los gustos de todos.

**Job to be done.** *Cuando quiero organizar un viaje, quiero obtener un plan completo que se ajuste a lo que me gusta a mí y a quienes viajan conmigo, para no pasar horas buscando información en muchas herramientas distintas.*

**Estado de la evidencia.** El problema y el usuario son, por ahora, hipótesis del equipo basadas en experiencias propias organizando viajes. Todavía no los hemos contrastado con usuarios reales (ver apartado 4.6).

### 4.3 Uso y valor

**Situación de uso.** Un grupo de cinco amigos quiere viajar a Japón durante 10 días. Les interesa la cultura japonesa, los videojuegos, la gastronomía y visitar lugares poco turísticos, con un presupuesto de 1.500 € por persona. Uno de ellos crea el viaje en la aplicación, escribe estas preferencias e invita al resto. La IA genera una ruta organizada por días y horarios, con mapas y tiempos aproximados de desplazamiento, actividades, restaurantes y una estimación del presupuesto. Como a un participante le interesan los museos y a otro la naturaleza, la IA busca un itinerario equilibrado entre ambos. Después, el grupo vota entre dos excursiones y uno de ellos pide «busca actividades más económicas para el tercer día». Finalmente, durante el viaje empieza a llover y la aplicación propone cambiar la ruta por actividades de interior.

**Valor.** El grupo obtiene en pocos minutos una propuesta completa que puede ajustar conversando, en lugar de dedicar varias tardes a buscar información en distintas herramientas. Además, todos ven el mismo itinerario, pueden opinar sobre él y saben en todo momento cuánto han gastado.

**Hipótesis de valor.** Una aplicación que genera y adapta el plan de viaje a partir de las preferencias de todos reduce el tiempo de organización y facilita los acuerdos frente a planificar con varias herramientas y el chat del grupo.

### 4.4 Datos

**Información necesaria.** Lugares, actividades y restaurantes de cada destino con su ubicación; tiempos de desplazamiento; previsión meteorológica; precios y disponibilidad de alojamientos y transportes; y las preferencias y gastos de los usuarios, que se generarán en la propia aplicación.

| Fuente | Contenido | Estado del acceso | Condiciones de uso y restricciones |
|---|---|---|---|
| [Google Maps Platform](https://developers.google.com/maps) o [Mapbox](https://www.mapbox.com/) | Mapas, lugares, restaurantes y tiempos de desplazamiento | **Hipótesis.** Pendiente de crear una clave de API y probarla | Ambas ofrecen un uso gratuito limitado y de pago a partir de cierto volumen; revisar las condiciones de uso y almacenamiento de los datos |
| [Open-Meteo](https://open-meteo.com/) | Previsión meteorológica diaria | **Hipótesis.** Pendiente de prueba de la API | Gratuita para uso no comercial. Las previsiones a largo plazo son menos fiables que las de los próximos días |
| APIs de proveedores turísticos (vuelos, hoteles y transporte) | Precios, horarios y disponibilidad | **Hipótesis.** Proveedores por identificar | Suelen requerir registro como empresa, acuerdos comerciales o pago. Es la fuente con más incertidumbre |
| Guías de viaje para el sistema RAG (por ejemplo, [Wikivoyage](https://www.wikivoyage.org/)) | Información sobre destinos, barrios y lugares | **Hipótesis.** Pendiente de descarga | Licencia CC BY-SA en el caso de Wikivoyage: permite reutilizar el contenido citando la fuente |
| Datos de los usuarios | Preferencias, itinerarios, votaciones y gastos del grupo | Se generarán en la aplicación | Datos personales; se almacenarán con las medidas de protección adecuadas |

**Privacidad.** La aplicación guardará preferencias, itinerarios y gastos de los participantes. Para el MVP solo se pedirá un alias y un correo para invitar al grupo, y no se almacenarán datos de pago.

### 4.5 Primera versión o MVP

**Usuario y tarea principal.** Una persona que organiza un viaje en grupo y quiere obtener un plan completo que tenga en cuenta las preferencias de todos.

**Qué mostraríamos funcionando.**

1. **Planificador de viajes con IA.** El usuario escribe en lenguaje natural lo que quiere hacer y la IA genera un itinerario por días y horarios, con mapa y tiempos de desplazamiento. El usuario puede modificarlo conversando, sin empezar de cero.
2. **Organización en grupo.** Un espacio compartido en el que se invita a los participantes, cada uno indica sus preferencias y la IA busca puntos en común entre todos.
3. **Meteorología inteligente.** Relación entre la previsión y las actividades programadas, con alternativas cuando el tiempo afecta al plan.
4. **Presupuesto.** Estimación del coste del viaje y control del presupuesto restante.

**Tecnologías previstas.** Flutter o React para el frontend; Python y FastAPI para el backend; PostgreSQL como base de datos; una API de LLM con RAG; Google Maps Platform o Mapbox para los mapas; Open-Meteo para la meteorología; y APIs de proveedores turísticos para vuelos y hoteles.

**Qué queda fuera por ahora.** El buscador integrado de vuelos, hoteles y transportes con precios reales (depende del acceso a las APIs de los proveedores), la gestión detallada de gastos compartidos y el asistente personal durante el viaje. Estas funciones forman parte de la idea completa y se incorporarían en versiones posteriores.

**Criterio de éxito.**

| Nivel | Pregunta | Evidencia esperada |
|---|---|---|
| Producto | ¿Resuelve un problema relevante para el usuario? | Al menos 3 de 5 organizadores de prueba usarían el plan generado como punto de partida en lugar de empezar desde cero |
| Experiencia | ¿Lo entiende y sabe cuándo confiar en él? | Los usuarios consiguen modificar el itinerario conversando y entienden qué preferencias de cada participante cubre el plan |
| IA/Data | ¿El sistema funciona lo suficiente para este uso? | Los itinerarios generados son realistas (lugares existentes, horarios y desplazamientos coherentes) y se ajustan al presupuesto indicado en un conjunto de casos de prueba |

### 4.6 Viabilidad y dudas

**Principal incertidumbre.** El acceso a datos reales de precios y disponibilidad. La IA por sí sola no conoce la disponibilidad ni los precios actualizados, por lo que los resultados reales dependen de integrar APIs de proveedores externos, que suelen tener acceso restringido o de pago.

**Qué necesitamos comprobar.**

- Las condiciones de acceso y el coste de Google Maps Platform o Mapbox, y de al menos una API de vuelos u hoteles.
- Que la IA genera itinerarios realistas y sin lugares o datos inventados cuando se apoya en datos reales mediante RAG.
- Qué parte del producto permite desarrollar un modelo de Machine Learning propio para la actividad 4, por ejemplo la recomendación de actividades según las preferencias del grupo o la estimación del presupuesto.

**Cómo validaremos el problema y el valor.** Haremos entrevistas cortas a 5–8 personas que hayan organizado un viaje recientemente, preferiblemente en grupo, preguntando cómo lo planificaron, qué herramientas usaron, cuánto tiempo les llevó y qué fue lo más difícil. De esta forma, comprobaremos si el problema existe y si es relevante. Más adelante, cuando la aplicación esté disponible, haremos una prueba de usabilidad con usuarios reales.

**Riesgos identificados.**

- **Dependencia de APIs externas.** Sin acceso a precios y disponibilidad reales, parte de las funciones solo podrían mostrarse con datos de ejemplo.
- **Información inventada por la IA.** El LLM podría proponer lugares, horarios o precios que no existen. Las propuestas deben apoyarse en datos verificados y citar su origen.
- **Fiabilidad de la meteorología.** Las previsiones a largo plazo no son igual de fiables que las de los próximos días, por lo que las alternativas por mal tiempo serán más útiles cerca de la fecha del viaje.
- **Diferenciación.** Existen aplicaciones de viajes y asistentes de IA generales que ya generan itinerarios. El valor diferencial debe estar en la organización en grupo y en la adaptación continua del plan.
- **Alcance.** La idea completa incluye muchas funciones, por lo que será necesario priorizar para terminar el MVP con calidad.

**Encaje con el máster.** El proyecto permite trabajar la adquisición de datos mediante APIs (actividad 1), el modelo de datos de viajes, participantes, actividades y gastos en PostgreSQL (actividad 2), un análisis estadístico de las preferencias o del presupuesto (actividad 3), un modelo de recomendación de actividades (actividad 4), la interfaz con mapa e itinerario (actividad 5), el planificador conversacional con LLM y RAG (actividad 6), el despliegue del backend con FastAPI (actividad 7) y la arquitectura Cloud de la aplicación (actividad 8).

---

## 5. Idea 3. Sistema de IA para optimización energética y mantenimiento predictivo industrial

### 5.1 Título y descripción

Plataforma basada en Inteligencia Artificial para el sector industrial que analiza las series temporales de telemetría de la maquinaria para modelar el consumo energético, detectar anomalías de forma automática y asistir a los ingenieros de planta en la resolución de incidencias. El sistema combina modelos de Machine Learning para predecir la demanda de energía y detectar ineficiencias con un asistente basado en IA generativa (RAG) que interpreta las anomalías a partir de los manuales de mantenimiento. Los resultados se presentan en cuadros de mando interactivos y se ofrecen a través de una API predictiva.

### 5.2 Problema y usuario

**Usuario.** Ingenieros de planta y personal de mantenimiento de una instalación industrial con maquinaria pesada y alto consumo eléctrico.

**Necesidad.** Anticipar la demanda de energía de la planta y detectar a tiempo comportamientos anómalos en el consumo que indiquen ineficiencias o el inicio de un fallo mecánico.

**Solución actual.** El mantenimiento suele ser correctivo: se actúa cuando el fallo ya se ha producido. El consumo energético se controla principalmente a través de la factura o de lecturas de los contadores, y ante una incidencia el técnico consulta los manuales de mantenimiento o recurre a su experiencia.

**Dificultad.** El consumo energético es uno de los principales costes operativos (OPEX) de una planta de fabricación y tiene un impacto directo en la huella de carbono y en el cumplimiento normativo. Sin embargo, las lecturas de los sensores se almacenan de forma pasiva y no se transforman en información para actuar. Por este motivo, las ineficiencias y los primeros síntomas de fallo se detectan tarde.

**Mejora propuesta.** Pasar de un mantenimiento correctivo a uno predictivo, convirtiendo las lecturas de los sensores en predicciones, alertas y recomendaciones que el personal de planta pueda usar para decidir.

**Job to be done.** *Cuando superviso el funcionamiento de la planta, quiero anticipar el consumo y saber si algún equipo se está comportando de forma anómala, para actuar antes de que se produzca una avería o un sobrecoste energético.*

**Estado de la evidencia.** El problema se basa en la experiencia profesional de un integrante del equipo como ingeniero aeroespacial e industrial. Todavía no lo hemos contrastado con otros profesionales del sector (ver apartado 5.6).

### 5.3 Uso y valor

**Situación de uso.** Javier es ingeniero de mantenimiento en una planta de fabricación. Al empezar su turno abre el cuadro de mando y consulta la previsión de consumo de energía activa para las próximas horas. Después ve una alerta: durante la noche, con la planta en reposo, se registró un pico de energía reactiva que se sale del comportamiento habitual. Finalmente, pregunta al asistente qué puede indicar esa anomalía. El asistente le responde en lenguaje natural con las posibles causas y el protocolo de revisión recogido en el manual de mantenimiento de la planta.

**Valor.** Javier detecta el problema el mismo día, sin esperar a la factura ni a que el fallo sea evidente. Con la información del panel y del asistente decide revisar el equipo afectado. De esta forma, puede evitar una avería, reducir el consumo innecesario y documentar la incidencia.

**Hipótesis de valor.** Un sistema que predice el consumo, detecta anomalías y las explica a partir de la documentación técnica permite al personal de planta actuar antes y con más información que con el mantenimiento correctivo.

### 5.4 Datos

**Información necesaria.** Series temporales de consumo energético y variables de estado de una planta industrial, junto con la documentación técnica de mantenimiento que utilizará el asistente.

| Fuente | Contenido | Estado del acceso | Condiciones de uso y restricciones |
|---|---|---|---|
| [Steel Industry Energy Consumption](https://archive.ics.uci.edu/dataset/851/steel+industry+energy+consumption) (UCI Machine Learning Repository) | 35.040 registros a intervalos de 15 minutos durante un año, procedentes de la planta siderúrgica DAEWOO Steel Co. Ltd (Gwangyang, Corea del Sur). Variables: energía activa (kWh), energía reactiva (kVarh), factor de potencia, emisiones de CO₂, intensidad de carga (Light/Medium/Maximum) y variables temporales | **Confirmado.** Descarga pública sin registro | Licencia CC BY 4.0: permite el uso y la transformación citando la fuente |
| Manuales de mantenimiento y documentación técnica | Protocolos de mantenimiento y documentación de equipos para el asistente RAG | **Hipótesis.** Documentos por seleccionar | Revisar las condiciones de reutilización de cada documento |

**Privacidad y confidencialidad.** El dataset no contiene datos personales. Si en algún momento se incorporan datos o manuales de una empresa, se guardarán fuera del repositorio.

### 5.5 Primera versión o MVP

**Usuario y tarea principal.** El ingeniero de planta que quiere conocer la demanda prevista de energía y detectar anomalías en el consumo para decidir qué revisar.

**Qué mostraríamos funcionando.**

1. **Predicción de la demanda.** Un modelo supervisado que predice la energía activa (kWh) a corto plazo en función de las variables operativas y la carga de trabajo de la instalación.
2. **Detección de anomalías.** Un modelo no supervisado que identifica desviaciones y comportamientos anómalos en el consumo, como picos de energía reactiva en reposo.
3. **Asistente documental.** Un sistema RAG que interpreta las anomalías detectadas y responde en lenguaje natural a partir de los manuales de mantenimiento.
4. **Cuadros de mando.** Una interfaz en Power BI y Plotly que cruza las predicciones y las anomalías con indicadores de gestión.
5. **API predictiva.** Un servicio que permite consultar las predicciones de los modelos.

**Tecnologías previstas.** Python, Pandas y Scikit-learn para el procesamiento; XGBoost y LightGBM para la predicción; Isolation Forest para la detección de anomalías; LangChain, una API de LLM y FAISS para el asistente; FastAPI, Docker y AWS para el despliegue; y Power BI y Plotly para la visualización.

**Qué queda fuera por ahora.** La conexión con los sensores de una planta en funcionamiento y la integración con los sistemas de gestión de mantenimiento de una empresa. El MVP trabajará con el dataset histórico, simulando la llegada de nuevas lecturas.

**Criterio de éxito.**

| Nivel | Pregunta | Evidencia esperada |
|---|---|---|
| Producto | ¿Resuelve un problema relevante para el usuario? | Al menos 3 de 5 profesionales del sector consultados consideran que las predicciones y las alertas les ayudarían a anticipar incidencias |
| Experiencia | ¿Lo entiende y sabe cuándo confiar en él? | Los usuarios entienden por qué se genera cada alerta y en qué documentación se basa la respuesta del asistente |
| IA/Data | ¿Los modelos funcionan lo suficiente para este uso? | El modelo de predicción mejora el error (RMSE y MAE) de un modelo base, y el detector identifica las anomalías con un número de falsas alarmas aceptable |

### 5.6 Viabilidad y dudas

**Principal incertidumbre.** Cómo evaluar la detección de anomalías. El dataset no indica qué periodos corresponden a fallos o ineficiencias reales, por lo que no es posible medir directamente si el detector acierta.

**Qué necesitamos comprobar.**

- La calidad del dataset: valores nulos, valores atípicos y estacionalidad de la serie.
- Una forma de validar el detector, por ejemplo insertando anomalías simuladas en la serie y midiendo cuántas detecta, junto con la revisión experta de las anomalías encontradas.
- La disponibilidad de manuales de mantenimiento públicos y reutilizables para el asistente RAG.
- Que Power BI es válido para la actividad 5, ya que el enunciado pide una herramienta libre. Si no lo fuera, el cuadro de mando de esa actividad se construiría con Plotly.

**Cómo validaremos el problema y el valor.** Haremos entrevistas cortas a 5–8 profesionales de mantenimiento o gestión energética en la industria, preguntando por la última vez que detectaron un consumo anómalo o una avería: cómo lo descubrieron, cuánto tardaron y qué consecuencias tuvo. De esta forma, comprobaremos si el problema existe y si es relevante. Más adelante, cuando el cuadro de mando esté disponible, haremos una prueba de usabilidad con algunos de ellos.

**Riesgos identificados.**

- **Datos agregados de una sola planta.** El dataset mide el consumo de toda la planta y no de cada máquina, por lo que puede ser difícil relacionar una anomalía con un equipo concreto.
- **Validación sin etiquetas.** Sin registros de fallos reales, la evaluación del detector dependerá de anomalías simuladas y de la revisión experta.
- **Generalización.** Los modelos entrenados con una planta siderúrgica pueden no funcionar igual en otro tipo de industria.
- **Respuestas del asistente.** El asistente podría dar explicaciones incorrectas. Las respuestas deben citar la documentación en la que se basan y presentarse como apoyo, no como diagnóstico.

**Encaje con el máster.** Las fases del proyecto se corresponden con las actividades del máster: la limpieza, el estudio de la estacionalidad, la codificación cíclica de variables temporales y las variables retardadas (actividad 1); el modelo de datos de lecturas, predicciones y alertas (actividad 2); el análisis estadístico del consumo (actividad 3); la predicción de carga y el motor de anomalías (actividad 4); los cuadros de mando (actividad 5); el copiloto industrial con RAG (actividad 6); la API, el empaquetado de los modelos y el despliegue (actividad 7); y la arquitectura Cloud en AWS (actividad 8).
