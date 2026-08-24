# MVP — Classificação do Posicionamento de Preço de Veículos

Este projeto utiliza uma base de veículos anteriormente empregada em um problema de regressão do Valor FIPE e a reformula como um problema de **classificação multiclasse**.

## Problema

O objetivo é classificar cada veículo em uma das seguintes categorias:

- **Abaixo do esperado**
- **Dentro do esperado**
- **Acima do esperado**

O preço de referência é calculado pela mediana do `Valor FIPE` de veículos da mesma **Montadora + Ano Modelo**.

### Regra de classificação

| Classe | Regra |
|---|---|
| Abaixo do esperado | FIPE < 90% do preço de referência |
| Dentro do esperado | 90% ≤ FIPE ≤ 110% do preço de referência |
| Acima do esperado | FIPE > 110% do preço de referência |

Para grupos com menos de 3 veículos, é usada a mediana da Montadora como fallback. Se necessário, a mediana geral da base é utilizada.

## Variáveis

### Features

- Montadora
- Modelo
- Cor
- Grupo
- Situação
- Ano Modelo

### Target

- `posicionamento_preco`

O `Valor FIPE`, o preço de referência e o índice de preço **não entram nas features**, pois são utilizados na construção do target.

## Modelos

O notebook compara:

1. Dummy Classifier
2. Regressão Logística
3. Random Forest
4. Random Forest otimizado com GridSearchCV

## Métricas

- Acurácia
- Precisão ponderada
- Recall ponderado
- F1 ponderado
- F1 Macro
- Matriz de confusão
- Análise de overfitting

A principal métrica de seleção é o **F1 Macro**, pois trata as três classes com o mesmo peso.

## Estrutura

```text
mvp_posicionamento_preco_veiculos/
├── MVP_Posicionamento_Preco_Veiculos.ipynb
├── README.md
├── requirements.txt
└── .gitignore
```

## Execução no Google Colab

1. Abra o notebook `MVP_Posicionamento_Preco_Veiculos.ipynb`.
2. Execute as células em ordem.
3. Faça upload da base original de veículos quando solicitado.
4. O notebook aceita `.xlsx`, `.xls` e `.csv`.

## Requisitos da base

A base deve possuir:

- `Montadora`
- `Modelo`
- `Cor`
- `Grupo`
- `Situação`
- `Ano Modelo`
- `Valor FIPE`

## Aplicação prática

O MVP pode apoiar:

- análise de portfólio de veículos;
- identificação de veículos fora do padrão de preço;
- gestão de frotas;
- triagem comercial;
- análise de ativos.

## Observação metodológica

O conceito de "barato" ou "caro" neste MVP é **relativo ao benchmark da própria base** e não representa uma avaliação completa do mercado. Variáveis como quilometragem, versão, combustível, opcionais e região poderiam melhorar significativamente a análise.

## Autor

Andre Luiz Marques Serrano
