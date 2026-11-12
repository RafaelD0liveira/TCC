# Estratégias de *factor investing* no universo do ISE B3 (2016 a 2025)

Código, dados e resultados do Trabalho de Conclusão de Curso de Rafael Diniz Oliveira, do curso de
Ciências Econômicas da Faculdade Ibmec de Brasília, orientado pelo Prof. Ms. Laerte Jun Takeuti.

O estudo monta, a cada ano, carteiras com as ações do Índice de Sustentabilidade Empresarial da B3
(ISE B3), escolhidas pelos fatores *momentum*, baixa volatilidade, valor e qualidade, e compara o
desempenho dessas carteiras com o do IBrX-100 e com o do próprio ISE B3. Este repositório reúne
tudo o que é necessário para reproduzir as tabelas, os gráficos e os números do trabalho.

## O que há no repositório

| Item | Conteúdo |
|---|---|
| `carteira_factor_investing.py` | O código do estudo, em um único arquivo. O cabeçalho indica em que parte do código está cada seção, tabela e equação do TCC. |
| `requirements.txt` | As bibliotecas do Python, nas versões usadas no trabalho. |
| `dados/` | Os dados lidos pelo código. |
| `resultados/` | As tabelas, os gráficos e os números gerados pelo código. |

## Como reproduzir os resultados

1. Instalar o Python 3.11 ou mais recente.
2. Na pasta do repositório, instalar as bibliotecas:

   ```
   python -m pip install -r requirements.txt
   ```

3. Rodar o estudo, o que leva cerca de dez segundos:

   ```
   python carteira_factor_investing.py
   ```

O código roda sem internet e sem token, porque todos os dados usados estão na pasta `dados/`.
A tela mostra as Tabelas 1 a 7 do TCC e os números citados no texto, e tudo é gravado de novo em
`resultados/`. Com as versões de `requirements.txt`, os resultados são iguais aos do trabalho.

## Onde está cada resultado do TCC

| No TCC | Arquivo em `resultados/` |
|---|---|
| Tabela 1 – Número de ações em cada ano | `tabela_1_acoes_por_ano.csv` |
| Tabela 2 – Desempenho das carteiras e dos índices | `tabela_2_desempenho.csv` |
| Tabela 3 – Retorno de cada ano | `tabela_3_retorno_de_cada_ano.csv` |
| Tabela 4 – Quedas do IBrX-100 e recuperações | `tabela_4_quedas_e_recuperacoes.csv` |
| Tabela 5 – Participação dos setores | `tabela_5_setores.csv` |
| Tabela 6 – Custos de negociação | `tabela_6_custos.csv` |
| Tabela 7 – Ciclo completo de cada grande queda | `tabela_7_ciclos_completos.csv` |
| Gráfico 1 – Evolução de R$ 100 | `figuras/grafico_1_patrimonio.png` |
| Gráfico 2 – Queda acumulada | `figuras/grafico_2_quedas.png` |
| Apêndice A – Ações de cada carteira, ano a ano | `apendice_A_acoes_de_cada_carteira.csv` |
| Apêndice B – Ações que ficaram fora da escolha | `detalhes/exclusoes.csv` |
| Números citados no texto, com a seção | `numeros_citados_no_texto.csv` |

As tabelas estão no formato do Excel em português, com ponto e vírgula entre as colunas e vírgula
decimal. A pasta `resultados/detalhes/` traz os dados completos, sem arredondamento: retornos
diários, fatores de cada ação, composição das carteiras, exclusões, remontagens e custos, eventos
societários, quedas e setores.

## Os dados

As ações do ISE B3 de cada ano e os códigos de negociação que mudaram estão escritos no próprio
código (Parte 2). Os demais dados estão em `dados/`:

| Arquivo | Conteúdo | Fonte |
|---|---|---|
| `precos.csv` | Fechamentos diários das ações, ajustados por proventos e desdobramentos | Laboratório de Finanças, com o Yahoo Finance como fonte alternativa |
| `indices_e_selic.csv` | Valores diários do ISE B3 e do IBrX-100 e taxa Selic | Estatísticas históricas da B3 e série 1178 do Banco Central do Brasil |
| `fundamentos/` | Dez consultas de P/VP, ROE, ROIC e setor, uma para cada data de montagem das carteiras | Laboratório de Finanças |
| `eventos.json` | Eventos societários aplicados às carteiras, com a relação de troca | Documentos das empresas e da B3 |
| `documentos_eventos/` | O documento de cada evento societário | Empresas e B3 |

O código confere o código de verificação (SHA-256) de cada consulta de `fundamentos/` e recusa
qualquer dado com data posterior à da escolha das ações. Os arquivos de `dados/` não devem ser
alterados, porque os resultados do trabalho dependem deles.

## Token do Laboratório de Finanças (opcional)

O código roda sem token, porque todas as consultas usadas no estudo estão guardadas em
`dados/fundamentos`. O token é necessário apenas para baixar esses dados novamente da fonte. Ele é
pessoal, é obtido com uma conta no site do Laboratório de Finanças (laboratoriodefinancas.com) e
muda todos os dias; por isso, deve ser gerado no dia do uso.

Para baixar as consultas novamente:

1. Abrir `carteira_factor_investing.py` e ir à Parte 1 (Configuração).
2. Colar o token entre as aspas de `TOKEN_LAB_FINANCAS = ""`.
3. Na linha seguinte, trocar `ATUALIZAR_FUNDAMENTOS = False` por `True`.
4. Rodar o estudo normalmente.

As consultas baixadas substituem as guardadas. Se a fonte tiver revisado algum dado desde a data do
estudo, os resultados podem mudar; por isso, recomenda-se fazer esse teste em uma cópia da pasta.
O código não deve ser divulgado com o token preenchido.
