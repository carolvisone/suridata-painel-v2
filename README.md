# Suridata · Performance Comercial 2026

Painel gerencial do time comercial da Suridata. Mostra geração de demanda, avanço do pipeline, contratos fechados, receita e previsibilidade de vendas de 2026, lendo os dados ao vivo da planilha comercial.

Este repositório é a versão nova, em teste. O painel atual continua no repositório `suridata-painel` e não é afetado.

## Como funciona

- Um único arquivo, `index.html`, feito em React (carregado via CDN, sem etapa de build).
- A cada abertura, o painel lê as abas da planilha "Base de Dados - Acompanhamento Comercial" pelo Google Sheets.
- Nenhum dado fica gravado no repositório. Para atualizar os números, basta atualizar a planilha e clicar em "Atualizar dados" no painel.
- O Vercel publica automaticamente a cada commit na branch `main`.

## Fonte de dados

Planilha: Base de Dados - Acompanhamento Comercial (Google Sheets).
Requisito: compartilhamento como "Qualquer pessoa com o link pode ver".

Abas lidas:

- **Agendamentos**: reuniões, no-show, nível ICP e origem.
- **Atividades Semanais**: tentativas, leads, conectados e agendamentos gerados pelo time SDR.
- **Contratos**: contratos fechados, MRR, setup, implantação e competência.
- **Cancelamentos**: churn.
- **Pipeline**: posição atual das oportunidades.
- **Histórico de Etapas** (opcional): uma linha por mudança de etapa. Libera propostas por mês, avanços, pipeline no fim de cada mês e safra completa.
- **Metas** (opcional): metas mensais de reuniões, contratos e MRR. Libera o card de meta versus realizado.

Os nomes das abas e das colunas precisam ser mantidos. Colunas novas podem ser adicionadas no fim sem quebrar nada.

## O que o painel mostra

- **Visão executiva**: agendamentos, reuniões realizadas, oportunidades qualificadas, propostas, contratos e receita fechada. Também traz o funil do período, pipeline ativo, forecast, meta versus realizado, evolução mensal e oportunidades que exigem acompanhamento.
- **Geração de demanda**: resultado do time SDR consolidado, sem separação por pessoa.
- **Fechamentos e receita**: contratos do período, ticket médio, ciclo de vendas, ciclo de implantação, novo MRR faturado e churn.
- **Pipeline**: oportunidades por etapa e tabela detalhada.
- **Base de dados**: data do último registro de cada aba, pontos de atenção na planilha e definição de cada indicador.

Filtros disponíveis: mês, trimestre, acumulado no ano, ano todo e intervalo personalizado, com comparação com o período anterior. Há duas visões:

- **Por atividade** (padrão): o que aconteceu dentro do período.
- **Por safra**: corretoras com a 1ª reunião no período e o que aconteceu com elas depois.

## Regras de cálculo

- Apenas registros de 2026. Nenhum número é estimado.
- Período sem registro na planilha aparece como "Sem registro", nunca como zero.
- Quando a base não tem a informação, o painel mostra "Dados insuficientes".
- Oportunidade qualificada: reunião realizada com Nível ICP 2 ou 3.
- Contrato fechado: cada combinação de corretora e data de contrato conta como um negócio.
- Receita fechada: MRR das apólices. Setup e serviços aparecem separados.
- Forecast (MRR potencial): Short List, Aceite Verbal e Contrato. Simulador e Proposta ficam só como referência.
- Ciclo de vendas: dias entre a 1ª reunião realizada e a data do contrato.

## Como atualizar o painel

1. Edite o `index.html` (ou peça a nova versão ao Claude no projeto "Indicadores Comerciais").
2. No GitHub: Add file → Upload files → envie o `index.html` novo → Commit changes.
3. O Vercel publica sozinho em cerca de um minuto.

## Configuração no Vercel

- Framework Preset: Other
- Build Command: vazio
- Output Directory: vazio (raiz do repositório)

## Configurações dentro do código

No início do script do `index.html`, o bloco `CONFIG` define:

- `SHEET_ID`: identificador da planilha.
- `ANO`: ano analisado (2026).
- `ABAS`: nomes das abas lidas.
- `DIAS_ALERTA`: dias sem movimentação para marcar uma oportunidade como parada (padrão 14).

## Responsável

Ana Carolina Visone · Head de Marketing e Novos Negócios · Suridata
