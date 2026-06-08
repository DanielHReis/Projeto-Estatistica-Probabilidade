📊 Análise dos Resultados do ENEM 2024
Projeto de análise de dados educacionais desenvolvido para a disciplina Fundamentos de Ciência de Dados, utilizando os microdados oficiais do ENEM 2024 disponibilizados pelo INEP/MEC.

Instituição: Belém, Pará — 2026
Dataset: ENEM 2024 — INEP / MEC (RESULTADOS_2024.csv)


📁 Estrutura do Projeto
├── Analise.ipynb                    # EDA e pré-processamento
├── Bayes.ipynb                      # Análise probabilística (Teorema de Bayes)
├── AlgoritmosDeClassificação.ipynb  # Modelos de classificação supervisionada
├── dashboard/                       # Dashboard Power BI
└── README.md

🗃️ Sobre o Dataset
AtributoDescriçãoOrigemINEP / MEC — Microdados ENEM 2024Instâncias originais~4,3 milhões de registrosInstâncias após tratamento~2,8 milhões de registrosAtributos originais76 colunasAtributos utilizados17 colunasVariável-alvoRegiao (derivada de Sigla_Estado)Encoding originallatin-1, separador ;

⚙️ Pipeline de Pré-processamento
O pré-processamento foi implementado no Analise.ipynb e cobriu as seguintes etapas:

Remoção de colunas irrelevantes — 18 colunas com gabaritos, respostas e códigos administrativos
Renomeação de colunas — de nomenclatura técnica INEP (NU_NOTA_CN) para nomes semânticos (Nota_CN)
Conversão de tipos e decodificação — variáveis categóricas codificadas como inteiros mapeadas para rótulos legíveis
Filtragem de participantes — mantidos apenas os presentes nos dois dias de prova, sem desclassificação
Consolidação de colunas redundantes — colunas de prova e presença por dia unificadas
Remoção de outliers — método IQR (fator 1,5) aplicado às 5 colunas de notas; >95% dos dados preservados
Engenharia de atributos — criação de 4 novas colunas:

ColunaFórmulaDescriçãoMedia_ObjetivasMédia das 4 notas objetivasDesempenho sem redaçãoMedia_FinalMédia das 5 notasDesempenho globalNivelpd.cut em 5 faixasVariável categórica ordinalRegiaoMapeamento UF → RegiãoVariável-alvo para classificação

🔍 Principais Insights da EDA

Nota_MT apresentou a maior dispersão, com distribuição levemente bimodal — polarização entre alto e baixo domínio
Nota_Redacao concentrou-se em torno de 600–700 pontos, com pico pronunciado nessa faixa
Correlação quase perfeita entre Media_Final e Media_Objetivas (r ≈ 0,98)
~60% dos participantes estão nos níveis "Baixo" e "Médio"; apenas ~3% atingem o nível "Excelente"
Nordeste concentra ~35% dos participantes; Sudeste, ~30%
Sul e Sudeste apresentaram as maiores médias finais; Norte registrou o menor desempenho — diferença de ~40–50 pontos entre extremos regionais

Distribuição por Nível de Desempenho
NívelFaixa (pts)% AproximadoMuito Baixo0 – 450~25%Baixo450 – 550~30%Médio550 – 650~30%Alto650 – 750~12%Excelente750 – 1000~3%

🧮 Análise Probabilística — Teorema de Bayes
Implementado no Bayes.ipynb para responder:

"Dado que um participante obteve determinado Nível de desempenho, qual é a probabilidade de ele ser proveniente de cada Região?"

P(Região | Nível) = [ P(Nível | Região) × P(Região) ] / P(Nível)
Resultado: Acurácia ≈ 40,74% (~1,14 milhões de acertos em ~2,80 milhões de registros)
A acurácia reflete o comportamento de um classificador baseline — o Nível de desempenho isoladamente não discrimina a Região, pois a distribuição proporcional de níveis é similar entre as regiões brasileiras.

🤖 Algoritmos de Classificação
Implementados no AlgoritmosDeClassificação.ipynb com a seguinte configuração:

Variável preditora: Nivel (One-Hot Encoded)
Variável-alvo: Regiao (5 classes)
Divisão: 70% treino / 30% teste (estratificado)

MétodoAcuráciaInterpretabilidadeTeorema de Bayes~40,74%AltaÁrvore de Decisão~40,74%AltaRandom Forest~40,74%Média
Os três métodos convergiram para a mesma acurácia, confirmando empiricamente que Nivel não é um preditor regional eficaz — resultado antecipado pela EDA.

✅ Conclusões

O pré-processamento foi a etapa mais crítica, transformando 4,3M de registros brutos em um conjunto limpo e analiticamente rico
A EDA antecipou os resultados da classificação antes de qualquer modelo ser treinado
O Teorema de Bayes, com uma única feature e sem hiperparâmetros, foi tão preciso quanto algoritmos de ensemble
A desigualdade educacional regional é estatisticamente mensurável e consistente em mais de 2 milhões de observações


⚠️ Limitações

Apenas Nivel foi usado como preditor — inclusão de Nota_MT, Lingua_Estrangeira e variáveis socioeconômicas poderia melhorar a acurácia
Variável-alvo desbalanceada (Nordeste ~35%, Norte ~8%)
Dados socioeconômicos do questionário ENEM não foram utilizados


🔭 Trabalhos Futuros

Incluir múltiplas features na classificação (notas individuais, município, idioma)
Aplicar GaussianNB para features contínuas
Integrar dados socioeconômicos do questionário do ENEM
Aplicar clustering não-supervisionado (K-Means) para identificar perfis de desempenho


📄 Fonte dos Dados
Os dados são públicos e disponibilizados pelo INEP/MEC em conformidade com a Lei de Acesso à Informação (LAI).
Acesse em: gov.br/inep — Microdados ENEM
