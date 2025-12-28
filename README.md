# Classificação de Raças de Cães e Gatos 🐶🐱

Este projeto consiste em um estudo comparativo de técnicas de Visão Computacional e Aprendizado de Máquina para a classificação de imagens de quatro raças específicas de cães e gatos.

O foco central do trabalho é a **análise experimental de diferentes métodos de extração de características** (Feature Extraction), contrastando abordagens clássicas com Deep Learning, além da aplicação de redução de dimensionalidade e validação robusta.

## 🎯 Objetivo

Classificar corretamente imagens nas seguintes 4 classes:
*   **American Bulldog**
*   **Bengal**
*   **Pug**
*   **Ragdoll**

## 🧪 Técnicas e Abordagem Experimental

Este projeto destaca-se pela variedade de cenários de teste construídos para avaliar o impacto da representação dos dados na performance dos classificadores.

### 1. Extração de Características (Feature Extraction)

Foram gerados e comparados **12 datasets distintos** baseados em diferentes configurações:

#### A. HOG (Histogram of Oriented Gradients) - Abordagem Clássica
Foram testadas variações na resolução da imagem e no tamanho das células para capturar gradientes e bordas:
*   **Resoluções:** 128x128 e 256x256 pixels.
*   **Células:** 16x16 e 20x20.
*   *Total: 4 variações.*

#### B. CNN (Convolutional Neural Networks) - Transfer Learning
Utilizou-se redes pré-treinadas na *ImageNet* apenas como extratoras de características (sem retreino/fine-tuning), testando diferentes arquiteturas e métodos de pooling:
*   **Arquiteturas:** VGG16 e VGG19.
*   **Pooling:** Global Average Pooling e Global Max Pooling.
*   **Resoluções:** 128x128 e 256x256 pixels.
*   *Total: 8 variações.*

### 2. Redução de Dimensionalidade
*   **PCA (Principal Component Analysis):** Aplicado às 6 melhores bases (identificadas na etapa anterior) para reduzir o número de atributos para 10 componentes principais, visando analisar o comportamento da acurácia com menos features e menor ruído.

### 3. Modelos de Classificação
Os datasets gerados alimentaram dois tipos de classificadores supervisionados, onde foram variados seus hiperparâmetros:
*   **k-NN (k-Nearest Neighbors):** Testes com $k$ variando de 1 a 10.
*   **Árvore de Decisão (Decision Tree):** Testes com profundidade máxima (`max_depth`) variando de 2 a 10.

### 4. Validação dos Modelos
Para garantir a robustez dos resultados, todos os experimentos foram submetidos a duas estratégias de validação:
1.  **Hold-out:** Divisão 70% Treino / 30% Teste (com estratificação).
2.  **Cross-Validation:** Validação cruzada estratificada com 10 folds (10-fold CV).

## 📊 Resultados Observados

O notebook contém uma análise detalhada (tabelas e rankings), mas as conclusões gerais apontam para:
*   **Superioridade das CNNs:** As características extraídas via VGG16/VGG19 superaram drasticamente o HOG, demonstrando a capacidade das redes neurais de capturar padrões semânticos complexos (texturas, formas) que o HOG (focado em bordas) não consegue.
*   **Impacto do PCA:** A redução para apenas 10 componentes principais em bases extraídas por CNN manteve ou até aumentou a acurácia, indicando alta redundância nas features originais da VGG e eficiência do PCA em filtrar ruído.
*   **Pooling:** Variações entre Max e Average pooling mostraram diferenças sutis dependendo da resolução da imagem.

## 🛠️ Tecnologias Utilizadas

*   **Linguagem:** Python
*   **Ambiente:** Jupyter Notebook / Google Colab
*   **Bibliotecas Principais:**
    *   `scikit-learn`: Para modelos (k-NN, Decision Tree), PCA, métricas e validação.
    *   `scikit-image`: Para pré-processamento e extração HOG.
    *   `tensorflow.keras`: Para carregar as arquiteturas VGG16 e VGG19.
    *   `pandas` & `numpy`: Manipulação de dados.

## 🚀 Como Executar

1.  Clone este repositório.
2.  Abra o arquivo `Atividade_AM.ipynb` em um ambiente Jupyter ou Google Colab.
3.  O notebook foi estruturado para fazer o upload das imagens e processá-las em sequência.
4.  Execute as células sequencialmente para reproduzir a extração de características, o treinamento e a geração das tabelas de resultados.

---
*Este projeto foi desenvolvido como atividade acadêmica focada em Aprendizado de Máquina.*
