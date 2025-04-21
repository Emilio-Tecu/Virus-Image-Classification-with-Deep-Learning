# VirusMNIST-Classifier

Este proyecto utiliza redes neuronales convolucionales (CNN) para identificar y clasificar imágenes de software benigno y de malware, usando imágenes similares a MNIST generadas a partir de ejecutables.

## Descripción

VirusMNIST es un conjunto de datos que transforma archivos `.exe` en imágenes de 28x28 píxeles en escala de grises. Este modelo es capaz de distinguir entre **10 clases**, que incluyen tanto software benigno como varios tipos de malware (Adware, Trojan, Crypto, etc.).

> Dataset disponible en:  
👉 [https://www.kaggle.com/datasets/datamunge/virusmnist](https://www.kaggle.com/datasets/datamunge/virusmnist)

## Clases del Dataset

| Clase | Grupo    | Tipo       | Ejemplo        | Frecuencia |
|-------|----------|------------|----------------|------------|
| 0     | Beneware | Good       | putty.exe      | 2,516      |
| 1     | Malware  | Adware     | IESettings     | 7,684      |
| 2     | Malware  | Trojan     | Supreme.exe    | 3,037      |
| 3     | Malware  | Trojan     | myfile.exe     | 2,404      |
| 4     | Malware  | Installer  | myfile.exe     |   796      |
| 5     | Malware  | Backdoor   | myfile.exe     | 6,662      |
| 6     | Malware  | Crypto     | Powershell     | 15,377     |
| 7     | Malware  | Backdoor   | BitTorrent.exe | 7,494      |
| 8     | Malware  | Downloader | myfile.exe     | 2,571      |
| 9     | Malware  | Heuristic  | myfile.exe     | 3,339      |

## Preprocesamiento con filtros
Como parte del preprocesamiento de datos, se aplicó un **filtro de gaussiano** a cada imagen con el fin de reducir el ruido. 
```python
def aplicar_gaussiano(img):
    # Se aplica un filtro gaussiano para suavizar la imagen,
    # lo cual ayuda a reducir el ruido y resalta las estructuras más relevantes.
    return gaussian_filter(img, sigma=1)
```

## Modelo

Se entrenó una red neuronal convolucional con:

- 2 capas Conv2D + MaxPooling
- Dropout para evitar overfitting
- Capa densa final con activación `softmax` para 10 clases
- Métrica principal: accuracy

## Resultados
El modelo alcanzó **87% de precisión** en el conjunto de prueba, no obstante existen pequeñas dificultades al trabajar con virus benignos, pues la identificación de los mismos es confusa para el modelo.  

