# Pipeline ETL para Engajamento de Clientes com IA (Gemini)

Este projeto consiste na implementação de um pipeline de **ETL (Extract, Transform, Load)** desenvolvido em Python. O objetivo principal é simular um sistema automatizado de CRM (Customer Relationship Management) bancário que consome dados de clientes e utiliza Inteligência Artificial Generativa para criar campanhas de marketing altamente personalizadas e segmentadas por tipo de plano.

## 🚀 Contexto do Desafio & Resiliência
No projeto original da Santander Dev Week, a extração e o salvamento dos dados dependiam de uma API externa baseada em Java. Como esse ambiente público de demonstração foi descontinuado, a arquitetura desta solução foi totalmente reestruturada para focar no que mais importa: **o fluxo do dado e a resiliência do pipeline**. 

Substituindo a dependência da API web instável, o script extrai as informações diretamente de uma base de dados em nuvem via Google Sheets (CSV), realiza o enriquecimento inteligente e faz o carregamento local, garantindo que o pipeline funcione de forma autônoma e offline.

---

## 🛠️ Principais Tecnologias e Bibliotecas
* **Python 3**: Linguagem base utilizada para a construção e orquestração de todo o pipeline;
* **Pandas**: Biblioteca de análise de dados usada na etapa de **Extração** para manipulação de DataFrames e leitura direta de arquivos CSV na nuvem;
* **Google GenAI SDK (Nova SDK Oficial)**: Integração de ponta na etapa de **Transformação** utilizando o modelo `gemini-1.5-flash` para geração automatizada de textos em larga escala com baixo custo e alta velocidade;
* **JSON (Built-in)**: Estrutura nativa utilizada na etapa de **Carregamento** para formatação, higienização de strings e gravação do banco de dados final padronizado.

---

## 🔄 O Fluxo do Pipeline (ETL)

### 1. Extração (Extract)
O script conecta-se a uma URL pública que exporta dados estruturados de clientes. O Pandas faz o parse dessas linhas brutas, limpa espaços em branco nos metadados das colunas e carrega as entidades na memória estruturadas em dicionários Python nativos. Uma lista vazia de `news` é acoplada a cada cliente para seguir o padrão do modelo de dados original.

### 2. Transformação (Transform)
Aqui entra a inteligência de negócios orientada por IA. O script analisa o campo `Plano` de cada usuário e toma decisões em tempo de execução:
* **Clientes do Plano Free**: A IA recebe um prompt contextualizado para criar uma abordagem de conversão de vendas persuasiva, destacando vantagens de migrar para o Premium.
* **Clientes do Plano Premium**: A IA adota uma postura de retenção (*churn*) e marketing de indicação, oferecendo recompensas por novos membros indicados (*Member-Get-Member*).

### 3. Carregamento (Load)
Após o enriquecimento dos dados pela IA, os objetos são consolidados e exportados localmente em um arquivo físico estruturado (`campanha_crm_clientes.json`). Esse arquivo final gerado segue rigorosamente o padrão relacional esperado pelo ecossistema do aplicativo e fica pronto para consumo por equipes de marketing ou dashboards analíticos.

---

## 📁 Estrutura dos Dados Gerados
O resultado final do pipeline gera um arquivo JSON estruturado exatamente assim:

```json
[
  {
    "ID": 1,
    "Nome": "Gabriel Silva",
    "Plano": "Premium",
    "news": [
      {
        "icon": "[https://digitalinnovationone.github.io/santander-dev-week-2023-api/icons/credit.svg](https://digitalinnovationone.github.io/santander-dev-week-2023-api/icons/credit.svg)",
        "description": "Gabriel, obrigado por ser Premium! ✨ Explore novas ferramentas hoje e indique um amigo para ganhar 1 mês grátis! 🚀"
      }
    ]
  }
]
```

---

## 💻 Como Executar o Projeto Localmente
Clone este repositório:
```
Bash
	git clone [https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git](https://github.com/SEU-USUARIO/NOME-DO-REPOSITORIO.git)
```
Instale as dependências necessárias:
```
Bash
	pip install pandas google-genai
```
Configure a sua chave de API do Google AI Studio no arquivo principal antes de rodar o script.

## Execute o pipeline:
```
Bash
	python pipeline.py
```
## 🔗 Links Úteis e Referências
Google AI Studio: Plataforma onde a chave de API e os testes com o modelo Gemini foram gerenciados. (https://aistudio.google.com/)

Se achou este projeto interessante para a sua base de estudos de Engenharia de Dados ou pipelines de IA, sinta-se à vontade para dar um ⭐️ no repositório! Conexões e feedbacks sobre boas práticas de arquitetura são sempre muito bem-vindos! 🚀
