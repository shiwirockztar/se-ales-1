🐕 DogSpeak Dataset
Descripción

DogSpeak es un dataset de vocalizaciones caninas diseñado para el desarrollo y evaluación de modelos de Machine Learning, Deep Learning y bioacústica computacional.

El dataset contiene grabaciones reales de perros obtenidas de videos disponibles en Internet, por lo que incluye vocalizaciones registradas en diferentes condiciones y contextos del mundo real.

A diferencia de datasets recopilados únicamente en ambientes controlados, DogSpeak busca proporcionar una mayor diversidad acústica para estudiar las vocalizaciones naturales de los perros.

📊 Información del dataset
Característica	Información
Nombre	DogSpeak
Tipo de datos	Audio / Vocalizaciones caninas
Número de secuencias	77.202 Bark Sequences
Número de perros	156
Número de razas	5
Formato de audio	WAV
Etiquetas principales	Raza y sexo
Licencia	CC BY-NC-SA 4.0
Razas incluidas

El dataset contiene vocalizaciones de las siguientes razas:

Chihuahua

German Shepherd

Husky

Pitbull

Shiba Inu

Sexo

Cada vocalización puede estar asociada con el sexo biológico del perro:

male

female

📁 Estructura del dataset

La estructura de los archivos es similar a la siguiente:

DogSpeak/
├── dogspeak_released/
│   ├── dog_1/
│   │   ├── 0_chihuahua_M_dog_1.wav
│   │   └── ...
│   ├── dog_2/
│   │   ├── 1_chihuahua_M_dog_2.wav
│   │   └── ...
│   ├── dog_7a/
│   │   ├── 0_chihuahua_M_dog_7a.wav
│   │   └── ...
│   └── dog_7b/
│       ├── 5957_chihuahua_M_dog_7b.wav
│       └── ...
└── metadata.csv


Cada carpeta corresponde a un perro identificado mediante un dog_id.

Los archivos de audio están almacenados en formato WAV.

Nota: la carpeta original dog_7 fue dividida en dog_7a y dog_7b debido a las limitaciones en el número de archivos permitidos por directorio en el repositorio. Ambas carpetas contienen los datos correspondientes al mismo perro.

📝 Metadata

El archivo metadata.csv contiene información asociada a cada secuencia de vocalización.

Campo	Descripción
filename	Nombre y ubicación del archivo de audio
breed	Raza del perro
sex	Sexo biológico del perro
dog_id	Identificador único del perro

Ejemplo:

filename,breed,sex,dog_id
dogspeak_released/dog_1/0_chihuahua_M_dog_1.wav,chihuahua,male,dog_1

🎯 ¿Para qué sirve?

DogSpeak puede utilizarse para diferentes aplicaciones relacionadas con inteligencia artificial y análisis de audio.

Algunos ejemplos son:

Clasificación de raza

Entrenar un modelo que reciba una vocalización y prediga la raza del perro.

Audio
  ↓
Modelo de Machine Learning
  ↓
Chihuahua / German Shepherd / Husky / Pitbull / Shiba Inu

Clasificación de sexo

También puede utilizarse para estudiar si las características acústicas de una vocalización permiten distinguir entre:

Audio
  ↓
Modelo
  ↓
Male / Female

Análisis de vocalizaciones

El dataset puede utilizarse para extraer características acústicas como:

Frecuencia fundamental.

Espectrogramas.

Mel-spectrogramas.

MFCCs.

Energía.

Duración.

Características temporales y espectrales.

Deep Learning

Puede utilizarse para entrenar modelos basados en:

CNN

RNN

LSTM

GRU

Transformers

Audio Transformers

Modelos de embeddings de audio

⚠️ Limitaciones

Es importante tener en cuenta que DogSpeak no es un dataset de traducción de lenguaje canino.

Por ejemplo, el dataset no proporciona necesariamente etiquetas como:

"El perro tiene hambre"
"El perro está triste"
"El perro está jugando"
"El perro tiene miedo"


Por lo tanto, no debería interpretarse directamente como un dataset para construir un "traductor de ladridos".

Su principal objetivo está relacionado con la clasificación y representación de vocalizaciones caninas, especialmente utilizando información como raza y sexo.

Para estudiar emociones, comportamientos o estados de ánimo sería necesario utilizar datasets que contengan ese tipo de anotaciones.

🧪 Ejemplo de carga

El dataset puede cargarse utilizando Python:

from pathlib import Path
import pandas as pd
import soundfile as sf

root = Path("DogSpeak")

# Cargar metadata
meta = pd.read_csv(root / "metadata.csv")

# Seleccionar una muestra
row = meta.iloc[0]

# Cargar audio
audio, sr = sf.read(
    root / "dogspeak_released" / row["filename"]
)

print("Forma del audio:", audio.shape)
print("Sample rate:", sr)
print("Raza:", row["breed"])
print("Sexo:", row["sex"])
print("Dog ID:", row["dog_id"])

🤖 Posibles proyectos

Este dataset puede utilizarse como base para proyectos como:

Clasificador de razas mediante audio.

Clasificador de sexo mediante vocalizaciones.

Sistema de reconocimiento de sonidos caninos.

Extracción de embeddings de ladridos.

Sistema de búsqueda de vocalizaciones similares.

Entrenamiento de modelos de audio con Deep Learning.

Investigación de patrones acústicos entre diferentes razas.

Preentrenamiento de modelos de bioacústica.

Análisis espectral y temporal de ladridos.

Investigación sobre comunicación animal.

🔬 Dataset relacionado

Existe otro dataset relacionado llamado Canine Age Transition Vocalization Dataset (CATVD).

CATVD está orientado al estudio del desarrollo vocal de los perros a lo largo de diferentes edades.

Incluye información como:

Edad en meses.

Grupo de edad.

Raza.

Tipo de ladrido.

Transcripciones EDBU.

Alineaciones temporales de unidades de ladrido.

CATVD contiene aproximadamente:

79.142 Bark Units

55.718 Bark Sequences

125 perros

6 razas

Aproximadamente 11,4 horas de vocalizaciones

Si se utilizan ambos datasets, se debe tener especial cuidado con posibles perros presentes en ambos conjuntos para evitar data leakage entre entrenamiento y evaluación.

⚖️ Licencia

DogSpeak se distribuye bajo la licencia:

Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)

Esto permite:

Compartir el dataset.

Adaptarlo.

Utilizarlo con fines no comerciales.

Siempre se debe proporcionar la atribución correspondiente y las obras derivadas deben distribuirse bajo la misma licencia.

Antes de utilizar el dataset en un proyecto comercial, se debe revisar cuidadosamente las condiciones de la licencia.

📚 Referencias
Paper

DogSpeak: A Canine Vocalization Classification Dataset

Lekhak, Hridayesh; Wang, Theron S.; Dang, Tuan M.; Zhu, Kenny Q.

Proceedings of the 33rd ACM International Conference on Multimedia, 2025.

Cita
@inproceedings{lekhak2025dogspeak,
  title={DogSpeak: A Canine Vocalization Classification Dataset},
  author={Lekhak, Hridayesh and Wang, Theron S and Dang, Tuan M and Zhu, Kenny Q},
  booktitle={Proceedings of the 33rd ACM International Conference on Multimedia},
  pages={13369--13375},
  year={2025}
}

📌 Resumen

DogSpeak es un dataset de gran escala de vocalizaciones caninas reales que puede utilizarse para investigar la relación entre las características acústicas de los ladridos y diferentes características del perro.

Con 77.202 secuencias de vocalización, 156 perros y 5 razas, proporciona una base útil para experimentar con Machine Learning, Deep Learning, procesamiento de señales, reconocimiento de audio y bioacústica computacional.

Importante: DogSpeak permite estudiar patrones en las vocalizaciones de los perros, pero no debe interpretarse como un dataset que contenga una traducción directa del "lenguaje" de los perros.