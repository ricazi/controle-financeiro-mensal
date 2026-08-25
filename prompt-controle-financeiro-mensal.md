# Prompt — Controle Financeiro Pessoal Mensal (Ricardo)

> Este arquivo é a "receita" reutilizável para montar a planilha mensal.
> Cole este prompt inteiro no Claude (junto com os extratos do mês) para gerar a planilha atualizada.

## O que enviar todo mês
1. Extrato Banrisul (conta corrente) — período completo do mês
2. Extrato Sicredi (conta corrente 20338-9) — período completo do mês
3. Extrato Nubank (conta corrente) — período completo do mês
4. Fatura do cartão Sicredi (Mastercard Black, conta de Scheila Stroschein) — a fatura cujo *conteúdo* cobre o mês em questão (normalmente a fatura com vencimento no mês seguinte)
5. Fatura do cartão Nubank — a fatura cujo *conteúdo* cobre o mês em questão (mesma lógica acima)
6. Extrato de Custódia Nubank (investimentos) — posição mais recente
7. Print do app Sicredi > Investimentos (Sicredinvest CDI100) — posição mais recente
8. Print do app Banricap > Parcelas pagas — mês em questão
9. Qualquer gasto em dinheiro/espécie que não passou pelos bancos (avisar por escrito)

## Instruções para o Claude

Você vai montar um controle financeiro pessoal mensal para o Ricardo (contador, Santa Rosa/RS), separando o que é fluxo de caixa pessoal real do que é ruído (repasses, pass-through, pagamento de fatura já contado, transferências entre contas próprias).

### Regras de exclusão (não contar como receita nem despesa pessoal)
- Transferências entre contas do próprio Ricardo (ex: Sicredi ↔ Nubank ↔ Banrisul).
- Pagamento da fatura do cartão de crédito feito a partir da conta corrente — **os gastos do cartão já entram detalhados item a item**, então o pagamento da fatura em si (débito na conta ou PIX para a Scheila cobrindo a fatura Sicredi) é excluído para não duplicar.
- Repasses onde o Ricardo só serve de intermediário (dinheiro que entra e sai no mesmo valor para outra pessoa, ex: aluguel recebido para repassar a terceiros, valores que são da Scheila passando pela conta PJ/PF dele).
- Reembolsos de despesas já feitas pelo escritório (ex: presente comprado e depois ressarcido pela PJ).
- Acertos pessoais pontuais sem relação com o mês corrente (ex: ajuste de IR entre familiares).

### Cartão de crédito
- **Sicredi**: considerar apenas as linhas com cartão final **8219** (nome "Ricardo Zimmermann"). Ignorar linhas do cartão 8912 e das linhas sem número de cartão (são da Scheila).
- **Nubank**: o cartão é 100% do Ricardo, considerar tudo.
- Usar a fatura cujas transações (mesmo com datas variadas por causa de parcelas antigas) representam a cobrança **daquele mês** — isso normalmente é a fatura com vencimento no início do mês seguinte.

### Receitas
- Retiradas do escritório (pró-labore/lucros) — perguntar ao Ricardo se algum valor recebido da PJ é repasse para a Scheila ou receita própria, caso não fique óbvio.
- "Rendimentos diversos": PIX recebidos de pessoas físicas/jurídicas sem relação de repasse óbvia — perguntar item a item se for a primeira vez, reaproveitar classificação de meses anteriores para contrapartes recorrentes.
- Cashback / Nota Fiscal Gaúcha etc.

### Despesas — peça para o Ricardo caracterizar
Assim como fizemos em julho/2026: monte uma lista dos lançamentos de PIX/débito na conta corrente cuja contraparte não é óbvia (não é convênio de utilidade, não é fatura de cartão, não é família/escritório já identificado) e peça para o Ricardo preencher o "o que é isso" antes de categorizar — ele pode te devolver uma planilha simples (Data, Banco, Contraparte, Valor, O que) como fez em julho.

### Investimentos
- Nubank (Caixinha/RDB, Fundo RF, CDB) e Sicredi Investimentos: como normalmente só temos a foto do dia (custódia/posição atual), estimar o rendimento do mês aplicando a taxa CDI mensal vigente sobre o saldo (buscar a taxa CDI atual do mês via web search). Deixar claro que é estimativa.
- Se em algum mês houver o saldo do início E do fim do mês, calcular o rendimento real por diferença em vez de estimar.
- Banrisul CDB: o extrato já traz o rendimento diário ("REND CDB AUT") — somar os valores do mês, é real, não estimado.
- Banricap: registrar a parcela paga no mês como aporte (categoria "Investimento/Poupança", não despesa).
- Poupança para terceiros (ex: valores que vão para a poupança da Laura): categoria separada, não é despesa de consumo nem investimento do Ricardo.

### Estrutura da planilha (.xlsx) a entregar
4 abas:
1. **Resumo** — Total Receitas, Total Despesas, Saldo do mês (fórmulas), tabela de despesas por categoria com coluna "% do Total", gráfico de pizza das despesas por categoria, tabela de receitas por categoria, seção de investimentos (posição total + rendimento estimado/real).
2. **Lançamentos** — todas as movimentações incluídas: Data | Origem | Descrição | Categoria | Valor | Tipo (fórmula). Esta aba alimenta o Resumo via SUMIFS — categorias podem ser editadas aqui e o Resumo recalcula sozinho.
3. **Investimentos** — Instituição | Produto | Posição (texto) | Fonte/Data | Saldo Bruto | Rendimento Real | Rendimento Estimado, com nota explicando a metodologia de estimativa.
4. **Não Computado** — toda transação excluída, com data, origem, descrição, valor e motivo da exclusão — para o Ricardo auditar as exclusões.

Regras técnicas: usar `openpyxl`, fórmulas de verdade (nunca valor fixo), fonte Arial, moeda com negativo em vermelho, rodar `recalc.py` no final e garantir zero erros antes de entregar.

### Nome do arquivo
`MMAAAA_controle_financeiro.xlsx` (ex: `082026_controle_financeiro.xlsx` para agosto/2026)

---
*Histórico: metodologia consolidada a partir do controle de julho/2026. Ajuste este arquivo sempre que uma nova regra de categorização for definida, para manter a rotina mensal consistente.*
