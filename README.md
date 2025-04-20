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
Como parte del preprocesamiento de datos, se aplicó un **filtro de Sobel** a cada imagen con el fin de resaltar los bordes y contornos. Esta técnica permite al modelo captar mejor las características visuales que podrían ser distintivas entre distintas clases de virus.

```python
from scipy.ndimage import sobel
import numpy as np

# Aplicar filtro de Sobel en eje x e y
sobel_x = sobel(imagen, axis=0)
sobel_y = sobel(imagen, axis=1)
imagen_filtrada = np.hypot(sobel_x, sobel_y)
```

## Modelo

Se entrenó una red neuronal convolucional con:

- 2 capas Conv2D + MaxPooling
- Dropout para evitar overfitting
- Capa densa final con activación `softmax` para 10 clases
- Métrica principal: accuracy

## Resultados
El modelo alcanzó aproximadamente **88% de precisión** en el conjunto de prueba.  
Incluye visualización de la matriz de confusión y un `classification_report` detallado.

![Matriz de confusión](![image](https://github.com/user-attachments/assets/57e746a1-83bd-4960-bc73-1f8a8953598b))

## Cómo usar

```bash
git clone https://github.com/tuusuario/VirusMNIST-Classifier.git
cd VirusMNIST-Classifier
pip install -r requirements.txt
python virus_classifier.py
```
