# Planejador de Turmas NR

Programa para saber quais colaboradores precisam reciclar treinamentos de NR nos próximos meses e montar as turmas automaticamente.

## Como usar

1. Abra o arquivo `planejador-nr.html` no navegador (Chrome, Edge ou Firefox). Precisa de internet só para carregar a biblioteca de planilhas.
2. Clique em **Baixar modelo**, preencha com seus colaboradores (uma linha por colaborador e por NR) e salve.
3. Clique em **Carregar planilha** e escolha o arquivo (.xlsx, .xls ou .csv).
4. Ajuste o período, vagas por turma (padrão 12), mínimo por turma (padrão 3) e turmas por semana, se precisar.
5. Clique em **Exportar resultado (Excel)** para baixar turmas, lista de quem vence e pendências.

Os dados ficam só no seu computador; nada é enviado para a internet.

## Colunas da planilha

| Coluna | Obrigatória | Exemplo |
|---|---|---|
| Matrícula | sim | 10001 |
| Nome | sim | Maria Silva |
| Setor, Função | não | Manutenção / Eletricista |
| NR | sim | NR-10, NR 35, NR-33 |
| Data Último Treinamento | se não tiver Vencimento | 15/01/2025 |
| Vencimento | se não tiver a data do último | 15/01/2027 |
| Escala | sim* | 14x14, 7x7, 14x7 (dias trabalhados x dias de folga) |
| Início da Escala | sim* | data que foi o 1º dia de trabalho de um ciclo |

\* Pode ser trocada pela aba **Folgas** (Matrícula, Data), listando cada dia de folga, para escalas irregulares.
Aba opcional **Feriados** (Data, Descrição) para feriados locais. Os feriados nacionais já são considerados.

Sem vencimento, ele é calculado pela data do último treinamento + validade da NR, que pode ser editada na tela
(padrões: NR-05, 11, 20, 23 e 33 = 12 meses; NR-10, 12, 13, 18 e 35 = 24 meses; confira com o seu SESMT).

## Regras da montagem das turmas

- Entra quem tem treinamento vencido ou vencendo até o fim do período planejado.
- Turmas só de segunda a sexta, fora de feriados.
- O treinamento cai numa folga do colaborador, **nunca no primeiro nem no último dia da folga**. Escalas com folga de 1 ou 2 dias (5x2, 6x1) não têm data possível e aparecem em "Sem turma" com o motivo.
- A data fica dentro da janela de antecedência (padrão 90 dias) e antes do vencimento. Vencidos podem ir em qualquer data, com prioridade.
- Quem vence primeiro é encaixado primeiro; cada turma é marcada no dia que junta mais gente da mesma NR (no empate, o mais perto do vencimento), respeitando o limite de vagas.
- O programa tenta garantir **pelo menos 2 turmas por semana** (configurável), remanejando colaboradores sem deixar nenhuma turma abaixo do mínimo. Semanas em que não houve gente suficiente ficam sinalizadas.
- Toda turma tem **no mínimo 3 e no máximo 12 pessoas** (configurável). Se não houver 3 pessoas da mesma NR com folga possível no mesmo dia, o colaborador aparece em "Sem turma" com esse motivo.
- Ninguém é colocado em dois treinamentos no mesmo dia.
