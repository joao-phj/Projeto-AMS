# Relatório de desempenho da linha de base — modelo

<!--
Item 3 da N2. Este relatório tem as quatro informações que o slide 28 do
E4 cobra, mais a leitura de onde erra (slide 30) — a saída do medir.py já
traz quase tudo pronto: rode `python medir.py` na pasta do D2-06 (ou do
seu projeto) e cole no lugar marcado. Responda NOS COLCHETES, apagando
nada das seções.
-->

**Projeto:** [nome do seu projeto] · **Data:** [data da medição]

## 1. A métrica primária

Score = 0,5 × recall de risco alto + 0,3 × acurácia de normas + 0,2 × acurácia de LOTO

## 2. O valor

Métrica primária: acerto da decisão (casos com decisão igual à rotulada, sobre o total)
Valor: 5/30 = 0.1667
Conjunto: casos-de-reserva-4.csv — 30 casos rotulados {'seguir_operando': 19, 'inspecionar_antes_de_operar': 5, 'parar_para_manutencao': 6}

## 3. O conjunto

Usei o conjunto de reserva, adaptando para o o dataset ai4i2020.csv

## 4. Onde o agente erra

Onde erra (o rótulo que o agente não deu):
  caso C01: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C02: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C03: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C06: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C07: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C08: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C09: decidiu parar_para_manutencao, correto era seguir_operando
  caso C10: decidiu parar_para_manutencao, correto era seguir_operando
  caso C11: decidiu parar_para_manutencao, correto era seguir_operando
  caso C12: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C13: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C14: decidiu parar_para_manutencao, correto era seguir_operando
  caso C15: decidiu parar_para_manutencao, correto era seguir_operando
  caso C16: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C17: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C18: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C20: decidiu parar_para_manutencao, correto era seguir_operando
  caso C21: decidiu inspecionar_antes_de_operar, correto era parar_para_manutencao
  caso C22: decidiu inspecionar_antes_de_operar, correto era parar_para_manutencao
  caso C23: decidiu inspecionar_antes_de_operar, correto era parar_para_manutencao
  caso C24: decidiu inspecionar_antes_de_operar, correto era parar_para_manutencao
  caso C26: decidiu inspecionar_antes_de_operar, correto era parar_para_manutencao
  caso C27: decidiu parar_para_manutencao, correto era inspecionar_antes_de_operar
  caso C28: decidiu inspecionar_antes_de_operar, correto era parar_para_manutencao
  caso C29: decidiu parar_para_manutencao, correto era inspecionar_antes_de_operar

## 5. A tabela comparativa de busca (item 4 da N2)

| Busca | Custo | Ações | Nós expandidos | Nós gerados | Prof. máx. | Segundos |
|---|---:|---:|---:|---:|---:|---:|
| largura | 17.0 | 5 | 1938 | 4246 | 5 | 0.0125 |
| custo_uniforme | 17.0 | 5 | 382 | 1289 | 5 | 0.0023 |
| profundidade_limitada(limite=32) | 17.0 | 5 | 6 | 5 | 5 | 0.0 |
| aprofundamento_iterativo(limite=32) | 17.0 | 5 | 880 | 2689 | 5 | 0.004 |

| Busca | Custo | Ações | Nós expandidos | Nós gerados | Prof. máx. | Segundos |
|---|---:|---:|---:|---:|---:|---:|
| gulosa[admissivel] | 17.0 | 5 | 6 | 45 | 5 | 0.0001 |
| a_estrela[admissivel] | 17.0 | 5 | 77 | 266 | 5 | 0.0003 |
| gulosa[inadmissivel] | 68.0 | 11 | 12 | 66 | 11 | 0.0001 |
| a_estrela[inadmissivel] | 47.0 | 8 | 9 | 60 | 8 | 0.0001 |

o A estrela não manteve custo ótimo e expandiu significativemnte menos que o custo uniforme. Ele economizou cerca de 0.0022 segundos. Isso indica que meu espaço de estado talvez não tenha profundida necessária para avaliar a fundo essas buscas. 