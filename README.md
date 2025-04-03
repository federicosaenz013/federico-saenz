# federico-saenz
# Optimización de Prompts para Changuita con IA

## 1. Instalación e Importación de Librerías

# Instalamos librerías necesarias (descomentar si es necesario)
# !pip install openai
# !pip install pillow

import openai  # Para probar los prompts en modelos de IA
from PIL import Image  # Para pruebas de generación de imágenes
import requests
from io import BytesIO

## 2. Configuración de la API (Reemplazar con tu clave si es necesario)
openai.api_key = "TU_API_KEY"

## 3. Generación de Prompts - Texto a Texto

def generar_respuesta(prompt):
    """Genera una respuesta usando GPT-4 a partir del prompt."""
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "system", "content": "Eres un asistente experto en recomendación de servicios."},
                  {"role": "user", "content": prompt}],
        max_tokens=200
    )
    return response['choices'][0]['message']['content']

# Ejemplo de prueba con un prompt optimizado
prompt_test = "Encuentra un electricista calificado con buenas reseñas en un radio de 5km."
respuesta_test = generar_respuesta(prompt_test)
print("Respuesta del modelo:", respuesta_test)

## 4. Generación de Imágenes con IA

def generar_imagen(prompt):
    """Genera una imagen basada en un prompt usando IA."""
    response = openai.Image.create(
        prompt=prompt,
        n=1,
        size="512x512"
    )
    image_url = response['data'][0]['url']
    return image_url

# Ejemplo de generación de imagen
prompt_imagen = "Ilustración de un electricista trabajando en una instalación segura y moderna."
url_imagen = generar_imagen(prompt_imagen)

# Mostrar la imagen generada
response = requests.get(url_imagen)
img = Image.open(BytesIO(response.content))
img.show()

## 5. Optimización de Prompts con Técnicas Avanzadas

# Ejemplo de Chain-of-Thought Prompting
prompt_cot = "Piensa paso a paso. ¿Cómo puedo encontrar un plomero confiable en mi ciudad?"
respuesta_cot = generar_respuesta(prompt_cot)
print("Respuesta con Chain-of-Thought:", respuesta_cot)

# Ejemplo de Few-Shot Prompting
prompt_fewshot = "Aquí tienes un ejemplo de un buen anuncio de servicio: 'Soy Juan, carpintero con 10 años de experiencia.' Ahora genera uno para un electricista."
respuesta_fewshot = generar_respuesta(prompt_fewshot)
print("Respuesta con Few-Shot Prompting:", respuesta_fewshot)
