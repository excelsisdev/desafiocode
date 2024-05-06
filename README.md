# Hackathon ```<code/>```
## Consideraciones iniciales
En la cuenta de github deben crear un nuevo repositorio que debe ser nombrado igual que el nombre del equipo y debe estar **publico**.
Dentro del repositorio, incluir un archivo readme.md que debe contener los suguientes datos:
- El nombre del equipo 
- El nombre de los integrantes del equipo con sus correos personales
- Herramientas de programación utilizados (framework, pluggins, etc).

Una ves terminado el desarrollo, deben levantar todo el proyecto al github del equipo y enviar un correo a desarrollo_adm@excelsis.com.py con el asunto **Hackathon - Code**.
Dentro del correo deben incluir:
- El nombre del equipo
- El nombre de los integrantes del equipo 
- La URL del repositorio github para su posterior evaluación técnica.

## Enunciado
El Ministerio de Agricultura y Ganadería en conjunto con la Dirección de meteorología e hidrología del Paraguay están trabajando para encontrar una solución a las perdidas de cultivos ocasionadas por el cambio abrupto del clima de la región. Es por esto, que se pone en contacto con ustedes para desarrollar una página que permita alertar a los productores sobre posibles fenómenos meteorológicos que perjudiquen la producción. 

## Requerimientos funcionales
**Descripción General:** Desarrollar y diseñar una página web que permita mostrar a los productores, el pronóstico extendido de los departamentos estudiados en el país, que por el momento son: Central, Boquerón, Caaguazú.
- El usuario debe ser capaz de seleccionar un departamentos y poder visualizar el pronostico extendido.
- La página debe estar preparada para mostrar mas departamentos a medida que se vayan obteniendo los datos en un futuro. 
- El pronóstico extendido debe mostrar todas las variables meteorológicas obtenidas: temperatura, clima, viento, visibilidad, probabilidad de precipitación y el volumen de lluvia predicho.
- El diseño de la página debe contar con imágenes alucivas al estado del tiempo. Los posibles valores esperados son (nublado_total, soleado, lluvia, tormenta_electrica, nublado_parcialemente, nieve). Por supuesto, se espera de la creatividad del diseñador para mostrar cada una de la variables meteorológicas que se tienen lectura de una forma concisa y entendible.
- El pronóstico extendido además, debe mostrar los *tipo de alerta*, que deberá se calculada en base a las variables meteorológicas por cada día. Estas alertas servirán como ayuda a los productores para tomar decisiones con respecto a sus cultivos.
- El *tipo de alerta* está categorizada de la siguiente manera:
	- óptimo: indica que las variables meteorológicas es el ideal para el cultivo.
 	- precaución: indica que las variables meteorológicas puede ser perjudicial si no se toman medidas preventivas.
  	- peligroso: indica que las variables meteorológicas tiene grandes probabilidades de provocar daños irreparables del cultivo.
- La página debe poder adaptarse a las distintas resoluciones de pantalla.
- Si bien se cuenta con un mockup básico de lo que se espera ver en la página web. También se espera que el equipo de desarrolladores sea capaz de mejorar la idea inicial, siempre tomando en cuenta el objetivo de la página, que consisten en comunicar de una manera fácil e intuitiva a los productores sobre los posibles cambios climátivos abruptos que puedan ocurrir en la región.

**Cálculos solicitados**
- Grados Fahrenheit: Se espera que la temperatura pueda visualizarse en grados Celsius y Fahrenheit. (Fahrenheit debe ser calculado en base al celsius).
- Tipos de Alerta: El criterio para calcular los tipo de alertas dependerá de cada equipo, tomando en cuenta las variables extraídas del API. Formará como parte de la evaluación del desafío, la creatividad y la complejidad aplicada a este calculo. Para eso, se solicita a cada equipo implementar el método ```getAlertType(array weatherDataPerDay) return string;```, que calcule y devuelva como resultado el tipo de alerta (óptimo, precaución, peligroso) correspondiente a un día, que será recibida como entrada del método.
```
    /**
     * Método de ejemplo hecho con lenguaje PHP
     * 
     * Toma en cuenta como único valor de entrada, la velocidad del viento, para calcular el tipo de alerta
     * Se espera que cada equipo tome en cuenta mas valores y combinaciones para calcular el tipo de alerta.
     * Usen la creatividad y por sobre todo, el sentido común para llegar a un cálculo coherente dentro de la aplicación.
     * Los tipo de alertas pueden ser (optimo, precaución, peligroso)
     *
     * @param array $weatherDataPerDay
     * @return string
     */
    private function getAlertType(array $weatherDataPerDay): string
    {
        $alertaType = '';
        $vientoVelocidadPrevista = floatval($weatherDataPerDay['viento']['velocidad']);

        if($vientoVelocidadPrevista >= 0 && $vientoVelocidadPrevista < 50){
            $alertaType = 'optimo';
        }
        if($vientoVelocidadPrevista >= 50 && $vientoVelocidadPrevista < 70){
            $alertaType = 'precaucion';
        }
        if($vientoVelocidadPrevista >= 70){
            $alertaType = 'peligroso';
        }

        return $alertaType;
    }
```


## Set de datos
Se provee un API REST público donde se detalla el pronostico extendido de los próximos 3 días, incluyendo además, el día de hoy, correspondiente a cada departamento estudiado (Central, Caaguazú, Boquerón) bajo la URL https://xxxx.xxxx/xxx. 
Cada equipo deberá consumir estos datos y utilizarlo dentro de la aplicación.

### Ejemplo de respuesta de API en formato JSON
```
{
    "cod": "200",
    "message": 0,
    "departamento_list": [
        {
            "id": 11,
            "nombre": "Central",
            "población": 1866562,
            "coord": {
                "lat": -25.380646,
                "lon": -57.602323
            },
            "pronostico_extendido_list": [
                {
                    "fecha_hora_txt": "2024-05-11 06:00:00",
                    "dia_text": "hoy",
                    "main": {
                        "temp": 21.34,
                        "temp_min": 21.34,
                        "temp_max": 30.24,
                        "humedad": 100
                    },
                    "clima": [
                        {
                            "id": 1,
                            "tipo": "lluvia",
                            "description": "lluvia"
                        }
                    ],
                    "viento": {
                        "velocidad": 40.05,
                        "direccion": 66
                    },
                    "visibilidad": 5000,
                    "probabilidad_precipitacion": 0.99,
                    "lluvia": {
                        "volumen_1h": 0.4
                    }
                },
		{
			...
		}
            ]
        },
        {
            "id": 12,
            "nombre": "Boqueron",
            "población": 68595,
            "coord": {
                "lat": -22.125705,
                "lon": -60.737641
            },
            "pronostico_extendido_list": [
                {
			...
		}
	    ]
        },
        {
            "id": 13,
            "nombre": "Caaguazú",
            "población": 131143,
            "coord": {
                "lat": -25.460147,
                "lon": -56.026884
            },
            "pronostico_extendido_list": [
                {
			...
		}
	    ]
        }
    ]
}
```

### Campos de respuesta API en formato JSON

 - `cod` Parámetro interno
 - `message`Parámetro interno
 - `departamento_list`
	 - `id`Identificador del departamento
	 - `nombre`Nombre del departamento
	 - `poblacion`Población del departamento
	 - `coord`
		 - `lat`Ubicación geográfica, latitud
		 - `lon`Ubicación geográfica, longitud
	 - `pronostico_extendido_list`
		 - `fecha_hora_txt`fecha y hora del momento que se tomó las medidas en formato texto
		 - `dia_text`el día en formato texto. Puede tener como valor **hoy** que hace relación al día de la medición
       - `main`
         - `temp`Temperatura. Unidad predeterminada, medidas en grados celsius
         - `temp_min`Temperatura mínima en el momento del cálculo, medidas en grados celsius
         - `temp_max`Temperatura máxima en el momento del cálculo, medidas en grados celsius
         - `humedad`Medidas en porcentaje (%)
       - `clima`
         - `id`Identificador del clima
         - `tipo` Posibles valores (nublado_total, soleado, lluvia, tormenta_electrica, nublado_parcialemente, nieve)
         - `descripcion` Descripción del tipo de clima
       - `viento`
         - `velocidad` Velocidad del viento. Medidos en kilometros/hora.
         - `direccion` Dirección del viento. Medidos en grados
       - `visibilidad` Visibilidad media. Medidos en metros.
       - `probabilidad_precipitacion` Los valores del parámetro varían entre 0 y 1, donde 0 es igual al 0%, 1 es igual al 100%
       - `lluvia`
         - `volumen_1h` Volumen de lluvia de la última hora, medida en milimetros

## Recursos digitales
Dentro del repositorio, en la carpeta llamada *recursos_digitales* encontrarán lo siguiente:
- Un mockup básico que les servirá como guía de lo que se espera en el desarrollo de la página.
- La presentación del desafío hecho en powerpoint.
