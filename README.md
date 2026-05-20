# FarmTech Solutions - Fase 3

## Identificação

**Aluno:** Pedro Vinicius Gomes dos Santos  
**RM:** 571446  
**Turma:** 1TIAOB-2026  

---

## 1. Objetivo do Projeto

Este projeto faz parte da **Fase 3 do PBL FarmTech Solutions**.  
O objetivo foi importar para um banco de dados Oracle os dados simulados dos sensores utilizados na Fase 2, permitindo armazenar, consultar e analisar informações de uma fazenda inteligente.

A proposta representa um cenário de **agricultura de precisão**, onde sensores IoT monitoram variáveis do solo e do ambiente para apoiar decisões sobre irrigação.

---

## 2. Contexto da Solução

Na Fase 2, o projeto simulou sensores agrícolas utilizando ESP32, DHT22, LDR e botões para representar:

- Umidade do solo;
- pH do solo;
- Nutrientes NPK;
- Acionamento da irrigação.

Nesta Fase 3, esses dados foram organizados em um arquivo CSV e importados para o banco Oracle utilizando o **Oracle SQL Developer**.

---

## 3. Base de Dados Utilizada

O arquivo utilizado para a importação foi:

`data/sensores_farmtech_v2.csv`

A base foi enriquecida para representar uma fazenda inteligente com múltiplas variáveis agrícolas.

### Campos da base

| Campo | Descrição |
|---|---|
| id | Identificador da leitura |
| data_hora | Data e hora simulada da coleta |
| cultura | Cultura agrícola monitorada |
| umidade | Umidade simulada do solo |
| temperatura | Temperatura ambiente simulada |
| ph | pH simulado do solo |
| npk_n | Presença de Nitrogênio |
| npk_p | Presença de Fósforo |
| npk_k | Presença de Potássio |
| luminosidade | Intensidade luminosa simulada |
| chuva_mm | Volume de chuva em milímetros |
| irrigacao | Status da irrigação |
| status_solo | Classificação do solo |

---

## 4. Lógica dos Dados

A base considera diferentes culturas agrícolas, como tomate, milho e soja.

A irrigação é acionada automaticamente quando a umidade do solo está baixa.

### Regras utilizadas

- **SECO:** umidade abaixo de 35%;
- **IDEAL:** umidade entre 35% e 65%;
- **ÚMIDO:** umidade acima de 65%;
- **IRRIGAÇÃO ON:** umidade abaixo de 40%;
- **IRRIGAÇÃO OFF:** umidade igual ou superior a 40%.

Os valores NPK foram representados da seguinte forma:

- **0:** nível insuficiente;
- **1:** nível adequado.

---

## 5. Processo de Importação no Oracle

O processo foi realizado no **Oracle SQL Developer** seguindo as etapas:

1. Criação da conexão com o banco Oracle da FIAP;
2. Acesso à área de tabelas;
3. Uso da opção **Importar Dados**;
4. Seleção do arquivo `sensores_farmtech_v2.csv`;
5. Criação da tabela `SENSORES_FARMTECH`;
6. Validação da importação por meio de consultas SQL.

---

## 6. Tabela Criada

A tabela criada no Oracle foi:

`SENSORES_FARMTECH`

Ela contém 30 registros simulados de sensores agrícolas.

---

## 7. Consultas SQL Utilizadas

As consultas estão disponíveis no arquivo:

`sql/consultas.sql`

### Consulta geral

```sql
SELECT * FROM SENSORES_FARMTECH;
```

### Leituras com umidade baixa

```sql
SELECT *
FROM SENSORES_FARMTECH
WHERE UMIDADE < 40;
```

### Média de umidade por cultura

```sql
SELECT CULTURA, AVG(UMIDADE) AS MEDIA_UMIDADE
FROM SENSORES_FARMTECH
GROUP BY CULTURA;
```

### Total por status do solo

```sql
SELECT STATUS_SOLO, COUNT(*) AS TOTAL
FROM SENSORES_FARMTECH
GROUP BY STATUS_SOLO;
```

### Irrigação ligada

```sql
SELECT *
FROM SENSORES_FARMTECH
WHERE IRRIGACAO = 'ON';
```

### Média de temperatura por cultura

```sql
SELECT CULTURA, AVG(TEMPERATURA) AS MEDIA_TEMPERATURA
FROM SENSORES_FARMTECH
GROUP BY CULTURA;
```

---

## 8. Evidências do Processo

### Importação realizada com sucesso

![Importação com sucesso](prints/importacao_sucesso.jpeg)

### Consulta geral da tabela

![Select todos](prints/select_todos.jpeg)

### Consulta de umidade baixa

![Umidade baixa](prints/umidade_baixa.jpeg)

### Média de umidade por cultura

![Média de umidade](prints/media_umidade_cultura.jpeg)

### Total por status do solo

![Status do solo](prints/status_solo.jpeg)

### Irrigação acionada

![Irrigação ON](prints/irrigacao_on.jpeg)

---

## 9. Análise dos Resultados

As consultas demonstram que os dados foram importados corretamente e podem ser explorados por meio de SQL.

Foi possível identificar:

- registros com baixa umidade;
- culturas com diferentes médias de umidade;
- distribuição dos registros por status do solo;
- momentos em que a irrigação foi acionada;
- relação entre condição do solo e necessidade de irrigação.

Essas análises são importantes porque permitem que uma fazenda inteligente tome decisões com base em dados armazenados de forma estruturada.

---

## 10. Importância do Banco de Dados

O uso do Oracle permite que os dados dos sensores deixem de existir apenas em arquivos locais e passem a ser armazenados em um banco relacional.

Isso traz benefícios como:

- organização dos dados;
- facilidade de consulta;
- histórico das leituras;
- integração futura com dashboards;
- possibilidade de uso em modelos de Inteligência Artificial.

---

## 11. Vídeo Demonstrativo

Cole aqui o link do vídeo publicado no YouTube como **não listado**:

`COLE_AQUI_O_LINK_DO_VIDEO`

---

## 12. Conclusão

A Fase 3 permitiu consolidar os dados simulados da FarmTech Solutions em um banco de dados Oracle.

Com a importação da tabela `SENSORES_FARMTECH`, foi possível realizar consultas SQL para analisar umidade, irrigação, status do solo e comportamento das culturas agrícolas.

Esse processo é essencial para a evolução do projeto, pois cria uma base organizada para futuras aplicações de dashboards, análise de dados e modelos de IA no agronegócio.
