# projeto_final_classificacao_multiclasses

# Projeto Final - Classificação de Textos: Multirrótulo e Multiclasse

Este repositório contém dois projetos complementares de classificação de textos, utilizando a mesma base de dados, com foco em problemas de:

- **Classificação Multirrótulo (Multilabel)**
- **Classificação Multiclasse (Multiclass)**

Ambos os projetos foram desenvolvidos em Python utilizando `TensorFlow` e `scikit-learn`.

---

## 📁 Estrutura dos Projetos

### 1. Classificação Multirrótulo

> Cada amostra pode possuir **mais de um rótulo**.

- **Métricas Avaliadas**:
  - `Precision@K`
  - `Recall` médio por amostra
  - `F1-score` médio por amostra
  - `Hamming Loss`

#### ✅ Resultados obtidos:

| Modelo                      | Precision | Recall | F1     | Hamming Loss |
|----------------------------|-----------|--------|--------|---------------|
| Modelo Base                | 0.7900    | 0.5377 | 0.5959 | 0.0198        |
| Modelo Base + PCA          | 0.7073    | 0.5899 | 0.5992 | 0.0220        |
| Modelo Base + Blocos       | 0.8046    | 0.4004 | 0.5013 | 0.0212        |
| Modelo Customizado         | 0.4600    | 0.1820 | 0.2505 | 0.0267        |

---

### 2. Classificação Multiclasse

> Cada amostra pertence **a apenas um rótulo**.

- A base de dados multirrótulo foi adaptada com uma estratégia de **remapeamento para rótulo único**.
- **Saída**: Softmax sobre o total de classes.
- **Função de Perda**: `sparse_categorical_crossentropy`.
- **Métricas Avaliadas**:
  - `Precision`
  - `Recall`
  - `F1-score` macro

#### ✅ Resultados obtidos:

| Modelo                      | Precision | Recall | F1     |
|----------------------------|-----------|--------|--------|
| Modelo Base                | 0.5355    | 0.6100 | 0.5515 |
| Modelo Base + Blocos       | 0.5952    | 0.6200 | 0.5898 |
| Modelo Base + PCA          | 0.4703    | 0.5850 | 0.5019 |
| Modelo Customizado         | 0.4832    | 0.5050 | 0.4264 |

---

## 🧠 Arquiteturas dos Modelos

- **Modelo Base**: MLP simples com uma camada densa.
- **Modelo Base + PCA**: Redução dimensional das features de entrada.
- **Modelo Base + Blocos**: Uso de camadas intermediárias com Dropout e BatchNormalization.
- **Modelo Customizado**: Arquitetura mais profunda com ajuste de learning rate, número de neurônios, dropout e regularizações.

---

## 📊 Visualizações e Avaliação

Todos os notebooks apresentam:
- Código comentado e organizado por seções.
- Avaliação por época com callback customizado.
- Gráficos de perda, métricas e matriz de confusão (multiclasse).
- Seção final com **código completo para execução direta**.

---

Conclusão
O projeto alcançou com sucesso os objetivos propostos para os dois cenários de classificação: multirrótulo e multiclasse.

A base utilizada foi o conjunto RCV1 (Reuters Corpus Volume 1), carregado diretamente via sklearn.datasets.fetch_rcv1. Essa base é composta por milhares de notícias jornalísticas com múltiplas categorias por documento — o que a torna ideal para problemas de classificação multirrótulo. Para este projeto, foi utilizado um subconjunto de 1.000 amostras para facilitar a prototipação e testes computacionais.

Na classificação multirrótulo, os modelos conseguiram prever múltiplos rótulos por amostra com boa precisão e baixa taxa de erro (Hamming Loss). O modelo com blocos adicionais (BatchNorm e Dropout) foi o que apresentou melhor equilíbrio entre precisão e robustez.

Para a classificação multiclasse, a base multirrótulo foi adaptada convertendo cada amostra para um único rótulo dominante. O remapeamento foi eficaz, e os modelos apresentaram resultados satisfatórios, com destaque para o modelo com camadas ocultas adicionais, que obteve o melhor desempenho geral.

Apesar das limitações impostas pelo número reduzido de amostras, os resultados demonstraram que as arquiteturas propostas são capazes de aprender representações úteis e generalizáveis. Assim, o experimento foi bem-sucedido, comprovando a aplicabilidade de redes neurais profundas tanto para problemas de múltiplos rótulos simultâneos quanto para classificação exclusiva por classe.

