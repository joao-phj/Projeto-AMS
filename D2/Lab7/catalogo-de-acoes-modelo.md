# Catálogo de ações — modelo para preencher

<!--
Este arquivo é para preencher: uma linha por ação que o SEU agente vai
poder executar. As perguntas de cada coluna estão aqui em comentário.

As quatro perguntas que decidem se uma linha está boa:
  - Ação de ESCRITA também? As que alteram o mundo são as que exigem
    cuidado — e são justamente as que mais ficam de fora.
  - COMUNICAR é ação? Avisar, escalar, transferir, pedir confirmação:
    entram com entrada, saída e risco como as outras.
  - "É reversível?" pergunta se o efeito pode ser DESFEITO sem custo
    maior que o da própria ação.
  - O risco diz risco DE QUÊ — "baixo" não é descrição; "paga duas vezes
    uma nota que já estava paga" é.

Este catálogo é, literalmente, a lista de ferramentas que você vai
implementar em D10. Cada linha vira uma função com contrato.
-->

| Ação | Entrada | Saída | É reversível? | Risco se errar |
|---|---|---|---|---|
| ler sensores | valores dos sensores | sugestão de ação relativo aquela máquina | sim | parada ou continuação inadequada da máquina |
| consultar normas | normas aplicaveis de intervenção | intervenções aplicaveis aquela máquina | sim | ausência de uma norma pertinente ou ausência de uma nroma adequada |
| consultar histórico de manutenção | histórico de manutenção da máquina | avaliação de risco da máquina | sim | qualificação de risco inadequada da máquina |
| sugerir parada | leitura de sensores, tipo de máquina e histórico de manutenção | decisão de ação sobre a máquina | não | ação incorreta tomada perante a máquina |

**Quem executa cada ação** o agente sozinho

**O que o agente JAMAIS executa sozinho:** desligar uma maquina
