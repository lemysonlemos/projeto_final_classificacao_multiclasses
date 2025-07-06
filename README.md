# projeto_final_classificacao_multiclasses

Projeto: Classificação Multilabel de Vídeos Usando Embeddings
Este projeto implementa uma pipeline completa para classificação multilabel em um problema com 4.800 classes (como no YouTube-8M), usando embeddings pré-extraídos de vídeos e áudio (simulados aqui para facilitar).

O objetivo é desenvolver e comparar diferentes arquiteturas de modelos MLP seguindo as seguintes etapas:

Estrutura do Trabalho
1. Modelo Base
Modelo MLP simples (Dense Layer) que recebe como entrada embeddings de vídeo+áudio.

Camada de saída com 4.800 neurônios com ativação sigmoid (para multilabel).

Função de perda: binary_crossentropy, apropriada para multilabel.

Métricas: precision@k (ex: top 20), recall, f1-score multilabel, hamming loss.

Treinamento com callback customizado para cálculo e exibição das métricas.

2. Modelo Base + Variações de n_features
Exploração do uso separado das features de áudio e vídeo.

Uso de PCA para redução dimensional (exemplo reduzindo 1152 para 256 features).

Avaliação do impacto da redução dimensional no desempenho.

3. Modelo Base + Blocos
Adição de camadas BatchNormalization e Dropout para regularização.

Uso de múltiplas camadas densas com funções de ativação ReLU.

Modelo mais profundo que o base para melhor capacidade de representação.

4. Seu Modelo
Arquitetura própria, mais complexa, com mais camadas e regularizações.

Ajuste do learning rate, dropout, ativação e número de neurônios.

Exemplo dado com 3 camadas densas, BatchNorm, Dropout e taxa de aprendizado menor.

Métricas e Avaliação
Precision@k: Mede a precisão entre as top-k predições para cada amostra.

Recall e F1-Score multilabel: Usando média por amostra para avaliar acurácia global.

Hamming Loss: Mede a fração de rótulos incorretamente previstos.

Matriz de confusão multilabel pode ser feita, mas não é trivial neste contexto.

Como o código funciona
Simula os dados de entrada (1000 amostras, 1152 features, 4800 classes multilabel).

Divide em treino (80%) e validação (20%).

Define 4 modelos diferentes, um para cada etapa descrita.

Treina cada modelo por 5 épocas e imprime métricas ao final de cada época.

Métricas calculadas via callbacks customizados durante o treino.

Como executar
Clone este repositório

Instale as dependências:
pip install tensorflow scikit-learn numpy

