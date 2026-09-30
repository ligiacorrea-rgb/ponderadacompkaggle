# Campeonato Inteli Módulo 3 2026 — Entrega final

Previsão de resultados do Brasileirão (LogLoss multiclasse), competição Kaggle
"Campeonato Inteli Módulo 3 2026".

## Conteúdo

- `entrega_kaggle_futebol.zip` — pacote com o notebook e os dois CSVs abaixo.
- `final_notebook_v3_v4.ipynb` — notebook completo (executado do início ao fim) com
  todo o processo: features, validação temporal (walk-forward por temporada) e geração
  das duas submissões finais.
- `submission_v3.csv` / `submission_v4.csv` — as duas submissões selecionadas na aba
  "Submissions" do Kaggle para contar na nota final.

## Modelo

Blend (média ponderada) de três modelos do Scikit-Learn — `LogisticRegression`,
`RandomForestClassifier` e `HistGradientBoostingClassifier` — treinados sobre 17
features originais (Elo, forma recente, descanso, confronto direto) mais algumas
features derivadas (diferenças entre mandante/visitante, `elo_diff` ao quadrado,
probabilidade estilo Elo). Hiperparâmetros e pesos do blend escolhidos por validação
walk-forward (treino sempre no passado, validação na temporada seguinte, sem
embaralhar).

Scores no placar público do Kaggle: `v3` = 1.02095, `v4` = 1.02118 — ambos bem abaixo
dos benchmarks da competição (1.0594 sem modelo, 1.047 do notebook de partida).

## Conformidade com as regras da competição

- Apenas NumPy, Pandas e Scikit-Learn usados na modelagem.
- Nenhum dado externo: apenas `train.csv`/`test.csv` fornecidos pela competição.
- Cada previsão usa só as colunas da própria linha do `test.csv` — nenhuma comparação
  entre partidas do conjunto de teste.
- Validação sempre respeitando a ordem temporal (treino no passado, nunca `shuffle`).
- O notebook foi executado do início ao fim e reproduz exatamente os dois CSVs
  submetidos (verificado por diff).
