# Anotações — Laboratório 02, a descida à mão

> O critério do slide 11: as quatro perguntas respondidas por escrito, com o
> número que sustenta cada resposta. Preencha a tabela rodando o esqueleto
> com as três taxas do slide 12 e copiando a última linha de cada execução.

## A última linha de cada taxa

| Taxa | Última linha da saída (perda, w, b) |
|---|---|
| 0,001 | perda 22462.1 w 215.016 b -17.7381 |
| 0,1 | perda 0.752176 w 300.008 b 4.91185 |
| 1,5 | perda inf w -3.12216e+190 b 4.826e+189 |

## As quatro perguntas do slide 11

**1. A perda está caindo a cada passo, ou oscilando?**

R: Depende da taxa, com 0,1, ele caiu a cada passo, com as demais oscilou e até mesmo cresceu

**2. Ela estabiliza, ou continua descendo até o fim?**

R: Ela estabilizou em 0,1 e continuou oscilando nos demais

**3. Os pesos encontrados batem com os que geraram os dados?**

R: Em 0,1 sim. Nos demais não

**4. Se algo divergiu, qual foi o primeiro passo estranho?**

R:
