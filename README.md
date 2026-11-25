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
| 4 | [`Punto4_Arquitectura_Modelos_Video.docx`](punto%204/Punto4_Arquitectura_Modelos_Video.docx) | Documento sobre la **arquitectura de los modelos de generación de video** actuales: VAE causal 3D, parches espaciotemporales, Diffusion Transformers, flow matching y casos (Sora, Veo 3, Movie Gen, HunyuanVideo, Wan, CogVideoX). |

## Resultados

> Valores obtenidos al ejecutar los notebooks en Google Colab con GPU T4.

**Punto 1A · MNIST** (1.000 imágenes, distancias contra el conjunto de prueba)

| Conjunto | FID ↓ | KID×1000 ↓ | Classifier Score ↑ |
|---|---|---|---|
| Real (línea base) | _completar_ | _completar_ | _completar_ |
| Generadas (DDPM) | _completar_ | _completar_ | _completar_ |
| Ruido (peor caso) | _completar_ | _completar_ | _completar_ |

**Punto 1B · CIFAR-10** (2.000 imágenes, InceptionV3)

| Conjunto | FID ↓ | KID×1000 ↓ | IS ↑ |
|---|---|---|---|
| Real (línea base) | _completar_ | _completar_ | _completar_ |
| DDPM (1000 pasos) | _completar_ | _completar_ | _completar_ |
| DDIM (100 pasos) | _completar_ | _completar_ | _completar_ |
| Ruido (peor caso) | _completar_ | _completar_ | _completar_ |

**Punto 2 · Oxford Flowers** — KID generadas vs. reales: _completar_ (piso real vs. real: _completar_)

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
| 1A · MNIST | ~20 min |
| 1B · CIFAR-10 | ~45 min |
| 2 · Oxford Flowers (100 épocas) | ~1 h |
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
