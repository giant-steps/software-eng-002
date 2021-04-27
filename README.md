# Desafio

Obrigado por se candidatar a Giant Steps. Gostaríamos de propor-lhe um desafio técnico para que você tenha a oportunidade de demonstrar sua experiência e habilidades.

## Contexto

Ao longo dos últimos meses, Alice poupou dinheiro para fazer investimentos e aumentar seu patrimônio. Ela tem acompanhado de perto os ativos financeiros A e B e vê neles uma oportunidade de ganho de capital. Por isso, Alice elaborou uma estratégia de investimentos para operar (isto é, comprar e/ou vender) exclusivamente  esses dois ativos. Sua estratégia opera esses ativos várias vezes por dia.

Alice quer saber se sua estratégia está dando bons resultados, e por isso precisa de uma ferramenta para analisar a rentabilidade gerada por ela. Seu desafio é escrever um programa para fazer essa análise de acordo com as especificações a seguir.

## Especificações

Seu programa produzirá para Alice um relatório sobre sua estratégia contendo a evolução patrimonial e
rentabilidade acumulada dela para um determinado período com uma taxa de amostragem em minutos. O programa terá como entrada um patrimônio inicial (número decimal) e três arquivos CSV: o Arquivo de
Operações (`trades.csv`) e os Arquivos de Preços (`pricesA.csv` e `pricesB.csv`).

### Capital Inicial

É o valor financeiro, em dinheiro, que Alice iniciou suas operações. Ao longo do tempo, ela utiliza esse dinheiro em caixa para comprar os ativos, isto é, para cada registro de compra, subtrai-se o valor em caixa e quando vende adiciona.
**Para este desafio considere que Alice iniciou com R$100.000,00 de capital inicial.**

### Arquivo de operações

O arquivo de operações (`trades.csv`) descreve as operações de compras e vendas feitas por Alice dos ativos A e B durante o período todo. Ele possui uma linha por operação feita no dia e 5 colunas:
1. **time** - horário da operação no formato "AAAA-MM-DD HH:MM:SS";
2. **symbol** - "A" ou "B", especificando o ativo operado;
3. **side** - "BUY" ou "SELL", dizendo se Alice comprou ou vendeu o ativo especificado na coluna anterior;
4. **price** - número decimal - preço a que foi comprado ou vendido o ativo;
5. **quantity** - número inteiro - quantas unidades do ativo foram compradas ou vendidas por Alice no instante `time`.

### Arquivos de preços

Os arquivos de preços descrevem os preços de mercado dos ativos A e B ao longo do período. 
A taxa de amostragem de preço é de um minuto, isto é, uma linha para cada minuto e contendo 2 colunas:
1. **time** - horário da cotação do ativo no formato "AAAA-MM-DD HH:MM:SS" e
2. **price** - número decimal - preço do ativo em Reais no minuto especificado
   na coluna `time`.

Os preços dados em cada linha desse arquivo valem do segundo 0 do minuto `time`
até o segundo 59 do mesmo minuto (esta é uma simplificação - preços de ativos
financeiros no mundo real podem variar muitas vezes por segundo).

Assuma que os arquivos serão sempre íntegros e que seu programa não precisará
verificar inconsistências nos preços.

## Relatório de Evolução de Patrimônio Total e Rentabilidade Acumulada

Conforme dito anteriormente, a saída do seu programa será a evolução de patrimônio total de Alice ao longo do período e o retorno acumulado.

O cálculo do patrimônio total e do retorno acumulado deve ocorrer em uma taxa de amostragem parametrizável, isto é, ser em janelas regulares de tempo.

Considere que o tamanho da janela de tempo será dado em minutos.

### Cáculo do Patrimônio Total

O Patrimônio Total representa o valor em dinheiro que Alice tem em caixa, somado aos valores da carteira de ativos (`preçoA(t) * unidadesA(t) + preçoB(t) * unidadesB(t)` no caso de Alice, sendo `preçoX(t)` o preço do ativo X para o instante t e `unidadesX(t)` a quantidade de ativos X presentes na carteira de Alice no mesmo instante).

Por exemplo: se Alice iniciou o dia com R$ 10 e comprou no dia 2 unidades do ativo A e uma unidade do ativo B por um total de R$ 7, ela, ao fim do dia, terá em dinheiro R$ 3,00. Suponha que os preços dos ativos A e B no fim do dia eram R$ 4 e R$ 5, respectivamente. Então o valor da carteira de ativos de Alice no fim do dia é de `2 * R$4 + 1 * R$5 = R$13` e, portanto, o Patrimônio Total ao final do dia é dado por `R$3,00 + R$13,00 = R$ 16,00`.

### Cálculo da Rentabilidade Acumulada

A Rentabilidade Acumulada representa a variação percentual do Patrimônio Total dentro de uma
janela de tempo (entre t0 e t1), o cálculo então seria: `rent_acumulada(t1) = (patrimonio_total(t1) / patrimonio_total(t0)) - 1)`.

Por exemplo: se Alice no instante t0 tem R$10,00 de Patrimônio Total e no instante t1 tem R$13,00 temos: `rent_acumulada(t1) = (R$13,00 / R$10,00) - 1 = 0.3 = 30%`.


## Exemplos

### Exemplo 1

Alice gostaria de ver o relatório de 1 de março de 2021 até 7 de março de 2021 com uma taxa de amostragem de 10 min.

#### 3 primeiras linhas do relatório

| timestamp           | Patrimônio Total | Rentabilidade Acumulada |
| ------------------- | ---------------- | ----------------------- |
| 2021-03-01 10:00:00 | 100.000,00       | 0                       |
| 2021-03-01 10:10:00 |                  | 0                       |
| 2021-03-01 10:20:00 |                  | 0                       |

#### 3 últimas linhas do relatório

| timestamp           | Patrimônio Total | Rentabilidade Acumulada |
| ------------------- | ---------------- | ----------------------- |
| 2021-03-07 17:30:00 |                  |                         |
| 2021-03-07 17:40:00 |                  |                         |
| 2021-03-07 17:50:00 |                  |                         |

### Exemplo 2

Alice gostaria de ver o relatório de 5 de março de 2021 até 12 de março de 2021 com uma taxa de amostragem de 10 min.

#### 3 primeiras linhas do relatório

| timestamp           | Patrimônio Total | Rentabilidade Acumulada |
| ------------------- | ---------------- | ----------------------- |
| 2021-03-05 10:00:00 |                  | 0                       |
| 2021-03-05 10:10:00 |                  |                         |
| 2021-03-05 10:20:00 |                  |                         |

#### 3 últimas linhas do relatório

| timestamp           | Patrimônio Total | Rentabilidade Acumulada |
| ------------------- | ---------------- | ----------------------- |
| 2021-03-12 17:30:00 |                  |                         |
| 2021-03-12 17:40:00 |                  |                         |
| 2021-03-12 17:50:00 |                  |                         |


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
* Responda a pergunta no README
* Não esqueça das dependências do projeto


## Perguntas Frequentes (FAQ)

* Devo usar alguma biblioteca ou framework específico para a resolução?
  * Nenhum em específico: utilize as ferramentas que você estiver mais confortável. O objetivo desse teste é você mostrar suas habilidades de programador e engenheiro de software. O único requisito técnico é que a implementação seja feita usando uma dessas linguagens de programação: Python, Java ou C++.
* O desafio pede uma boa cobertura de testes, isso quer dizer que deve cobrir 100% do código?
  * Não necessariamente. O mais importante é que seu código tenha bons testes e casos de teste, essa parte é tão importante quanto o código da solução.