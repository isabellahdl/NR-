# Planejador de Turmas NR

Programa para saber quais colaboradores precisam reciclar treinamentos de NR nos próximos meses e montar as turmas automaticamente.

## Como usar

1. Abra o arquivo `planejador-nr.html` no navegador (Chrome, Edge ou Firefox). Precisa de internet só para carregar a biblioteca de planilhas.
2. Clique em **Modelo de treinamentos**, preencha com seus colaboradores (uma linha por colaborador e por NR) e salve.
3. Clique em **Modelo de escala** e preencha a escala do ano (veja abaixo). Ela fica num arquivo separado porque muda todo ano.
4. Clique em **Carregar treinamentos** e depois em **Carregar escala** (.xlsx, .xls ou .csv). A ordem não importa.
5. Ajuste o período, vagas por turma (padrão 12), mínimo por turma (padrão 3) e turmas por semana, se precisar.
6. Clique em **Exportar resultado (Excel)** para baixar turmas, lista de quem vence e pendências.

Os dados ficam só no seu computador; nada é enviado para a internet.

## Planilha de treinamentos

| Coluna | Obrigatória | Exemplo |
|---|---|---|
| Matrícula | sim | 10001 |
| Nome | sim | Maria Silva |
| Setor, Função | não | Manutenção / Eletricista |
| NR | sim | NR-10, NR 35, NR-33 |
| Data Último Treinamento | se não tiver Vencimento | 15/01/2025 |
| Vencimento | se não tiver a data do último | 15/01/2027 |
| Grupo | não | A, B, C… (turma/letra da escala, se a planilha de escala for por grupo) |
| Escala | não* | 14x14, 7x7, 14x7 (dias trabalhados x dias de folga) |
| Início da Escala | não* | data que foi o 1º dia de trabalho de um ciclo |

\* Só precisa se você não carregar a planilha de escala. Também dá para usar uma aba **Folgas** (Matrícula, Data).

## Planilha de escala (separada, atualizada todo ano)

Tem prioridade sobre as colunas de escala da planilha de treinamentos. Aceita qualquer um destes formatos (pode misturar em abas diferentes):

- **Por colaborador:** Matrícula, Escala (ex.: 6x4) e **Início da Folga** (qualquer data que foi o 1º dia de folga). Se todos seguem a mesma escala, a coluna Escala pode ficar de fora: vale a **Escala padrão** da tela (6x4). No lugar do Início da Folga também vale o Início da Escala (1º dia de trabalho).
- **Escala mensal** (recomendada quando não há turno fixo): uma aba por mês com o mês no nome (ex.: "Janeiro 2027") ou num título acima da tabela, Matrícula e/ou Nome nas linhas, dias 1 a 31 nas colunas e **F** (ou Folga/DSR) nos dias de folga. O programa usa exatamente os dias marcados.
- **Calendário com datas:** igual ao mensal, mas com datas completas no cabeçalho.
- **Por grupo:** Grupo (ou Turma/Letra), Escala, Início da Folga. A planilha de treinamentos precisa da coluna Grupo.
- **Lista de folgas:** Matrícula e Data, uma linha por dia de folga.

Quem não for encontrado na escala aparece num aviso e na aba "Sem turma". Matrículas com zeros à esquerda (0123 e 123) são consideradas iguais. Se a escala não tiver matrícula, o colaborador é procurado pelo nome.

Na escala 6x4 a folga tem 4 dias, então o treinamento só pode cair no 2º ou no 3º dia de folga (e precisa ser dia útil).
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
