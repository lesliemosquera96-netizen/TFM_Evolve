# Actividad 0. Equipos, ideas de producto y repositorio

**Estado del proyecto:** Exploración de ideas
**Repositorio:** [enlace al repositorio](https://github.com/usuario/nombre-repositorio)

---

## 1. Composición del equipo

| Integrante | Usuario de GitHub |
|---|---|
| Leslie Mosquera | [@lesliemosquera96-netizen](https://github.com/lesliemosquera96-netizen ) |
| Carlos Apellido | [@usuario](https://github.com/usuario) |
| Antonio Apellido | [@usuario](https://github.com/usuario) |


**Organización del equipo.** Todos los integrantes participarán en todas las fases del proyecto y conocerán el producto completo. Para cada actividad se asignará una persona responsable de coordinar la entrega y revisar que la documentación del repositorio esté actualizada. 

---

## 2. Resumen de las propuestas

| | Idea 1. DermaVision | Idea 2. TripMatch | Idea 3. *[Nombre]* |
|---|---|---|---|
| **Usuario** | Adultos que compran productos de cuidado facial sin saber qué necesita su piel | Organizador de una escapada de 2 a 4 días para un grupo de amigos | |
| **Problema** | No saben interpretar las imperfecciones de su piel ni qué cuidado elegir | Combinar los intereses y presupuestos de todos lleva mucho tiempo y genera desacuerdos | |
| **Producto** | Aplicación web que detecta imperfecciones faciales en una foto y da recomendaciones de cuidado | Aplicación web que genera un itinerario equilibrado según las preferencias del grupo | |
| **Datos principales** | Imágenes faciales con imperfecciones anotadas (Roboflow, ACNE04) | OpenStreetMap, Inside Airbnb, Open-Meteo, Wikivoyage | |
| **Estado fuente de los datos** | Validado | Hipótesis (fuentes abiertas sin descarga de prueba) | |
| **Principal riesgo** | Datos desbalanceados y de varias fuentes; fiabilidad de la detección | Diferenciación frente a asistentes de IA generales | |

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

**Cómo validaremos el problema y el valor.** Haremos entrevistas cortas a 10-12 personas que compran productos de cuidado facial, preguntando por su última compra: cómo eligieron el producto, qué información usaron y si quedaron satisfechas. De esta forma, comprobaremos si el problema existe y si es relevante para el usuario. Más adelante, cuando la aplicación esté disponible, haremos una prueba de usabilidad para comprobar si los usuarios entienden el resultado y si la recomendación les ayuda a decidir.

**Riesgos identificados.**

- **Desbalance de clases.** Las clases con pocos ejemplos pueden no aprenderse bien. Por este motivo, el MVP empieza con pocas clases y amplía solo cuando haya datos suficientes.
- **Imperfecciones pequeñas.** Muchas lesiones ocupan una parte muy pequeña de la imagen, lo que dificulta su detección.
- **Diferencias entre datos de entrenamiento y fotos reales.** Las imágenes públicas se suelen tomar con buena iluminación, mientras que las del usuario pueden ser de menor calidad.
- **Diversidad de tonos de piel.** Si los datos no cubren distintos tonos, el modelo puede funcionar peor para parte de los usuarios.
- **Confianza y uso indebido.** El usuario podría interpretar el resultado como un diagnóstico o confiar en una detección errónea. La interfaz debe mostrar el nivel de confianza de cada detección, dejar claro el carácter orientativo de la herramienta y permitir al usuario indicar si un resultado le parece incorrecto.
- **Problema no validado.** Es posible que el usuario prefiera el consejo de una persona en la farmacia. Las entrevistas nos permitirán comprobarlo.

**Encaje con el máster.** El proyecto permite trabajar la preparación de datos de imagen de varias fuentes (actividad 1), el almacenamiento del historial y de la base de recomendaciones en SQL (actividad 2), un análisis estadístico de los resultados (actividad 3), un experimento con modelo base y modelos de detección (actividad 4), la interfaz de usuario (actividad 5) y recomendaciones generadas con un LLM a partir de fuentes documentadas (actividad 6).

---

## 4. Idea 2. TripMatch: planificador de escapadas en grupo según las preferencias de todos

### 4.1 Título y descripción

TripMatch es una aplicación web que ayuda a un grupo de amigos a planificar una escapada de pocos días a una ciudad. Cada participante indica sus intereses, su presupuesto y el ritmo de viaje que prefiere. A partir de esta información, el sistema propone un itinerario por días que equilibra los gustos de todos, estima el coste del alojamiento por zona y adapta las actividades a la previsión meteorológica.

### 4.2 Problema y usuario

**Usuario.** La persona que organiza una escapada de 2 a 4 días a una ciudad para un grupo de 3 a 6 amigos.

**Necesidad.** Proponer un plan que encaje con los intereses y el presupuesto de todos, sin dedicar horas a buscar información y a poner de acuerdo al grupo.

**Solución actual.** El organizador busca información en blogs, Google Maps y plataformas de alojamiento, y la reúne en una hoja de cálculo o en notas. Las decisiones se toman en el chat del grupo, donde las opiniones se mezclan y se pierden. Algunos usan asistentes generales como ChatGPT para generar un itinerario, pero este no tiene en cuenta las preferencias individuales de cada miembro del grupo.

**Dificultad.** Cada persona tiene intereses y presupuestos distintos, y el organizador no tiene una forma sencilla de combinarlos. Como resultado, el plan suele reflejar los gustos de quien organiza o de quien más participa en el chat, y la planificación se alarga.

**Mejora propuesta.** Recoger las preferencias de cada participante de forma estructurada y generar automáticamente una propuesta equilibrada, con una estimación de coste y alternativas según el tiempo.

**Job to be done.** *Cuando organizo una escapada con mis amigos, quiero proponer un plan que encaje con lo que le gusta a cada uno y con lo que puede gastar, para cerrar el viaje rápido y sin discusiones.*

**Estado de la evidencia.** El problema y el usuario son, por ahora, hipótesis del equipo basadas en experiencias propias organizando viajes en grupo. Todavía no los hemos contrastado con usuarios reales (ver apartado 4.6).

### 4.3 Uso y valor

**Situación de uso.** Andrés quiere organizar con cuatro amigos un fin de semana largo en una ciudad europea. Crea el viaje en la aplicación y comparte un enlace con el grupo. Cada amigo marca sus intereses (museos, gastronomía, vida nocturna, naturaleza), su presupuesto máximo y si prefiere un ritmo tranquilo o intenso. Con estas respuestas, la aplicación propone un itinerario de tres días con actividades agrupadas por zonas para reducir desplazamientos, indica qué intereses de cada persona quedan cubiertos y estima el precio medio del alojamiento en los barrios más convenientes. Además, como la previsión indica lluvia el sábado, sugiere cambiar la excursión al aire libre por un museo.

**Valor.** Andrés obtiene en pocos minutos una propuesta que puede compartir con el grupo, en lugar de pasar varias tardes buscando información. Además, como cada persona ve qué parte del plan responde a sus preferencias, es más fácil llegar a un acuerdo.

**Hipótesis de valor.** Un itinerario que combina de forma explícita las preferencias de cada participante reduce el tiempo de organización y facilita el acuerdo del grupo frente a planificar con el chat y búsquedas manuales.

### 4.4 Datos

**Información necesaria.** Puntos de interés de la ciudad (tipo, ubicación y horarios), precios de alojamiento por zona, previsión meteorológica y descripciones de los lugares para que el asistente pueda explicar sus propuestas. Además, las preferencias de los participantes, que se recogerán en la propia aplicación.

| Fuente | Contenido | Estado del acceso | Condiciones de uso y restricciones |
|---|---|---|---|
| [OpenStreetMap](https://www.openstreetmap.org/copyright) (vía Overpass API) | Puntos de interés con categoría, ubicación y, en algunos casos, horarios | **Hipótesis.** Pendiente de descarga de prueba | Licencia ODbL: uso permitido citando la fuente. Los horarios y categorías pueden estar incompletos |
| [Inside Airbnb](https://insideairbnb.com/get-the-data/) | Anuncios de alojamiento por ciudad con precio, barrio, capacidad y valoraciones | **Hipótesis.** Pendiente de descarga | Confirmar licencia y ciudades disponibles. Los precios son de anuncios, no de reservas reales |
| [Open-Meteo](https://open-meteo.com/) | Previsión meteorológica diaria y datos históricos | **Hipótesis.** Pendiente de prueba de la API | Gratuita para uso no comercial; confirmar condiciones y límites de uso |
| [Wikivoyage](https://www.wikivoyage.org/) | Guías de viaje por ciudad con descripciones de barrios y lugares | **Hipótesis.** Pendiente de descarga | Licencia CC BY-SA: permite reutilizar el contenido citando la fuente |
| Preferencias de los usuarios | Intereses, presupuesto y ritmo de cada participante | Se generarán en la aplicación | Datos personales mínimos; no se pedirá información identificativa más allá de un alias |

**Privacidad.** La aplicación solo necesita un alias y las preferencias de viaje de cada participante. No se almacenarán datos de pago ni de ubicación en tiempo real.

### 4.5 Primera versión o MVP

**Usuario y tarea principal.** El organizador de una escapada en grupo que quiere obtener una propuesta de itinerario que tenga en cuenta las preferencias de todos.

**Qué mostraríamos funcionando.** Una aplicación web, limitada a una sola ciudad, en la que:

1. El organizador crea un viaje (fechas y número de días) y comparte un enlace con el grupo.
2. Cada participante completa un formulario corto con sus intereses, presupuesto y ritmo de viaje.
3. El sistema genera un itinerario por días, con actividades agrupadas por zonas y un mapa.
4. Se muestra qué intereses de cada participante cubre el plan y una estimación del coste de alojamiento por barrio.
5. Si la previsión indica lluvia para algún día, se proponen alternativas de interior.

**Qué queda fuera por ahora.** La búsqueda y reserva de vuelos, hoteles y transporte; los viajes a varias ciudades; la gestión de gastos compartidos; las votaciones dentro del grupo; y el asistente durante el viaje. La modificación del itinerario conversando con un LLM se incorporaría en la actividad 6.

**Criterio de éxito.**

| Nivel | Pregunta | Evidencia esperada |
|---|---|---|
| Producto | ¿Resuelve un problema relevante para el usuario? | Al menos 3 de 5 organizadores de prueba usarían la propuesta como punto de partida en lugar de empezar desde cero |
| Experiencia | ¿Lo entiende y sabe cuándo confiar en él? | Los participantes entienden por qué se ha elegido cada actividad y qué preferencias cubre |
| IA/Data | ¿El sistema funciona lo suficiente para este uso? | Los itinerarios cubren las preferencias de todos los participantes de forma equilibrada y el modelo de precios mejora a un modelo base (mediana por barrio) |

### 4.6 Viabilidad y dudas

**Principal incertidumbre.** Si existe un componente de Data Science suficiente más allá de generar itinerarios con un LLM. Un asistente general ya puede proponer un viaje, por lo que el valor diferencial debe estar en combinar las preferencias del grupo y en estimaciones basadas en datos reales.

**Qué necesitamos comprobar.**

- La cobertura y calidad de los puntos de interés de OpenStreetMap para la ciudad elegida, especialmente categorías y horarios.
- La disponibilidad de datos de Inside Airbnb para esa ciudad y sus condiciones de uso.
- Que la combinación de preferencias puede plantearse como un problema de recomendación o de optimización evaluable con métricas.

**Cómo validaremos el problema y el valor.** Haremos entrevistas cortas a 5–8 personas que hayan organizado un viaje en grupo recientemente, preguntando cómo lo planificaron, cuánto tiempo les llevó y qué fue lo más difícil. De esta forma, comprobaremos si el problema existe y si es relevante. Más adelante, cuando la aplicación esté disponible, haremos una prueba de usabilidad con grupos reales.

**Riesgos identificados.**

- **Diferenciación.** Existen muchas aplicaciones de viajes y asistentes de IA generales. Si la propuesta no mejora claramente lo que ya ofrecen, el producto tendrá poco valor.
- **Calidad de los datos abiertos.** Los datos de OpenStreetMap pueden tener categorías u horarios incompletos, lo que afectaría a la calidad del itinerario.
- **Evaluación del itinerario.** No existe una métrica única para valorar si un plan es bueno. Será necesario definir criterios medibles (cobertura de preferencias, distancias, coste) y complementarlos con la opinión de los usuarios.
- **Alcance.** La idea original incluye muchas funciones. El riesgo principal es intentar construirlas todas y no terminar ninguna con calidad.

**Encaje con el máster.** El proyecto permite trabajar la adquisición de datos abiertos mediante APIs (actividad 1), el modelo de datos de viajes, participantes y lugares en SQL (actividad 2), un análisis estadístico de precios por barrio (actividad 3), un experimento con modelo base y modelos de predicción de precio o de recomendación (actividad 4), la interfaz con mapa e itinerario (actividad 5) y un asistente conversacional con RAG sobre guías de viaje (actividad 6).

---

## 5. Idea 3. *[Nombre provisional]*

### 5.1 Título y descripción

*[Nombre provisional y dos o tres frases sobre en qué consiste el producto.]*

### 5.2 Problema y usuario

**Usuario.** *[Quién tiene el problema. Ser lo más concreto posible: perfil, contexto, situación.]*

**Necesidad.** *[Qué necesita conseguir.]*

**Solución actual.** *[Cómo lo resuelve hoy.]*

**Dificultad.** *[Qué le cuesta o qué no funciona de la solución actual.]*

**Mejora propuesta.** *[Qué cambiaría con el producto.]*

**Job to be done.** *[Cuando [situación], quiero [progreso que busca el usuario], para [resultado].]*

**Estado de la evidencia.** *[Indicar si el problema es una hipótesis del equipo o si ya se ha contrastado con usuarios.]*

### 5.3 Uso y valor

**Situación de uso.** *[Ejemplo concreto: qué necesita hacer el usuario, qué recibe del producto y cómo le ayuda a actuar o decidir.]*

**Valor.** *[Qué gana el usuario frente a la solución actual.]*

**Hipótesis de valor.** *[Una frase que se pueda comprobar con usuarios.]*

### 5.4 Datos

**Información necesaria.** *[Qué datos y para qué.]*

| Fuente | Contenido | Estado del acceso | Condiciones de uso y restricciones |
|---|---|---|---|
| *[Nombre y enlace]* | | **Confirmado** / **Hipótesis** | |
| *[Nombre y enlace]* | | **Confirmado** / **Hipótesis** | |

**Privacidad.** *[Datos personales o sensibles y cómo se protegerán.]*

### 5.5 Primera versión o MVP

**Usuario y tarea principal.** *[Un usuario y una tarea.]*

**Qué mostraríamos funcionando.** *[Pocas funciones, en orden de uso.]*

**Qué queda fuera por ahora.** *[Alcance excluido.]*

**Criterio de éxito.**

| Nivel | Pregunta | Evidencia esperada |
|---|---|---|
| Producto | ¿Resuelve un problema relevante para el usuario? | *[...]* |
| Experiencia | ¿Lo entiende y sabe cuándo confiar en él? | *[...]* |
| IA/Data | ¿El modelo o sistema funciona lo suficiente para este uso? | *[...]* |

### 5.6 Viabilidad y dudas

**Principal incertidumbre.** *[La duda más importante.]*

**Qué necesitamos comprobar.** *[Pasos concretos para resolverla.]*

**Cómo validaremos el problema y el valor.** *[Entrevistas, prototipo, Wizard of Oz u otra técnica.]*

**Riesgos identificados.** *[Datos, técnica, uso, privacidad.]*

---

## 6. Opción preferida

*[Indicar la idea preferida por el equipo y explicar por qué. Criterios sugeridos: importancia del problema para el usuario, acceso confirmado a los datos, posibilidad de validar el problema con usuarios reales, alcance del MVP y encaje con las actividades del máster. Las tres propuestas se mantienen para recibir feedback.]*

## 7. Preguntas para el feedback

*[Dudas concretas que el equipo quiere resolver con el profesorado. Por ejemplo, para la idea 1: ¿es razonable limitar el MVP a tres imperfecciones (acné, manchas y ojeras) o conviene incluir desde el inicio el tipo de piel?]*
