# MVP1 de SSD - Classificação do Posicionamento de Preço de Veículos

**Disciplina:** Sistemas de Suporte à Decisão  
**Universidade de Brasília (UnB)**  
**Aluno:** Juliano Teles Abrahao - 231013411

Este projeto apresenta um MVP de classificação do posicionamento de preço de veículos, utilizando uma base de dados com informações como **montadora, modelo, cor, grupo, situação, ano do modelo e Valor FIPE**.

## Objetivo

Treinar e comparar modelos de Machine Learning para classificar o posicionamento de preço dos veículos em 3 categorias:

- **Abaixo do esperado**
- **Dentro do esperado**
- **Acima do esperado**

A classificação é realizada comparando o **Valor FIPE de cada veículo com um valor de referência de veículos semelhantes**, permitindo identificar automaticamente se seu preço está abaixo, dentro ou acima do padrão esperado.

## Definição do Problema

O projeto é tratado como um problema de **classificação multiclasse**.

Para cada veículo, é calculado um preço de referência utilizando a mediana do `Valor FIPE` de veículos da mesma **Montadora + Ano Modelo**.

### Regra de classificação

| Classe | Regra |
|---|---|
| Abaixo do esperado | FIPE < 90% do preço de referência |
| Dentro do esperado | 90% ≤ FIPE ≤ 110% do preço de referência |
| Acima do esperado | FIPE > 110% do preço de referência |

Quando um grupo possui menos de 3 veículos, é utilizada a mediana da montadora como referência. Se necessário, é usada a mediana geral da base.

## Hipótese

Características como **Modelo, Grupo, Situação, Cor, Montadora e Ano Modelo** contêm informação suficiente para explicar se um veículo tende a ficar abaixo, dentro ou acima do padrão de preço de veículos semelhantes.

O `Valor FIPE`, o preço de referência e o índice de preço são utilizados apenas para construir a variável alvo e **não entram como features do modelo**, evitando vazamento de informação.

## Variáveis Utilizadas

### Features

- Montadora
- Modelo
- Cor
- Grupo
- Situação
- Ano Modelo

### Target

- `posicionamento_preco`

## Modelos Comparados

1. **Dummy Classifier** — baseline mínimo
2. **Regressão Logística** — baseline supervisionado
3. **Random Forest** — modelo principal
4. **Random Forest otimizado** com GridSearchCV

## Métricas de Avaliação

- Acurácia
- Precisão ponderada
- Recall ponderado
- F1-Score ponderado
- F1-Score Macro
- Matriz de confusão
- Análise de overfitting

A métrica principal para comparação dos modelos é o **F1 Macro**, pois atribui o mesmo peso às três classes.

## Estrutura do Repositório

```text
mvp_posicionamento_preco_veiculos/
├── MVP1_SSD_Posicionamento_Preco_Veiculos.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Requisitos da Base

A base deve conter as seguintes colunas:

- `Montadora`
- `Modelo`
- `Cor`
- `Grupo`
- `Situação`
- `Ano Modelo`
- `Valor FIPE`

## Aplicações

O MVP pode ser utilizado para:

- análise de portfólio de veículos;
- identificação de veículos fora do padrão de preço;
- gestão de frotas;
- triagem comercial;
- análise de ativos.

## Limitações

O conceito de veículo "abaixo", "dentro" ou "acima" do preço esperado é relativo ao benchmark construído a partir da própria base.

Variáveis como quilometragem, versão, combustível, câmbio, opcionais e localização poderiam melhorar a precisão e a interpretação do posicionamento de preço.

---

**Aluno:** Juliano Teles Abrahao  
**Matrícula:** 231013411  
**Disciplina:** Sistemas de Suporte à Decisão  
**Universidade de Brasília (UnB)**
