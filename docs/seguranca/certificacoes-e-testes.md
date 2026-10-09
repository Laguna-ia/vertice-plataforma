# Certificações, testes de segurança e gestão de vulnerabilidades

| Campo | Valor |
|---|---|
| Responsável | Paulo Nogueira (Segurança) |
| Versão do documento | 1.5 |
| Plataforma de referência | v4.11.2 |
| Data de revisão | 18/09/2026 |
| Classificação | **Interno** (o resumo do §1 é compartilhável com cliente) |

> Simulação — dados sintéticos para treinamento.

## 1. Situação atual

| Item | Situação |
|---|---|
| SOC 2 Tipo I | **Concluído** em 03/2026. Relatório disponível sob acordo de confidencialidade |
| SOC 2 Tipo II | **Em andamento.** Período de observação iniciado em 04/2026; relatório previsto para o 1º trimestre de 2027, **sem garantia de data** |
| ISO/IEC 27001 | **Não possui.** Não há projeto de certificação aprovado |
| Teste de intrusão externo | Anual, por empresa independente. Último: **05/2026**, sem achados críticos abertos; 2 achados de severidade média corrigidos em 06/2026. Sumário executivo disponível sob acordo de confidencialidade |
| Programa de divulgação de vulnerabilidades | Canal `seguranca@vertice.example` |

## 2. Gestão de vulnerabilidades

- Varredura de dependências e de imagens a cada build.
- Prazos de correção: crítica 7 dias, alta 30 dias, média 90 dias.

## 3. Pessoas e acesso interno

- Acesso de engenharia à produção por acesso just-in-time, com MFA e registro.
- Treinamento anual de segurança e privacidade para todos os funcionários.
- Acordos de confidencialidade com funcionários e prestadores.

## 4. O que não está documentado aqui

- Questionários de terceiros (ex.: planilhas de clientes) devem ser respondidos com base nestes documentos. Perguntas sem cobertura aqui são encaminhadas a Segurança: **não responder de memória**.
