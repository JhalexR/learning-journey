
</details>

#### 20/09/2026

##### Hoy aprendí

### HTTP/HTTPS en Detalle 

### `HTTP`
+ Estructura de una ***petición** `HTTP`
	+ Una petición `HTTP` indica qué recurso quiere utilizar el cliente, qué operación quiere realizar, proporciona información adicional mediante **headers** y, cuando es necesario, envía datos en el **body.**

+ Estructura de una **Respuesta** `HTTP` 
	+ La estructura de una respuesta `HTTP`  es muy importante porque te permitirá entender posteriormente los códigos de estado, las APIs, los errores `HTTP` y las herramientas de diagnóstico.
	+ Una respuesta HTTP le indica al cliente qué ocurrió con su petición, proporciona información adicional mediante headers y, cuando corresponde, devuelve datos en el body.

+ HTTP Petición vs Respuesta
	+ «La diferencia fundamental está en la primera línea.»
		+ Petición HTTP → Qué quiere hacer el cliente.
		+ Respuesta HTTP → Qué ocurrió con la petición.
	+ Códigos de estado HTTP → están organizados en cinco grandes categorías
		+ se agrupan según su primer número
			+ 1xx → Información
			+ 2xx → Éxito
			+ 3xx → Redirección
			+ 4xx → Problema con la solicitud
			+ 5xx → Problema en el servidor
		+ Observaciones 
		+ `401 Unauthorized` → Aunque el nombre diga `Unauthorized`, en la práctica HTTP `401` está relacionado principalmente con **autenticación**.
		+ 401 VS 403 
			+ 401 → ¿Quién eres?
			+ 403 → Sé quién eres, pero no tienes permiso.

+ Códigos de Estado HTTP
	+ Los códigos de estado de la respuesta `HTTP`son EXTREMADAMENTE IMPORTANTES para los desarrolladores porque permiten saber rápidamente qué ocurrió.
	+ No es necesario memorizar todos los códigos al principio, pero si es importante recordar los mas frecuentes
	+ Cuando aparezca un codigo HTTP mientras se esta desarrollando, se puede empezar por la siguiente pregunta:
		+ > _**¿Con qué número comienza?**_
	+ | Código  |        Significado                        |
| ------- | ----------------------------------------- |
| **2xx** | Éxito                                     |
| **3xx** | Redirección / caché                       |
| **4xx** | Revisar la petición del cliente           |
| **5xx** | Investigar el servidor o sus dependencias |

	+ No todos los códigos HTTP representan errores. es mejor pensar en ellos como indicadores del resultado de la interacción HTTP, no simplemente como "códigos de error".

##### Tengo que investigar

+ CORS (Cross-Origin Resource Sharing)

</details>
