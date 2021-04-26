# Desafio

Obrigado por se candidatar a Giant Steps. Gostaríamos de propor-lhe um desafio técnico para que você tenha a oportunidade de demonstrar sua experiência e habilidades.

## Contexto

Ao longo dos últimos meses, Alice poupou dinheiro para fazer investimentos e aumentar seu patrimônio. Ela tem acompanhado de perto os ativos financeiros A e B e vê neles uma oportunidade de ganho de capital. Por isso, Alice elaborou uma estratégia de investimentos para operar (isto é, comprar e/ou vender) exclusivamente  esses dois ativos. Sua estratégia opera esses ativos várias vezes por dia.

Alice quer saber se sua estratégia está dando bons resultados, e por isso precisa de uma ferramenta para analisar a rentabilidade gerada por ela. Seu desafio é escrever um programa para fazer essa análise de acordo com as especificações a seguir.

## Especificações

Seu programa produzirá para Alice um relatório sobre sua estratégia contendo a
rentabilidade dela numa dada data de referência. O programa terá como entrada um
patrimônio líquido inicial (número decimal) e três arquivos CSV: o Arquivo de
Operações (`trades.csv`) e os Arquivos de Preços (`pricesA.csv` e `pricesB.csv`).

### Patrimônio Líquido Inicial

É o valor financeiro, em Reais (BRL), com que Alice iniciou o dia. Ao longo do dia, o patrimônio varia: conforme ela compra ativos o patrimônio líquido diminui, e conforme ela os vende o patrimônio líquido aumenta.

### Arquivo de operações

O arquivo de operações (`trades.csv`) descreve as compras e vendas feitas por
Alice dos ativos A e B na data de referência. Ele possui uma linha por operação
feita no dia e 5 colunas:
1. **time** - horário da operação no formato "AAAA-MM-DD HH:MM:SS";
2. **symbol** - "A" ou "B", especificando o ativo operado;
3. **side** - "BUY" ou "SELL", dizendo se Alice comprou ou vendeu o ativo especificado na coluna anterior;
4. **price** - número decimal - preço a que foi comprado ou vendido o ativo;
5. **quantity** - número inteiro - quantas unidades do ativo foram compradas ou vendidas por Alice no instante `time`.

### Arquivos de preços

Os arquivos de preços descrevem os preços de mercado dos ativos A e B ao longo do
dia. Eles possuem uma linha para cada minuto do dia entre 14:00 e 17:59, e 2
colunas:
1. **time** - horário da cotação do ativo no formato "AAAA-MM-DD HH:MM:SS" e
2. **price** - número decimal - preço do ativo em Reais no minuto especificado
   na coluna `time`.

Os preços dados em cada linha desse arquivo valem do segundo 0 do minuto `time`
até o segundo 59 do mesmo minuto (esta é uma simplificação - preços de ativos
financeiros no mundo real podem variar muitas vezes por segundo).

Assuma que os arquivos serão sempre íntegros e que seu programa não precisará
verificar inconsistências nos preços.

## Relatório de rentabilidade

Conforme dito anteriormente, a saída do seu programa será um relatório de
rentabilidade da estratégia de Alice num determinado dia.

O cálculo da rentabilidade deve se dar em janelas regulares de tempo de
tamanho parametrizável - ou seja, dado um mesmo conjunto de arquivos de
entrada, podemos obter diferentes relatórios dependendo do tamanho de janela
passado como parâmetro.

Considere que o tamanho da janela de tempo será dado em minutos.

### Cálculo da rentabilidade

A rentabilidade representa a variação percentual do patrimônio dentro de uma
janela de tempo. Entenda "patrimônio" como **a soma do patrimônio líquido
com o não líquido** - isto é, a soma do dinheiro "em caixa" mais o valor total
da carteira (`preçoA * unidadesA + preçoB * unidadesB` no caso de Alice,
sendo `preçoX` o preço do ativo X no fim da janela temporal e `unidadesX` a
quantidade de ativos X presentes na carteira de Alice naquele momento).

Por exemplo: se Alice iniciou o dia com R$ 10 e comprou no dia 2 unidades do
ativo A e uma unidade do ativo B por um total de R$ 7, ela, ao fim do dia,
terá um patrimônio líquido de R$ 3. Suponha que os preços dos ativos A e B no
fim do dia eram R$ 4 e R$ 5, respectivamente. Então, o patrimônio total de
Alice no fim do dia é de `R$3 + 2 * R$4 + R$5 = $16` e, portanto, ela teve uma
rentabilidade no dia de 60% (variação percentual entre R$ 16, patrimônio final,
e R$ 10, patrimônio inicial, ou `R$ 16 / R$ 10 - 1 = 0.6 = 60%`).

Lembre-se, porém, que você deverá calcular a rentabilidade para janelas de
tempo regulares de tamanho passado por parâmetro, e não apenas a rentabilidade
total do dia. Por exemplo, dados os arquivos de exemplo de operações e de preços
disponibilizados nesse desafio (`trades.csv`, `pricesA.csv` e `pricesB.csv`),
um patrimônio líquido inicial de R$ 100.000,00 e janelas de 15 minutos, temos:

| Horário   | Rentabilidade        |
| -------   | -------------------- |
| 14:00:00  | 0                    |
| 14:15:00  | 0.00017              |
| ...       | ...                  |
| 17:45:00  | -0.00112833          |
| 18:00:00  | 0.000749737591842825 |

## Arquivos de Exemplo

Conforme citado acima, são fornecidos para você alguns arquivos de exemplo para
que você possa verificar se sua solução está correta (`trades.csv`,
`pricesA.csv` e `pricesB.csv`) - use a tabela acima para verificar os valores
obtidos na janela de 15 minutos. Use as explicações sobre cálculo de
rentabilidade e testes automatizados para garantir que sua solução funciona
para janelas de outros tamanhos também.

Adicionalmente, estamos fornecendo 3 arquivos extras: `march_2021_trades.csv`,
`march_2021_pricesA.csv` e `march_2021_pricesB.csv`. Esses arquivos possuem
dados de trades e preços para um mês inteiro, para que você possa fazer outros
tipos de testes. Eles foram gerados considerando um Patrimônio Líquido Inicial
de R$ 100.000,00.

## Instruções de Entrega
Entregue sua solução escrita em Python, C++ ou Java num repositório no Github **privado**,
liberando acesso apenas para nosso avaliador. Sua solução deve conter testes
automatizados.

Inclua no seu repositório um README explicando **detalhadamente** os passos
necessários para rodar seu código - seu software pode estar, preferencialmente
mas não obrigatoriamente, dockerizado.

Adicionalmente, responda à pergunta em seu README:

Considerando um patrimônio inicial de R$ 100.000,00, os arquivos de exemplo `trades.csv`, `pricesA.csv` e `pricesB.csv` e o retorno que Alice conseguiu com os seus trades nesse período, seria melhor para Alice se ela tivesse comprado no início do dia 100% do seu dinheiro no ativo A ou 100% no ativo B ao invés de ter operado ao longo do dia como ela operou? Justifique sua resposta.

Resumindo sua entrega deverá conter:
* Repositório **privado** no Github com a solução
* Solução programada em uma das 3 linguagens Python, Java ou C++
* Testes automatizados com uma boa cobertura
* README com instruções para execução da solução e os testes
* Não esqueça das dependências do projeto


## Perguntas Frequentes (FAQ)

* Devo usar alguma biblioteca ou framework específico para a resolução?
  * Nenhum em específico: utilize as ferramentas que você estiver mais confortável. O objetivo desse teste é você mostrar suas habilidades de programador e engenheiro de software. O único requisito técnico é que a implementação seja feita usando uma dessas linguagens de programação: Python, Java ou C++.
* O desafio pede uma boa cobertura de testes, isso quer dizer que deve cobrir 100% do código?
  * Não necessariamente. O mais importante é que seu código tenha bons testes e casos de teste, essa parte é tão importante quanto o código da solução.