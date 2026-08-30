# Cuando la información falla: una reflexión desde una experiencia hospitalaria
### _Un ejercicio de pensamiento de ingeniería de software_
> ...antes de continuar, una situación real me hizo detenerme a pensar en para qué sirven realmente todos estos conceptos...

## 1. Introducción

Desde el mes de Julio de 2026 quise registrar los conceptos de programación es decir mi estudio/repaso en un repositorio de Github para tener ese conocimiento "siempre a la mano" lo llame "Learning-journey" y aunque lo hice constantemente a principios del mes de agosto tuve que pausar mis estudio debido a algunos síntomas de salud que me impidieron continuar.

Tuve que ser hospitalizado para unos exámenes y durante la estancia de mas de una semana en la clínica, tuve la oportunidad de observar algo que, aunque inicialmente parecía ser simplemente una diferencia de criterios entre miembros del personal, terminó haciéndome pensar en un problema de ingeniería de software.

### 1.1 Una experiencia que me hizo pensar

En diferentes momentos recibí indicaciones que parecían contradictorias. Por ejemplo, mientras el personal de enfermería me indicaba que debía permanecer acompañado, algunos médicos que me atendieron consideraban que esto no era necesario

En otra ocasión estaba programada la administración de un medicamento durante varios días y, durante uno de los cambios de turno, aparentemente se produjo una confusión y una de las dosis no fue administrada como estaba previsto.

Aun estoy a la espera de unos resultados de exámenes médicos que no he recibido ni tengo idea de como me serán enviados debido a que los sistemas del hospital/clínica y los de la EPS son diferentes.

### 1.2 El antecedente: mi proyecto de arquitectura de software

En mi estudio de la universidad el año pasado en la asignatura de arquitectura de software realicé un estudio relacionado a temas médicos. 

En arquitectura de software nos pidieron crear un pequeño proyecto de software construido bajo uno de los patrones de software para aprender aplicar un patrón de arquitectura para solucionar problemas específicos.

En mi caso escogí el patrón pub/sub para resolver el siguiente problema:

Situación problema identificada: 
+ Una compañía de salud que gestiona historias clínicas electrónicas utiliza una estructura orientada a servicios, pero se ha detectado un problema vinculado con la interoperabilidad entre sistemas internos y externos.
+ El acceso a resultados de laboratorio, la programación de citas y el historial médico se llevan a cabo de manera independiente; debido a que no tienen una comunicación estandarizada.
+ Esto provoca incoherencias en la información, duplicación de datos y demoras en el acceso resultados clínicos para los médicos y pacientes.
+ No solo la calidad del servicio se ve afectada por el problema, sino que además pone en peligro la seguridad y la confidencialidad de los datos delicados de los pacientes.

En el ejercicio hipotético de arquitectura de software pensaba en un paciente que se realiza un examen medico, y aunque los resultados están listos no son visibles en la historia clínica ni por el medico especialista, hasta después de transcurrido un tiempo -generalmente pasados tres días en horario de la mañana (muy similar a algunas transacciones bancarias)-, con el patrón pub/sub pensaba que apenas se emitieran los resultados el publicador (servicio de laboratorio) emitiera el mensaje para que los dos suscriptores (servicio agendamiento de citas) - (servicio historial medico) pudieran actualizar el resultado de los exámenes en sus bases de datos.

Como es necesario que se conozcan los resultados para poder autorizar el siguiente paso en el tratamiento, en este caso el agendamiento de cita de lectura de exámenes o de control por parte del medico especialista, y entre mas rápido se actualice la información en el servicio agendamiento de citas e historia clínica mas cercana es la cita y tratamiento, lo cual puede llegar a ser un factor critico en la salud de los pacientes.

Durante la realización de este proyecto aprendí también sobre conceptos muy importantes dentro del software medico tales como:

+ EHR / EMR (Historia Clínica Electrónica / Registros Médicos Electrónicos): Sistemas digitales para almacenar, organizar y consultar el historial médico de los pacientes.

+ Interoperabilidad: Capacidad de los diferentes sistemas de información en salud para intercambiar datos de manera segura y estandarizada

+ SaMD (Software como Dispositivo Médico): Programas informáticos que cumplen funciones médicas sin necesidad de estar alojados en un hardware físico exclusivo

+ SiMD (Software en Dispositivo Médico): Es el software que viene integrado dentro de un aparato físico para controlarlo o hacer funcionar su hardware.

No conocía que hay leyes regulatorias que impulsan la mejora continua de los servicios médicos tales como la Ley HITECH y la Ley HIPAA:

+ Ley HITECH (2008): Impulsó la adopción de tecnologías de información sanitaria y el uso de HCE por parte de los médicos mediante incentivos y normativas de interoperabilidad.

+ Ley HIPAA: Protege la privacidad y seguridad de la información médica contenida en las HCE mediante estrictas normas de divulgación.

>> https://cprcare.com/es/course/hipaa/6/

En Colombia existe la Ley 2015 de 2020: Crea y regula la Historia Clínica Electrónica Interoperable (IHCE).

También existen resoluciones específicas que regulan la Historia Clínica Electrónica (HCE) y exigen su interoperabilidad entre las entidades de salud.

>> https://www.minsalud.gov.co/ihce/Paginas/Normatividad.aspx

>> https://caseguard.com/es/articles/la-ley-hitech-y-la-implementacion-de-las-historias-clinicas-electronicas/

### 1.3 La conexión entre ambas experiencias

Fue inevitable mientras estaba en el hospital acordarme de lo estudiado en la materia de arquitectura de software, nunca imagine que fuera estar en una situación tan similar a la situación hipotética que había planteado para presentar una investigación universitaria.

Cuando se presentaron las situaciones con la aplicación de los medicamentos, las instrucciones de acompañamiento entre otras cosas imaginaba a cada persona de la enfermería y doctores con una Tablet de manera que pudiera tener a la mano toda mi evolución y conocer el diagnostico medico, los conceptos del neurólogo, y demás médicos especialistas, en ocasiones le comentaba a la enfermería que en la noche necesitaba la ayuda del profesional terapista y por falta de comunicación solo se presento dos veces y creo que era porque no había o elementos, estándar de comunicación, protocolos o tal vez un buen software.

A pesar de todo me sentí muy bien atendido en la clínica y se que estas situaciones son normales y habituales mas por burocracia y temas administrativos que por falta de voluntad de los médicos tratantes e incluso de las instituciones, no es fácil implementar estos cambios y llevarlos a buen termino.

## 2. Del problema observado al problema de ingeniería

Finalmente, estas situaciones no tuvieron una consecuencia grave en mi caso. Sin embargo, como estudiante de ingeniería de software, me hicieron pensar en algo diferente:

> _¿qué ocurre en un sistema complejo cuando diferentes personas necesitan compartir información y coordinar acciones, pero esa información no siempre llega de la misma manera a todos los participantes?_

Esta pregunta me llevó a investigar cómo se utilizan los sistemas de información y otras herramientas de software para mejorar la comunicación, la continuidad y la seguridad durante la atención hospitalaria.

un ingeniero de software no empieza pensando "¿qué aplicación puedo programar?"

Empieza preguntándose:

+ ¿Cuál es realmente el problema?
+ ¿Dónde se produce?
+ ¿Quién interviene?
+ ¿Qué información necesita cada persona?
+ ¿Dónde puede perderse esa información?
+ ¿Qué sucede cuando alguien se equivoca?
+ ¿Qué partes del proceso pueden estandarizarse?
+ ¿Qué debería hacer el software?
+ ¿Qué cosas NO debería intentar hacer el software?

Mientras estaba en la habitación de la clínica, meditaba, planeaba e intentaba construir la diagramación de forma muy general mediante software una solución para evitar estas situaciones con un paciente.

Sentí que era un ejercicio mental que debía hacer porque era muy interesante, el tratar de resolver una situación de la vida real mientras la estaba viviendo; no como una solución completa y definitiva, sino un ejercicio mental de como empezaría a plantear una solución de software desde mi escaso conocimiento, mi inexperiencia, y lo que estaba viendo a mi alrededor

por lo que había estudiado en la asignatura de arquitectura de software el primer concepto que vino a mi mente fue _interoperabilidad_

La ONC explica que la _interoperabilidad_ permite que la información sanitaria electrónica pueda intercambiarse y utilizarse entre diferentes sistemas y organizaciones, con el objetivo de facilitar una atención segura y coordinada

>> https://healthit.gov/interoperability/

imaginaba el proceso como:

```
Médico
  │
  ▼
Sistema A
  │
  │ interoperabilidad
  ▼
Sistema B
  │
  ▼
Enfermería
```

En lugar de tener información aislada.

creo que algo que se podría implementar como política en un supuesto software para mejorar esta problemática debería ser

+ "fuente única de verdad"

```
Médico A
   │
   ├── "Debe permanecer acompañado"
   │
   ▼
Paciente

Enfermería
   │
   ├── "Debe permanecer acompañado"
   │
   ▼
Paciente

Médico B
   │
   ├── "No es necesario"
   │
   ▼
Paciente
```


¿Dónde está la decisión vigente?

¿Quién tiene autoridad?

¿Cuándo cambió?

¿Quién modificó la indicación?

¿Los demás miembros del equipo lo saben?

Un sistema bien diseñado podría intentar responder preguntas como:

+ ¿Cuál es la orden vigente?
+ ¿Quién la emitió?
+ ¿Cuándo?
+ ¿Está activa?
+ ¿Fue modificada?
+ ¿Por quién?
+ ¿Quién debe ejecutarla?
+ ¿Se completó?
+ ¿Si no se completó, alguien fue notificado?

también vino a mi mente la _trazabilidad_

Cada transición introduce una posibilidad de pérdida de información.

Por ejemplo:

```
Orden creada
    ↓
2026-08-XX 09:15
    ↓
Médico X
    ↓
Orden #1234
    ↓
Asignada a enfermería
    ↓
Cambio de turno
    ↓
Enfermero Y
    ↓
Administración registrada
    ↓
2026-08-XX 14:02
```
Si algo falla, el sistema debería permitir reconstruir:

+ qué ocurrió, 
+ cuándo ocurrió, 
+ quién realizó la acción 
+ cuál era el estado del sistema en ese momento.