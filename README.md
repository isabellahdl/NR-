# Planejador de Turmas NR

Programa para saber quais colaboradores precisam reciclar treinamentos de NR nos próximos meses e montar as turmas automaticamente.

## Como usar

1. Abra o arquivo `planejador-nr.html` no navegador (Chrome, Edge ou Firefox). Precisa de internet só para carregar a biblioteca de planilhas.
2. Carregue as três planilhas, em qualquer ordem:
   1. **Escala de revezamento:** a escala do ano, como já é usada (colunas F com as turmas de folga).
   2. **Colaboradores e turmas:** Matrícula, Nome e Turma (A, B, C, D, E). Setor e Função são opcionais.
   3. **Treinamentos vencidos e a vencer:** Matrícula, NR e Vencimento (ou Data do Último Treinamento).
3. Cada campo tem um botão **Modelo** com a planilha pronta para preencher.
4. Ajuste o período, as vagas (padrão 12), o mínimo por turma (padrão 3) e as turmas por semana, se precisar.
5. Clique em **Exportar resultado (Excel)** para baixar as turmas, a lista de quem vence e as pendências.

Quando a escala acaba (ex.: em 31/12), o programa continua o ciclo 6x4 sozinho, desde que os últimos dias da escala sigam esse ciclo. As turmas marcadas nesse período aparecem como "pela projeção da escala". Quando a escala do ano seguinte sair, troque só o arquivo da escala.

Feriados não são considerados, a menos que a opção **Pular feriados nacionais** seja marcada.

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
| Turma | sim, se a escala for por turma | A, B, C, D… (a turma da escala do colaborador) |
| Escala | não* | 14x14, 7x7, 14x7 (dias trabalhados x dias de folga) |
| Início da Escala | não* | data que foi o 1º dia de trabalho de um ciclo |

\* Só precisa se você não carregar a planilha de escala. Também dá para usar uma aba **Folgas** (Matrícula, Data).

## Planilha de escala (separada, atualizada todo ano)

Tem prioridade sobre as colunas de escala da planilha de treinamentos.

### Escala de revezamento (formato usado hoje)

A planilha "Escala de Revezamento" (uma aba por ano, blocos por mês com as colunas **Dias**, **Turnos 1, 2, 3** e duas colunas **F** com as turmas de folga de cada dia) é lida do jeito que está:

- as turmas que aparecem nas colunas **F** são as que estão de folga naquele dia;
- dá para ter várias abas (2024, 2025, 2026…) no mesmo arquivo; um bloco de JANEIRO no fim do segundo semestre conta como janeiro do ano seguinte;
- quando sair a escala do ano seguinte, basta incluir a nova aba (ou carregar o novo arquivo).

A turma de cada colaborador vem da planilha **Colaboradores e turmas** (ou de uma coluna Turma na planilha de treinamentos).

### Folga por turma (lista)

Uma linha por dia, com a data e a turma (ou turmas) de folga:

| Data | Turma de folga |
|---|---|
| 08/11/2026 | D |
| 09/11/2026 | D e E |

- Liste **todos** os dias de folga de cada turma (na 6x4, os 4 dias seguidos). Assim o programa sabe qual é o 1º e o último dia da folga.
- Mais de uma turma no mesmo dia: separe com "e", vírgula ou barra. "Turma D" e "D" são entendidos como a mesma turma.
- Também vale um calendário com uma coluna por turma (Data | A | B | C …) e **F** nos dias de folga.
- Cada colaborador é ligado à turma dele pela coluna **Turma** da planilha de treinamentos, ou por uma aba **Matrícula + Turma** na planilha de escala.

### Outros formatos aceitos

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
- Turmas só de segunda a sexta (feriados só são pulados se a opção estiver marcada).
- O treinamento cai numa folga do colaborador, **nunca no primeiro nem no último dia da folga**. Escalas com folga de 1 ou 2 dias (5x2, 6x1) não têm data possível e aparecem em "Sem turma" com o motivo.
- A data fica dentro da janela de antecedência (padrão 90 dias) e antes do vencimento. Vencidos podem ir em qualquer data, com prioridade.
- Quem vence primeiro é encaixado primeiro; cada turma é marcada no dia que junta mais gente da mesma NR (no empate, o mais perto do vencimento), respeitando o limite de vagas.
- O programa tenta garantir **pelo menos 2 turmas por semana** (configurável), remanejando colaboradores sem deixar nenhuma turma abaixo do mínimo. Semanas em que não houve gente suficiente ficam sinalizadas.
- Toda turma tem **no mínimo 3 e no máximo 12 pessoas** (configurável). Se não houver 3 pessoas da mesma NR com folga possível no mesmo dia, o colaborador aparece em "Sem turma" com esse motivo.
- Cada turma de treinamento junta só pessoas do **mesmo treinamento (NR)** e da **mesma turma da escala** (A, B, C…).
- Ninguém é colocado em dois treinamentos no mesmo dia.
