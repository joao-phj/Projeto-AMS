# agent-spec.md — modelo do meu agente

<!--
Este arquivo é para preencher, não para ler e devolver. As perguntas de cada
seção estão em comentário como este: elas não aparecem na pré-visualização,
aparecem no editor. Responda ABAIXO de cada seção, apagando nada delas.

As seções que ainda não foram vistas em aula ficam de pé, com a linha
"quando se preenche" dizendo o encontro em que isso acontece. O documento
cresce a cada laboratório — o de hoje é o primeiro.

Preencha com exemplos concretos do SEU domínio. Uma linha que funcionaria
para qualquer empresa é uma linha genérica — o exemplo do seu segmento
(agente-spec-exemplo.pdf, no mesmo pacote) mostra o contraste.
-->

**Domínio:** Assistente de Manutenção Segura
**Autor(a):** João Passos · **Última revisão:** 09/10/2026

---

## 1. PEAS

<!-- Perguntas que guiam o preenchimento:
  - Performance: o que conta como sucesso, em uma fórmula? Sobre o quê se
    conta, sobre qual conjunto, quanto é sucesso? Qual termo impede a
    trapaça mais óbvia (fechar rápido sem resolver)?
  - Environment: onde o agente opera? O que existe lá — sistemas, pessoas,
    documentos, ruído? Cite elementos concretos.
  - Actuators: o que o agente pode FAZER? Inclua comunicar e escalar:
    informar a decisão é uma ação, e passar adiante também é.
  - Sensors: o que o agente consegue PERCEBER? Só o que ele enxerga existe
    para ele.
  Um PEAS que menciona tecnologia de solução (banco vetorial, nome de modelo)
  está descrevendo a solução — o PEAS descreve o problema.
-->
**Quando se preenche:** no Laboratório 01, hoje. Refinado na Atividade Orientada.

**Performance:**

O agente é considerado bem-sucedido quando, para cada ordem de serviço, ele identifica corretamente: (i) o nível de risco de falha da máquina (baixo/médio/alto), (ii) as normas aplicáveis à intervenção (NR-10, NR-12 ou NR-35), e (iii) se a atividade exige bloqueio e etiquetagem (LOTO) antes do início. Em fórmula, o score principal é:

Score = 0,5 × recall de risco alto + 0,3 × acurácia de normas + 0,2 × acurácia de LOTO

calculado sobre o conjunto de ordens de serviço do dataset de manutenção e das intervenções de referência. O critério de sucesso é manter recall de risco alto acima de 0,90 e taxa de erro de LOTO abaixo de 0,05, sem “ganhar” pontos apenas por responder rápido; um agente que classifica tudo como “baixo risco” para ser rápido falha nesta métrica.

**Environment:**

O agente opera no ambiente de manutenção industrial de uma planta: o técnico recebe uma ordem de serviço com a máquina, a descrição da intervenção e as leituras atuais de sensores; o supervisor de segurança revisa a recomendação; a decisão se relaciona com normas regulatórias e rotina de trabalho em campo. O ambiente inclui sensores de temperatura, rotação, torque e desgaste, histórico de falhas do dataset AI4I 2020, documentação de normas em PDF, e ruído real do processo: descrições incompletas, leituras fora de faixa, máquina em tipo L/M/H, e variação entre intervenções simples e críticas.

**Actuators:**

O agente pode: (1) classificar o risco da máquina em baixo, médio ou alto; (2) listar as normas aplicáveis à intervenção; (3) decidir se a tarefa exige LOTO; (4) emitir uma justificativa em linguagem natural para o técnico; (5) sinalizar necessidade de revisão humana quando a situação for crítica; e (6) escalar a recomendação ao supervisor de segurança ou ao responsável por bloqueio da área. Em outras palavras, ele comunica a decisão, explica o porquê e passa a situação adiante quando o risco justifica.

**Sensors:**

O agente enxerga apenas o que está disponível na ordem de serviço e no contexto de manutenção: valores dos sensores (temperatura do ar, temperatura de processo, rotação, torque, desgaste, potência, delta de temperatura), o tipo da máquina/produto, o histórico de falha e os indicadores binários de falha por modo (TWF, HDF, PWF, OSF, RNF), além da descrição textual da intervenção. Também pode consultar o corpus documental das normas NR-10, NR-12 e NR-35, mas não vê o que não está registrado em dados, documentos ou comunicação do processo.

---

## 2. O ambiente em sete dimensões

<!--
Perguntas que guiam o preenchimento (uma por dimensão):
  - Observabilidade: existe algo que muda a decisão e o agente não mede?
  - Número de agentes: existe alguém cujas ações mudam o seu resultado?
    Um humano que reage ao agente conta.
  - Determinismo: a mesma ação no mesmo estado dá sempre o mesmo efeito?
  - Episódico ou sequencial: a decisão de agora afeta as decisões seguintes?
  - Estático ou dinâmico: o ambiente muda enquanto o agente delibera?
  - Discreto ou contínuo: estados e ações são contáveis?
  - Conhecido ou desconhecido: o agente sabe de antemão as regras? (Trata do
    que ele SABE, não do que ele VÊ.)
  Cada classificação vem com uma frase de justificativa — a etiqueta sozinha
  não vale nada.
-->
**Quando se preenche:** no Laboratório 02, no sábado (encontro 2).

| Dimensão | Minha classificação | Justificativa (uma frase) |
|---|---|---|
| Observabilidade | parcial | O ambiente é limitado aos sensores que tem a disposição, demais aspectos que podem perifericamente afetar esses sensores são desconsiderados |
| Número de agentes | único | Apenas um agente realiza a avaliação e recomendação pautado nas normas e valores dos sensores |
| Determinismo | determinístico | Os mesmos dados provenientes dos mesmos sensores para duas maquinas identicas retornam o mesmo valor |
| Episódico ou sequencial | sequencial | A decisam de realizar o bloqueio geram alterações no estado da máquina |
| Estático ou dinâmico | dinâmico | A latência da resposta pode acarretar em alterações no estado da máquina e consequentemente alteração no score |
| Discreto ou contínuo | discreto | É possível enumerar o score e estados, logo, é discreto |
| Conhecido ou desconhecido | conhecido | É conhecido as normas e os valores dos sensores, tornanando assim o ambiente conhecido |

---

## 3. Tipo de agente pretendido

<!--
Perguntas que guiam o preenchimento:
  - O tipo mais simples que resolve: reativo simples, baseado em modelo,
    baseado em objetivos, baseado em utilidade, ou um deles com aprendizagem?
  - A caracterização do ambiente (seção 2) é que decide — parcialmente
    observável elimina o reativo simples.
  - Justifique com a dimensão do ambiente que obriga a escolha.
-->
**Quando se preenche:** no sábado (encontro 2, manhã).

[o tipo mais simples que resolve, justificado pela dimensão
do ambiente que o obriga]

---

## 4. Medida de desempenho

<!--
Perguntas que guiam o preenchimento:
  - A fórmula do campo Performance, agora em definição operacional: como se
    calcula, passo a passo, sem ambiguidade?
  - Métrica primária e duas secundárias. As secundárias pegam o que a
    primária deixa passar (custo, latência, reabertura).
  - O conjunto de casos: de onde vêm, quantos são, de que período.
  - O limiar de sucesso e o valor de hoje.
-->
**Quando se preenche:** a fórmula começa no Laboratório 01; a definição
operacional completa — primária, secundárias, conjunto e limiar — é item da
Atividade Orientada.

[métrica primária e duas secundárias, cada uma com: como se
calcula, sobre qual conjunto, qual o limiar de sucesso e o
valor de hoje]

---

## 5. Restrições

<!--
Perguntas que guiam o preenchimento:
  - Latência aceitável: a partir de quantos segundos a resposta perde valor?
  - Custo aceitável: quanto pode custar cada resolução?
  - O que o agente jamais pode fazer: a ação irreversível que ele não executa
    sozinho. Esta linha vira política em D12.
  - A troca que você aceita: quanto de qualidade por quanto de custo?
    Um exemplo numérico vale mais que a fórmula.
-->
**Quando se preenche:** na Atividade Orientada.

[latência aceitável, custo aceitável, o que o agente jamais
pode fazer sozinho, e a troca qualidade × custo que você
aceita — com um exemplo numérico]

---

## 6. Catálogo de ações

<!--
Perguntas que guiam o preenchimento:
  - Para cada ação: nome, entrada, saída, é reversível?, qual o risco se
    errar? As quatro colunas são obrigatórias — "baixo" não é descrição de
    risco.
  - Ações de leitura E de escrita: as que alteram o mundo são as que exigem
    cuidado, e são justamente as que mais ficam de fora.
  - Este catálogo é, literalmente, a lista de ferramentas que você vai
    implementar em D10.
-->
**Quando se preenche:** na Atividade Orientada — o pacote `D2-07` traz o
modelo da tabela e dois exemplos preenchidos.

[tabela: nome · entrada · saída · é reversível? · risco se
errar — ações de leitura e de escrita]

---

## 7. Formulação por busca

<!--
Perguntas que guiam o preenchimento:
  - Qual fatia do problema é um espaço de estados? (Nem toda fatia é — e
    reconhecer a que não é vale tanto quanto formular a que é.)
  - Os cinco componentes: estado inicial, ações, modelo de transição, teste
    de objetivo, custo de caminho. Comece pelo teste de objetivo.
  - O estado descreve a SITUAÇÃO, não a história de como se chegou nela.
-->
**Quando se preenche:** no Laboratório 03, sábado à tarde (encontro 2).

[os cinco componentes do seu subproblema: estado inicial,
ações, transição, teste de objetivo, custo]
