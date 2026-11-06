# Análise — modelo de uma página

<!--
Item 5 da N2 — a única escrita genuinamente nova, e o tema é fixo:
quais propriedades do ambiente tornam o problema difícil, e que tipo de
agente o problema realmente exige. Um parágrafo por pergunta abaixo; a
meta é UMA página. O que separa o adequado do excelente é a EVIDÊNCIA:
citar o número que apareceu, o caso que errou, a linha da tabela — algo
que só quem rodou saberia. Responda NOS COLCHETES.
-->

## O que torna o problema difícil

[Duas ou três propriedades do ambiente (da caracterização do lab-02), cada
uma amarrada a um comportamento observado: onde a linha de base errou e por quê
(a lista do `medir.py`), onde a busca gastou nós, o que a heurística
precisava saber e não sabia. Exemplo da forma: "a observabilidade parcial
não é rótulo aqui: a linha de base perdeu os casos C07 e C08 porque a falha
intermitente não aparece nas leituras — a informação que decide não está
na percepção do instante."]

Determinismo - determinístico
O baseline segue uma série de regras claras (4 IFs comparam os valores do dataset aos limiares), logo o resultado de duas máquinas distintas devem retronar exatamente a mesma classificação para ambas as máquinas. O dataset limitado, não apresentou este caso, mas existe a segurança de que caso houvesse esse seria o reusltado.

Episódico ou sequencial - sequencial
Para avaliar estados futuros, o dataset não foi populado com os resultados de avaliação do agente, logo não se tornou sequencial este agente e sim estático.



## Que tipo de agente o problema realmente exige

[Dado o parágrafo anterior: reativo simples basta? Precisa de estado
interno (e de quanto histórico)? Precisa de objetivos e busca? O que a
escolha OBRIGA o projeto a ter — e o que ela DISPENSA. Se você apagou a
segunda condição da linha de base porque o seu ambiente é totalmente
observável, este é o lugar da justificativa — a escolha do tipo é parte do
que a rubrica avalia.]

Reativo simples, não precisa de estado interno. Uma comparação simples com os limiares estipulados, assim que ajustados, é suficiente para a formulação da sugestão de açao referente a máquina. Não necessita de objetivos nem busca. 

## O que isto muda no projeto (fecho, três ou quatro linhas)

[A consequência de projeto da análise: o que a D10 precisa trazer para o
seu agente com modelo funcionar melhor que a linha de base — novo sensor,
novo dado, verificador externo? Onde a linha de base é competitiva, e por
quê isso é informação valiosa e não fracasso.]

O projeto necessita de uma melhor linha de avaliação, mais dados relativos ao histórico de falhas para melhor escolher ações para a máquina. Mais consideração do dataset original e suas possiveis ramificações no funcionamento e seleção do agente. A linha de base eh competitiva em casos medianos, onde o resultado se encontra no intermédio dos limiares, demais casos provaram ser dificeis de classificar.
