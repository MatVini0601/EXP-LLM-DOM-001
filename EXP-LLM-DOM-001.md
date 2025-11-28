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
