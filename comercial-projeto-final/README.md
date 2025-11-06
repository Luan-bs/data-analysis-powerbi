# 🧾 Dashboard Comercial – Bpk Vendas

Dashboard desenvolvido no **Power BI** com base em um conjunto de dados simulados contendo **35.762 registros de notas fiscais**.  
O projeto foi criado para analisar o **desempenho comercial da empresa fictícia “Bpk Vendas”**, abrangendo produtos, clientes, vendedores, fornecedores e formas de pagamento.

🔗 **Dashboard público:** [Visualizar no Power BI](https://app.powerbi.com/view?r=eyJrIjoiZWNiYTdmNzEtZWI2MS00MmY2LTg4YzktMTRhYjNiMWE1OTI0IiwidCI6ImRhZGFhOGQzLTIxYWEtNGRjNS05ODBlLTFiZjI0ZWY5Yzc0OCJ9)
---
![Dashboard](https://github.com/Luan-bs/data-analysis-powerbi/blob/main/comercial-projeto-final/dashboard_imagem.png)
## 🎯 Objetivos do Projeto
- Realizar uma **análise exploratória de dados** voltada ao setor comercial.  
- Aplicar técnicas de **limpeza, normalização e modelagem** no Power Query.  
- Criar um **dashboard interativo** com múltiplas páginas e indicadores de desempenho (KPIs).  
- Fornecer insights para decisões estratégicas de **vendas, clientes e produtos**.  

---

## Modelagem Dimensional
O modelo foi estruturado em **Esquema Estrela (Star Schema)**, com a tabela fato **Vendas** conectando-se às dimensões:  
- Produto  
- Cliente  
- Vendedor  
- Fornecedor  
- Categoria  
- Forma de Pagamento  
- Nota  

![Modelo de Dados](https://github.com/Luan-bs/data-analysis-powerbi/blob/main/comercial-projeto-final/modelagem_dados.png)

---

## ⚙️ Ferramentas e Linguagens
- **Power BI Desktop**
- **Power Query**
- **DAX (Data Analysis Expressions)**

---

## Principais Medidas DAX

```DAX
Total_Faturado = SUMX(Vendas, Vendas[QUANTIDADE] * RELATED(Produto[VALOR_UNITARIO]))
Total_vendas = DISTINCTCOUNT(Vendas[IDNOTA])
Total_lucro = SUM(Vendas[LUCRO_TOTAL])
%_Lucro = DIVIDE([Total_lucro], [Total_Faturado])
Ticket_medio = DIVIDE([Total_Faturado], DISTINCTCOUNT(Vendas[IDNOTA]))
Media_itens_por_venda = SUM(Vendas[QUANTIDADE]) / [Total_vendas]
Media_Receita_Top_5_Clientes = AVERAGEX(TOPN(5,VALUES(Cliente[NOME]),[Receita Total]),[Receita Total])
Media_de_itens_venda = SUM(Vendas[QUANTIDADE]) / [Total_vendas]
