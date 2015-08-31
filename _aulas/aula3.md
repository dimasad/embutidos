---
layout: page
title: "Aula 3: Binário, operações bit a bit e registradores"
permalink: /aula3/
---

Nesta aula vamos ver a representação interna de variáveis inteiras em sistemas
digitais e as operações bit a bit na linguagem C.
Em seguida vamos usar essas operações para escrever nos registradores do
microcontrolador e controlar seu comportamento usando uma interface de baixo
nível.
Também vamos ver como obter as informações necessárias no datasheet do 
microcontrolador e esquemático do Arduino.

#### Índice: ####
{:.no_toc}

1. seções
{:toc}

Bases de sistemas numerais
==========================

As informações em sistemas eletrônicos digitais são armazenadas internamente
na forma de números binários.
Para entendê-los melhor, vamos rever a representação subjacente aos números
decimais.
O número 139, por exemplo, e dado pela soma do produto dos seus algarismos
pelo valor equivalente à sua posição:

$$
1\times 10^2 + 3 \times 10^1 + 9 \times 10^0 = 100 + 30 + 9 = 139.
$$

A mesma lógica pode ser aplicada para outras bases diferentes de 10.
Os números binários são a representação no sistema numeral de base 2.
Eles possuem somente 2 algarismos, 0 e 1, e cada lugar corresponde a uma
potência de 2. 
Por exemplo:[^repr-base]

[^repr-base]:
    Para simplificar a notação, vamos representar a base dos números com um
    subscrito: $$ 10_{16} = 16_{10} = 10000_2 $$.

$$
1011_2 = 1\times 2^3 + 0 \times 2^2 + 1\times 2^1 + 1\times 2^0 = 11_{10}.
$$

Cada algarismo binário é denominado **bit**, do inglês *binary digit*.
Os bits são agrupados em unidades de 8 bits denominados **bytes**.
A base 16, dos números **hexadecimais**, também é muito usada em sistemas.
As letras A a F são usadas para representar os algarismos de 10 a 15.
Essa representação é vantajosa pois
cada algarismo hexadecimal corresponde a 4 bits e cada byte
corresponde a exatamente dois dígitos hexadecimais.

Na linguagem C, os números hexadecimais são representados com o prefixo `0x`,
conforme representado abaixo.
{% highlight c %}
int x = 0x11; // Atribui o valor 17 (em decimal) para a variável x
{% endhighlight %}

Representação de números negativos
==================================

Em C, números negativos em binário são representados em **complemento de dois**.
O bit mais significativo do número indica o sinal, 0 indicando positivo e 1
negativo.
Os números negativos são então obtidos invertendo todos os bits do número e
adicionando um.
Por exemplo: a representação em complemento de dois de $$-2_{10}$$, com 4 bits,
obtida da seguinte forma:

- obtém-se a representação em binário do número positivo, $$0010_2$$,
- inverte-se todos os bits, obtendo $$1101_2$$,
- soma-se 1 e se obtém $$1110_2$$.

Alguns exemplos:

base 10 | Complemento de 2
:------:|:-----------:
-1      | 1111
--------|--------------
-2      | 1110
--------|--------------
-3      | 1101
--------|--------------
-4      | 1100
--------|--------------

Operações bit a bit
===================

A linguagem C possui diversas operações que operam bit a bit nas variáveis
e facilitam operações com registradores:

* complemento: `~x`,
* e: `a & b`,
* ou: `a | b`,
* ou exclusivo: `a ^ b`,
* deslocamento para esquerda: `a << b`,
* deslocamento para direita: `a >> b`.

#### Operador "E" ####

a  | b | a & b
:-:|:-:|:-----:
 0 | 0 | 0
---|---|------
 0 | 1 | 0
---|---|------
 1 | 0 | 0
---|---|------
 1 | 1 | 1
---|---|------

#### Operador "Ou" ####

a  | b | a | b
:-:|:-:|:-----:
 0 | 0 | 0
---|---|------
 0 | 1 | 1
---|---|------
 1 | 0 | 1
---|---|------
 1 | 1 | 1
---|---|------

#### Operador "Ou exclusivo" ####

a  | b | a ^ b
:-:|:-:|:-----:
 0 | 0 | 0
---|---|------
 0 | 1 | 1
---|---|------
 1 | 0 | 1
---|---|------
 1 | 1 | 0
---|---|------

#### Operador deslocamento para esquerda ####

![deslocamento para esquerda]({{site.baseurl}}/images/Rotate_left_logically.svg)

#### Operador deslocamento para direita (sem sinal) ####

![deslocamento para direita]({{site.baseurl}}/images/Rotate_right_logically.svg)

#### Operador deslocamento para direita (com sinal) ####

![deslocamento para direita]({{site.baseurl}}/images/Rotate_right_arithmetically.svg)

Registradores das portas de E/S
===============================

Operações bit a bit para escrita nos registradores
==================================================

Lendo o esquemático
===================


-------------------------------------------------------------------------------
Figuras obtidas do Wikimedia Commons.
