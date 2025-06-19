# Projeto - GD

# Arquitetura de Dados: Camadas Bronze, Silver e Gold (Medalhão)

Este repositório implementa uma arquitetura em camadas (conhecida como **"medalhão"**) utilizando Databricks e AWS S3, com o objetivo de estruturar o fluxo de ingestão, tratamento e disponibilização de dados de forma escalável, segura e organizada.

---

## 📌 Estrutura das Camadas

A divisão em camadas ajuda a separar os dados por nível de tratamento, facilitando a manutenção, rastreabilidade e governança.

### 🥉 Camada Bronze – Dados Brutos (Raw Ingestion)

- **Objetivo:** Armazenar os dados exatamente como foram recebidos.
- **Fonte:** Arquivos `.csv` armazenados em bucket S3.
- **Transformações:** Nenhuma ou mínimas (ex: adição de timestamp de carga).
- **Formato:** Delta Lake (`.delta`)
- **Exemplo:**  
  `s3a://grao-direto-mmk/bronze/grain_logistic_shipping`


---

### 🥈 Camada Silver – Dados Tratados

- **Objetivo:** Limpar, padronizar e aplicar regras de negócio básicas.
- **Transformações típicas:**
  - Conversão de tipos de dados
  - Remoção de duplicatas
  - Tratamento de nulos e inconsistências
  - Normalização de campos
- **Formato:** Delta Lake
- **Benefício:** Dados prontos para análise exploratória.

---

### 🥇 Camada Gold – Dados Prontos para Consumo

- **Objetivo:** Dados agregados, otimizados e modelados para consumo por ferramentas de BI, APIs ou relatórios.
- **Transformações típicas:**
  - Cálculo de KPIs
  - Agregações
  - Criação de tabelas fato e dimensão
- **Formato:** Delta Lake
- **Benefício:** Alta performance, dados prontos pra contar história (ou salvar o time de negócio).

---

## 🔗 Tecnologias utilizadas

- **Databricks (na AWS)** – Engine de processamento e gerenciamento de pipelines.
- **AWS S3** – Data Lake para armazenamento escalável.
- **Delta Lake** – Formato de dados transacional (ACID).
- **PySpark** – Transformações e lógica de dados.
- **Unity Catalog** – Governança e controle de acesso (Databricks).

---

## 🚨 Observações

- Os dados das camadas Bronze, Silver e Gold são armazenados em **pastas separadas dentro de um bucket dedicado no S3**.
- O Unity Catalog gerencia os metadados e impede acesso direto a arquivos internos. Toda consulta deve ser feita via tabelas.

---

## 📁 Estrutura no S3

```bash
grao-direto-mmk/
├── raw/
├── bronze/
├── silver/
└── gold/
