# Plano Experimental — Análise Comparativa de Desempenho entre Diferentes Modelos de LLMs

### 1. Identificação Básica
**Título:** Análise Comparativa de Desempenho entre Diferentes Modelos de LLMs  
**ID:** EXP-LLM-DOM-001  
**Versão:** v1.0  
**Data de criação:** 2025-11-23  
**Última atualização:** 2025-11-23  
**Autores:** Matheus Vinicius(Pesquisador) 
**Responsável Principal (PI):** Matheus Vinicius(matheus.rodrigues.1462287@sga.pucminas.br)
**Projeto Relacionado:** Estudo de qualidade e desempenho de sistemas baseados em IA generativa

### 2. Contexto e Problema
#### 2.1 Descrição do Problema / Oportunidade
##### Problema Principal:
Como comparar objetivamente o desempenho de diferentes modelos de LLMs considerando múltiplas dimensões de qualidade (precisão, velocidade, custo, capacidade de raciocínio, criatividade e robustez) de forma sistemática, reproduzível e estatisticamente válida?

##### Manifestação do Problema:
Desenvolvedores, pesquisadores e organizações enfrentam diariamente a decisão crítica de qual modelo LLM adotar para suas aplicações específicas. Atualmente, essas decisões são frequentemente baseadas em:

- Informações anedóticas e experiências pessoais limitadas
- Marketing corporativo e benchmarks proprietários
- Testes informais sem rigor metodológico
- Comparações unidimensionais (apenas custo ou apenas qualidade)

##### Sintomas Observados:

1. **Ausência de consenso:** Diferentes fontes apresentam rankings contraditórios de modelos
2. **Trade-offs não quantificados:** Falta clareza sobre custo-benefício e compensações entre métricas
3. **Variabilidade não documentada:** Pouco conhecimento sobre consistência e determinismo dos modelos
4. **Generalização incerta:** Resultados de um domínio não se aplicam necessariamente a outros

##### Oportunidade:
Conduzir um experimento controlado e sistemático que forneça evidências empíricas para orientar a escolha de modelos baseadas em requisitos específicos, estabelecer uma metodologia replicável para avaliação comparativa, identificar nichos de superioridade de cada modelo e quantificar trade-offs entre custo, qualidade e eficiência

#### 2.2 Contexto técnico

- **Modelos Avaliados:** 4 LLMs estado-da-arte (GPT-4, Claude Sonnet 3.5, Gemini Pro 1.5, LLaMA 3.1 70B)
- **Infraestrutura:** APIs comerciais + servidor com GPU para execução local
- **Ferramentas:** Python 3.11, bibliotecas de APIs oficiais, R para análise estatística
- **Ambiente de Desenvolvimento:** Jupyter Notebooks, RStudio, Docker para isolamento

##### Domínio de Aplicação:
O experimento abrange 5 categorias representativas de uso de LLMs:

1. Geração de código (desenvolvimento de software)
2. Análise de texto (processamento de documentos)
3. Raciocínio lógico (resolução de problemas)
4. Criatividade (geração de conteúdo)
5. Perguntas factuais (consulta informacional)

#### 2.3 Trabalhos e evidências prévias
Nessa sessão estão organizados os trabalhos relevantes para a pesquisa.

##### Trabalhos Externos Relevantes:

**1. MMLU (Massive Multitask Language Understanding):** Avalia conhecimento em 57 disciplinas, mas foca apenas em precisão factual, não em aspectos práticos como custo e velocidade.
**2. HumanEval:** Benchmark específico para geração de código, com 164 problemas de programação. Limitação: não avalia qualidade além da correção funcional.
**3. BigBench:** Conjunto de 204 tarefas diversas, mas com foco em capacidades cognitivas gerais, não em aplicações práticas.
**4. Chatbot Arena (LMSYS):** Comparação via votação humana em conversas abertas. Limitação: subjetivo e sem controle experimental rigoroso.

##### Estudos Acadêmicos:

- **Liang et al. (2023) - "Holistic Evaluation of Language Models (HELM)":** Propõe framework multidimensional mas não compara modelos específicos em profundidade.
- **Zheng et al. (2024) - "Judging LLM-as-a-Judge":** Avalia uso de LLMs para avaliar outros LLMs, mas questiona confiabilidade dessa abordagem.

#### 2.4 Referencial teórico

**1. Large Language Models (LLMs):**
Modelos de aprendizado profundo baseados em arquitetura Transformer, treinados em grandes volumes de texto para prever sequências de tokens. Principais características: emergência de capacidades (reasoning, coding, etc.) e comportamento não-determinístico controlado por temperatura.

**2. Avaliação de Sistemas de IA:**
Framework GQM (Goal-Question-Metric) de Basili & Rombach para estruturar avaliações empíricas sistemáticas.

**3. Métricas de Qualidade:**
- **Objetivas:** Accuracy, F1-score, taxa de compilação
- **Subjetivas:** Avaliação humana com escalas Likert
- **Consistência:** Similaridade semântica entre execuções (cosine similarity de embeddings)

##### Teorias Relevantes:

- **Teoria de Trade-offs em Sistemas:**
Não existe solução universalmente ótima; diferentes modelos podem ser superiores em diferentes dimensões (teorema "No Free Lunch").

- **Psicometria e Confiabilidade:**
Concordância inter-avaliadores medida por Kappa de Cohen para validar métricas subjetivas.

**Resultados Empíricos Prévios:**

- Modelos maiores tendem a ter melhor desempenho mas maior custo (relação não linear)
- Temperatura afeta criatividade vs. determinismo (temperatura alta = mais criativo, menos consistente)
- Avaliação humana muitas vezes diverge de métricas automáticas
- Desempenho varia significativamente entre domínios (ex: modelo bom em código pode ser fraco em criatividade)

**Metodologia Experimental:** 

Baseada em princípios de Fisher (aleatorização, replicação, controle local) e adaptações para contextos de software por Wohlin et al. (2012) - "Experimentation in Software Engineering".

### 3. Objetivos e Questões (GQM)
#### 3.1 Objetivo Geral

Analisar diferentes modelos de Large Language Models (GPT-4, Claude Sonnet 3.5, Gemini Pro 1.5 e LLaMA 3.1) com o propósito de compará-los e caracterizá-los quanto à qualidade das respostas, eficiência computacional, relação custo-benefício e consistência, sob a perspectiva de desenvolvedores, pesquisadores e tomadores de decisão técnica, no contexto de cinco categorias de tarefas representativas: geração de código, análise de texto, raciocínio lógico, criatividade e perguntas factuais; executadas em ambiente controlado com prompts padronizados.

#### 3.2 Objetivos Específicos
- **OE1: Avaliar a Qualidade das Respostas:**
Mensurar e comparar a precisão, relevância, completude e correção das respostas geradas pelos quatro modelos em diferentes tipos de tarefas, utilizando tanto avaliação humana especializada quanto métricas automáticas, para identificar qual modelo produz respostas de maior qualidade em cada categoria.
- **OE2 : Analisar Eficiência Computacional:**
Quantificar e comparar o tempo de resposta, latência e throughput dos modelos em condições controladas, identificando diferenças de desempenho que impactem a experiência do usuário e escalabilidade de aplicações, para determinar qual modelo oferece melhor desempenho temporal.
- **OE3 : Avaliar Custo-Benefício:**
Estabelecer a relação entre o custo financeiro de utilização dos modelos (custo por token/resposta) e a qualidade das respostas obtidas, permitindo análise de viabilidade econômica para diferentes casos de uso e identificando a melhor relação custo-qualidade.
- **OE4 : Medir Consistência e Robustez:**
Avaliar a variabilidade das respostas geradas pelos modelos quando submetidos repetidamente aos mesmos prompts, medindo determinismo, estabilidade e confiabilidade dos resultados, para caracterizar a previsibilidade de cada modelo.

#### 3.3 Tabela GQM
| Objetivo | Pergunta | Métricas |
|---------|----------|----------|
| OE1 | Q1: Qual modelo produz respostas mais precisas e corretas para tarefas factuais? |**M1:** Taxa de acerto (accuracy)<br> **M2:** Score F1 para tarefas de classificação |
| OE1 | Q2: Qual modelo gera código mais funcional e com menos erros? | **M3:** Taxa de sucesso de compilação <br> **M4:** Número de bugs identificados por revisão |
| OE1 | Q3: Qual modelo apresenta maior qualidade segundo avaliação humana especializada? | **M5:** Score médio de avaliação humana (escala Likert 1-5)<br>  **M6:** Índice de concordância inter-avaliadores (Kappa de Cohen) |
| OE2 | Q4: Qual modelo apresenta menor tempo de resposta? | **M7:** Tempo médio de resposta (segundos)<br>  **M8:** Percentil 95 do tempo de resposta |
| OE2 | Q5: Qual modelo mantém melhor desempenho sob diferentes cargas? | :**M7:** Tempo médio de resposta (segundos)<br>  **M9:** Desvio padrão do tempo de resposta |
| OE2 | Q6: Existe correlação entre tamanho da resposta e tempo de processamento? | **M7:** Tempo médio de resposta (segundos)<br>  **M10:** Número de tokens gerado |
| OE3 | Q7: Qual modelo oferece melhor relação custo-qualidade? | **M11:** Custo por resposta (USD)<br>  **M5:** Score médio de avaliação humana |
| OE3 | Q8: O custo adicional de modelos premium se justifica pela qualidade superior? | **M11:** Custo por resposta (USD)<br>  **M1:** Taxa de acerto (accuracy) |
| OE3 | Q9: Qual modelo é mais econômico para tarefas simples vs. complexas? | **M11:** Custo por resposta (USD)<br>  **M12:** Índice de complexidade da tarefa |
| OE4 | Q10: Qual modelo apresenta maior consistência entre execuções repetidas? | **M13:** Coeficiente de variação das respostas<br>  **M14:** Similaridade semântica entre respostas (cosine similarity) |
| OE4 | Q11: Qual modelo é mais robusto a variações sutis no prompt? | **M1:** Taxa de acerto (accuracy)<br>  **M13:** Coeficiente de variação das respostas |
| OE4 | Q12: Qual modelo apresenta menor taxa de alucinações ou respostas incorretas? | **M15:** Taxa de alucinação (% respostas com informações falsas) <br> **M1:** Taxa de acerto (accuracy) |

#### 3.4 Tabela de Métricas
| Métrica | Definição | Unidade | Fonte dos Dados | Método de Coleta |
|--------|-----------|---------|------------------|-------------------|
| **M1: Taxa de acerto (accuracy)** | Proporção de respostas corretas em relação ao total de respostas para tarefas com resposta objetiva verificável | Percentual (0-100%) | Respostas dos modelos + gabarito pré-definido | Comparação automatizada resposta vs. gabarito |
| **M2: Score F1** | Média harmônica entre precisão e recall para tarefas de classificação, balanceando falsos positivos e negativos | Adimensional (0-1) | Respostas dos modelos + gabarito | Cálculo: F1 = 2×(precisão×recall)/(precisão+recall) |
| **M3: Taxa de sucesso de compilação** | Proporção de códigos gerados que compilam sem erros sintáticos | Percentual (0-100%) | Código gerado pelos modelos | Execução em sandbox com compilador/interpretador |
| **M4: Número de bugs identificados** | Quantidade de erros lógicos, de runtime ou problemas funcionais identificados por revisão humana no código gerado | Contagem (≥ 0) | Código gerado + revisão de especialista | Inspeção manual + análise estática (linting) |
| **M5: Score médio de avaliação humana** | Média das avaliações de qualidade atribuídas por especialistas usando escala Likert de 5 pontos (1=muito ruim, 5=excelente) | Escala Likert (1-5) | Formulários de avaliação | Plataforma web com rubrica padronizada |
| **M6: Índice de concordância inter-avaliadores** | Coeficiente Kappa de Cohen medindo concordância entre múltiplos avaliadores humanos | Adimensional (-1 a 1) | Avaliações dos 3 especialistas | Cálculo estatístico: κ = (Po-Pe)/(1-Pe) |
| **M7: Tempo médio de resposta** | Tempo decorrido desde o envio do prompt até o recebimento completo da resposta | Segundos (s) | Timestamps de requisição e resposta | Medição automática via script Python |
| **M8: Percentil 95 do tempo de resposta** | Valor de tempo de resposta abaixo do qual 95% das requisições são concluídas | Segundos (s) | Timestamps coletados | Cálculo estatístico sobre distribuição de tempos |
| **M9: Desvio padrão do tempo de resposta** | Medida de dispersão dos tempos de resposta, indicando variabilidade/estabilidade | Segundos (s) | Timestamps coletados | Cálculo: σ = √[Σ(xi-μ)²/n] |
| **M10: Número de tokens gerados** | Quantidade total de tokens na resposta produzida pelo modelo | Contagem (> 0) | Metadados da API | Extração automática do campo "usage.completion_tokens" |
| **M11: Custo por resposta** | Custo financeiro total para gerar uma resposta, baseado no pricing da API (input + output tokens) | Dólares (USD) | Tokens consumidos + tabela de preços | Cálculo: custo = (tokens_input × preço_input) + (tokens_output × preço_output) |
| **M12: Índice de complexidade da tarefa** | Score composto considerando: tamanho do prompt, especificidade da tarefa, conhecimento especializado requerido (escala 1-10) | Escala numérica (1-10) | Classificação prévia por especialistas | Rubrica de complexidade aplicada ao dataset de prompts |
| **M13: Coeficiente de variação das respostas** | Razão entre desvio padrão e média de uma métrica específica entre execuções repetidas, indicando consistência | Percentual (%) | Métricas das 3 execuções | Cálculo: CV = (σ/μ) × 100% |
| **M14: Similaridade semântica entre respostas** | Cosine similarity entre embeddings de respostas geradas repetidamente para o mesmo prompt | Adimensional (0-1) | Respostas das 3 execuções | Embeddings (sentence-transformers) + cosine similarity |
| **M15: Taxa de alucinação** | Proporção de respostas contendo informações factualmente incorretas ou inventadas, identificadas por verificação humana | Percentual (0-100%) | Respostas + verificação factual | Revisão humana + busca em bases de conhecimento |


### 4. Escopo
**O experimento incluí:**

O experimento compara quatro modelos de LLMs — GPT-4 Turbo, Claude Sonnet 3.5, Gemini Pro 1.5 e LLaMA 3.1 (70B) — avaliando-os em cinco categorias de tarefas: geração de código, análise de texto, raciocínio lógico, criatividade e respostas factuais.
Serão utilizados 250 prompts (50 por categoria), cada um executado três vezes, totalizando 750 execuções por modelo, permitindo mensurar desempenho e consistência.

A avaliação envolve métricas objetivas (tempo de resposta, custo, acurácia, compilação), métricas subjetivas (avaliação de especialistas) e métricas de consistência (variação entre execuções).

A análise estatística utilizará ANOVA, Kruskal-Wallis, testes post-hoc, tamanhos de efeito, correlações e visualizações comparativas para explorar diferenças entre modelos e trade-offs entre desempenho, custo e estabilidade.

Por fim, o estudo será documentado de maneira completa, incluindo protocolo experimental, dataset público, scripts de automação e análise, além de um relatório técnico e artigo científico, garantindo reprodutibilidade e transparência.

**O experimento não incluí:**

O experimento não inclui nenhuma forma de fine-tuning, treinamento adicional ou avaliação de modelos multimodais. Também não contempla testes com modelos muito pequenos, análises de viés ou segurança, nem experimentos envolvendo técnicas avançadas de prompt engineering ou contextos extremamente longos. Além disso, não fará parte do estudo a construção de sistemas completos, integrações com aplicações reais, testes em idiomas diferentes de português e inglês ou avaliação de assistentes conversacionais com memória. Do ponto de vista econômico e operacional, o experimento não investigará custos de infraestrutura, impactos ambientais, licenciamento ou escalabilidade. Por fim, não serão analisados aspectos temporais, como evolução dos modelos, efeitos de atualizações ou análises longitudinais.

#### 4.2 Contexto do Estudo
A pesquisa será conduzida em uma instituição acadêmica caracterizando-se como um experimento controlado de natureza estritamente científica e não associado ao desenvolvimento de produtos comerciais. Trata-se de um estudo de baixa criticidade, uma vez que seus resultados não impactam sistemas essenciais ou decisões de negócio imediatas, mas sim contribuem para o avanço do conhecimento na área de modelos de linguagem.

Os participantes do estudo possuem perfis bem definidos. O pesquisador principal é um estudante de graduação na área de Engenharia de Software. Além dele, o experimento contará com três avaliadores humanos especializados em inteligência artificial e aprendizado de máquina, todos com pelo menos dois anos de experiência. Esses avaliadores têm conhecimento multidisciplinar abrangendo código, análises textuais e raciocínio lógico e fluência tanto em português quanto em inglês, o que os capacita a avaliar com precisão as respostas produzidas pelos modelos.

A execução do experimento ocorrerá em um ambiente composto por infraestrutura em nuvem ou recursos locais capazes de acessar APIs comerciais. Se necessário, será utilizado um servidor equipado com GPU para suportar a execução local do modelo LLaMA. Para a implementação e análise dos resultados, serão empregadas ferramentas de desenvolvimento amplamente utilizadas na pesquisa científica, como Python, R e Jupyter Notebook.

Todo o processo experimental está previsto para ser realizado ao longo de um período de um ano, abrangendo preparação, execução, análise e documentação final dos resultados.

#### 4.3 Premissas
##### Premissas Técnicas:

- As APIs dos modelos comerciais (GPT-4, Claude, Gemini) permanecerão estáveis e disponíveis durante o período de coleta de dados
- O acesso ao modelo LLaMA 3.1 (70B) via infraestrutura local ou cloud será viável tecnicamente e economicamente
- Os modelos responderão consistentemente às requisições via API de acordo com suas especificações técnicas
- As métricas automáticas de avaliação serão aplicáveis e calculáveis para as tarefas selecionadas
- Existe infraestrutura computacional suficiente para processar e analisar o volume de dados gerado (3.000 execuções)

##### Premissas Metodológicas:

- É possível recrutar e treinar 3 avaliadores humanos especializados com conhecimento suficiente para avaliar qualidade em todas as categorias
- A escala Likert de 5 pontos é suficientemente granular para capturar diferenças de qualidade entre modelos
- Três execuções por prompt são suficientes para avaliar consistência dos modelos
- O dataset de 250 prompts (50 por categoria) é representativo das aplicações reais de LLMs
- Diferenças estatisticamente significativas nas métricas correspondem a diferenças práticas relevantes

#### 4.4 Restrições
##### Restrições Orçamentárias:

* Orçamento Total: Limitado a US$ 500 para chamadas de API
**Impacto:** Limita número de prompts e repetições possíveis
**Contingência:** Priorização de categorias críticas se necessário
<br>

* Infraestrutura: Acesso limitado a servidores com GPU
**Impacto:** Pode inviabilizar execução local do LLaMA 3.1
**Alternativa:** Uso de APIs comerciais para LLaMA (Together AI, Replicate)

##### Restrições Técnicas:

* Rate Limiting: APIs têm limites de requisições por minuto
**GPT-4:** ~10k tokens/min (tier gratuito/básico)
**Claude:** ~5k tokens/min
**Gemini:** ~60 requisições/min
**Impacto:** Necessidade de pausas entre requisições
<br>

* Tamanho de Contexto: Limitações de tokens por prompt
**Restrição:** Prompts devem ser < 4k tokens para compatibilidade
**Impacto:** Não é possível testar tarefas com contexto muito longo

### 5. Stakeholders
#### 5.1 Stakeholders principais
| STAKEHOLDER | DESCRIÇÃO  | PAPEL NO EXPERIMENTO  |
|----------------------------|-------------------------------------------------------------|------------------------------------------------------------|
| Desenvolvedores de Software | Profissionais que integram LLMs em aplicações               | Beneficiários dos resultados para decisões de arquitetura |
| Pesquisadores em IA/ML     | Acadêmicos estudando LLMs e avaliação de modelos            | Usuários da metodologia e dataset público                 |
| Gestores de Tecnologia     | CTOs, líderes técnicos que decidem investimentos em IA      | Tomadores de decisão baseados nas evidências geradas      |
| Avaliadores Especialistas  | 3 profissionais que participam da avaliação humana          | Participantes ativos do experimento                       |
| Comunidade Open Source     | Desenvolvedores de modelos abertos (LLaMA, etc.)            | Interessados em comparações transparentes                 |
| Fornecedores de LLMs       | OpenAI, Anthropic, Google, Meta                             | Potencialmente impactados por resultados (positiva ou negativamente) |

#### 5.2 Interesses e expectativas dos stakeholders
Os stakeholders envolvidos no experimento apresentam interesses complementares e expectativas convergentes quanto à produção de evidências confiáveis sobre o desempenho comparativo de modelos de LLMs. Desenvolvedores de software buscam identificar o modelo mais adequado para suas aplicações, esperando um framework decisório claro fundamentado em trade-offs entre custo, qualidade e velocidade, de modo a embasar escolhas técnicas com dados empíricos. Pesquisadores em IA e aprendizado de máquina demandam rigor metodológico, reprodutibilidade e transparência, esperando acesso a um protocolo detalhado, um dataset público e análises estatísticas robustas que permitam replicação, extensão e utilização científica dos resultados.

Gestores de tecnologia apresentam interesse estratégico na otimização de investimentos em IA, esperando análises que evidenciem retorno financeiro, eficiência operacional e custo-efetividade dos modelos avaliados, permitindo decisões mais embasadas sobre contratação e alocação orçamentária. Os avaliadores especialistas, responsáveis pelas medidas subjetivas, têm interesse em participar de um processo estruturado e metodologicamente sólido, com expectativa de treinamento adequado e reconhecimento do esforço, contribuindo simultaneamente para o avanço científico e para seu próprio desenvolvimento profissional.

A comunidade open source, por sua vez, busca evidências transparentes que permitam comparar de forma justa modelos abertos e comerciais, utilizando os resultados para orientar esforços de desenvolvimento e apoiar argumentos de adoção. Já os fornecedores de LLMs têm interesse em compreender o posicionamento de seus modelos no cenário competitivo, esperando avaliações imparciais que permitam identificar pontos fortes e limitações, com potencial impacto em estratégias de melhoria contínua e comunicação baseada em evidências.


### 6. Riscos e Premissas
| ID  | Risco                                                             | Categoria     | Prob. | Impacto | Severidade | Estratégia de Mitigação                                                                                         |
|-----|-------------------------------------------------------------------|---------------|-------|---------|------------|------------------------------------------------------------------------------------------------------------------|
| **R1**  | Mudanças nas APIs dos modelos comerciais durante experimento      | Técnico       | Média | Alto    | Alta       | Versionamento rigoroso, distribuição temporal uniforme, monitoramento de anúncios, análise de sensibilidade     |
| **R2**  | Custo de execução exceder orçamento planejado                     | Financeiro    | Média | Médio   | Média      | Monitoramento contínuo, rate limiting, priorização de tarefas críticas, contingência orçamentária               |
| **R3**  | Falhas técnicas na execução do LLaMA 3.1 (GPU indisponível)       | Técnico       | Baixa | Alto    | Média      | Backup em cloud GPU, testes preliminares, alternativa de API comercial                                           |
| **R4** | Baixa concordância inter-avaliadores compromete validade          | Metodológico  | Média | Médio   | Média      | Treinamento rigoroso, rubrica detalhada, sessões de calibração, análise de Kappa                                 |
| **R5** | Viés na seleção de prompts favorece determinados modelos          | Metodológico  | Média | Alto    | Alta       | Revisão independente, balanceamento, validação por especialistas externos                                         |
| **R6**  | Impossibilidade de publicar resultados devido a ToS               | Legal         | Baixa | Alto    | Média      | Revisão jurídica prévia, anonimização se necessário, consulta aos fornecedores                                   |
| **R7**  | Resultados não generalizáveis além do contexto específico         | Científico    | Média | Médio   | Média      | Diversificação de tarefas, documentação clara de limitações, replicações futuras                                 |
| **R8**  | Indisponibilidade temporária de APIs afeta coleta                 | Técnico       | Média | Médio   | Média      | Coleta distribuída temporalmente, monitoramento de status, retry automático                                      |
| **R9**  | Desistência de avaliadores durante o experimento                  | Operacional   | Baixa | Alto    | Média      | Compromisso formal prévio, compensação adequada, avaliador reserva                                               |
| **R10** | Violação de pressupostos estatísticos invalida análises           | Estatístico   | Média | Médio   | Média      | Testes de pressupostos, transformações de dados, alternativas não-paramétricas                                   |
| **R11** | Atrasos no cronograma comprometem conclusão                       | Cronograma    | Média | Médio   | Média      | Buffer temporal, priorização de atividades críticas, plano de contingência                                       |
| **R12** | Perda de dados por falhas de sistema                              | Técnico       | Baixa | Alto    | Média      | Backup incremental automático, versionamento, armazenamento redundante                                           |

### 6.2 Critérios de Sucesso Globais (Go / No-Go)
#### Critérios de Sucesso Técnico:

| ID   | Critério                         | Descrição                                                                                                                                                     | Medição                                                             | Go/No-Go                                                                                       |
|------|----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| CS1  | Completude da Coleta             | Obter respostas válidas de todos os 4 modelos para ≥ 95% dos 250 prompts (mínimo 237 completos).                                                               | Contagem de prompts com 4 respostas válidas.                         |Se < 90% → investigar causas e decidir continuidade.                                              |
| CS2  | Confiabilidade das Avaliações    | Kappa de Cohen ≥ 0.60 (concordância substancial).                                                                                                               | Cálculo estatístico após avaliações humanas.                         |Se Kappa < 0.40 → recalibração ou maior peso em métricas objetivas.                              |
| CS3  | Significância Estatística        | Identificar diferenças significativas (p < 0.05) em ≥ 60% das comparações principais.                                                                            | Proporção de testes com p < 0.05.                                    |Se < 30% → questionar sensibilidade das métricas ou homogeneidade dos modelos.                   |
| CS4  | Controle de Variância            | Coeficiente de variação intra-modelo < 30% para métricas principais.                                                                                            | CV = (σ/μ) × 100%.                                                   |Se CV > 50% → questionar confiabilidade das medições.                                             |
| CS5  | Reprodutibilidade                | Documentação completa permitindo replicação independente.                                                                                                       | Checklist de documentação (protocolo, scripts, dados).               | Documentação mínima obrigatória antes da publicação.                                           |
| CS6  | Publicabilidade                  | Qualidade suficiente para submissão em conferência ou periódico científico.                                                                                     | Revisão por orientador/comitê.                                       | Se não publicável → identificar lacunas e corrigir.                                            |
| CS7  | Dataset Público                  | Disponibilização de dataset anonimizado e scripts em repositório público.                                                                                       | Repositório GitHub com documentação adequada.                        | Obrigatório para conclusão do experimento.                                                     |
| CS8  | Insights Originais               | Identificação de ≥ 3 descobertas não triviais sobre comportamento dos modelos.                                                                                  | Lista de insights validados com especialistas.                       | Avaliação subjetiva, mas essencial para valor científico.                                      |
| CS9  | Aplicabilidade                   | Produção de framework/matriz de decisão para seleção de modelos.                                                                                                | Artefato concreto (árvore de decisão, tabela de recomendações).      | Essencial para impacto prático.                                                                |
| CS10 | Viabilidade Orçamentária         | Execução dentro do orçamento planejado (≤ US$ 500).                                                                                                             | Soma de gastos com APIs.                                             | Se Exceder 20% → ajustar escopo.                                                                  |
| CS11 | Cumprimento de Prazo             | Conclusão em 1 ano).                                                                                                                      | Acompanhamento do cronograma.                                        | Atrasos > 1 mês exigem reavaliação.                                                        |

#### 6.3 Critérios de parada antecipada (pré-execução)
| ID  | Condição                                                                                                   | Ação                                                                                                      | Responsável                           |
|-----|-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|----------------------------------------|
| CP1 | Impossibilidade de acesso a ≥ 2 dos 4 modelos por problemas técnicos ou contratuais                         | Adiar até resolução ou replanejar com modelos alternativos                                               | Pesquisador Principal                  |
| CP2 | Estimativa de custo real > 2× orçamento disponível após testes piloto                                      | Reduzir escopo (menos prompts ou modelos) ou buscar financiamento adicional                               | Pesquisador Principal + Orientador     |
| CP3 | Menos de 2 avaliadores qualificados disponíveis                                                             | Adiar até conseguir equipe mínima ou ajustar para métrica puramente objetiva                              | Pesquisador Principal                  |
| CP4 | Termos de serviço proíbem comparação pública ou publicação de resultados                                    | Negociar com fornecedores ou anonimizar resultados                                                        | Pesquisador Principal + Assessoria Jurídica |
| CP5 | Piloto revela problemas fundamentais em > 30% das execuções (erros de API, métricas não calculáveis)       | Revisar protocolo, ajustar métricas ou infraestrutura antes de prosseguir                                 | Pesquisador Principal                  |
| CP6 | Mudanças institucionais que impedem dedicação necessária ao experimento                                     | Adiar ou transferir responsabilidade para outro pesquisador                                               | Orientador + Instituição               |


### 7. Modelo Conceitual e Hipóteses
#### 7.1 Modelo Conceitual do Experimento
Modelo Teórico de Desempenho de LLMs:
O desempenho observável de um Large Language Model pode ser decomposto em múltiplas dimensões inter-relacionadas mas conceitualmente distintas:

**DESEMPENHO_LLM** = f(Qualidade, Eficiência, Custo, Consistência)

Onde:
- Qualidade = f(Precisão, Relevância, Completude, Correção)
- Eficiência = f(Velocidade, Latência, Throughput)
- Custo = f(Tokens_Processados, Pricing_API, Infraestrutura)
- Consistência = f(Variabilidade, Determinismo, Robustez)

**Diagrama conceitual**<br>
![Diagrama Conceitual](https://github.com/MatVini0601/EXP-LLM-DOM-001/blob/main/images/diagramaConceitual.png)

**Relações Causais Hipotéticas:**

RC1: Complexidade x Qualidade Diferenciada
- H: Tarefas mais complexas amplificam diferenças entre modelos
**Mecanismo:** Modelos mais sofisticados têm vantagem maior em raciocínio complexo

RC2: Categoria x Especialização
- H: Modelos apresentam pontos fortes em categorias específicas
**Mecanismo:** Viés de treinamento ou arquitetura favorece certos tipos de tarefa

RC3: Custo x Qualidade (Não-Linear)
- H: Existe correlação positiva mas com diminishing returns
**Mecanismo:** Modelos premium são melhores mas não proporcionalmente ao custo

RC4: Temperatura x Trade-off Criatividade/Consistência
- H: Temperaturas mais altas aumentam criatividade mas reduzem consistência
**Mecanismo:** Aumento de aleatoriedade na geração

RC5: Tamanho do Prompt x Tempo (Linear)
- H: Tempo de resposta aumenta linearmente com tokens de entrada
**Mecanismo:** Complexidade computacional O(n) do processamento de entrada

**Moderadores Identificados:**

Categoria da Tarefa: Modera relação Modelo x Qualidade
Complexidade: Modera magnitude das diferenças entre modelos
Idioma: Pode moderar desempenho (português vs. inglês)

#### 7.2 Hipóteses Formais (H0, H1)
##### Hipótese Nula Principal (H0_geral):

H0: Não existem diferenças estatisticamente significativas no desempenho médio geral entre os quatro modelos de LLMs avaliados (GPT-4, Claude Sonnet 3.5, Gemini Pro 1.5, LLaMA 3.1).

##### Hipótese Alternativa Principal (H1_geral):

H1: Existem diferenças estatisticamente significativas (p < 0.05) no desempenho médio geral entre pelo menos dois dos quatro modelos avaliados.

#### Hipóteses Específicas por Dimensão:
**Grupo 1:** Qualidade
- H0_qual: μ_qualidade(GPT4) = μ_qualidade(Claude) = μ_qualidade(Gemini) = μ_qualidade(LLaMA)
- H1_qual: Pelo menos duas médias de qualidade diferem significativamente

**Grupo 2:** Eficiência Computacional
- H0_efic: μ_tempo(GPT4) = μ_tempo(Claude) = μ_tempo(Gemini) = μ_tempo(LLaMA)
- H1_efic: Pelo menos duas médias de tempo diferem significativamente


**Grupo 3:** Custo-Benefício
- H0_custo: A relação Qualidade/Custo é equivalente entre todos os modelos
- H1_custo: Pelo menos um modelo apresenta relação Qualidade/Custo significativamente diferente

**Grupo 4:** Consistência e Robustez
- H0_consist: σ_intra(GPT4) = σ_intra(Claude) = σ_intra(Gemini) = σ_intra(LLaMA)
- H1_consist: Pelo menos um modelo apresenta variabilidade significativamente diferente


**Grupo 5:** Interações e Moderadores
H9 (Interação Modelo × Categoria): O desempenho relativo entre modelos depende significativamente da categoria da tarefa.

H0_9: Não há efeito de interação Modelo × Categoria
H1_9: Existe efeito significativo de interação (p < 0.05)

### 8. Variáveis, Fatores, Tratamentos e Objetos de Estudo
#### 8.1 Objetos de Estudo

Os objetos de estudo são as respostas geradas pelos modelos de LLMs para prompts específicos. Cada resposta constitui uma instância de análise que será avaliada segundo múltiplas dimensões.

Caracterização:

- **Natureza:** Textos em linguagem natural (incluindo código quando aplicável)
- **Origem:** Gerados sinteticamente pelos modelos em resposta a prompts padronizados
- **Quantidade:** 3.000 respostas totais (4 modelos × 250 prompts × 3 repetições)
- **Formato:** Strings de texto variando de poucos tokens a ~2.000 tokens
- **Contexto:** Cada resposta está vinculada a um prompt específico, modelo específico, categoria e número de execução

Granularidade de Análise:

- **Unidade Primária:** Resposta individual (n=3.000)
- **Unidade Agregada:** Média de 3 repetições por [modelo × prompt] (n=1.000)
- **Unidade Comparativa:** Modelo (n=4)

Propriedades Analisadas:

- Correção factual
- Qualidade do código (se aplicável)
- Clareza e estruturação
- Completude em relação ao solicitado
- Consistência entre repetições
- Características quantitativas (tokens, tempo, custo)

#### 8.2 Variáveis independentes
**Fator Principal 1: MODELO LLM**

Tipo: Variável categórica nominal, between-subjects
Definição: Modelo de Large Language Model utilizado para gerar a resposta
Níveis (n=4):

- Nível 1: GPT-4 Turbo (gpt-4-turbo-2024-04-09) - OpenAI
- Nível 2: Claude Sonnet 3.5 (claude-sonnet-3-5-20241022) - Anthropic
- Nível 3: Gemini Pro 1.5 (gemini-1.5-pro) - Google
- Nível 4: LLaMA 3.1 70B (meta-llama/Meta-Llama-3.1-70B-Instruct) - Meta


**Manipulação:** Cada prompt é submetido aos 4 modelos independentemente
**Justificativa:** Fator primário de interesse para comparação

**Fator Principal 2: CATEGORIA DA TAREFA**

Tipo: Variável categórica nominal, within-subjects
Definição: Tipo ou domínio da tarefa apresentada no prompt
Níveis (n=5):

- Nível 1: Geração de Código (programação, algoritmos, debugging)
- Nível 2: Análise de Texto (sumarização, extração, análise de sentimento)
- Nível 3: Raciocínio Lógico (problemas matemáticos, puzzles, dedução)
- Nível 4: Criatividade (escrita criativa, brainstorming, storytelling)
- Nível 5: Perguntas Factuais (conhecimento geral, fatos verificáveis)


**Manipulação:** Dataset balanceado com 50 prompts por categoria
**Justificativa:** Permite identificar especialização de modelos por domínio

**Fator Secundário: COMPLEXIDADE DA TAREFA**

Tipo: Variável ordinal, within-subjects
Definição: Nível de dificuldade e especialização requerida pela tarefa
Níveis (n=3):

- Baixa: Tarefas simples, conhecimento básico (score 1-3)
- Média: Tarefas moderadas, requerem raciocínio intermediário (score 4-7)
- Alta: Tarefas complexas, conhecimento especializado (score 8-10)


**Distribuição:** 30% baixa, 50% média, 20% alta
**Manipulação:** Pré-classificação dos prompts por especialistas
**Justificativa:** Investigar se complexidade modera desempenho relativo

**Fator de Controle: NÚMERO DA EXECUÇÃO**

Tipo: Variável ordinal, within-subjects
Definição: Repetição sequencial do mesmo prompt para avaliar consistência
Níveis (n=3):

- Execução 1
- Execução 2
- Execução 3


**Manipulação:** Cada [modelo × prompt] executado 3 vezes
**Justificativa:** Medir variabilidade intra-modelo

#### 8.3 Tratamentos (Condições Experimentais)

O experimento segue um desenho fatorial completo envolvendo quatro modelos, cinco categorias de tarefa e três níveis de complexidade. O primeiro grupo experimental utiliza o GPT-4 Turbo da OpenAI, configurado com temperatura 0,7, limite de 2048 tokens e top_p de 0,9, por meio da API oficial. Esse grupo gera 750 observações resultantes de 250 prompts repetidos três vezes. O segundo grupo experimental segue a mesma configuração de parâmetros, mas emprega o modelo Claude Sonnet 3.5 da Anthropic, também com 750 observações. O terceiro grupo utiliza o modelo Gemini Pro 1.5 do Google, com as mesmas condições e número de observações. O quarto grupo experimental utiliza o LLaMA 3.1 70B da Meta, executado localmente ou via API comercial, mantendo-se os mesmos hiperparâmetros para garantir comparabilidade.

Todos os tratamentos utilizam exatamente os mesmos prompts, a mesma ordem de apresentação, o mesmo período temporal de coleta e os mesmos critérios de avaliação. Não há grupo controle no sentido tradicional; cada modelo representa um tratamento ativo, e a comparação entre eles constitui o objetivo central.

#### 8.4 Variáveis Dependentes (Respostas)
##### Categoria 1: Qualidade das Respostas
VD1: Taxa de Acerto (Accuracy)

**Definição:** Proporção de respostas corretas para tarefas com resposta verificável
**Tipo:** Variável contínua (razão)
**Unidade:** Percentual (0-100%)
**Método de Medição:** Comparação automática com gabarito + verificação humana
**Aplicável a:** Perguntas factuais, raciocínio lógico

VD2: Score F1

**Definição:** Média harmônica de precisão e recall para tarefas de classificação
**Tipo:** Variável contínua (razão)
**Unidade:** Adimensional (0-1)
**Método de Medição: **Cálculo estatístico baseado em matriz de confusão
**Aplicável a:** Tarefas de classificação, análise de texto

VD3: Taxa de Sucesso de Compilação

**Definição:** Proporção de códigos que compilam sem erros sintáticos
**Tipo:** Variável contínua (razão)
**Unidade:** Percentual (0-100%)
**Método de Medição:** Execução em sandbox com compilador/interpretador
**Aplicável a:** Geração de código

VD4: Número de Bugs Identificados

**Definição:** Quantidade de erros lógicos ou funcionais no código
**Tipo:** Variável discreta (contagem)
**Unidade:** Número inteiro ≥ 0
**Método de Medição:** Revisão humana + análise estática
**Aplicável a:** Geração de código

VD5: Score de Avaliação Humana

**Definição:** Qualidade percebida por especialistas
**Tipo:** Variável ordinal (Likert)
**Unidade:** Escala 1-5 (1=muito ruim, 5=excelente)
**Método de Medição:** Avaliação cega usando rubrica padronizada
**Aplicável a:** Todas as categorias

VD6: Kappa de Cohen (Concordância)

**Definição:** Concordância entre avaliadores além do acaso
**Tipo:** Variável contínua (razão)
**Unidade:** Adimensional (-1 a 1)
**Método de Medição:** Cálculo estatístico: κ = (Po-Pe)/(1-Pe)
**Aplicável a:** Meta-métrica para validar VD5

##### Categoria 2: Eficiência Computacional
VD7: Tempo Médio de Resposta

**Definição:** Duração do processamento
**Tipo:** Variável contínua (razão)
**Unidade:** Segundos (s)
**Método de Medição:** Timestamp_fim - Timestamp_início
**Aplicável a:** Todas as execuções

VD8: Percentil 95 do Tempo

**Definição:** Tempo máximo para 95% das requisições
**Tipo:** Variável contínua (razão)
**Unidade:** Segundos (s)
**Método de Medição:** Cálculo estatístico sobre distribuição
**Aplicável a:** Análise de SLA e piores casos

VD9: Desvio Padrão do Tempo

**Definição:** Variabilidade temporal
**Tipo:** Variável contínua (razão)
**Unidade:** Segundos (s)
**Método de Medição:** σ = √[Σ(xi-μ)²/n]
**Aplicável a:** Estabilidade de desempenho

VD10: Número de Tokens Gerados

**Definição:** Tamanho da resposta
**Tipo:** Variável discreta (contagem)
**Unidade:** Número de tokens
**Método de Medição:** Extração de metadados da API
**Aplicável a:** Todas as respostas

##### Categoria 3: Custo
VD11: Custo por Resposta

**Definição:** Custo financeiro total
**Tipo:** Variável contínua (razão)
**Unidade:** Dólares americanos (USD)
**Método de Medição:** (tokens_input × preço_input) + (tokens_output × preço_output)
**Aplicável a:** Todas as execuções

VD12: Índice de Complexidade da Tarefa

**Definição:** Score de dificuldade pré-atribuído
**Tipo:** Variável ordinal
**Unidade:** Escala 1-10
**Método de Medição:** Classificação por especialistas usando rubrica
**Aplicável a:** Caracterização dos prompts

##### Categoria 4: Consistência e Robustez

VD13: Coeficiente de Variação

**Definição:** Variabilidade relativa entre execuções
**Tipo:** Variável contínua (razão)
**Unidade:** Percentual (%)
**Método de Medição:** CV = (σ/μ) × 100%
**Aplicável a:** Análise de consistência intra-modelo

VD14: Similaridade Semântica

**Definição:** Consistência de conteúdo entre repetições
**Tipo:** Variável contínua (razão)
**Unidade:** Adimensional (0-1)
**Método de Medição:** Cosine similarity de embeddings
**Aplicável a:** Análise de determinismo

VD15: Taxa de Alucinação

**Definição:** Frequência de informações falsas/inventadas
**Tipo:** Variável contínua (razão)
**Unidade:** Percentual (0-100%)
**Método de Medição:** Verificação humana + busca em bases de conhecimento
**Aplicável a:** Principalmente perguntas factuais

#### 8.5 Variáveis de Controle / Bloqueio
VC1: Tamanho do Prompt (Tokens de Entrada)

**Justificativa:** Prompts maiores podem afetar tempo e custo
**Controle:** Documentação de todos os tamanhos; análise de correlação
**Tipo:** Contínua (contagem)

VC2: Idioma do Prompt

**Justificativa:** Modelos podem ter desempenho diferente em PT vs. EN
**Controle:** Balanceamento aproximado (60% português, 40% inglês)
**Tipo:** Categórica (2 níveis)

VC3: Horário da Execução

**Justificativa:** Carga de servidor pode afetar latência
**Controle:** Distribuição uniforme ao longo do dia; registro de timestamps
**Tipo:** Temporal (timestamp)

VC4: Avaliador Humano

**Justificativa:** Diferentes avaliadores podem ter critérios ligeiramente diferentes
**Controle:** Randomização de atribuição; análise de concordância inter-avaliadores
**Tipo:** Categórica (3 níveis)

VC5: Versão da API

**Justificativa:** Atualizações podem mudar comportamento
**Controle:** Versionamento explícito; documentação precisa
**Tipo:** Categórica (string de versão)

VC6: Ordem de Apresentação

**Justificativa:** Efeitos de ordem em avaliação humana
**Controle:** Randomização completa da ordem
**Tipo:** Ordinal

VC7: Hiperparâmetros do Modelo

**Justificativa:** Configurações afetam comportamento
**Controle:** Fixação: temperatura=0.7, max_tokens=2048, top_p=0.9 para todos
**Tipo:** Múltiplas contínuas (fixadas)

#### 8.6 Possíveis variáveis de confusão

As possíveis variáveis de confusão que podem afetar os resultados incluem mudanças temporais nos modelos, já que fornecedores podem atualizar versões silenciosamente durante o experimento, o que pode levar a diferenças atribuídas ao modelo quando, na verdade, decorrem da versão utilizada. A mitigação envolve versionamento rigoroso, coleta concentrada em períodos curtos e análise temporal, acompanhada do monitoramento do desempenho entre a primeira e a última semana. Também há variações de carga de servidor, pois APIs podem apresentar latência instável dependendo da infraestrutura, fazendo com que tempos de resposta reflitam a carga e não o comportamento do modelo. Para reduzir esse efeito, recomenda-se distribuir medições ao longo do tempo, realizar múltiplas repetições e aplicar análise de variância, monitorando o desvio padrão dos tempos por modelo.

Outro fator relevante são as diferenças de motivação ou fadiga dos avaliadores, já que o estado psicológico pode influenciar a consistência das avaliações. Esse problema pode ser reduzido com pausas obrigatórias, randomização da ordem de análise e inspeção de tendências temporais, observando a correlação entre ordem e pontuação. O viés de familiaridade também deve ser considerado, pois avaliadores podem ter preferência prévia por certos modelos, influenciando julgamentos subjetivos. O cegamento das respostas é a principal forma de mitigação, enquanto o monitoramento envolve a análise dos padrões individuais de avaliação.

Além disso, alguns prompts podem favorecer inadvertidamente determinados modelos, o que torna a comparação injusta. A mitigação inclui revisão independente do dataset e diversificação máxima dos prompts, com monitoramento feito por meio da análise de interação entre modelo e prompt específico. Diferenças de infraestrutura também podem introduzir confusão, como no caso de LLaMA rodando localmente enquanto outros modelos utilizam APIs em nuvem, o que afeta a comparabilidade dos tempos. A solução é usar o mesmo tipo de infraestrutura ou analisar eficiência separadamente, sempre documentando o setup detalhadamente.

Por fim, existem efeitos de aprendizagem do dataset, já que modelos podem ter visto variações dos prompts durante o treinamento, produzindo respostas artificialmente boas. Para minimizar esse risco, recomenda-se o uso de prompts originais e variados, acompanhados de monitoramento que identifica respostas possivelmente memorizadas ou excessivamente perfeitas.

#### 9. Desenho Experimental
##### 9.1 Tipo de Desenho
Desenho Selecionado: Fatorial Completo (Full Factorial Design) com Medidas Repetidas
Estrutura: 4 × 5 × 3 (Modelo × Categoria × Repetição)
Características Principais:
Fatorial Completo:

Todos os níveis de todos os fatores são cruzados
Permite análise de efeitos principais E interações
4 modelos × 5 categorias × 50 prompts/categoria × 3 repetições = 3.000 observações

**Medidas Repetidas:**

Cada prompt é avaliado 3 vezes pelo mesmo modelo
Permite análise de consistência intra-modelo
Requer técnicas estatísticas apropriadas (ANOVA de medidas repetidas ou modelos mistos)

Between-Subjects (Modelo):

Cada resposta é gerada por apenas um modelo
Comparação entre modelos independentes

Within-Subjects (Categoria, Repetição):

Todos os modelos são expostos a todas as categorias
Cada [modelo × prompt] tem 3 repetições

**Classificação Formal:**

Tipo: Quasi-experimento (não há controle verdadeiro, mas rigoroso)
Estrutura: Fatorial misto (between + within)
Aleatorização: Parcial (ordem de execução e apresentação)
Cegamento: Duplo-cego na avaliação humana

**Justificativa da Escolha:**
A escolha do desenho experimental se justifica por sua ampla abrangência, já que o uso de um fatorial completo possibilita responder diversas questões de pesquisa de maneira integrada. Ele também se mostra eficiente porque a abordagem within-subjects aplicada à categoria maximiza a quantidade de informação obtida por observação, permitindo comparações diretas entre modelos em condições equivalentes. Além disso, a inclusão de repetições aumenta a consistência dos resultados ao possibilitar a análise da variabilidade intra-modelo, garantindo maior confiabilidade nas conclusões. O desenho também permite identificar interações importantes, verificando se os efeitos de um modelo dependem da categoria — aspecto fundamental para gerar recomendações práticas adequadas. Por fim, trata-se de uma alternativa viável, pois oferece um bom equilíbrio entre a quantidade de dados produzidos e os custos e o tempo necessários para conduzir o experimento.

#### 9.2 Randomização e Alocação

O Que É Randomizado:

**R1:** Ordem de Execução dos Prompts

- O quê: Sequência em que os 250 prompts são processados
Como: Gerador de números aleatórios (Python random.shuffle com seed fixo)
Por quê: Evitar efeitos de ordem ou temporais sistemáticos
Procedimento: Uma ordem aleatória única usada consistentemente para todos os 4 modelos

**R2:** Ordem de Apresentação para Avaliadores

- O quê: Sequência em que as 400 respostas são apresentadas para avaliação humana
Como: Random.shuffle independente para cada avaliador
Por quê: Evitar viés de ordem, fadiga sistemática
Procedimento: Cada avaliador recebe ordem única e diferente

**R3:** Seleção de Respostas para Avaliação Humana

- O quê: Qual das 3 execuções é selecionada para avaliação (1, 2 ou 3)
Como: Seleção aleatória uniforme
Por quê: Evitar viés de seleção sistemática (ex: sempre primeira execução)
Procedimento: Random.choice([1,2,3]) para cada [modelo × prompt]

**O Que NÃO É Randomizado:**

Alguns elementos do experimento não são randomizados. A alocação de prompts aos modelos permanece fixa, já que todos os modelos processam exatamente os mesmos prompts em um desenho completamente balanceado. Da mesma forma, a associação entre prompts e categorias não passa por randomização, pois cada prompt pertence naturalmente a uma categoria previamente definida. Os hiperparâmetros também não são sorteados: são mantidos em valores padrão e iguais para todos os modelos, garantindo comparabilidade. Por fim, os avaliadores não são distribuídos aleatoriamente entre subconjuntos de respostas; todos analisam as mesmas 400 respostas selecionadas, assegurando uniformidade nas avaliações.

##### 9.3 Balanceamento e Contrabalançamento
| Código | Tipo de Balanceamento                   | Descrição                                      | Justificativa / Objetivo                               |
|--------|------------------------------------------|------------------------------------------------|---------------------------------------------------------|
| **B1** | Entre Categorias                         | 50 prompts por categoria                       | Garante comparabilidade entre categorias                |
| **B2** | Entre Níveis de Complexidade (dentro das categorias) | 30% baixa, 50% média, 20% alta                | Representa uma distribuição realista de casos de uso    |
| **B3** | Entre Idiomas (aproximado)               | ~60% português, ~40% inglês                    | Balanceamento flexível conforme disponibilidade         |
| **B4** | Entre Modelos                            | Todos os modelos recebem os mesmos 250 prompts | Garante comparabilidade direta entre modelos            |

Contrabalanceamento:

| Código | Tipo de Contrabalançamento                | Descrição                                                     | Objetivo / Justificativa                                      |
|--------|---------------------------------------------|---------------------------------------------------------------|----------------------------------------------------------------|
| **CB1** | Ordem de Avaliação (entre avaliadores)      | Cada avaliador recebe uma ordem diferente de respostas        | Reduz efeitos de ordem, que se cancelam ao agregar resultados |
| **CB2** | Seleção de Execução para Avaliação          | Execuções 1, 2 e 3 são selecionadas de forma aproximadamente uniforme | Evita viés de sempre escolher a primeira ou última execução   |
| **CB3** | Timing da Coleta                            | Prompts executados uniformemente ao longo de 3 semanas, dias e horários | Distribui efeitos temporais (ex.: carga de servidor)          |


Verificações de Balanceamento Planejadas:

- Tabela de contingência: Modelo × Categoria (deve ser 50 para todas as células)
- Teste qui-quadrado de independência: Idioma × Modelo (verificar se distribuição é uniforme)
- Análise de distribuição temporal: Execuções por dia/horário
- ANOVA para verificar se características dos prompts (tamanho, complexidade) estão balanceadas entre categorias

##### 9.4 Número de Grupos e Sessões
| Dimensão      | Número de Grupos | Descrição                                                |
|----------------|-------------------|-----------------------------------------------------------|
| **Modelos**     | 4 grupos          | GPT-4, Claude, Gemini, LLaMA                             |
| **Categorias**  | 5 grupos          | Código, Texto, Lógica, Criatividade, Factual             |
| **Complexidade**| 3 níveis          | Baixa, Média, Alta                                       |
| **Total de Células** | 4 × 5 = 20  | Combinações Modelo × Categoria                           |

**Sessões/Rodadas:**
Para Coleta de Dados (Execução dos Modelos):

- Número de Sessões por [Modelo × Prompt]: 3 repetições
- Total de Execuções: 4 modelos × 250 prompts × 3 repetições = 3.000
- Distribuição Temporal: ~500 execuções por semana ao longo de 3 semanas

**Para Avaliação Humana:**

- Sessões por Avaliador: Flexível (pausas a cada 50 avaliações)
- Total de Avaliações por Avaliador: 400 respostas
- Sessões Estimadas: ~8 sessões de 50 avaliações cada
- Duração: ~5 dias úteis por avaliador

A escolha de utilizar três repetições por prompt (n = 3) fundamenta-se em um equilíbrio entre rigor metodológico e viabilidade prática. Esse número é suficiente para permitir a avaliação da consistência das respostas dos modelos, possibilitando o cálculo de estatísticas fundamentais como média, desvio padrão e coeficiente de variação. Além disso, trata-se de uma quantidade economicamente viável, pois o custo total correspondente a três execuções por prompt permanece dentro das restrições orçamentárias do estudo. A decisão também está alinhada com práticas consolidadas na literatura, na qual estudos comparativos entre modelos frequentemente utilizam de três a cinco repetições por condição experimental.

Apesar dessas vantagens, reconhece-se uma limitação inerente: três repetições oferecem poder estatístico limitado para análises aprofundadas de variabilidade intra-prompt, que idealmente requereriam entre cinco e dez repetições para estimativas mais robustas. Ainda assim, o estudo adota esse número como parte de um trade-off consciente. Optou-se por coletar 250 prompts com três repetições cada, em vez de reduzir o conjunto para 150 prompts com cinco repetições, uma vez que maximizar a diversidade de tarefas avaliadas traz maior representatividade ao experimento, preservando um nível aceitável de consistência estatística.

#### 10. População, Sujeitos e Amostragem
##### 10.1 População-Alvo
##### População de Modelos

**Definição:** Conjunto de todos os Large Language Models com as seguintes características:

| Critério | Descrição |
|---------|-----------|
| Multimodalidade | Texto como input e output |
| Tamanho | ≥ 7 bilhões de parâmetros |
| Disponibilidade | Pública (comercial ou open source) |
| Lançamento | 2023–2025 |
| Idiomas | Suporte ao inglês (preferencialmente também português) |
| Tamanho Estimado | 50–70 modelos |

**Exemplos de Membros:**

| Categoria | Modelos |
|----------|---------|
| Comerciais | GPT-4, Claude 3.x, Gemini, Command R+, Grok |
| Open Source | LLaMA 3.x, Mistral, Mixtral, Falcon, Phi-3 |
| Excluídos (especializados) | CodeLlama, WizardCoder |

##### População de Aplicações (Tarefas)

**Definição:** Universo de aplicações práticas de LLMs em contextos profissionais e acadêmicos.

| Domínio | Exemplos |
|---------|----------|
| Desenvolvimento de software | Programação, debugging |
| Processamento documental | Resumos, análises, extrações |
| Suporte à decisão | Solução de problemas, recomendações |
| Conteúdo criativo | Escrita, geração de ideias |
| Informação | Busca, organização, categorização |


##### População de Avaliadores Potenciais

| Critério | Descrição |
|----------|-----------|
| Formação | Graduação em área técnica |
| Experiência | ≥ 2 anos em tecnologia/IA |
| Localização | Brasil |
| Idiomas | Português e inglês |
| Tamanho estimado | Centenas de profissionais |


##### 10.2 Critérios de Inclusão de Sujeitos

##### Para Avaliadores Humanos

| Código | Critério Obrigatório |
|--------|------------------------|
| CI1 | Graduação completa em área de tecnologia |
| CI2 | ≥ 2 anos de experiência em software/IA/ML/dados |
| CI3 | Familiaridade com IA, ML e LLMs |
| CI4 | Fluência em português e inglês |
| CI5 | Disponibilidade de 20h ao longo de 2 semanas |
| CI6 | Aceite formal + confidencialidade |

**Critérios Desejáveis:**

| Código | Critério |
|--------|----------|
| — | Diversidade de background (código, NLP, dados) |
| — | Mestrado/Doutorado |
| — | Publicações na área |
| — | Experiência prévia em avaliação |


##### Para Prompts (Objetos de Estudo)

| Código | Critério |
|--------|----------|
| CI7 | Clareza |
| CI8 | Verificabilidade |
| CI9 | Relevância prática |
| CI10 | Resolvível em ≤ 2048 tokens |
| CI11 | Diversidade dentro da categoria |


#### 10.3 Critérios de Exclusão de Sujeitos

##### Para Avaliadores Humanos

| Código | Motivo de Exclusão |
|--------|---------------------|
| CE1 | Conflito de interesse com desenvolvedores dos modelos |
| CE2 | Viés declarado por modelos específicos |
| CE3 | Ausência de conhecimentos básicos necessários |
| CE4 | Indisponibilidade para cumprir cronograma |
| CE5 | Histórico ético insuficiente |
| CE6 | Barreiras linguísticas relevantes |

##### Para Prompts

| Código | Motivo de Exclusão |
|--------|---------------------|
| CE7 | Ambiguidade excessiva |
| CE8 | Conteúdo inadequado (ofensivo, ilegal, discriminatório) |
| CE9 | Dependência de contexto não fornecido |
| CE10 | Tarefas multimodais (imagem/áudio/vídeo) |
| CE11 | Respostas > 2048 tokens |
| CE12 | Duplicação de prompts no dataset |

#### 10.4 Tamanho da Amostra Planejado (por Grupo)

##### Amostra de Modelos

| Grupo | Modelo               | N (Prompts) | N (Execuções) | N (para Aval. Humana) |
|-------|-----------------------|-------------|----------------|-------------------------|
| G1    | GPT-4 Turbo           | 250         | 750            | 100                     |
| G2    | Claude Sonnet 3.5     | 250         | 750            | 100                     |
| G3    | Gemini Pro 1.5        | 250         | 750            | 100                     |
| G4    | LLaMA 3.1 70B         | 250         | 750            | 100                     |
| **TOTAL** | -                 | **250 únicos** | **3.000**   | **400**                 |


##### Amostra de Avaliadores

| Item | Valor |
|------|--------|
| Número de especialistas | **3** |
| Avaliações por avaliador | **400** respostas (100 por modelo) |
| Total de avaliações | **1.200** |


##### Limitações do Tamanho Amostral

| Limitação | Explicação |
|-----------|------------|
| Subgrupos pequenos | Combinações específicas (ex.: prompts muito complexos) podem ter apenas ~10 casos. |
| Poucos avaliadores | N = 3 é o mínimo aceitável; mais avaliadores aumentariam a confiabilidade. |

#### 11. Instrumentação e Protocolo Operacional

##### 11.1 Instrumentos de Coleta

| ID | Instrumento | Finalidade Principal | Tecnologias |
|----|-------------|----------------------|-------------|
| I1 | Script de Automação | Execução controlada de modelos e captura de respostas | Python 3.11, APIs OpenAI/Anthropic/Google, Transformers, Pandas, SQLAlchemy, PostgreSQL/SQLite |
| I2 | Ferramenta de Avaliação de Código | Compilar, testar e analisar código | Docker, gcc/javac/node/python, PyTest, SonarQube |
| I3 | Sistema de Verificação Factual | Checagem automática/semi-automática de fatos | Python, Wikipedia API, SPARQL, Selenium |
| I4 | Plataforma de Avaliação Humana | Avaliação cega em escala Likert | React, Node.js/Express, PostgreSQL, JWT |
| I5 | Análise de Similaridade Semântica | Embeddings e detecção de outliers | sentence-transformers, scikit-learn, UMAP, Python |
| I6 | Análise Estatística | Testes inferenciais e relatórios | R, tidyverse, lme4, ggplot2, psych, irr |


##### I1: Script de Automação de Execução

| Aspecto | Detalhes |
|---------|----------|
| Funções principais | Autenticação, leitura de prompts, envio de requisições, medir tempo, capturar tokens/custo, logging, retries, rate-limit, salvar em BD |
| Tecnologias | Python 3.11; openai, anthropic, google-generativeai, transformers, pandas, sqlalchemy |
| Banco de dados | PostgreSQL ou SQLite |
| Validação | Teste piloto com 10 prompts (precisão ±10ms) |

##### I2: Ferramenta de Avaliação de Código

##### Componentes

| Módulo | Função | Tecnologias |
|--------|--------|--------------|
| Compilação | Compilação segura em sandbox | Docker, gcc, javac, node, python |
| Testes | Execução de casos de teste e performance | PyTest |
| Análise Estática | Linting, complexidade, bugs | SonarQube API, ESLint, Pylint |


##### I3: Sistema de Verificação Factual

| Aspecto | Detalhes |
|---------|----------|
| Funções | Comparação com gabarito, busca automática, verificação lógica, marcação manual |
| Fontes | Wikipedia API, Wikidata/SPARQL, Google Search |
| Tecnologias | Python, wikipedia-api, SPARQL client, Selenium |


##### I4: Plataforma de Avaliação Humana

##### Funcionalidades para Avaliadores
- Login seguro  
- Resposta + prompt original  
- Escala Likert (1–5)  
- Comentários opcionais  
- Navegação Próximo/Anterior  
- Progresso (X/400)  
- Salvamento automático  
- Pausa obrigatória a cada 50 avaliações  

##### Funcionalidades para Administrador
- Dashboard e progresso por avaliador  
- Análise preliminar de concordância  
- Exportação dos dados  

##### Segurança
- Cegamento total (IDs anônimos)  
- Randomização da ordem  
- Auditoria das ações  

| Tecnologia | Uso |
|------------|-----|
| React.js | Frontend |
| Node.js + Express | Backend |
| PostgreSQL | Banco |
| JWT | Autenticação |


##### I5: Sistema de Similaridade Semântica

| Aspecto | Detalhes |
|---------|----------|
| Funções | Embeddings, cosine similarity, clusters, outliers, variabilidade |
| Modelo | all-MiniLM-L6-v2 (384 dims) |
| Tecnologias | Python, sentence-transformers, scikit-learn, UMAP, matplotlib/seaborn |


##### I6: Instrumentos de Análise Estatística

| Item | Conteúdo |
|------|----------|
| Ambiente | R 4.3.2 + RStudio |
| Pacotes principais | tidyverse, ggplot2, lme4, car, psych, irr, effsize, coin, dunn.test |
| Notebooks | 01_data_cleaning, 02_descriptive_stats, 03_inferential_tests, 04_visualizations, 05_final_report |


#### 11.2 Materiais de Suporte
##### MS1: Guia do Experimento (Documento Mestre)

Conteúdo:

- Visão geral do experimento
- Objetivos e questões de pesquisa
- Protocolo completo passo a passo
- Responsabilidades de cada participante
- Cronograma detalhado
- Contatos e suporte

**Formato:** PDF de 15-20 páginas

##### MS2: Guia do Avaliador

Conteúdo:

- Introdução e importância da tarefa
- Rubrica de avaliação detalhada
- Exemplos comentados de cada nível (1-5)
- FAQ sobre situações comuns
- Como lidar com dúvidas
- Política de pausas e bem-estar

**Formato:** PDF de 8-10 páginas + planilha de referência rápida (1 página)

#### 11.3 Procedimento Experimental: Versão Simplificada por Fases

##### **FASE 0 — Preparação**

**Objetivos da Fase**
- Configurar infraestrutura  
- Criar e validar dataset  
- Testar scripts e instrumentos  

**Resumo das Atividades**

| Atividade      | Descrição Simplificada |
|----------------|------------------------|
| Infraestrutura | Configurar servidor/VM, instalar dependências, validar APIs, configurar BD e testar conectividade |
| Dataset        | Coletar 400 prompts, adaptar/organizar, classificar por categoria/complexidade, criar gabaritos e balancear 250 prompts finais |
| Validação      | Revisão independente por 2 revisores e reunião de consenso |
| Teste Piloto   | Executar 120 testes iniciais, validar funcionamento e ajustar protocolo |


##### **FASE 1: Coleta Automatizada**

**Objetivos da Fase**
- Executar os 3.000 testes de modelos  
- Registrar tempo, tokens, custo e respostas  
- Executar verificações automáticas  

**Fluxo Simplificado**

**Execução diária**
- ~143 execuções/dia

**Para cada prompt × modelo × repetição**
1. Enviar requisição  
2. Registrar tempo, tokens, custo, resposta  
3. Repetir até 3 vezes em caso de erro  
4. Salvar no banco  

**Métricas automáticas**
- **Código:** compilação, testes, linting, bugs  
- **Factual/Lógico:** comparação com gabarito  
- **Consistência:** embeddings, similaridade, coeficiente de variação  

**Monitoramento**
- Dashboard atualizado por hora  
- Backups diários  
- Relatório semanal

##### **FASE 2: Avaliação Humana**

**Objetivos da Fase**
- Avaliar 400 respostas com 3 avaliadores  
- Garantir cegamento, concordância e consistência  

**Resumo das Atividades**

| Atividade       | Descrição Simplificada |
|------------------|------------------------|
| Preparação      | Selecionar 400 respostas e randomizar ordem para avaliadores |
| Treinamento     | Explicação da rubrica, prática e calibração (Kappa preliminar) |
| Refinamento (se necessário) | Recalibrar avaliadores se Kappa < 0.60 |
| Avaliação    | 400 avaliações por avaliador com pausas obrigatórias |
| Concordância    | Calcular Kappa, ICC e resolver discordâncias extremas |


##### **FASE 3:  Análise de Dados**

**Objetivos da Fase**
- Limpar, integrar e analisar dados  
- Testar hipóteses  
- Produzir visualizações e relatório final  

**Resumo das Atividades**

| Atividade | Descrição Simplificada |
|-----------|------------------------|
| Limpeza | Importar dados, tratar faltantes/outliers, transformar variáveis |
| Análises | Estatísticas descritivas, ANOVA/Kruskal, interação modelo×categoria, análise de trade-offs |
| Visualizações + Relatório | Criar gráficos finais e consolidar relatório/documentação |

![Fluxograma](https://github.com/MatVini0601/EXP-LLM-DOM-001/blob/main/images/fluxograma.png)

#### 12. Plano de Análise de Dados (Pré-Execução)

##### 12.1 Estratégia Geral de Análise

**Abordagem Multi-Nível:**

O plano de análise segue estrutura hierárquica para responder às questões de pesquisa:

**Nível 1: Análises Descritivas**
- Objetivo: Caracterizar dados e identificar padrões gerais
- Métodos: Estatísticas sumárias, visualizações exploratórias
- Output: Tabelas descritivas, gráficos preliminares

**Nível 2: Análises Inferenciais Principais**
- Objetivo: Testar hipóteses formais sobre diferenças entre modelos
- Métodos: ANOVA/Kruskal-Wallis, testes post-hoc, tamanhos de efeito
- Output: Tabelas de significância, comparações par-a-par

**Nível 3: Análises de Interações e Moderadores**
- Objetivo: Investigar se efeitos dependem de contexto (categoria, complexidade)
- Métodos: ANOVA fatorial, análise de efeitos simples
- Output: Gráficos de interação, tabelas estratificadas

**Nível 4: Análises de Relações e Trade-offs**
- Objetivo: Quantificar relações entre custo, qualidade, eficiência
- Métodos: Correlação, regressão, análise de custo-benefício
- Output: Scatter plots, modelos preditivos

**Nível 5: Análises Qualitativas Complementares**
- Objetivo: Extrair insights de comentários e casos especiais
- Métodos: Análise temática de comentários dos avaliadores
- Output: Lista de insights, exemplos ilustrativos

**Mapeamento Questões x Análises:**

| **Questão** | **Análise Principal** | **Análise Secundária** |
|-------------|----------------------|------------------------|
| Q1.1 (Precisão factual) | ANOVA de taxa_acerto por modelo | Post-hoc Tukey, Cohen's d |
| Q1.2 (Qualidade código) | ANOVA de taxa_compilacao | Análise de bugs, exemplos |
| Q1.3 (Avaliação humana) | ANOVA de score_humano | Kappa, análise por categoria |
| Q2.1 (Tempo) | ANOVA/KW de tempo_medio | Percentil 95, variabilidade |
| Q2.2 (Desempenho sob carga) | Análise de desvio_padrao | Correlação com horário |
| Q2.3 (Tempo vs. Tokens) | Correlação + Regressão | Scatter plots por modelo |
| Q3.1 (Custo-benefício) | Razão Qualidade/Custo | Ranking, fronteira de Pareto |
| Q3.2 (Justificativa premium) | Regressão Qualidade~Custo | Teste de proporcionali dade |
| Q3.3 (Economia por complexidade) | ANOVA 3-way: Modelo×Complexidade×Custo | Interações |
| Q4.1 (Consistência) | ANOVA de coef_variacao | Similaridade semântica |
| Q4.2 (Robustez) | Análise de sensibilidade | Casos com alta variação |
| Q4.3 (Alucinação) | ANOVA de taxa_aluc | Análise qualitativa de casos |

##### 12.2 Métodos Estatísticos Planejados

**Testes Paramétricos:**

**T1: ANOVA One-Way**
- **Uso:** Comparar médias entre 4 modelos para uma métrica
- **Pressupostos:** Normalidade, homogeneidade de variâncias, independência
- **Fórmula:** F = MS_entre / MS_dentro
- **Interpretação:** p < 0.05 indica diferença significativa entre grupos
- **Software:** R: `aov()`, `car::Anova()`

**T2: ANOVA Two-Way (Fatorial)**
- **Uso:** Avaliar efeitos de Modelo e Categoria + interação
- **Modelo:** Y ~ Modelo + Categoria + Modelo:Categoria
- **Interpretação:** 
  - Efeito principal de Modelo: diferença média entre modelos
  - Efeito principal de Categoria: diferença média entre categorias
  - Interação: efeito de modelo depende de categoria
- **Software:** R: `aov(Y ~ A * B)`

**T3: ANOVA de Medidas Repetidas**
- **Uso:** Analisar 3 repetições por [modelo × prompt]
- **Modelo:** Modelo misto com efeito aleatório de prompt
- **Software:** R: `lme4::lmer(Y ~ Modelo + (1|prompt_id))`

**T4: Testes Post-Hoc (Tukey HSD)**
- **Uso:** Comparações par-a-par após ANOVA significativa
- **Correção:** Controla taxa de erro familywise
- **Software:** R: `TukeyHSD()`

**T5: Test t Pareado**
- **Uso:** Comparar dois modelos específicos
- **Aplicação:** Testes direcionados para hipóteses específicas
- **Software:** R: `t.test(paired=TRUE)`

**Testes Não-Paramétricos (Se Pressupostos Violados):**

**T6: Kruskal-Wallis**
- **Uso:** Alternativa não-paramétrica ao ANOVA
- **Pressupostos:** Apenas independência (não assume normalidade)
- **Software:** R: `kruskal.test()`

**T7: Teste de Dunn**
- **Uso:** Post-# Testes Estatísticos, Tamanhos de Efeito e Confiabilidade

##### **Testes Não-Paramétricos**

##### **T7: Post-hoc para Kruskal-Wallis**

| Item | Descrição |
|------|-----------|
| **Correção** | Bonferroni ou Holm |
| **Software** | R: `dunn.test::dunn.test()` |


##### **T8: Teste de Wilcoxon**

| Item | Descrição |
|------|-----------|
| **Uso** | Comparação de dois grupos (alternativa ao t-test) |
| **Software** | R: `wilcox.test()` |

##### **Testes de Associação**

##### **T9: Correlação de Pearson**

| Item | Descrição |
|------|-----------|
| **Uso** | Relação linear entre variáveis contínuas (ex: custo vs. qualidade) |
| **Pressupostos** | Normalidade bivariada |
| **Interpretação** | r ∈ [-1, 1]; \|r\| > 0.7 = forte |
| **Software** | R: `cor.test(method = "pearson")` |

##### **T10: Correlação de Spearman**

| Item | Descrição |
|------|-----------|
| **Uso** | Alternativa não-paramétrica para relações monotônicas |
| **Software** | R: `cor.test(method = "spearman")` |


#### **Modelos de Regressão**

##### **T11: Regressão Linear Simples**

| Item | Descrição |
|------|-----------|
| **Uso** | Predizer qualidade a partir de custo |
| **Modelo** | Qualidade = β₀ + β₁ × Custo + ε |
| **Software** | R: `lm()` |


##### **T12: Regressão Linear Múltipla**

| Item | Descrição |
|------|-----------|
| **Uso** | Incluir múltiplos preditores |
| **Modelo** | Qualidade = β₀ + β₁×Custo + β₂×Tempo + β₃×Modelo_dummy + ε |
| **Software** | R: `lm()` |


##### **T13: Modelos Mistos (LMM)**

| Item | Descrição |
|------|-----------|
| **Uso** | Dados hierárquicos (repetições dentro de prompts) |
| **Modelo** | Y ~ Modelo + Categoria + (1 | prompt_id) |
| **Software** | R: `lme4::lmer()` |

##### **Tamanhos de Efeito**

##### **E1: Cohen's d**

| Item | Descrição |
|------|-----------|
| **Uso** | Diferença padronizada entre dois grupos |
| **Fórmula** | d = (M₁ - M₂) / SD_pooled |
| **Interpretação** | 0.2 = pequeno, 0.5 = médio, 0.8 = grande |
| **Software** | R: `effsize::cohen.d()` |

##### **E2: Eta-Squared (η²)**

| Item | Descrição |
|------|-----------|
| **Uso** | Proporção da variância explicada em ANOVA |
| **Fórmula** | η² = SS_efeito / SS_total |
| **Interpretação** | 0.01 = pequeno, 0.06 = médio, 0.14 = grande |
| **Software** | R: `effectsize::eta_squared()` |

##### **E3: Cliff's Delta**

| Item | Descrição |
|------|-----------|
| **Uso** | Tamanho de efeito não-paramétrico |
| **Interpretação** | Probabilidade de grupo1 > grupo2 |
| **Software** | R: `effsize::cliff.delta()` |

##### **Confiabilidade**

##### **C1: Kappa de Cohen**

| Item | Descrição |
|------|-----------|
| **Uso** | Concordância interavaliadores |
| **Fórmula** | κ = (Po − Pe) / (1 − Pe) |
| **Interpretação** | <0.4 = pobre; 0.4–0.6 = moderado;

#### 12.4 Plano de Análise para Dados Qualitativos (Versão Simplificada)

##### Fontes de Dados
- **DQ1 – Comentários dos Avaliadores:** justificativas, observações, problemas.
- **DQ2 – Observações do Piloto:** notas técnicas, falhas, feedback do treinamento.
- **DQ3 – Exemplos Ilustrativos:** respostas boas/ruins, discordâncias, alucinações.


##### Método: Análise Temática

**Etapa 1 — Familiarização**
- Ler todos os comentários.
- Identificar padrões iniciais.

**Etapa 2 — Codificação Inicial (exemplos)**
- `ERRO_FACTUAL`
- `INCOMPLETO`
- `EXCELENTE_INSIGHT`
- `PROBLEMA_CLAREZA`
- `CRIATIVIDADE_ALTA`
- `CODIGO_INEFICIENTE`
- `ALUCINACAO`

**Etapa 3 — Agrupamento Temático**
- Qualidade técnica  
- Clareza e apresentação  
- Criatividade  
- Problemas específicos por tarefa  

**Etapa 4 — Quantificação**
- Contar frequência dos códigos por modelo.
- Testar associação entre modelo e tipo de erro (ex: Qui-quadrado).

**Etapa 5 — Exemplos Representativos**
- Selecionar 2–3 exemplos por tema.
- Escolher exemplos variados entre modelos.
- Anonimizar se necessário.

**Etapa 6 — Integração com Quantitativos**
- Usar comentários para explicar padrões numéricos.
- Triangulação para validar resultados.

## Outputs Esperados
- **Tabela de Frequência de Códigos**
- **Seção narrativa no relatório**
- **Citações ilustrativas**

## Limitações
- Comentários são voluntários → amostra pequena.  
- Viés de seleção → mais comentários em casos extremos.  
- Codificação subjetiva → mitigada por regras claras.  


## Uso Adequado
- Complementar resultados quantitativos  
- Gerar hipóteses  
- Oferecer contexto  

#### 13. Avaliação de Validade (Ameaças e Mitigação)

##### Ameaças à Validade

| ID | Categoria | Descrição | Impacto | Mitigação |
|----|-----------|-----------|---------|-----------|
| **VCE-1** | Validade de Conclusão Estatística | Distribuições podem violar pressupostos de normalidade e homogeneidade necessários para testes paramétricos. | - p-valores incorretos<br>- Aumento de erros tipo I e II<br>- Intervalos de confiança imprecisos | - Testes de pressupostos (Shapiro-Wilk, Levene)<br>- Transformações (log, Box-Cox)<br>- Testes não paramétricos<br>- Bootstrap para ICs<br>- Reportar sensibilidade dos testes |
| **VCE-2** | Validade de Conclusão Estatística | Variâncias diferentes entre modelos comprometem ANOVA. | - ANOVA inválida<br>- Comparações injustas<br>- Erros estatísticos | - Teste de Levene<br>- ANOVA de Welch<br>- Transformações<br>- Reportar variâncias e médias |
| **VI-1** | Validade Interna | Variações temporais nas APIs durante 3 semanas. | - Efeito temporal confundido com efeito de modelo<br>- Diferenças irreproduzíveis | - Versionamento rigoroso<br>- Randomização temporal<br>- Monitoramento de changelogs<br>- ANOVA temporal<br>- Documentação de timestamps |
| **VI-2** | Validade Interna | Fadiga e efeitos de ordem dos avaliadores. | - Viés para início/fim da lista<br>- Redução da confiabilidade<br>- Tendência temporal | - Randomização completa da ordem<br>- Pausas a cada 50 avaliações<br>- Limite 80/dia<br>- Análise de tendência nos scores<br>- Excluir avaliador anômalo |
| **VI-3** | Validade Interna | Seleção não-aleatória de prompts. | - Resultados enviesados<br>- Baixa generalização<br>- Favorecimento indevido | - Revisão independente<br>- Diversificação de fontes<br>- Mistura PT/EN<br>- Teste piloto<br>- Sensibilidade por subconjuntos |
| **VC-1** | Validade de Constructo | Métricas simplificadas não capturam “qualidade” completa. | - Sub-representação do constructo<br>- Modelos parecem melhores do que são | - Múltiplas métricas (triangulação)<br>- Avaliação humana<br>- Transparência sobre limites |
| **VC-2** | Validade de Constructo | Reatividade: avaliadores sabem que estão sendo testados. | - Severidade artificial<br>- Julgamento não natural | - Instruções claras<br>- Ambiente relaxado<br>- Especialistas habituados |
| **VC-3** | Validade de Constructo | Viés de confirmação nas análises. | - Interpretação enviesada<br>- Descarte de resultados contrários | - Hipóteses pré-especificadas<br>- Revisão crítica<br>- Análise cega |
| **VE-1** | Validade Externa | Resultados são um “snapshot” temporal. | - Obsolescência rápida<br>- Versões futuras mudam desempenho | - Versionamento<br>- Discussão temporal<br>- Replicabilidade |
| **VE-2** | Validade Externa | Apenas PT e EN avaliados. | - Não generaliza para outros idiomas | - Escopo linguístico explícito<br>- Estudos futuros multilíngues |
| **VE-3** | Validade Externa | Apenas 3 avaliadores brasileiros. | - Viés cultural/profissional | - Avaliadores diversos<br>- Triangulação com métricas automáticas |

#### 14.2 Consentimento Informado

##### Processo de Consentimento

| Etapa | Descrição | Responsável | Prazo |
|------|------------|--------------|--------|
| **1. Convite inicial** | E-mail com visão geral do projeto | Pesquisador Principal | Semana -4 |
| **2. Envio do TCLE** | Termo de Consentimento Livre e Esclarecido (PDF) | Pesquisador Principal | Semana -4 |
| **3. Reunião de esclarecimento** | Videochamada para dúvidas (30 min) | Pesquisador Principal | Semana -3 |
| **4. Assinatura digital** | Plataforma DocuSign ou similar | Avaliador | Até Semana -2 |
| **5. Confirmação e registro** | Armazenamento seguro dos TCLEs | Pesquisador Principal | Semana -2 |


##### Conteúdo do Termo de Consentimento Livre e Esclarecido (TCLE)

**Seções obrigatórias:**

| Seção | Conteúdo Resumido |
|-------|---------------------|
| **1. Título e pesquisador** | "Análise Comparativa de Desempenho entre Diferentes Modelos de LLMs" <br> Pesquisador: Matheus Vinicius (matheus.rodrigues.1462287@sga.pucminas.br) |
| **2. Natureza da pesquisa** | Estudo científico sobre qualidade de modelos de inteligência artificial |
| **3. Participação** | • Avaliar 400 respostas geradas por LLMs <br> • Tempo estimado: 12-15 horas ao longo de 2 semanas <br> • Local: remoto (plataforma web) |
| **4. Riscos** | • Risco mínimo: fadiga cognitiva leve <br> • Mitigação: pausas obrigatórias, limite diário |
| **5. Benefícios** | • Compensação financeira: R$ 500,00 <br> • Contribuição científica <br> • Experiência em avaliação de IA <br> • Acesso antecipado aos resultados |
| **6. Confidencialidade** | • Identidade será pseudoanonimizada (Avaliador_A, B, C) <br> • Dados protegidos por senha <br> • Apenas pesquisador terá acesso aos nomes reais |
| **7. Voluntariedade** | • Participação totalmente voluntária <br> • Direito de desistir a qualquer momento sem justificativa <br> • Sem penalização por desistência |
| **8. Compensação** | • R$ 500,00 via PIX após conclusão <br> • Desistência após 50% concluído: compensação proporcional |
| **9. Contatos** | • Pesquisador: [telefone] / [e-mail] <br> • Orientador: [nome] / [e-mail] <br> • Instituição: PUC Minas |
| **10. Declarações** | • Li e compreendi todas as informações <br> • Tive oportunidade de fazer perguntas <br> • Concordo em participar voluntariamente |


#### 14.3 Privacidade e Proteção de Dados

##### Inventário de Dados Pessoais Coletados

| Categoria | Dados Coletados | Finalidade | Base Legal (LGPD) |
|-----------|------------------|-------------|---------------------|
| Identificação | Nome completo, e-mail, telefone | Comunicação e pagamento | Consentimento (Art. 7º, I) |
| Dados profissionais | Formação, experiência, área de atuação | Caracterização da amostra | Consentimento |
| Dados financeiros | Chave PIX (CPF/e-mail/telefone) | Compensação financeira | Consentimento |
| Dados de avaliação | Scores, comentários, timestamps | Coleta de resultados | Execução de pesquisa (Art. 7º, IV) |
| Dados técnicos | IP, navegador, tempo de resposta | Auditoria técnica | Interesse legítimo (Art. 7º, IX) |

**IMPORTANTE:** Nenhum dado sensível (Art. 5º, II da LGPD) será coletado.


##### Classificação de Sensibilidade

| Dado | Nível | Justificativa |
|------|--------|----------------|
| Nome, e-mail, telefone | MÉDIO | Identificação direta |
| Chave PIX | MÉDIO | Dado financeiro básico |
| Scores e comentários | BAIXO | Opiniões profissionais |
| Formação/experiência | BAIXO | Dados profissionais públicos |


##### 14.3.1 Pseudoanonimização

| Fase | Estratégia | Implementação |
|------|-------------|----------------|
| Coleta | Identificadores separados de dados avaliativos | • Tabela avaliadores (ID, nome, e-mail, PIX) <br> • Tabela avaliacoes (ID_avaliador, scores) <br> • Relação 1:N com chave criptografada |
| Análise | Uso apenas de códigos | Avaliador_A, Avaliador_B, Avaliador_C |
| Publicação | Remoção total de identificadores | Apenas “3 avaliadores com 2+ anos experiência” |


##### 14.3.2 Controles de Segurança Técnica

| Controle | Descrição | Tecnologia |
|----------|------------|---------------|
| Criptografia em trânsito | HTTPS obrigatório (TLS 1.3) | Let's Encrypt + Nginx |
| Criptografia em repouso | Dados sensíveis criptografados no BD | PostgreSQL + pgcrypto (AES-256) |
| Autenticação | Login com senha forte + 2FA opcional | bcrypt + JWT |
| Controle de acesso | RBAC | • Pesquisador: total <br> • Avaliador: apenas suas avaliações |
| Auditoria | Log de todos os acessos | Tabela audit_log |
| Backup | Backup diário criptografado | Armazenamento local + cloud |


##### 14.3.3 Controles Organizacionais

- Acesso restrito ao pesquisador principal  
- Termo de confidencialidade assinado  
- Minimização de dados  
- Separação entre dados financeiros e avaliativos  


##### Retenção e Descarte de Dados

| Tipo de Dado | Retenção | Justificativa | Descarte |
|--------------|-----------|----------------|-----------|
| Identificáveis | 6 meses após conclusão | Comunicação pós-estudo e auditorias | Exclusão permanente |
| Pseudoanonimizados | 10 anos | Reprodutibilidade científica | Arquivamento |
| Dataset público | Indefinido | Compartilhamento científico | N/A |
| TCLEs | 5 anos | Requisito legal | Destruição física/digital |


##### Compartilhamento de Dados

| Destinatário | Dados | Finalidade | Base Legal |
|--------------|---------|-----------|--------------|
| Comunidade científica | Dataset anonimizado | Reprodutibilidade | Consentimento |
| Orientador | Dados pseudoanonimizados | Supervisão científica | Necessário |
| PUC Minas | Relatórios agregados | Prestação de contas | Institucional |

**Garantia:** Nenhum dado identificável será compartilhado publicamente.


##### Direitos dos Titulares (LGPD, Art. 18)

| Direito | Como Exercer |
|---------|----------------|
| Confirmação e acesso | Solicitação via e-mail |
| Correção | Atualização na plataforma |
| Anonimização/eliminação | Solicitação formal em 15 dias |
| Portabilidade | Exportação CSV |
| Revogação do consentimento | E-mail ao pesquisador |


#### 14.4 Aprovações Necessárias

##### Status de Aprovações

| Órgão/Pessoa | Necessário? | Prazo | Observações |
|--------------|-------------|--------|----------------|
| Orientador | SIM | Semana -6 | Aprovação do plano |
| Coordenação | SIM | Semana -5 | Autorização institucional |

#### 15. Recursos, Infraestrutura e Orçamento

##### 15.1 Recursos Humanos e Papéis

##### Equipe do Experimento

| Papel | Nome / Perfil | Dedicação | Responsabilidades Principais |
|---|---:|---:|---|
| **Pesquisador Principal (PI)** | Matheus Vinicius | 20h/semana (12 meses) | • Coordenação geral do experimento<br>• Desenvolvimento de instrumentos<br>• Coleta automatizada de dados<br>• Análise estatística<br>• Redação de relatórios<br>• Prestação de contas |
| **Orientador Acadêmico** | [Nome do orientador] | 2h/semana (12 meses) | • Supervisão científica<br>• Revisão metodológica<br>• Aprovação de decisões críticas<br>• Orientação na análise<br>• Revisão de publicações |
| **Avaliador Especialista A** | [A definir — Engenharia/Ciência da Computação] | 15h (2 semanas) | • Avaliação de 400 respostas<br>• Comentários qualitativos<br>• Participação em calibração<br>• Feedback sobre rubrica |
| **Avaliador Especialista B** | [A definir — IA / Machine Learning] | 15h (2 semanas) | • Avaliação de 400 respostas<br>• Comentários qualitativos<br>• Participação em calibração<br>• Feedback sobre rubrica |
| **Avaliador Especialista C** | [A definir — Análise de Dados / NLP] | 15h (2 semanas) | • Avaliação de 400 respostas<br>• Comentários qualitativos<br>• Participação em calibração<br>• Feedback sobre rubrica |
| **Revisor Independente** | [A definir — Pesquisador sênior em IA] | 8h (pontual) | • Revisão do dataset de prompts<br>• Validação metodológica<br>• Identificação de vieses<br>• Parecer independente |
| **Suporte Técnico** | [Opcional — Infraestrutura TI] | 4h (pontual) | • Configuração de servidor/GPU<br>• Troubleshooting de APIs<br>• Backup e segurança |


##### Matriz RACI (Responsabilidade)

| Atividade | PI | Orientador | Avaliadores | Revisor | Suporte TI |
|---|---:|---:|---:|---:|---:|
| Desenho experimental | R | A | I | C | I |
| Criação de prompts | R | C | I | A | I |
| Desenvolvimento de scripts | R | I | I | I | C |
| Configuração de infraestrutura | R | I | I | I | C |
| Execução automatizada | R | I | I | I | C |
| Treinamento de avaliadores | R | C | A | I | I |
| Avaliação humana | I | I | R | I | I |
| Análise estatística | R | A | I | C | I |
| Redação de relatório | R | A | I | I | I |
| Publicação de resultados | R | A | I | I | I |

**Legenda:** R = Responsável (executa) • A = Aprovador (decide) • C = Consultado (opina) • I = Informado (recebe comunicação)


##### Critérios de Seleção dos Avaliadores

| Critério | Peso | Método de Avaliação |
|---|---:|---|
| Formação acadêmica | 25% | Graduação em área técnica (obrigatório); Pós-graduação (desejável) |
| Experiência profissional | 30% | ≥ 2 anos em software/IA/dados |
| Familiaridade com LLMs | 20% | Questionário sobre uso prévio de GPT/Claude/Gemini |
| Disponibilidade | 15% | Compromisso com 15h em 2 semanas |
| Diversidade de perfil | 10% | Balanceamento entre: código, análise, criatividade |


#### 15.2 Infraestrutura Técnica Necessária

##### Ambientes Computacionais

| Ambiente | Especificação | Finalidade | Provedor |
|---|---|---|---|
| Servidor de execução | CPU: 8 cores • RAM: 16 GB • Disco: 500 GB SSD • SO: Ubuntu 22.04 LTS | Execução de scripts Python, armazenamento de BD | AWS EC2 t3.xlarge / Google Cloud VM | 
| Banco de dados | PostgreSQL 15.x • 50 GB | Armazenamento de prompts, respostas, avaliações, logs | Mesmo servidor ou RDS | 
| Plataforma de avaliação | Servidor web: Node.js 18.x • Nginx • SSL/TLS | Interface para avaliadores | Mesmo servidor ou Heroku |


##### Ferramentas e Software

| Categoria | Ferramenta | Versão | Licença | Custo |
|---|---|---:|---:|---:|
| Linguagens | Python | 3.11+ | Open source | Gratuito |
| IDEs | VS Code | Última | MIT | Gratuito |
| Controle de versão | Git / GitHub | 2.x / conta | GPL / plano gratuito | Gratuito |
| Banco de dados | PostgreSQL | 15.x | PostgreSQL License | Gratuito |
| Conteinerização | Docker | 24.x | Apache 2.0 | Gratuito |
| APIs de LLMs | OpenAI SDK | 1.x | MIT | Gratuito (SDK)* |
|  | Anthropic SDK | 0.x | MIT | Gratuito (SDK)* |
|  | Google GenAI SDK | Última | Apache 2.0 | Gratuito (SDK)* |
| Visualização | matplotlib / seaborn | — | MIT / BSD | Gratuito |
| Comunicação | Slack / Teams | N/A | Plano gratuito | Gratuito |

> \*O limite sendo ultrapassado haveria necessidade de pagamento para utilização a API. **Custo estimado listado na seção 15.4**.


##### Repositórios e Armazenamento

| Recurso | Plataforma | Capacidade | Finalidade | Acesso |
|---|---|---:|---|---|
| Repositório de código | GitHub (privado) | Ilimitado | Scripts, notebooks, documentação | Pesquisador + orientador |
| Armazenamento de dados | Google Drive institucional | 1 TB | Backups, TCLEs, resultados brutos | Pesquisador (criptografado) |
| Documentação | GitHub Wiki | Ilimitado | Protocolos, instruções, FAQ | Equipe do experimento |


#### 15.3 Materiais e Insumos

##### Materiais Digitais

| Item | Quantidade | Formato | Responsável |
|---|---:|---|---|
| Dataset de prompts | 250 | JSON / CSV | Pesquisador + Revisor |
| Gabaritos de respostas | ~100 | JSON |  Pesquisador |
| Rubrica de avaliação | 1 | PDF + JSON | Pesquisador + Orientador |
| Termo de Consentimento (TCLE) | 1 template | PDF editável | Pesquisador |
| Guia do Avaliador | 1 | PDF (≈10 páginas) | Pesquisador |
| Templates de relatórios | 3 | LaTeX / Markdown | Pesquisador |


##### Formulários e Checklists

- Checklist de prontidão técnica: Google Sheets
- Formulário de recrutamento: Google Forms
- Formulário de feedback pós-avaliação: Google Forms
- Checklist de análise estatística: Markdown
- Template de log de execução: CSV automático

#### 15.4 Orçamento e Custos Estimados

##### Resumo Executivo

| Categoria | Custo Estimado (USD) | Custo Estimado (BRL) | % do Total |
|---|---:|---:|---:|
| APIs de LLMs | US$ 500 | R$ 2.500 | 45% |
| Compensação de avaliadores | US$ 300 | R$ 1.500 | 27% |
| Infraestrutura (cloud) | US$ 100 | R$ 500 | 9% |
| Licenças e ferramentas | US$ 20 | R$ 100 | 2% |
| Recursos humanos (horas do PI)* | US$ 800 | R$ 4.000 | 14% |
| Contingência (10%) | US$ 60 | R$ 300 | 5% |
| **TOTAL** | **US$ 1.120** | **R$ 5.600** | **100%** |

> \*Custo do PI é estimado para fins de planejamento, mas **não será desembolsado** (bolsa ou trabalho acadêmico).


##### 15.4.1 Custos de APIs de LLMs (resumo)

- Cálculo por modelo considerando prompts/repetições e tokens médios.
- Preço de referência: dezembro/2024 (sujeito a variação).  
- Margem de segurança aplicada (×2) para reexecuções e prompts maiores.  
- **SUBTOTAL APIs:** ~US$ 500


##### 15.4.2 Compensação de Avaliadores

| Item | Quantidade | Valor Unitário | Total (BRL) | Total (USD aprox.) |
|---|---:|---:|---:|---:|
| Avaliador A | 15 horas | R$ 33/h | R$ 500 | ~US$ 100 |
| Avaliador B | 15 horas | R$ 33/h | R$ 500 | ~US$ 100 |
| Avaliador C | 15 horas | R$ 33/h | R$ 500 | ~US$ 100 |
| **SUBTOTAL** | — | — | **R$ 1.500** | **~US$ 300** |

> Justificativa: taxa horária compatível com mercado brasileiro (R$ 30–50/h).


##### 15.4.3 Infraestrutura Cloud (detalhe)

| Recurso | Especificação | Duração | Custo/mês | Total |
|---|---|---:|---:|---:|
| Servidor EC2 / GCP | t3.xlarge (8 vCPU, 16 GB RAM) | 2 meses | US$ 120/mês | US$ 80 (uso parcial) |
| Armazenamento (S3 / GCS) | 100 GB | 2 meses | US$ 2.30/mês | US$ 5 |
| Transferência de dados | ~50 GB | — | US$ 5/GB | US$ 10 |
| DocuSign | Plano mensal | 1 mês | US$ 10 | US$ 10 |
| **SUBTOTAL** | — | — | — | **~US$ 105** |

**Alternativa econômica:** usar free tiers / créditos estudantis ou servidor local (reduzir para ~US$ 20).

##### 15.4.4 Licenças e Ferramentas

- Majoritariamente open-source (Python, R, PostgreSQL, Docker).  
- **SUBTOTAL licenças:** ~US$ 0

##### 15.4.5 Recursos Humanos (Estimativa Teórica — não desembolsado)

| Papel | Horas | Taxa Estimada | Total (BRL) |
|---|---:|---:|---:|
| Pesquisador Principal | 240h | R$ 50/h | R$ 12.000 |
| Orientador Acadêmico | 24h | R$ 150/h | R$ 3.600 |
| Revisor Independente | 8h | R$ 100/h | R$ 800 |
| Suporte Técnico | 4h | R$ 80/h | R$ 320 |
| **SUBTOTAL** |  |  | **R$ 16.720 ( US 3344)** |

> Observação: custos estimados para valoração do esforço; normalmente não desembolsados em trabalho acadêmico.

##### Orçamento Consolidado (Apenas Custos Diretos)

| Item | Valor (USD) | Valor (BRL) |
|---|---:|---:|
| APIs de LLMs | $500 | R$ 2.500 |
| Compensação de avaliadores | $300 | R$ 1.500 |
| Infraestrutura cloud | $100 | R$ 500 |
| Licenças (DocuSign) | $10 | R$ 50 |
| **SUBTOTAL** | **$910** | **R$ 4.550** |
| Contingência (10%) | $91 | R$ 455 |
| **TOTAL GERAL** | **~$1.000** | **~R$ 5.000** |

##### Fonte de Financiamento

| Fonte | Valor Aprovado |
|---|---:|
| Bolsa de pesquisa institucional | R$ 3.000 |
| Verba do orientador | R$ 1.000 |
| Recursos próprios | R$ 1.000 |
| **TOTAL** | R$ 5.000 |


##### Plano de Contingência Orçamentária

| Cenário | Impacto | Medida de Mitigação |
|---|---|---|
| Orçamento excede em 20% | Custo total → R$ 6.000 | Reduzir prompts de 250 para 200 (-20% custo APIs) |
| APIs mais caras que o previsto | +50% no custo de APIs | Priorizar modelos mais baratos (Gemini, LLaMA) |
| Infraestrutura cloud cara | +100% no custo cloud | Migrar para servidor local ou free tiers |
| Financiamento não aprovado | Falta de R$ 3.000 | Buscar fomento alternativo, reduzir escopo ou postergar experimento |

#### 16. Cronograma, Marcos e Riscos Operacionais

##### 16.1 Macrocronograma (até o início da execução)

##### **Visão Geral: 12 Meses**

| Fase | Duração | Período | Marco Principal |
|------|---------|---------|-----------------|
| FASE 0: Preparação | 10 semanas | Mês 1–3 | ✅ Aprovação do plano + Infraestrutura pronta |
| FASE 1: Coleta Automatizada | 3 semanas | Mês 3–4 | ✅ 3.000 execuções concluídas |
| FASE 2: Avaliação Humana | 3 semanas | Mês 4–5 | ✅ 1.200 avaliações concluídas |
| FASE 3: Análise de Dados | 8 semanas | Mês 5–7 | ✅ Relatório técnico finalizado |
| FASE 4: Documentação e Publicação | 12 semanas | Mês 7–10 | ✅ Artigo submetido + Dataset público |
| Buffer | 8 semanas | Mês 10–12 | Margem para imprevistos |


##### **Cronograma Detalhado — FASE 0: Preparação**

| Semana | Atividade Principal | Entregas | Responsável | Dependências |
|--------|----------------------|----------|--------------|--------------|
| S1–S2 | Finalização do plano experimental | • Versão 1.0 • Submissão ao orientador | PI | — |
| S2–S3 | Revisão e aprovação acadêmica | • Parecer • Versão 1.1 | Orientador, PI | S1–S2 |
| S3 | Submissão para aprovações institucionais | • Protocolo coordenação • Solicitação DPO • Orçamento | PI | S2–S3 |
| S4 | Desenvolvimento do dataset de prompts | • 400 prompts • Classificação inicial | PI | — |
| S4–S5 | Revisão independente do dataset | • Dataset validado (250 prompts) • Gabaritos | Revisor, PI | S4 |
| S5–S6 | Desenvolvimento dos scripts | • Execuções • APIs integradas • Testes | PI | S3 |
| S6 | Configuração de infraestrutura | • Servidor • BD • APIs | PI, TI | S3 |
| S7 | Plataforma de avaliação | • Interface web • BD integrado | PI | S6 |
| S7–S8 | Materiais de suporte | • Guia • Rubrica • TCLE • Templates | PI, Orientador | — |
| S8 | Recrutamento | • 3 avaliadores • TCLEs assinados | PI | S7–S8 |
| S9 | Treinamento | • Calibração • 50 pilotos • Kappa ≥0.60 | PI | S8 |
| S9–S10 | Piloto completo | • 120 execuções teste • Ajustes finais | PI | S6, S7, S9 |
| S10 | Go/No-Go | • Checklist • Aprovação final | PI, Orientador | Todas |

##### **Marcos Críticos (Milestones)**

| Marco | Data-Alvo | Critério | Impacto se Não Cumprido |
|-------|-----------|----------|---------------------------|
| M1 | Semana 3 | Plano aprovado | BLOQUEANTE |
| M2 | Semana 4 | Orçamento confirmado | BLOQUEANTE |
| M3 | Semana 5 | Dataset validado | CRÍTICO |
| M4 | Semana 6 | Infraestrutura operacional | BLOQUEANTE |
| M5 | Semana 7 | Plataforma pronta | CRÍTICO |
| M6 | Semana 9 | Avaliadores treinados | CRÍTICO |
| M7 | Semana 10 | Piloto OK (≥95%) | CRÍTICO |
| M8 | Semana 10 | Go/No-Go aprovado | BLOQUEANTE |


##### 16.2 Dependências entre Atividades

##### **Diagrama Simplificado**<br>

![Diagrama Dependencia de atividades](https://github.com/MatVini0601/EXP-LLM-DOM-001/blob/main/images/dependenciaAtividades.png)

#### 16.3 Riscos Operacionais e Plano de Contingência

##### **Riscos de Cronograma**

| ID | Risco | Prob. | Impacto | Gatilho | Contingência | Responsável |
|-----|--------|--------|----------|----------|---------------|--------------|
| R-C1 | Atraso aprovação | Média | Alto | Semana 4 | Escalar / reduzir escopo | PI |
| R-C2 | Falta de avaliadores | Média | Alto | < 3 candidatos | Ampliar divulgação / +20% | PI |
| R-C3 | Falha piloto | Baixa | Muito Alto | Sucesso <90% | Debug / reduzir escopo | PI, TI |
| R-C4 | APIs instáveis | Média | Médio | >10% falhas | Retry / mais dias | PI |
| R-C5 | Avaliador desiste | Baixa | Alto | Aviso | Reserva / redistribuir | PI |
| R-C6 | Infraestrutura cai | Média | Médio | >4h off | Backup / suporte | PI, TI |
| R-C7 | Análise estatística difícil | Baixa | Médio | Pressupostos violados | Estatístico / alternativas | PI |


##### **Riscos de Recursos**

| ID | Risco | Prob. | Impacto | Gatilho | Contingência |
|-----|--------|--------|----------|----------|--------------|
| R-R1 | Orçamento insuficiente | Média | Alto | >120% custo | Reduzir prompts / menos modelos |
| R-R2 | Indisponibilidade PI | Baixa | Muito Alto | Doença | Pausar / orientador assume |
| R-R3 | Perda de API | Baixa | Alto | ToS muda | Migrar / LLaMA local |
| R-R4 | Servidor indisponível | Média | Médio | Hardware falha | Migrar / laptop |
| R-R5 | Perda de dados | Muito baixa | Catastrófico | Falha BD | Restaurar backup |


##### **Riscos de Qualidade**

| ID | Risco | Prob. | Impacto | Gatilho | Contingência |
|-----|--------|--------|----------|----------|--------------|
| R-Q1 | Baixa concordância | Média | Alto | Kappa <0.40 | Recalibrar / substituir |
| R-Q2 | Dataset enviesado | Baixa | Alto | Viés detectado | Revisão / substituição |
| R-Q3 | Modelos atualizam | Média | Médio | Atualização anunciada | Coleta rápida / documentar |
| R-Q4 | Métricas fracas | Baixa | Alto | Piloto sem correlação | Complementar métricas |

#### 17. Governança do Experimento

##### 17.1 Papéis e Responsabilidades Formais

##### Matriz Detalhada de Responsabilidades (RACI + V)

| Atividade / Decisão | PI | Orientador | Avaliadores | Revisor | Suporte TI | Coord. Curso |
|---------------------|----|-----------| ------------|---------|-----------|--------------|
| **Planejamento** | | | | | | |
| Elaborar plano experimental | **R** | **A** | I | C | I | I |
| Aprovar escopo e metodologia | C | **A** | I | C | I | I |
| Definir orçamento | **R** | **A** | I | I | I | **A** |
| Aprovar dataset de prompts | C | C | I | **A** | I | I |
| **Preparação** | | | | | | |
| Desenvolver scripts/instrumentos | **R** | I | I | C | C | I |
| Configurar infraestrutura | **R** | I | I | I | **A** | I |
| Recrutar avaliadores | **R** | C | - | I | I | I |
| Treinar avaliadores | **R** | C | **A** | I | I | I |
| Aprovar início da operação (Go) | R | **A** | I | I | I | I |
| **Execução** | | | | | | |
| Executar coleta automatizada | **R** | I | I | I | C | I |
| Realizar avaliações humanas | I | I | **R** | I | I | I |
| Monitorar progresso | **R** | I | I | I | C | I |
| Resolver problemas técnicos | **R** | C | I | I | **A** | I |
| Decidir mudanças no protocolo | C | **A** | I | C | I | I |
| **Análise e Publicação** | | | | | | |
| Executar análises estatísticas | **R** | **A** | I | C | I | I |
| Interpretar resultados | **R** | **A** | I | C | I | I |
| Redigir relatório/artigo | **R** | **A** | I | I | I | I |
| Aprovar publicação | C | **A** | I | I | I | I |
| Disponibilizar dataset público | **R** | **A** | I | I | I | I |

**Legenda Estendida:**
- **R (Responsible):** Executa a atividade
- **A (Accountable):** Aprova e é responsável final
- **C (Consulted):** Deve ser consultado (opinião técnica)
- **I (Informed):** Deve ser informado do resultado
- **V (Verifies):** Verifica qualidade/conformidade

##### Descrição Detalhada de Papéis

##### Tabela de Papéis, Autoridades e Responsabilidades

| Papel | Autoridade | Responsabilidades | Limites / Observações |
|-------|------------|-------------------|------------------------|
| **Pesquisador Principal (PI)** | - Coordenar todas as atividades operacionais<br>- Tomar decisões técnicas do dia a dia<br>- Alocar recursos dentro do orçamento<br>- Propor mudanças no plano (com aprovação) | - Executar 90% das atividades<br>- Garantir conformidade com protocolo<br>- Comunicar status semanalmente<br>- Documentar decisões e desvios<br>- Garantir qualidade dos dados<br>- Prestar contas financeiras | **Limites:**<br>- Não pode alterar escopo<br>- Não pode gastar >110% do orçamento<br>- Pode ajustar cronograma (±3 dias)<br>- Pode decidir detalhes técnicos |
| **Orientador Acadêmico** | - Aprovar/rejeitar plano experimental<br>- Aprovar mudanças no protocolo<br>- Aprovar início e fim de fases<br>- Aprovar publicações | - Garantir rigor científico<br>- Orientar interpretação de resultados<br>- Revisar documentos<br>- Supervisão metodológica<br>- Mediar conflitos | **Interação mínima:** 1 reunião/semana (1h) |
| **Avaliadores Especialistas** | - Atribuir scores dentro da rubrica<br>- Sugerir melhorias na rubrica | - Avaliar 400 respostas cada<br>- Seguir rubrica rigorosamente<br>- Justificar scores discrepantes<br>- Manter confidencialidade<br>- Reportar problemas imediatamente | **Limites:**<br>- Não podem alterar rubrica<br>- Não podem compartilhar dados<br>- Podem pausar e retornar |
| **Revisor Independente** | - Vetar prompts com viés<br>- Solicitar ajustes no dataset | - Revisar dataset criticamente<br>- Identificar vieses<br>- Validar balanceamento<br>- Fornecer parecer escrito | **Independência:**<br>Não pode ter conflito de interesse |



#### 17.2 Ritos de Acompanhamento Pré-Execução

##### Reuniões Regulares

| Reunião | Frequência | Duração | Participantes | Pauta Típica | Artefato Gerado |
|---------|-----------|---------|---------------|--------------|-----------------|
| **Status Semanal** | Toda segunda-feira, 14h | 60 min | PI + Orientador | • Progresso vs. cronograma<br>• Problemas encontrados<br>• Decisões necessárias<br>• Próximas atividades | Ata de reunião (template) |
| **Revisão de Marco** | Ao atingir cada milestone | 90 min | PI + Orientador (+ Revisor se aplicável) | • Validação do marco<br>• Análise de entregas<br>• Go/No-Go para próxima fase<br>• Ajustes no plano | • Checklist de marco<br>• Decisão formal Go/No-Go |
| **Calibração de Avaliadores** | 1× antes do piloto<br>1× depois do piloto | 120 min | PI + 3 Avaliadores + Orientador | • Explicação da rubrica<br>• Prática com exemplos<br>• Discussão de discordâncias<br>• Ajuste de interpretações | • Kappa preliminar<br>• Rubrica ajustada |
| **Comitê de Crise** (se necessário) | Ad-hoc | 60 min | PI + Orientador + Suporte TI | • Problema crítico identificado<br>• Análise de impacto<br>• Decisão de contingência | Plano de ação emergencial |

##### Checkpoints Formais (Go/No-Go)

| Checkpoint | Quando | Critérios de Aprovação | Participantes | Consequência de "No-Go" |
|-----------|--------|------------------------|---------------|-------------------------|
| **CP1: Plano Aprovado** | Semana 3 | • Parecer positivo do orientador<br>• Metodologia sólida<br>• Orçamento viável | PI, Orientador, Coordenação | Revisar e resubmeter |
| **CP2: Dataset Validado** | Semana 5 | • Revisor aprova qualidade<br>• 250 prompts balanceados<br>• Gabaritos criados | PI, Revisor, Orientador | Ajustar prompts (prazo +1 semana) |
| **CP3: Infraestrutura Pronta** | Semana 6 | • Servidor operacional<br>• APIs conectadas<br>• BD configurado<br>• Testes passam | PI, Suporte TI | Corrigir problemas (prazo +3 dias) |
| **CP4: Piloto Bem-Sucedido** | Semana 10 | • ≥95% execuções sem erro<br>• Métricas calculáveis<br>• Kappa ≥0.60 | PI, Orientador, Avaliadores | Refazer piloto ou ajustar instrumentos |
| **CP5: GO FINAL para Operação** | Semana 10 (fim) | **Todos os critérios da Seção 20 atendidos** | PI, Orientador | Adiar início até resolver |

### Rituais de Documentação

| Ritual | Frequência | Responsável | Formato |
|--------|-----------|-------------|---------|
| **Log de Progresso** | Diário | PI | Planilha Google Sheets (5 min/dia) |
| **Relatório Semanal** | Segunda-feira | PI | E-mail estruturado (template) |
| **Atualização do Kanban** | Diário | PI | GitHub Projects ou Trello |
| **Registro de Decisões** | Quando decisão importante | PI | Documento "ADR" (Architecture Decision Records) |
| **Registro de Riscos** | Semanal | PI | Planilha de riscos atualizada |

#### Template de Ata de Reunião Semanal
```markdown
Ata de Reunião - [Data]

Participantes: [Lista]
Duração: [HH:MM]

1. Progresso da Semana
- [ ] Atividades concluídas
- [ ] Atividades em andamento
- [ ] Atividades bloqueadas

2. Indicadores
| Métrica | Meta | Realizado | Status |
|---------|------|-----------|--------|
| Aderência ao cronograma | 100% | X% | 🟢/🟡/🔴 |
| Consumo orçamentário | Y% (esperado) | Z% | 🟢/🟡/🔴 |

3. Problemas e Riscos
- [Problema 1]: [Descrição] → [Ação]
- [Risco 1]: [Descrição] → [Mitigação]

4. Decisões Tomadas
- [Decisão 1]: [Descrição]-> [Responsável]-> [Prazo]

5. Próximos Passos
- [ ] [Atividade 1] - [Responsável] - [Prazo]
- [ ] [Atividade 2] - [Responsável] - [Prazo]

6. Ação Requerida do Orientador
- [Se aplicável]
```

#### 17.3 Processo de Controle de Mudanças no Plano

##### Tipos de Mudanças

| Tipo | Exemplos | Nível de Aprovação |
|------|----------|-------------------|
| **Trivial** | • Ajuste de < 3 dias no cronograma<br>• Correção de typos<br>• Pequenos ajustes em scripts | PI (autonomia) |
| **Menor** | • Ajuste de 3-7 dias<br>• Substituição de 1 avaliador<br>• Mudança em métrica secundária | PI + Orientador (e-mail) |
| **Maior** | • Mudança de escopo (±20 prompts)<br>• Alteração metodológica significativa<br>• Ajuste orçamentário >10% | PI + Orientador (reunião formal) |
| **Crítica** | • Mudança de objetivos<br>• Remoção de modelo<br>• Cancelamento de fase | PI + Orientador + Coordenação |

##### Fluxo de Controle de Mudanças

##### Etapa 1: Identificação e Proposta
**Responsável:** PI (ou qualquer stakeholder)  
**Ação:** Preencher "Change Request Form" (CRF)

**Conteúdo do CRF:**
- ID da mudança: CRF-YYYYMMDD-NN
- Solicitante
- Data
- Tipo de mudança (Trivial/Menor/Maior/Crítica)
- Descrição detalhada do problema
- Mudança proposta
- Justificativa
- Impacto no cronograma
- Impacto no orçamento
- Impacto na qualidade
- Alternativas consideradas

#### Etapa 2: Análise de Impacto
**Responsável:** PI  
**Prazo:** 24-48h  
**Ação:** Avaliar consequências em todas as dimensões

#### Etapa 3: Aprovação
**Responsável:** Conforme nível (ver tabela acima)  
**Prazo:**
- Trivial: Imediato
- Menor: 2 dias úteis
- Maior: 5 dias úteis
- Crítica: 1 semana

**Critérios de aprovação:**
- Impacto justifica a mudança?
- Recursos disponíveis para implementar?
- Não compromete objetivos principais?
- Não viola restrições éticas?

#### Etapa 4: Implementação
**Responsável:** PI  
**Ação:**
- Atualizar plano experimental (controle de versão)
- Comunicar mudança a todos afetados
- Atualizar cronograma e orçamento
- Registrar em log de mudanças

#### Etapa 5: Verificação
**Responsável:** Orientador  
**Ação:** Confirmar que mudança foi implementada conforme aprovado

##### Registro de Mudanças (Change Log)

**Local:** `/projeto/documentacao/change_log.md`

**Formato:**
| ID | Data | Tipo | Descrição | Impacto | Aprovador | Status |
|----|------|------|-----------|---------|-----------|--------|
| CRF-20250215-01 | 15/02/2025 | Menor | Substituição Avaliador B | +3 dias | Orientador | Implementado |
| CRF-20250301-02 | 01/03/2025 | Maior | Redução de 250→200 prompts | -2 semanas, -20% custo | Orientador | Aprovado |

### Mudanças Proibidas Após "Go Final"

Após aprovação do CP5 (Go Final), as seguintes mudanças **NÃO são permitidas** sem reiniciar todo o processo:
- Alteração de objetivos ou hipóteses
- Mudança de modelos avaliados
- Alteração significativa na rubrica de avaliação
- Substituição de >1 avaliador
- Mudança de métricas principais


#### 18. Plano de Documentação e Reprodutibilidade

##### 18.1 Repositórios e Convenções de Nomeação

##### Estrutura de Repositórios

| Repositório | Plataforma | Visibilidade | Conteúdo | URL (exemplo) |
|-------------|-----------|--------------|----------|---------------|
| **Repositório Principal** | GitHub | Privado (durante) / Público (após) | Código, scripts, notebooks, docs | `github.com/MatVini0601/EXP-LLM-DOM-001` |
| **Dataset e Resultados** | GitHub | Público (após publicação) | Dados brutos, processados, resultados | `github.com/MatVini0601/EXP-LLM-DOM-001` |
| **Documentos Institucionais** | Google Drive (PUC Minas) | Restrito | Aprovações, TCLEs, atas | Drive institucional |
| **Backup Seguro** | Google Drive pessoal criptografado | Privado | Cópia de segurança completa | Drive pessoal |

##### Estrutura de Pastas do Repositório Principal
```markdown
EXP-LLM-DOM-001/
├── README.md                    # Visão geral do projeto
├── LICENSE                      # Licença (MIT ou CC-BY)
├── CITATION.cff                 # Metadados de citação
├── requirements.txt             # Dependências Python
├── environment.yml              # Ambiente Conda
│
├── docs/                        # Documentação
│   ├── plano_experimental.md    # Este documento
│   ├── protocolo_execucao.md    # Protocolo operacional
│   ├── guia_avaliador.pdf       # Guia do avaliador
│   ├── rubrica.pdf              # Rubrica de avaliação
│   ├── change_log.md            # Registro de mudanças
│   └── architecture_decisions/  # ADRs (Architecture Decision Records)
│
├── data/                        # Dados (gitignored, apenas estrutura)
│   ├── raw/                     # Dados brutos (não versionados)
│   │   ├── prompts/             # Prompts originais
│   │   ├── responses/           # Respostas dos modelos
│   │   └── evaluations/         # Avaliações humanas
│   ├── processed/               # Dados processados
│   └── final/                   # Dataset público final
│
├── src/                         # Código fonte
│   ├── data_collection/         # Scripts de coleta
│   │   ├── execute_models.py    # Execução dos modelos
│   │   ├── api_clients.py       # Wrappers para APIs
│   │   └── config.yaml          # Configurações
│   ├── evaluation/              # Ferramentas de avaliação
│   │   ├── compile_code.py      # Teste de código
│   │   ├── check_facts.py       # Verificação factual
│   │   └── compute_similarity.py# Similaridade semântica
│   ├── analysis/                # Análise estatística
│   │   ├── descriptive_stats.R  # Estatísticas descritivas
│   │   ├── inferential_tests.R  # Testes de hipóteses
│   │   └── visualizations.R     # Gráficos
│   └── utils/                   # Funções auxiliares
│       ├── database.py          # Conexão com BD
│       └── logger.py            # Sistema de logs
│
├── notebooks/                   # Jupyter/R Markdown Notebooks
│   ├── 01_data_exploration.ipynb
│   ├── 02_descriptive_analysis.Rmd
│   ├── 03_inferential_tests.Rmd
│   └── 04_final_report.Rmd
│
├── web_platform/                # Plataforma de avaliação
│   ├── frontend/                # React app
│   ├── backend/                 # Node.js API
│   └── database/                # Scripts SQL
│
├── results/                     # Resultados (gitignored)
│   ├── figures/                 # Gráficos finais
│   ├── tables/                  # Tabelas formatadas
│   └── reports/                 # Relatórios gerados
│
└── tests/                       # Testes automatizados
├── test_api_clients.py
├── test_metrics.py
└── test_database.py
```

##### Convenções de Nomeação de Arquivos

##### Arquivos de Dados

| Tipo | Padrão | Exemplo |
|------|--------|---------|
| **Prompts** | `prompts_cat-[CATEGORIA]_[DATA].json` | `prompts_cat-codigo_20250215.json` |
| **Respostas** | `responses_[MODELO]_[PROMPT_ID]_exec[N]_[TIMESTAMP].json` | `responses_gpt4_p042_exec1_20250301T143022.json` |
| **Avaliações** | `evaluations_avaliador[X]_[DATA].csv` | `evaluations_avaliadorA_20250315.csv` |
| **Logs** | `log_[COMPONENTE]_[DATA].log` | `log_api-execution_20250301.log` |

##### Scripts e Notebooks

| Tipo | Padrão | Exemplo |
|------|--------|---------|
| **Scripts Python** | `[verbo]_[objeto].py` | `execute_models.py`, `compute_similarity.py` |
| **Notebooks** | `[NN]_[descricao-breve].[ext]` | `01_data_exploration.ipynb` |
| **Scripts R** | `[NN]_[descricao].R` | `03_inferential_tests.R` |

##### Arquivos de Documentação

| Tipo | Padrão |
|------|--------|
| **Markdown** | `snake_case.md` |
| **PDFs** | `TitleCase_v[N.N].pdf` |
| **LaTeX** | `document_name.tex` |

##### Controle de Versão

| Elemento | Sistema | Estratégia |
|----------|---------|------------|
| **Código e scripts** | Git (GitHub) | • Commits atômicos<br>• Mensagens descritivas<br>• Branch `main` protegida<br>• PRs para mudanças significativas |
| **Dados brutos** | Backup manual | • Versionamento por data<br>• Imutável após coleta |
| **Documentos** | Git + Google Docs (rascunhos) | • Versão final em Git<br>• Histórico de revisões |
| **Plano experimental** | Git | • Tags para versões principais<br>• `v1.0`, `v1.1`, `v2.0` |

**Commits semânticos:**
- feat: adiciona função de cálculo de similaridade
- fix: corrige bug na conexão com API do Claude
- docs: atualiza README com instruções de instalação
- refactor: reorganiza estrutura de pastas
- test: adiciona testes para métricas de qualidade


#### 18.2 Templates e Artefatos Padrão

##### Templates de Documentos

| Template | Formato | Localização | Uso |
|----------|---------|-------------|-----|
| **Ata de Reunião** | Markdown | `/docs/templates/ata_reuniao.md` | Toda reunião semanal |
| **Change Request Form** | Markdown | `/docs/templates/change_request.md` | Proposta de mudanças |
| **Relatório Semanal** | Markdown | `/docs/templates/relatorio_semanal.md` | Status para orientador |
| **Checklist de Marco** | Markdown | `/docs/templates/checklist_marco.md` | Validação de milestones |
| **TCLE** | PDF editável | `/docs/templates/TCLE_template.pdf` | Consentimento de avaliadores |

##### Templates de Código

| Template | Linguagem | Localização | Uso |
|----------|-----------|-------------|-----|
| **API Client** | Python | `/src/templates/api_client_template.py` | Integração com novas APIs |
| **Teste Unitário** | Python | `/tests/templates/test_template.py` | Testes automatizados |
| **Notebook de Análise** | R Markdown | `/notebooks/templates/analysis_template.Rmd` | Análises estatísticas |
| **Script de Visualização** | R/Python | `/src/templates/viz_template.R` | Geração de gráficos |


##### Checklists Padrão

##### Checklist de Início de Semana (Segunda-feira)
```markdown
Checklist - Início de Semana [DATA]

Preparação
- [ ] Revisar cronograma da semana
- [ ] Verificar status de APIs (uptime)
- [ ] Checar saldo orçamentário
- [ ] Revisar registro de riscos

Comunicação
- [ ] Enviar relatório semanal ao orientador
- [ ] Agendar reunião semanal
- [ ] Responder e-mails pendentes

Técnico
- [ ] Executar backup semanal
- [ ] Verificar integridade do BD
- [ ] Atualizar Kanban/Trello
```

##### Checklist de Coleta de Dados (Diário)
```markdown
Checklist - Coleta [DATA]

Pré-execução
- [ ] Verificar conectividade com APIs
- [ ] Confirmar saldo de créditos
- [ ] Revisar prompts do dia

Durante
- [ ] Monitorar taxa de erro (<5%)
- [ ] Verificar armazenamento de respostas
- [ ] Log de problemas (se houver)

Pós-execução
- [ ] Validar integridade dos dados
- [ ] Atualizar dashboard de progresso
- [ ] Backup incremental
- [ ] Atualizar registro de custos
```

#### 18.3 Plano de Empacotamento para Replicação Futura

##### Objetivos de Reprodutibilidade

| Nível | Descrição | Requisitos |
|-------|-----------|------------|
| **Reproduzível** | Mesmos dados + mesmo código = mesmos resultados | Código + dados + ambiente |
| **Replicável** | Novo pesquisador pode repetir experimento com novos dados | Código + protocolo detalhado |
| **Robusto** | Resultados consistentes com variações menores | Documentação de sensibilidade |
| **Generalizável** | Metodologia aplicável a outros contextos | Framework abstrato |

**Meta:** Atingir nível **Replicável** (mínimo) e **Robusto** (desejável).

##### Pacote de Reprodutibilidade

##### Componentes Obrigatórios (Tier 1 - Essencial)

| Artefato | Conteúdo | Formato | Status |
|----------|----------|---------|--------|
| **README Completo** | • Visão geral<br>• Como instalar<br>• Como executar<br>• Como analisar | Markdown | A finalizar |
| **Plano Experimental** | Este documento completo | Markdown/PDF | Em progresso |
| **Dataset de Prompts** | 250 prompts anonimizados | JSON/CSV | A criar |
| **Gabaritos** | Respostas corretas esperadas | JSON | A criar |
| **Respostas dos Modelos** | 3.000 respostas (anonimizadas) | JSON | Após coleta |
| **Avaliações Humanas** | Scores + comentários (pseudoanonimizados) | CSV | Após FASE 2 |
| **Scripts de Coleta** | Código Python completo + config | .py + .yaml | Em desenvolvimento |
| **Scripts de Análise** | Código R/Python + notebooks | .R / .ipynb | A desenvolver |
| **Requirements** | Dependências exatas | requirements.txt / environment.yml | A gerar |

##### Componentes Desejáveis (Tier 2 - Recomendado)

| Artefato | Conteúdo | Formato | Status |
|----------|----------|---------|--------|
| **Container Docker** | Ambiente completo reproduzível | Dockerfile | 🟡 A criar |
| **Makefile** | Automatização de setup e execução | Makefile | 🟡 A criar |
| **Tutorial em Vídeo** | Passo a passo da replicação (15 min) | MP4 (YouTube) | 🔴 Após finalização |
| **Dados Intermediários** | Embeddings, logs processados | CSV/JSON | 🔴 Após análise |
| **Figuras e Tabelas** | Resultados visuais finais | PNG/PDF + LaTeX | 🔴 Após análise |

##### Componentes Opcionais (Tier 3 - Valor Adicional)

| Artefato | Conteúdo | Formato | Status |
|----------|----------|---------|--------|
| **Dashboard Interativo** | Exploração visual dos resultados | Shiny / Streamlit | 🔴 Opcional |
| **API de Consulta** | Endpoint para consultar resultados | REST API | 🔴 Opcional |
| **Dataset Sintético** | Dados fictícios para testes | JSON | 🟡 Para testes |

##### Metadados para Publicação

| Campo | Valor |
|-------|-------|
| **Título** | Comparative Analysis of Large Language Model Performance: A Controlled Experiment |
| **Autores** | Matheus Vinicius, [Orientador] |
| **Afiliação** | PUC Minas - Engenharia de Software |
| **Palavras-chave** | Large Language Models, LLM Evaluation, Comparative Study, GPT-4, Claude, Gemini, LLaMA |
| **Licença de código** | MIT License |
| **Licença de dados** | CC-BY 4.0 |
| **Data de publicação** | [Após aceitação do artigo] |
| **Versão** | 1.0 |


##### Testes de Reprodutibilidade

Antes da publicação, executar **teste de replicação** com pessoa externa:

| Teste | Descrição | Critério de Sucesso |
|-------|-----------|---------------------|
| **Setup Test** | Pessoa externa instala ambiente | Sucesso em <15 min |
| **Execution Test** | Executa análises principais | Mesmos resultados (±1% diferença numérica) |
| **Comprehension Test** | Entende protocolo sem perguntas | Questionário pós-teste ≥80% correto |


#### 19. Plano de Comunicação

##### 19.1 Públicos e Mensagens-Chave Pré-Execução

##### Mapeamento de Stakeholders

| Público | Interesse Principal | Frequência de Comunicação | Canal Preferencial |
|---------|---------------------|----------------------------|-------------------|
| **Orientador** | Progresso científico, qualidade metodológica | Semanal | Reunião presencial/Zoom + E-mail |
| **Coordenação do Curso** | Conformidade institucional, prazos | Mensal + marcos | E-mail formal |
| **Avaliadores** | Instruções claras, cronograma, pagamento | Diário (durante FASE 2) | WhatsApp + Plataforma Web |
| **Revisor Independente** | Qualidade do dataset, ausência de viés | Pontual (S4-S5) | E-mail + Reunião |
| **Suporte TI** | Questões técnicas, troubleshooting | Sob demanda | Slack/Teams + Telefone |
| **Comunidade Acadêmica** | Metodologia, resultados, dataset | Após publicação | Artigo + GitHub + Twitter/LinkedIn |
| **Fornecedores de APIs** (OpenAI, Anthropic, etc.) | Conformidade com ToS | Pontual (pré-execução) | E-mail oficial |


#### 19.2 Canais e Frequência de Comunicação

##### Matriz de Comunicação

| Canal | Público | Tipo de Mensagem | Frequência | Responsável |
|-------|---------|------------------|-----------|-------------|
| **E-mail Formal** | Orientador, Coordenação, Revisor | Relatórios, aprovações, decisões formais | Semanal / Pontual | PI |
| **Reunião Presencial/Zoom** | Orientador | Discussão técnica, resolução de problemas | Semanal (1h) | PI |
| **WhatsApp / Telegram** | Avaliadores | Instruções rápidas, lembretes, suporte | Diário (FASE 2) | PI |
| **Slack / Microsoft Teams** | Suporte TI, Equipe (se houver) | Questões técnicas, colaboração | Sob demanda | PI |
| **Plataforma Web (in-app)** | Avaliadores | Instruções contextuais, FAQ, progresso | Sempre disponível | PI |
| **GitHub Issues** | Comunidade (pós-publicação) | Dúvidas técnicas, bugs | Sob demanda | PI |
| **Twitter / LinkedIn** | Comunidade acadêmica | Divulgação de resultados | 1× (após publicação) | PI |
| **Apresentação Oral** | Banca de defesa | Resultados finais | 1× (defesa) | PI |

##### Calendário de Comunicações Planejadas

| Semana | Evento | Público | Canal | Conteúdo |
|--------|--------|---------|-------|----------|
| **S3** | Aprovação do plano | Orientador + Coordenação | E-mail | Plano aprovado, próximos passos |
| **S5** | Dataset validado | Revisor + Orientador | E-mail | Dataset finalizado, início da preparação técnica |
| **S8** | Convite a avaliadores | Avaliadores potenciais | E-mail | Convite formal + TCLE |
| **S9** | Treinamento | Avaliadores | Zoom + WhatsApp | Instruções detalhadas, calibração |
| **S10** | Go/No-Go | Orientador + Coordenação | Reunião + E-mail | Decisão formal para iniciar |
| **S11-S13** | Coleta em andamento | Orientador | E-mail semanal | Status de progresso |
| **S14-S16** | Avaliação humana | Avaliadores | WhatsApp diário | Lembretes, suporte, progresso |
| **S17** | Coleta concluída | Todos stakeholders | E-mail | Marco atingido, início da análise |
| **S25** | Análise concluída | Orientador + Coordenação | Reunião + E-mail | Resultados preliminares |
| **S40** | Artigo submetido | Orientador + Coordenação | E-mail | Submissão para conferência/periódico |
| **S48** | Dataset publicado | Comunidade acadêmica | GitHub + Twitter | Anúncio público do dataset |

#### 19.3 Pontos de Comunicação Obrigatórios

##### Eventos que Requerem Comunicação Formal

| Evento | Público | Canal | Prazo | Template |
|--------|---------|-------|-------|----------|
| **Aprovação do Plano** | Orientador, Coordenação | E-mail formal | Imediato | `docs/templates/aprovacao_plano.md` |
| **Mudanças Significativas no Escopo** | Orientador, Coordenação, Avaliadores (se impactados) | E-mail + Reunião | Antes da implementação | `docs/templates/change_notification.md` |
| **Atingimento de Marcos** | Orientador | E-mail | Até 24h após | `docs/templates/milestone_report.md` |
| **Problemas Críticos** (atraso >1 semana, estouro orçamentário >20%) | Orientador, Coordenação | E-mail + Telefonema | Imediato | `docs/templates/critical_issue.md` |
| **Adiamento de Prazo** | Todos stakeholders | E-mail | 1 semana antes do prazo original | `docs/templates/prazo_adiado.md` |
| **Cancelamento Parcial/Total** (se necessário) | Todos stakeholders | E-mail formal + Reunião | Imediato | `docs/templates/cancelamento.md` |
| **Início de Cada Fase** | Orientador, Stakeholders relevantes | E-mail | 2 dias antes | `docs/templates/inicio_fase.md` |
| **Conclusão de Cada Fase** | Orientador | E-mail + Reunião | Até 48h após | `docs/templates/conclusao_fase.md` |
| **Submissão de Artigo** | Orientador, Coordenação | E-mail | Imediato | `docs/templates/submissao_artigo.md` |
| **Publicação de Resultados** | Todos stakeholders + Comunidade | E-mail + Redes Sociais | Imediato | `docs/templates/publicacao_resultados.md` |

### Template: Comunicação de Problema Crítico
```markdown
Assunto: [URGENTE] Problema Crítico no Experimento - [Breve Descrição]

Para: [Orientador / Coordenação]  
De: Matheus Vinicius  
Data: [Data]

Natureza do Problema
[Descrição detalhada do problema]

Impacto
- Cronograma: [+X semanas de atraso] / [Nenhum impacto]
- Orçamento: [+X% de custo] / [Nenhum impacto]
- Qualidade: [Compromete objetivo Y] / [Nenhum impacto]

Causa Raiz
[Análise da causa]

Ações Já Tomadas
1. [Ação 1]
2. [Ação 2]

Plano de Contingência Proposto
[Descrição da solução]

Decisões Necessárias
- [Decisão 1] - Prazo: [Data]
- [Decisão 2] - Prazo: [Data]

Próximos Passos
[Lista de ações]

Disponibilidade para reunião urgente: [Horários]
```


#### 20. Critérios de Prontidão para Execução (Definition of Ready)

##### 20.1 Checklist de Prontidão (Itens que devem estar completos)

##### Checklist Mestre - Go/No-Go para Início da Operação

| Categoria | Item | Critério de Aceitação | Verificador | Data |
|-----------|------|----------------------|-------------|------|
| **APROVAÇÕES E CONFORMIDADE** | | | | | |
| A1 | Plano experimental aprovado | Parecer positivo do orientador | Orientador | ___ |
| A2 | Autorização da coordenação | Ofício/e-mail formal de aprovação | Coordenação | ___ |
| A3 | Orçamento aprovado | R$ 5.000 confirmados | Financeiro | ___ |
| A4 | Conformidade LGPD verificada | Parecer do DPO ou jurídico | DPO/Jurídico | ___ |
| A5 | Termos de Serviço das APIs revisados | Confirmação de conformidade para uso em pesquisa | PI | ___ |
| **DATASET E MATERIAIS** | | | | | |
| D1 | Dataset de 250 prompts finalizado | 250 prompts balanceados + classificados | PI | ___ |
| D2 | Revisão independente concluída | Parecer do revisor aprovando dataset | Revisor | ___ |
| D3 | Gabaritos criados | Respostas corretas para ~100 prompts factuais | PI | ___ |
| D4 | Rubrica de avaliação finalizada | Documento aprovado pelo orientador | Orientador | ___ |
| D5 | Guia do Avaliador completo | PDF de 8-10 páginas + exemplos | PI | ___ |
| D6 | TCLE finalizado | Documento aprovado (legal + ético) | PI/Orientador | ___ |
| **INFRAESTRUTURA E FERRAMENTAS** | | | | | |
| I1 | Servidor provisionado | Servidor operacional + acesso SSH | PI/Suporte TI | ___ |
| I2 | Banco de dados configurado | PostgreSQL instalado + tabelas criadas | PI | ___ |
| I3 | APIs de LLMs ativadas | Créditos carregados + testes bem-sucedidos (4/4) | PI | ___ |
| I4 | Scripts de automação funcionais | Testes unitários passando (>95%) | PI | ___ |
| I5 | Plataforma de avaliação operacional | Interface testada + integrada com BD | PI | ___ |
| I6 | Sistema de backup configurado | Backup automático diário funcionando | PI | ___ |
| I7 | Monitoramento/logging implementado | Logs sendo gerados corretamente | PI | ___ |
| **EQUIPE E TREINAMENTO** | | | | | |
| E1 | 3 avaliadores recrutados | 3 especialistas com perfil adequado | PI | ___ |
| E2 | TCLEs assinados | 3 TCLEs com assinatura digital | PI | ___ |
| E3 | Treinamento de avaliadores concluído | Sessão de calibração realizada | PI | ___ |
| E4 | Concordância inter-avaliadores adequada | Kappa ≥0.60 no piloto | PI | ___ |
| E5 | Avaliador reserva identificado | 1 pessoa backup caso desistência | PI | ___ |
| **TESTE PILOTO** | | | | | |
| T1 | Piloto executado | 120 execuções (10 prompts × 4 modelos × 3 rep.) | PI | ___ |
| T2 | Taxa de sucesso técnico | ≥95% de execuções sem erro fatal | PI | ___ |
| T3 | Métricas calculáveis | Todas as 16 métricas computadas com sucesso | PI | ___ |
| T4 | Tempo de execução viável | Tempo médio por resposta <5 min | PI | ___ |
| T5 | Custo dentro do esperado | Custo real ≤110% do estimado | PI | ___ |
| T6 | Plataforma de avaliação testada | 3 avaliadores conseguiram usar sem problemas | PI/Avaliadores | ___ |
| T7 | Problemas críticos resolvidos | Todos os bugs bloqueantes corrigidos | PI | ___ |
| **DOCUMENTAÇÃO** | | | | | |
| DOC1 | Plano experimental versionado | Versão final 1.0 no GitHub | PI | ___ |
| DOC2 | Protocolo operacional escrito | Documento detalhado de execução | PI | ___ |
| DOC3 | Instruções para avaliadores | Guia + FAQ acessíveis na plataforma | PI | ___ |
| DOC4 | Templates prontos | Todos os templates necessários criados | PI | ___ |
| DOC5 | Repositório Git configurado | Estrutura de pastas + README | PI | ___ |
| **COMUNICAÇÃO** | | | | | |
| C1 | Cronograma comunicado | Todos stakeholders informados de datas | PI | ___ |
| C2 | Canais de comunicação estabelecidos | WhatsApp, e-mail, Slack ativos | PI | ___ |
| C3 | Plano de contingência socializado | Todos sabem o que fazer em emergências | PI | ___ |

##### Critérios de Aprovação para Go/No-Go

| Resultado | Critério | Decisão |
|-----------|----------|---------|
| **GO** | ✅ **100% dos itens obrigatórios concluídos** | Iniciar execução na data planejada |
| **GO CONDICIONAL** | 95-99% concluído + nenhum item crítico pendente | Iniciar com restrições / Plano de mitigação |
| **NO-GO** | <95% concluído OU qualquer item crítico pendente | Adiar início até resolver pendências |

**Itens Críticos (não podem estar pendentes):**
- A1, A2, A3 (Aprovações)
- D1, D2 (Dataset validado)
- I3 (APIs funcionais)
- E1, E2 (Avaliadores recrutados e consentimento)
- T2 (Piloto bem-sucedido tecnicamente)


#### 20.2 Aprovações Finais para Iniciar a Operação

##### Processo de Aprovação Final (Go Decision)

##### Etapa 1: Autoverificação pelo PI
**Prazo:** Semana 10, Sexta-feira  
**Responsável:** Pesquisador Principal  
**Ação:** Preencher checklist completo (Seção 20.1) e gerar relatório de prontidão

**Formato do Relatório de Prontidão:**
```markdown
Relatório de Prontidão - Experimento EXP-LLM-DOM-001
Data: [DD/MM/AAAA]
Pesquisador: Matheus Vinicius

Resumo Executivo
- Itens concluídos: [XX/YY] ([Z%])
- Itens críticos pendentes: [Lista ou "Nenhum"]
- Recomendação: [GO / GO CONDICIONAL / NO-GO]

Detalhamento por Categoria
[Tabela do checklist preenchida]

Riscos Residuais
[Lista de riscos ainda presentes após preparação]

Plano de Ação para Pendências
[Se houver itens pendentes não-críticos]

Solicitação de Aprovação
Solicito formalmente aprovação para iniciar a FASE 1 (Coleta Automatizada)
em [DATA].

Assinatura: Matheus Vinicius
Data: [DD/MM/AAAA]
```

##### Etapa 2: Reunião de Go/No-Go
**Prazo:** Semana 10, Segunda-feira (início da semana seguinte)  
**Duração:** 90 minutos  
**Participantes obrigatórios:**
- Pesquisador Principal
- Orientador Acadêmico
- (Opcional) Revisor Independente

**Agenda:**
1. **Apresentação do Relatório de Prontidão** (15 min) - PI
2. **Revisão Item-a-Item do Checklist** (30 min) - PI + Orientador
3. **Discussão de Riscos Residuais** (20 min) - Todos
4. **Avaliação de Contingências** (15 min) - Todos
5. **Decisão Formal de Go/No-Go** (10 min) - Orientador (aprovador final)

#### Etapa 3: Documentação da Decisão
**Responsável:** PI  
**Prazo:** Até 24h após reunião

**Ata de Decisão Go/No-Go:**
```markdown
Ata de Decisão - Go/No-Go para Início da Operação

Data da Reunião: [DD/MM/AAAA]
Participantes: [Lista]

Decisão Final
**GO** / **GO CONDICIONAL** / **NO-GO**

Justificativa
[Explicação da decisão]

Condições para GO CONDICIONAL (se aplicável)
- [Condição 1]
- [Condição 2]

Data de Início Autorizada
[DD/MM/AAAA]

Assinaturas
- Orientador (Aprovador): ___________________  
- Pesquisador Principal: ___________________  
- Data: ___/___/_____

Próximos Passos Imediatos
1. [Ação 1] - [Responsável] - [Prazo]
2. [Ação 2] - [Responsável] - [Prazo]
```
