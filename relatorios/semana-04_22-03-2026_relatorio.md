# Relatório Semanal – Semana 04

---

## 1. Identificação

- **Semana:** 04

- **Período:** 22 a 28 de março de 2026

- **Carga horária estimada:** 10 horas

- **Projeto:** Estudo de diferentes métodos de imputação para dados faltantes

- **Orientador(a):** Profa. Dra. Lourdes Coral Contreras Montenegro

- **Discente:** Isabela G. dos Santos


---


## 2. Objetivos da Semana

### Objetivo Principal

- Simular diferentes mecanismos de dados faltantes (MCAR, MAR e MNAR) em uma base de dados real e avaliar seus impactos sobre análises estatísticas.


### Objetivos Secundários

- Comparar descritiva e inferencialmente os efeitos de cada mecanismo.

- Gerar visualizações (histogramas e densidades) para análise exploratória.


---


## 3. Atividades Realizadas

Descrição técnica e objetiva das atividades desenvolvidas.

### Leituras Realizadas

- Leitura do capítulo introdutório de van Buuren (2018) sobre classificação de mecanismos de missing data.

- Revisão da documentação dos pacotes `tidyverse` e `skimr`.


### Implementações / Códigos

- Criação de três bases simuladas a partir da base `equipment`:

  - `equip_mcar`: missing em `valueadded` completamente aleatório.
  
  - `equip_mar`: missing em `valueadded` dependente da variável `capital`.
  
  - `equip_mnar`: missing em `valueadded` dependente da própria variável `valueadded`.
  
- Construção de um dataframe unificado (`analises`) contendo:

  - Média, mediana, desvio padrão, correlação.
  
  - Coeficientes de regressão (capital e trabalho), R2 e erro padrão ajustado.
  
  - Proporção de NAs e tamanho amostral efetivo.
  
- Cálculo de viés absoluto e relativo para cada mecanismo.

- Geração de gráficos de histograma e densidade comparativa.


### Análises Exploratórias / Testes

- Comparação entre a base original e as três versões com missing.

- Identificação de padrões de distorção: MCAR < MAR < MNAR.

- Observação de falsa precisão em MAR e MNAR (erro padrão reduzido artificialmente).


### Discussões / Reflexões Teóricas

- O R2 manteve-se relativamente estável mesmo com viés nos coeficientes, mostrando que bom ajuste não garante ausência de viés.

- MAR e MNAR alteraram substancialmente a correlação e a interpretação dos coeficientes de regressão.

- A redução do erro padrão ajustado em MAR e MNAR não indica melhora real na precisão, mas sim uma falsa confiança.


---


## 4. Resultados Parciais / Produtos Gerados


### Scripts / Códigos

- Script completo em R (formato `.Rmd`) com todas as simulações, análises e visualizações.


### Produtos Gerados

- Tabela comparativa com 10 métricas (média, mediana, dp, correlação, coeficientes, R², erro padrão, proporção de NA, n efetivo).

- Gráficos de histograma para cada base (`hist_equipment.png`, `hist_equip_mcar.png`, `hist_equip_mar.png`, `hist_equip_mnar.png`).

- Gráfico de densidade comparativa (`dens_comparacao.png`).


---


## 5. Problemas e Dificuldades Encontradas


### Dados

- Base `equipment` original não possui missing; foi necessário simular todos os cenários.


### Metodológicos / Técnicos

- Ajuste fino das probabilidades para garantir aproximadamente 40% de missing em todos os mecanismos.

- Garantir que a simulação MAR dependesse exclusivamente de variável observada (`capital`) e não de `valueadded`.


---


## 6. Decisões Tomadas e Justificativas

- Uso de `pnorm(scale(...))` para modelar probabilidades: garante que as chances de missing sejam monotônicas e contidas entre 0 e 1.

- Ajuste da probabilidade média para 40%: permite comparabilidade entre os três mecanismos.

- Cálculo de viés absoluto e relativo: possibilita avaliar impacto em termos absolutos e proporcionais simultaneamente.

- Exclusão de `prop_NA` e `n_alterado` do cálculo de viés: essas métricas não representam parâmetros estimados, apenas descritores da perda de dados.


---


## 7. Próximos Passos (Planejamento)

- Estudar alguns métodos de imputação.

- Comparar eficácia de cada método de imputação por tipo de mecanismo de missing.

- Documentar resultados em novo relatório.


---


## 8. Referências Utilizadas

- BUUREN, Stef van. **Flexible Imputation of Missing Data**. 2. ed. Boca Raton: CRC Press, 2018.

- POSIT TEAM. **RStudio: Integrated Development Environment for R**. Boston: Posit Software, PBC, 2026.

- WARING, Elin et al. **skimr: Compact and Flexible Summaries of Data**. Versão 2.2.2, 2026.

- WICKHAM, Hadley et al. Welcome to the tidyverse. *Journal of Open Source Software*, v. 4, n. 3, p. 1686, 2019.

- ZELLNER, Arnold; RYU, Hang. Alternative Functional Forms for Production, Cost, and Returns to Scale Functions. *Journal of Applied Econometrics*, v. 13, n. 2, p. 101-127, 1998.


---


## 9. Observações Gerais

- Os resultados confirmam a literatura: MCAR é o mecanismo menos prejudicial, enquanto MAR e MNAR introduzem viés significativo, especialmente em coeficientes de regressão.

- A aparente estabilidade do R2 e a redução do erro padrão em MAR/MNAR podem levar a conclusões enganosas se não forem devidamente interpretadas.

- O script desenvolvido está pronto para ser estendido com rotinas de imputação.