# Análise de Sinistros de Seguros Automotivos 🚗

## Descrição do Projeto

Este projeto realiza uma análise completa de dados de sinistros de seguros automotivos. O objetivo é identificar padrões, riscos e oportunidades de negócio através da auditoria, tratamento e segmentação dos dados.

**Total de Registros:** 10.000 clientes
**Base de Dados:** Car_Insurance_Claim.csv

---

## 📋 Estrutura do Projeto

```
TesteTecnico/
├── README.md
├── analise_car_insurance/
│   ├── TesteTecnico.ipynb
│   └── data/
│       └── Car_Insurance_Claim.csv
```

---

## 🔧 Como Executar a Análise

### Pré-requisitos
```bash
pip install pandas numpy matplotlib seaborn
```

### Executar no Jupyter
1. Abra `TesteTecnico.ipynb` no Jupyter Notebook, Jupyter Lab ou Google Colab
2. Execute todas as células sequencialmente
3. Os gráficos e análises aparecem inline no notebook

### Estrutura das Células
O notebook está organizado em seções com títulos em Markdown seguidas de células Python:
- **Importação de Bibliotecas**: Setup inicial
- **Carregamento de Dados**: Leitura do CSV
- **Auditoria**: Verificação de qualidade
- **Tratamento**: Imputação de valores faltantes
- **KPIs**: Cálculo de indicadores
- **Segmentação**: Análises por grupos
- **Relatórios**: Interpretações e insights

---

## 📊 Variáveis da Base de Dados

| Campo | Descrição | Tipo |
|-------|-----------|------|
| ID | Identificador único do cliente | Numérico |
| AGE | Faixa etária | Categórico |
| GENDER | Gênero | Categórico |
| RACE | Raça/Etnia | Categórico |
| DRIVING_EXPERIENCE | Anos de experiência na direção | Categórico |
| EDUCATION | Nível de educação | Categórico |
| INCOME | Classe socioeconômica | Categórico |
| CREDIT_SCORE | Score de crédito (0-1) | Numérico |
| VEHICLE_OWNERSHIP | Proprietário do veículo | Binário |
| VEHICLE_YEAR | Período do ano do veículo | Categórico |
| MARRIED | Estado marital | Binário |
| CHILDREN | Possui filhos | Binário |
| POSTAL_CODE | Código postal | Categórico |
| ANNUAL_MILEAGE | Quilometragem anual | Numérico |
| VEHICLE_TYPE | Tipo de veículo | Categórico |
| SPEEDING_VIOLATIONS | Número de infrações por excesso de velocidade | Numérico |
| DUIS | Número de registros dirigindo sob efeito | Numérico |
| PAST_ACCIDENTS | Número de acidentes passados | Numérico |
| OUTCOME | Acionou sinistro? (1=Sim, 0=Não) | Binário |

---

## 💻 Fases da Análise

### 1. **AUDITORIA DOS DADOS** 🔍

Nesta fase, foi realizada uma verificação completa da qualidade e integridade dos dados para identificar possíveis problemas antes da análise.

#### Bibliotecas Utilizadas
- `pandas` - Manipulação e análise de dados
- `numpy` - Operações numéricas
- `matplotlib` - Visualização de gráficos
- `seaborn` - Visualizações estatísticas avançadas

#### Verificações Realizadas

**1. Integridade dos Dados**
- ✅ Não foram identificados erros de tipagem relevantes
- Campos `MARRIED` e `CHILDREN` são variáveis binárias (valores 0 ou 1)
- **Recomendação:** Conversão para tipo booleano para melhorar performance e clareza semântica

**2. Duplicidade de Dados**
- ✅ Nenhum registro duplicado encontrado
- Chaves primárias estão corretamente ajustadas
- Integridade estrutural preservada

**3. Análise de Outliers**

Foram identificados outliers em diversos campos:

| Campo | Observação |
|-------|-----------|
| **CREDIT_SCORE** | Quantidade considerável de valores abaixo do primeiro quartil - requer análise detalhada |
| **POSTAL_CODE** | Valor divergente pode indicar erro de digitação ou registro inconsistente |
| **ANNUAL_MILEAGE** | Alguns poucos valores acima do terceiro quartil, dentro do comportamento esperado |
| **SPEEDING_VIOLATIONS, DUIS, PAST_ACCIDENTS** | Devem ser monitorados com atenção; valores acima de 0 indicam maior probabilidade de risco |

**4. Dados Faltantes (Missing Values)**
- `CREDIT_SCORE`: ~10% dos registros
- `ANNUAL_MILEAGE`: ~10% dos registros
- Total: aproximadamente 10% dos dados necessitavam tratamento

**5. Análise de Sinistros**
- 31,33% dos clientes acionaram sinistro
- 68,67% não acionaram sinistro
- **Conclusão:** Aproximadamente 1 a cada 3 clientes acionou sinistro

---

### 2. **TRATAMENTO DOS DADOS** 🧠

Nesta fase, os dados incompletos foram processados para permitir análises mais robustas.

#### Estratégia Adotada

**Imputação de Valores Ausentes**

Remover 10% dos dados seria inviável pois comprometeria a representatividade da amostra. Portanto:

- **Método:** Imputação pela **mediana**
- **Campos Tratados:**
  - `CREDIT_SCORE`: preenchido com a mediana
  - `ANNUAL_MILEAGE`: preenchido com a mediana

**Vantagens da Mediana:**
- Resistente a outliers
- Preserva a distribuição dos dados
- Apropriada para variáveis numéricas

**Flags de Falta de Dados**

Foram criadas flags para rastrear registros com dados imputados:
- `MISSING_CREDIT_SCORE`: indica registros onde o score foi imputado
- `MISSING_ANNUAL_MILEAGE`: indica registros onde a quilometragem foi imputada

Isso permite análises futuras que considerem a qualidade original dos dados.

---

### 3. **KPIs - INDICADORES-CHAVE DE DESEMPENHO** 📊

| Métrica | Valor |
|---------|-------|
| **Total de Clientes** | 10.000 |
| **Total de Sinistros** | 3.133 |
| **Taxa de Sinistros** | 31,33% |

Estes KPIs servem como baseline para avaliação de performance e comparações futuras.

---

### 4. **SEGMENTAÇÃO E ANÁLISE DE PADRÕES** 📈

Foram realizadas análises detalhadas para identificar quais grupos demográficos e comportamentais apresentam maior incidência de sinistros.

#### 4.1 **Faixa Etária (AGE)**

**Padrão Identificado:** Incidência significativamente maior em clientes mais jovens

- **16-25 anos:** Taxa mais alta de sinistros
- **26-39 anos:** Redução moderada
- **40-64 anos:** Menor incidência
- **65+ anos:** Redução contínua com a idade

**Interpretação:** Motoristas menos experientes tendem a acionar mais sinistros, possivelmente devido a:
- Menor tempo de habilitação
- Menor maturidade na condução
- Maior exposição a comportamentos de risco

---

#### 4.2 **Experiência de Direção (DRIVING_EXPERIENCE)**

**Padrão Identificado:** Forte correlação entre experiência e segurança

- Menos experiência → Maior taxa de sinistros
- Mais experiência → Menor taxa de sinistros

---

#### 4.3 **Tipo de Veículo (VEHICLE_TYPE)**

**Padrão Identificado:** Diferenças significativas entre tipos

- **Sedan:** Taxa moderada de sinistros
- **Sports Car:** Comportamento diferenciado (possível correlação com condutor)

---

#### 4.4 **Ano do Veículo (VEHICLE_YEAR)**

**Padrão Identificado:** Veículos antigos apresentam risco muito maior

- **Antigos (before 2015):** Taxa elevada de sinistros
- **Novos (after 2015):** Taxa consideravelmente menor

**Possíveis Causas:**
- Maior desgaste mecânico
- Menor presença de tecnologias de segurança modernas
- Custos maiores de manutenção preventiva
- Componentes estruturais menos desenvolvidos

---

#### 4.5 **Classe Socioeconômica (INCOME)**

**Padrão Identificado:** Mayor risco em classes econômicas mais baixas

**Ordem de Risco (maior para menor):**
1. Pobreza (Poverty)
2. Classe Trabalhadora (Working Class)
3. Classe Média (Middle Class)
4. Classe Alta (Upper Class)

**Possíveis Explicações:**
- Condições de uso mais intensivas do veículo
- Maior exposição a áreas de risco
- Negligência com manutenção preventiva por questões de custo
- Diferenças socioeconômicas correlacionadas com comportamentos de risco

---

#### 4.6 **Score de Crédito (CREDIT_SCORE)**

**Padrão Identificado:** Relação clara e inversa com sinistros

- **Score Muito Baixo:** Risco significativamente maior
- **Score Progressivamente Maior:** Redução contínua do risco

**Interpretação:** Score de crédito é um indicador robusto de confiabilidade e responsabilidade, aspectos que também se refletem na condução.

---

#### 4.7 **Quilometragem Anual (ANNUAL_MILEAGE)**

**Padrão Identificado:** Incidência aumenta com maior quilometragem

- **Até 13.000 milhas/ano:** Risco moderado
- **Acima de 13.000 milhas/ano:** Risco aumentado significativamente

**Interpretação:** Maior exposição ao trânsito = maior probabilidade de sinistros. Relação de causa-efeito lógica e esperada.

---

#### 4.8 **Infrações por Excesso de Velocidade (SPEEDING_VIOLATIONS)** ⚠️

**Padrão Identificado:** CONTRAINTUITIVO

- **Sem infrações:** Taxa MAIOR de sinistros
- **Com infrações:** Taxa MENOR de sinistros

**Hipóteses para Explicar este Padrão:**
1. Sinistros de menor gravidade (ex: troca de pneus, pequenos danos) podem ser mais frequentes entre condutores cautelosos
2. Possível subnotificação de infrações na base de dados
3. Perfil de condutor mais cauteloso, porém mais propenso a acionar coberturas menores

**⚠️ Recomendação:** Análise aprofundada necessária para validação desta hipótese

---

#### 4.9 **Dirigindo Sob Efeito de Substâncias (DUIS)** ⚠️

**Padrão Identificado:** INESPERADO

- **Sem registros de DUI:** Quantidade de sinistros similar a clientes com múltiplas ocorrências

**Hipóteses:**
1. Problemas de qualidade de dados
2. Diferença entre "ocorrências registradas" e "sinistros reais"
3. Possível subnotificação nos registros

**⚠️ Recomendação:** Investigação adicional essencial

---

#### 4.10 **Histórico de Acidentes (PAST_ACCIDENTS)** ⚠️

**Padrão Identificado:** ALTAMENTE CONTRAINTUITIVO

- **Sem acidentes registrados:** Taxa MUITO ALTA de sinistros
- **Com múltiplos acidentes:** Taxa MENOR de sinistros

**⚠️ ALERTA:** Este padrão sugere possíveis problemas de qualidade de dados

**Hipóteses para Investigação:**
1. Diferença semântica entre "acidente registrado" e "sinistro acionado"
2. Clientes novos (sem histórico) podem estar gerando muitos sinistros menores
3. Possível erro de classificação ou consistência de dados
4. Variáveis com definições diferentes entre bases de dados

**⚠️ Recomendação CRÍTICA:** Uma auditoria técnica completa é necessária antes de usar esta variável em modelos preditivos

---

## 💡 Implicações de Negócio e Insights Estratégicos

### 🎯 1. **Precificação Baseada em Risco**

Com base na análise de segmentação, recomenda-se:

- **Jovens (16-25 anos):** Precificação diferenciada mais cara ou franquias mais altas
- **Veículos Antigos:** Ajuste de prêmio para cima
- **Alta Quilometragem (>13.000 milhas/ano):** Fator importante no cálculo atuarial
- **Score de Crédito Baixo:** Fortemente correlacionado com risco - deve ter papel relevante
- **Classe Socioeconômica Baixa:** Indicador complementar importante de risco

### 🔍 2. **Necessidade Urgente de Auditoria e Validação**

Os seguintes pontos **EXIGEM** revisão técnica antes de decisões críticas:

✋ **Clientes sem histórico de acidente acionando muito mais sinistros**
- Por quê? Precisa de investigação

✋ **Relação inesperada entre ausência de infrações de velocidade e maior acionamento**
- Contradição com expectativas teóricas

✋ **DUIs não impactando significativamente o risco**
- Esperado que tivesse correlação forte

✋ **Padrão inverso em variáveis de violação**
- Sugere possíveis problemas de classificação ou definição inconsistente

**Possíveis Causas:**
- Problemas de tipagem/classificação nos dados
- Inconsistência no registro histórico
- Variáveis com definições diferentes entre múltiplas fontes
- Subnotificação de alguns tipos de infrações

### 🚀 3. **Oportunidades Estratégicas**

- **Programas de Educação:** Criar iniciativas de direção defensiva direcionadas para jovens
- **Incentivos de Manutenção:** Oferecer benefícios para proprietários de veículos antigos que mantêm manutenção preventiva
- **Parcerias com Oficinas:** Verificar condição de veículos como critério para redução de prêmios
- **Programa de Fidelidade:** Recompensar clientes de baixo risco com prêmios reduzidos

---

## 📝 Conclusões Finais

### ✅ Validado
- Dados em geral íntegros e sem duplicação
- Padrões lógicos em idade, experiência e ano do veículo
- Correlação clara entre score de crédito e risco

### ⚠️ Requere Atenção
- Comportamento inesperado em variáveis de violação e acidentes
- Aproximadamente 10% de valores faltantes tratados por imputação
- Alguns outliers que podem ou não ser válidos

### 🎯 Próximos Passos Recomendados
1. Auditoria técnica das variáveis contraintuitivas
2. Validação com especialistas de negócio
3. Desenvolvimento de modelo preditivo com variáveis validadas
4. Testes A/B em estratégias de precificação baseadas em risco
5. Investigação dos padrões inesperados com dados históricos adicionais

---

## 👤 Autor
**José Luis Tavares** - Análise Técnica de Dados

---

**Última Atualização:** Fevereiro de 2026
