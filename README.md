# FIAP - Faculdade de Informática e Administração Paulista

<p align="center">
<img width="600" height="150" alt="Image" src="https://github.com/user-attachments/assets/5746c27f-0276-4eb3-b7da-6f249578a58d" /></a>
</p>

<br>

# 🎓 Graduação ON em Inteligência Artificial  
## 📚  CHALLENGE INTELLIWAY

## 👨‍🎓 Integrantes: 
- <a href="https://www.linkedin.com/in/paulo-pereira-de-souza-junior-mba-msc-0b497825/">Paulo Pereira de Souza Junior</a>

## 👨‍🎓 Apresentacao: 
- <a href="https://youtu.be/6IrO9j_jJ9E">Video Apresentação - YOUTUBE</a>

## 👨‍🎓 Git Hub: 
- <a href="https://github.com/ppsj1983/GS_2026_01">GS 2026 1º Semestre</a>

## 👩🏻‍💻 CO objetivo deste Challenge é desenvolver um serviço de segurança, independente e consumido por API, capaz de detectar tentativas de prompt injection em Português do Brasil e devolver uma decisão clara para o sistema que o consulta

## 👩🏻‍💻 Linha de Pesquisa: Segurança de IA
 
## 👩🏻‍💻 Sprint 1, estruturação da base do projeto, focando na compreensão do problema e das ameaças, no planejamento do dataset em PT-BR, na definição da arquitetura do serviço e na escolha de quais User Stories

## 👩🏻‍💻 Visão do projeto: Serviço Inteligente de Detecção e Prevenção de Prompt Injection
Serviço independente de segurança de IA destinado à identificação de tentativas de *prompt injection*, com foco prioritário em conteúdos escritos em Português do Brasil.
A solução será posicionada como uma camada de proteção entre conteúdos potencialmente não confiáveis e aplicações baseadas em IA.
O objetivo é permitir que sistemas consumidores submetam textos ou conteúdos convertidos em texto para análise e recebam uma decisão estruturada:

- 📌ALLOW: conteúdo considerado suficientemente seguro;
- 📌REVIEW: conteúdo ambíguo ou de risco intermediário;
- 📌BLOCK: forte indicação de tentativa de Prompt Injection.

---

## 🎯 Objetivo

Este trabalho tem como objetivo:

Desenvolver um *prompt injection PT-BR*, independente e consumível por uma API, capaz de analisar conteúdo potencialmente não confiável e retornar uma decisão de segurança baseada no risco identificado.
A arquitetura será desacoplada do sistema consumidor, portanto não dependerá do código, banco ou infraestrutura do EvaGPT.

## 🎯 Objetivo Específicos

O projeto terá os seguintes objetivos:
- 📌construir um dataset especializado em ataques e conteúdos legítimos em PT-BR;
- 📌treinar e comparar um classificador profundo;
- 📌produzir um risk_score entre 0 e 1;
- 📌transformar o score em ALLOW / REVIEW / BLOCK;
- 📌disponibilizar a classificação por API;
- 📌fornecer um portal administrativo;
- 📌suportar imagem e PDF digitalizado por OCR;
- 📌avaliar precision, recall, F1-score, AUC e falsos positivos;
---

## 🧠Classificação do tipo de ameaça

Todo conteúdo analisado é tratado como dado potencialmente não confiável. Entre os ativos a proteger estão prompt base e políticas do agente, dados privados recuperados por RAG, contexto da conversa, informações de sistemas conectados, permissões de ferramentas e integridade das decisões executadas pelo agente. 

*Taxonomia inicial*

A taxonomia sugerida no documento de User Stories inclui, entre outras categorias, conforme imagem a seguir:

<p align="center">
<img width="600" height="470" alt="Image" src="https://github.com/user-attachments/assets/92c60691-9ce4-4260-b611-06370ef5e80b" />
</p>

## 🧠 Escolha de User Story

Nesta etapa, selecionamos todas as *User Stories do P0 como núcleo do projeto*.
Épico A: Motor
P0
- 📌 US-MOT-01: Dataset PT-BR
- 📌 US-MOT-02: Treinamento do modelo
- 📌 US-MOT-03: Avaliação e definição de limiares
- 📌 US-MOT-04: Imagem/PDF + OCR
- 📌 US-API-01: análise;
- 📌 US-API-02: validação e erros;
- 📌 US-ADM-02: dashboard;
- 📌 US-ADM-03: histórico;
- 📌 US-ADM-04: avaliação LLM + revisão humana;
- 📌 US-ADM-05: exportação de dados rotulados.

## 🧠 Estratégia do dataset PT-BR

Nesta etapa vamos combinar datasets públicos traduzidos, exemplos próprios e exemplos sintéticos revisados. Também criação de estrutura para treino, validação e teste, sem repetição de exemplos.

- 📌 Camada 1: dados públicos: Como ponto inicial, utilizaremos dataset deepset/prompt-injections como possível fonte pública. 

- 📌 Camada 2: exemplos originalmente escritos em PT-BR: Tambem trabalharemos na criar de exemplos específicos do contexto brasileiro envolvendo:
```bash
    atendimento
    suporte técnico
    documentos
    procedimentos
    e-mails empresariais
    RAG
    assistentes virtuais
    automações
```
- 📌 Camada 3: ataques sintéticos: Utilizaremos IA Generativa poderá auxiliar na preparação de diferentes variações.

### 📊 Proposta conceitual de Estrutura de Detecção (prompt injections)

O desenvolvimento do motor de detecção será estruturado em três níveis.

- 📌 Nível 1: Baseline Baseada em Regras (Regex)

• Abordagem: Implementação de um fluxo de normalização textual para o português do Brasil (PT-BR), seguido da aplicação de expressões regulares (Regex) para a identificação de padrões e termos suspeitos.
• Objetivo: Funcionar como o primeiro benchmark do projeto. Embora não represente a solução final devido à sua rigidez, estabelecerá a capacidade mínima de deteção do sistema.

- 📌 Nível 2: Baseline Estatística (TF-IDF)

• Abordagem: Criação de um pipeline clássico de Processamento de Linguagem Natural (PLN): extração de características via TF-IDF, seguida pelo treino de um classificador supervisionado tradicional para calcular a probabilidade de ataque.
• Objetivo: Servir como um elo comparativo intermédio, permitindo quantificar com precisão o valor acrescentado e a evolução do modelo de aprendizagem profunda (Deep Learning) face aos métodos estatísticos tradicionais.

- 📌 Nível 3: Modelo de Aprendizagem Profunda (Deep Learning)

• Abordagem: Utilização do modelo pré-treinado de última geração protectai/deberta-v3-base-prompt-injection-v2. Numa fase posterior, o modelo será adaptado especificamente para o contexto de PT-BR através de fine-tuning, recorrendo a técnicas de eficiência paramétrica como LoRA (Low-Rank Adaptation).
• Objetivo: Constituir o estado da arte do motor, maximizando a precisão na deteção de injeções de prompt (prompt injections).




### 📊 Matriz de Comparação dos Modelos

A tabela abaixo detalha a configuração técnica e o propósito de cada iteração dentro do fluxo experimental:

| Fase | Abordagem Técnica | Inputs / Pré-processamento | Papel no Projeto |
| :--- | :--- | :--- | :--- |
| **1. Regex** | Expressões Regulares estruturadas | Normalização textual básica (PT-BR) | **Baseline 1:** Estabelece o limiar mínimo de segurança e a taxa base de deteção. |
| **2. TF-IDF** | Matriz de frequência + Classificador Supervisionado | Tokenização tradicional de PLN | **Baseline 2:** Quantifica o ganho obtido por métodos estatísticos clássicos. |
| **3. DeBERTa v2** | `protectai/deberta-v3-base-prompt-injection-v2` | Tokenizador nativo do modelo | **Modelo Base:** Demonstra o salto de desempenho através de *Deep Learning* (*zero-shot*). |
| **4. DeBERTa + LoRA** | Fine-tuning com Low-Rank Adaptation (LoRA) | Dataset especializado em PT-BR | **Modelo Final:** Estado da arte do motor, otimizado para as nuances do português. |

```bash
    A [Entrada de Conteúdo] --> B [Normalização/OCR]
    B --> C [Detecção]
    C --> D [Risk Score]
    D --> E {ALLOW / REVIEW / BLOCK}
    E --> F [Auditoria]
    F --> G [Avaliação]
    G --> H [Feedback]
    H --> I [Retreino]
    I --> A
```
## 🧠 Tabelas e Banco de Dados
---

Imagem abaixo demonstra a estrutura do banco de dados, neste projeto, utilizamos 6 tabelas
<p align="center">
<img width="318" height="266" alt="Image" src="https://github.com/user-attachments/assets/50838172-38b4-49d8-b5fb-3282a252fb33" /></a>
</p>

*DADOS_CLIMA_GS_206_S1:* Estrutura contendo dados climáticos brutos extraídos diretamente das bases do INMET. Serve como fonte primária para as análises de monitoramento.

<p align="center">
<img width="753" height="510" alt="Image" src="https://github.com/user-attachments/assets/6dd46d1a-4be1-40d5-b001-818982be1484" /></a>
</p>

*DF_CADASTRO_ESTACOES:* Catálogo estruturado de 597 estações meteorológicas de medição. Inclui metadados como posição geográfica, altitude e distância em relação à Linha do Equador.

<p align="center">
<img width="722" height="292" alt="Image" src="https://github.com/user-attachments/assets/fdf7b7a3-376b-4462-8c0a-487f97f38b3c" /></a>
</p>

<p align="center">
<img width="1295" height="555" alt="Image" src="https://github.com/user-attachments/assets/d7df3923-8161-48aa-be53-6944dc8a4525" /></a>
</p>

*DADOS_NOAA:* Consolidação das temperaturas da superfície do oceano Pacífico, utilizada para a identificação e classificação de períodos e ciclos climáticos (El Niño, La Niña e Neutro).

<p align="center">
<img width="769" height="263" alt="Image" src="https://github.com/user-attachments/assets/87ea4157-f3cf-4a95-b726-9c8b2bac5177" /></a>
</p>

*HISTORICO_CHUVA:* Série histórica de precipitação climática (em milímetros), com agregação mensal e estruturada pela coluna ANO_MES.

*HISTORICO_TEMPERATURA:* Série histórica de temperaturas, apresentada em médias mensais, categorizada e identificada pela coluna ANO_MES.

*HISTORICO_UMIDADE:* Série histórica de Umidade Relativa do Ar, apresentada em médias mensais e estruturada pela coluna ANO_MES.

*HISTORICO_VENTOS:* Série histórica de medições de vento, com visão de média mensal e estruturada pela coluna ANO_MES.

<p align="center">
<img width="254" height="428" alt="Image" src="https://github.com/user-attachments/assets/24ddeb23-cb5c-47f3-8906-9227ecda07e8" /></a>
</p>


## 🧠 Processamento de Informações
---
No arquivo *DADOS_INMET_NOAA.ipynb* realizamos todo o processamento das informações e atualização das tabelas, durante cada etapa, inserimos testes para monitoramento de cada passo, conforme demonstrado a seguir

*DADOS_CLIMA_GS_206_S1:* Processamento de arquivos CSV's extraidos de <a href="https://bdmep.inmet.gov.br/">Banco de Dados Meteorológicos do INMET </a>, nesta etapa foram processados 10046

<p align="center">
<img width="766" height="673" alt="Image" src="https://github.com/user-attachments/assets/e3026f43-d615-45bf-90d5-a082cb90e71d" /></a>
</p>

Após processamento dos CSV's, criamos uma tabela auxiliar para armazenar todas as informações climatologicas, com resumos obtidos a partir da tabela *DADOS_CLIMA_GS_206_S1*
<p align="center">
<img width="850" height="784" alt="Image" src="https://github.com/user-attachments/assets/79e7c99f-0800-4c21-a956-7c6cf85cfef9" /></a>
</p>

*DF_CADASTRO_ESTACOES:* Tambem inserimos uma etapa para processamento das estações, gerando um resumo com registros cadastrais de todos os terminais metereologicos.
<p align="center">
<img width="996" height="631" alt="Image" src="https://github.com/user-attachments/assets/46b21e77-98c7-4aa4-9242-a842908d3085" /></a>
</p>
Etapa de carga da tabela DF_CADASTRO_ESTACOES no servidor FIAP
<p align="center">
<img width="861" height="691" alt="Image" src="https://github.com/user-attachments/assets/315e3629-0027-4cfc-b93a-a4782f40555a" /></a>
</p>

*DADOS_NOAA:* Etapa de importação de dados do site <a href="https://www.cpc.ncep.noaa.gov/">NOAA Climate Prediction Center</a>, processamento das informações e armazenamento no servidor FIAP
<p align="center">
<img width="785" height="482" alt="Image" src="https://github.com/user-attachments/assets/c3b912c2-7206-4c98-9683-d7f1410f3061" /></a>
</p>

As tabelas *HISTORICO_CHUVA, HISTORICO_TEMPERATURA, HISTORICO_UMIDADE e HISTORICO_VENTOS*, tambem são processadas individualmentes, reduzindo a quantidade de registros para utilização nos modelos preditivos
<p align="center">
<img width="797" height="640" alt="Image" src="https://github.com/user-attachments/assets/588c069e-95fb-4c96-b148-8bbebd15c6f7" /></a>
</p>

## 🧠 Algoritmo de Machine Learning

Utilizamos o algoritmo Random Forest Classifier para a realização de previsões climatológicas. Este método foi aplicado para calcular as previsões climáticas considerando variáveis contínuas (Volume de Chuvas, Temperatura, Velocidade do Vento e Humidade) e, complementarmente, para a modelação binomial da probabilidade de ocorrência de chuva para um determinado mês.

<p align="center">
<img width="1074" height="787" alt="Image" src="https://github.com/user-attachments/assets/82b656f4-c084-4f37-88c3-ea366f0615a9" /></a>
</p>

## 🧠 Painel Streamlit

No painel Streamlit foi adicionando um menu para seleção dos parametros simulação climatologica 

<p align="center">
<img width="948" height="440" alt="Image" src="https://github.com/user-attachments/assets/9c1eef19-142e-4d12-bdb6-3e62dca43b0f" /></a>
</p>


Tambem adicionamos uma função para exportação de mapas html
<p align="center">
<img width="1149" height="689" alt="Image" src="https://github.com/user-attachments/assets/c593f238-9d75-4764-988e-13048936e898" /></a>
</p>



## 🧠 Resultados Obtidos 

No teste de validação, a taxa de acerto global do algoritmo fixou-se em 77,75% para a previsão do cenário binomial de chuva, comprovando a robustez do modelo preditivo adaptado

<p align="center">
<img width="1163" height="257" alt="Image" src="https://github.com/user-attachments/assets/fbcdbed2-582a-42c8-963b-4342f30fc88a" /></a>
</p>

A análise climática baseada nos dados do El Niño para junho confirma que a região Sul do Brasil concentra os maiores índices pluviométricos. Importa destacar que as projeções do algoritmo estão alinhadas e convergem com os comportamentos históricos de precipitação locais.

<p align="center">
<img width="1377" height="669" alt="Image" src="https://github.com/user-attachments/assets/83657562-928d-4de3-8229-8bdcafe06809" /></a>
</p>

Através da análise da distribuição espacial do mapa, evidencia-se uma elevada concentração pluviométrica distribuída por todos os estados da região Sul.

<p align="center">
<img width="1193" height="876" alt="Image" src="https://github.com/user-attachments/assets/87818c2f-1d79-43a6-8e26-969ac23931e4" /></a>
</p>

A ferramenta geoespacial permite a análise simultânea de três variáveis preditivas: o volume estimado de precipitação (mm), a temperatura (°C) e a probabilidade percentual de ocorrência de chuva

<p align="center">
<img width="1413" height="857" alt="Image" src="https://github.com/user-attachments/assets/c989567d-36a7-4c2d-a6b4-855e6f27d8b6" /></a>
</p>





## 📋 Licença


https://conexaosafra.com/

https://www.bbc.com/portuguese/resources/idt-54f4e985-a7fb-48b2-8246-f3be0d699402

http://enos.cptec.inpe.br/
