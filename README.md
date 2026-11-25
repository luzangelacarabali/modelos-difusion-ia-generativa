# Modelos generativos de imágenes basados en difusión

**Universidad Autónoma de Occidente** · Facultad de Ingeniería y Ciencias Básicas
Inteligencia Artificial Generativa · Ingeniería de Datos e Inteligencia Artificial
Profesores: Jesús Alfonso López – José Luis Paniagua

Autora: **Luz Ángela Carabalí Mulato** · [GitHub](https://github.com/luzangelacarabali) · [LinkedIn](https://www.linkedin.com/in/luz-angela-carabali-mulato-12b561306)

---

Este repositorio reúne el entregable sobre **modelos de difusión** para generación de imágenes. Va desde entrenar un DDPM desde cero hasta desarmar Stable Diffusion pieza por pieza, y termina con un documento sobre la arquitectura de los modelos actuales de generación de video.

## Contenido

| Punto | Archivo | Qué hace |
|---|---|---|
| 1A | [`Punto1A_Difusion_MNIST.ipynb`](punto%201/punto%201A/Punto1A_Difusion_MNIST.ipynb) | DDPM (UNet + programación coseno, T = 4000) entrenado con **MNIST**. Evaluación con FID, KID, *Classifier Score*, confianza y cobertura de clases usando un clasificador propio de MNIST. |
| 1B | [`Punto1B_Difusion_CIFAR10.ipynb`](punto%201/punto%201B/Punto1B_Difusion_CIFAR10.ipynb) | Adaptación a imágenes **a color (CIFAR-10, 32×32×3)**: UNet más ancha, aumento de datos, pesos EMA y muestreo **DDPM vs. DDIM**. Evaluación con **FID, KID e Inception Score** sobre InceptionV3. |
| 2 | [`Punto2_Difusion_OxfordFlowers.ipynb`](punto%202/Punto2_Difusion_OxfordFlowers.ipynb) | Réplica del capítulo 17 de *Deep Learning with Python, 3.ª ed.* (Chollet & Watson): difusión con **Oxford Flowers 102** a 128×128. Incluye experimentos extra: número de pasos, proceso inverso, interpolación en el espacio de ruido y KID. |
| 3 | [`Punto3_StableDiffusion_Componentes.ipynb`](punto3/Punto3_StableDiffusion_Componentes.ipynb) | **Stable Diffusion v1.5** desarmado con `diffusers`: tokenizer + CLIP, VAE (latente **4×64×64** vs. píxeles **3×512×512**), U-Net, scheduler, ciclo de generación escrito a mano, mapas de atención cruzada y efecto de la guía (CFG). |
| 4 | [`Punto4_Arquitectura_Modelos_Video.pdf`](punto%204/Punto4_Arquitectura_Modelos_Video.pdf) | Documento sobre la **arquitectura de los modelos de generación de video** actuales: VAE causal 3D, parches espaciotemporales, Diffusion Transformers, flow matching y casos (Sora, Veo 3, Movie Gen, HunyuanVideo, Wan, CogVideoX). |

## Resultados

> Valores obtenidos al ejecutar los notebooks. El análisis completo está al final de cada notebook.

**Punto 1A · MNIST** (1.000 imágenes, distancias contra el conjunto de prueba)

| Conjunto | FID ↓ | KID×1000 ↓ | Classifier Score ↑ |
|---|---|---|---|
| Real (línea base) | 21,9 | 36.805 | 9,41 |
| **Generadas (DDPM)** | **373,2** | **1.001.998** | **7,08** |
| Ruido (peor caso) | 2.532,8 | 1.952.986 | 1,00 |

Los diez dígitos aparecen en proporciones entre 7,7 % y 14 % (entropía de clases 2,28 de un máximo de 2,30): no hay colapso de modos. El KID está en una escala arbitraria porque las características del clasificador no están normalizadas.

**Punto 1B · CIFAR-10** (2.000 imágenes, InceptionV3)

| Conjunto | FID ↓ | KID×1000 ↓ | IS ↑ |
|---|---|---|---|
| Real (línea base) | 26,2 | 0,01 | 9,70 |
| **DDPM (1000 pasos)** | **79,0** | **46,3** | **4,33** |
| **DDIM (100 pasos)** | **75,6** | **44,8** | **4,34** |
| Ruido (peor caso) | 610,5 | 896,6 | 1,27 |

DDIM con 100 pasos iguala la calidad de DDPM con 1000 y es 10 veces más rápido (0,028 frente a 0,274 s por imagen).

**Punto 2 · Oxford Flowers** — 100 épocas en ~3 h sobre una T4; la pérdida bajó de 0,92 a 0,134. Las muestras reproducen pétalos, colores y fondos de las fotos reales, con 20 pasos de DDIM.

<!-- Opcional: agrega aquí imágenes de muestra, por ejemplo:
![Dígitos generados](imagenes/mnist_generados.png)
![Proceso de Stable Diffusion](imagenes/proceso_stable_diffusion.gif)
-->

## Cómo ejecutarlo

Los notebooks están pensados para **Google Colab con GPU**:

1. Abre [colab.research.google.com](https://colab.research.google.com) → **Subir** → escoge el notebook.
2. **Entorno de ejecución → Cambiar tipo de entorno de ejecución → T4 GPU**.
3. **Entorno de ejecución → Ejecutar todas**.

Tiempos aproximados en una T4:

| Notebook | Tiempo |
|---|---|
| 1A · MNIST | ~30 min |
| 1B · CIFAR-10 | ~45 min |
| 2 · Oxford Flowers (100 épocas) | ~3 h |
| 3 · Stable Diffusion | ~15 min (sin entrenamiento) |

> En Windows, TensorFlow no tiene soporte de GPU, así que no se recomienda entrenar localmente.

## Tecnologías

TensorFlow · Keras (legacy y Keras 3) · PyTorch · Hugging Face `diffusers` y `transformers` · NumPy · SciPy · Matplotlib

## Referencias

- Ho, Jain & Abbeel (2020). [Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2006.11239).
- Nichol & Dhariwal (2021). [Improved Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2102.09672).
- Song, Meng & Ermon (2021). [Denoising Diffusion Implicit Models](https://arxiv.org/abs/2010.02502).
- Rombach et al. (2022). [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752).
- Chollet & Watson. [Deep Learning with Python, 3.ª ed., capítulo 17](https://deeplearningwithpython.io/chapters/chapter17_image-generation/).
- Géron, A. *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow*, 3.ª ed., capítulo 17 (código base del DDPM de clase).
- Heusel et al. (2017). [GANs Trained by a Two Time-Scale Update Rule (FID)](https://arxiv.org/abs/1706.08500).
