---
layout: post
title:  "Competitive Programmer Calouro's Guide - First Accepted"
date:   2020-01-29 15:00:00
img: calouros.jpg
description: Guia para o calouros sair com seu primeiro accepted.
---

# **Competitive Programmer Calouro's Guide**

Eai calouro.

Este guia tem o objetivo de te adiantar algumas coisas sobre programação competitiva, e que, sabendo nada ou sabendo muito sobre programação, você saia daqui com seu primeiro <span style="color:#0a0"> **_accepted_** </span>.

# Programming:
> Carinhosamente abreviado para **_codar_**

Se você já sabe os comandos básicos(input, operações matemáticas e output) de alguma linguagem de programação (menos visualg) pode clicar [aqui](#competitive-programming) para pular esta parte.

Esta seção vai te mostrar os comandos básicos para você fazer o seu primeiro código. Sem dúvida o mais rápido e fácil nesse momento é aprender Python.
Para iniciarmos, [instale o python3 no seu computador](https://www.google.com/search?q=instalar+python+3) e adicionar ele às suas variáveis de ambiente Se tiver dificuldades, use um [compilador online](https://www.onlinegdb.com/). Para já familizar vocês, vou colocar também alguns exemplos em C

Com o ambiente **_setado_**, hora de codar! Abra seu editor de texto, crie um arquivo `a.py`.
Neste primeiro passo vamos aprender a dar um _output_, o famoso **print**. É complicado, vá com calma:

Para printar palavras:<br>
`print("Ola  Mundo")`

Printar números inteiros:<br>
`print(10)`

Printar números reais:<br>
`print(10.566666)`

Printar variáveis:<br>
`a = 5`<br>
`print(a)`

Printar variáveis formatando a saída(o mais importante até aqui):<br>
`a = 5`<br>
`print('Ola mundo {}'.format(a))`

<img src="https://pics.conservativememes.com/declares-variables-when-learning-python-we-dont-do-that-here-41880532.png" title="Meme" style="width:300px; height:300px;">

Para rodar seu código é só ir até o terminal ou prompt de comando (`ctrl + t` no Ubuntu), navegar até a [pasta](https://www.google.com/search?q=como+navegar+pelas+pastas+no+prompt+de+comando&oq) em que você criou o arquivo e executar `python3 nome_do_arquivo.py`.

Beleza, já sabemos sair com dados, agora vamos aos comandos de entrada:

`a = input()`<br>
`a` será do tipo _string_/texto, para fazer a conversão quando você quer um número inteiro:<br>
`a = int(a)`<br>
ou diretamente na entrada:<br>
`a = int(input())`<br>

Continhas matemáticas:<br>
`a = 2`<br>
`b = a + a`<br>
Neste caso, o `+` pode ser substituído por qualquer uma das outras operações (`-, *, /, %`)
> O operador % significa resto da divisão inteira. 5 % 3 = 2, pois 5/3 = 1 e sobra 2

Agora juntando tudo:
```python
a = int(input())
b = a + a
print("a = {}".format(b))
```
em C:

```c
#include <stdio.h>

int main(){
    int a; scanf("%i", &a);
    int b = a+a;
    printf("a = %i\n", b);
}
```

Esse é o básico que eu queria que você soubesse para passar para a próxima seção. Vamos então aplicar os conhecimentos de programação na programação competitiva.


<img src="https://pvsmt99345.i.lithium.com/t5/image/serverpage/image-id/41242i1D8397BD21B07DA8/image-size/large?v=1.0&px=999" title="Meme" style="width:300px; height:300px;">

# Competitive Programming:

Para falar de programação competitiva, primeiramente:

### ***JA FEZ UMA CONTA NO URI????!11***

URI é o _online judge_ que a gente mais usa na UDESC, pelo menos nesse começo... E entrar na competição do ranking da UDESC vai ser um bom incentivo.


## - Mas o que são online judges?

São corretores de código automáticos sem coração, olhos ou ouvidos. O que quero dizer é que eles não vão olhar seu código diretamente, não vão ver suas variáveis ou seus comentários xingando o judge.

> The only thing that matters is the output. (unknown,2020)

Ou seja, a correção será feita comparando o que você printou com a resposta esperada, por isso a resposta deve ser **exatamente** como é pedida nos probleminhas.

<img src="https://pics.awwmemes.com/online-judge-when-i-submit-the-same-code-the-5th-60062139.png" title="Weiss" style="width:250px; height:250px;">

## - Probleminhas:

Os problemas sempre são compostos por um enunciado, uma explicação sobre a entrada que vai ser dada, sobre como a saída é esperada, e um _input sample_.
O input sample é um caso exemplo do problema, isso te ajuda a testar antes de dar o _submit_.

## - Hora do primeiro *submit*

*Submit* do inglês submeter, mandar. É quando você, no caso do URI, cola seu texto, manda para a correção, e torce pelo tão esperado accepted. O URI tem o problema 1001 solucionado em várias linguagens no site, mas espero que você faça seu próprio código para entender melhor.

Abra o problema [1001 - Extremamente Básico](https://www.urionlinejudge.com.br/judge/pt/problems/view/1001) veja o que é pedido e tente fazer seu código com o que você sabe.

E **hora do submit!**, teste seu código e pode mandar. No menu, clique em **submissões** para ver a resposta recebida.

## - As respostas do Judge:

<span style="color:#0a0"> **Accepted** </span>: Se você conseguiu essa resposta parabéns, você solucionou o problema - mas mesmo assim leia o que significam as outras respostas. Se não foi aceito faz parte, tanto que esse problema vale bastante pontos, leia o significado das outras respostas para saber o que errou.

<span style="color:#660"> **Presentation error** </span>: Um dos erros mais comuns no problema 1001, é quando você acerta as entradas mas não do jeito que foi pedido no problema. Quando, por exemplo, esquecemos de quebrar linha (**\n**) no final de todos os prints.
> Em Python, todo print já quebra linha, então nem se preocupa. Em C você deve sempre colocar um `printf("\n")` no final de tudo.

<span style="color:red"> **Wrong anwser(%x)** </span>: Sim, resposta errada, você não fez o código esperado, tente consertar e realizar testes que quebram sua solução. A porcentagem entre parenteses é quantas das resposta você errou.

<span style="color:#004fc5"> **Time limit exceeded** </span>: É uma das coisas que torna os problemas difíceis mais difíceis, o seu código tem um tempo limite para executar e dar a resposta, geralmente 1s, e se passar disso terá o tempo limite excedido. É por causa desse erro que você vai ouvir muito falar em complexidade de algoritmo.

<span style="color:#0AA"> **Runtime error** </span>: Alguma coisa quebrou seu código durante a execução, uma divisão por zero, uma posição de vetor errada... Alguma coisa assim.

<span style="color:#e5af25"> **Compilation error** </span>: Erro para compilar seu código, provavelmente algo errado na sintaxe da linguagem. Se você fez um código em Python e mandou em C é essa a resposta que vai ter ou se você usou algum recurso de uma biblioteca que não importou.

# Pronto.

Agora que você já sabe o básico é só ir em frente, vendo os próximos problemas, saber mais sobre a linguagem, pesquisar como fazer alguma coisa é o que mais ajuda a aprender coisas específicas. Nos próximos problemas algumas coisas com números reais como formatação do print para esses números vai ser necessário, pesquise, aprenda, e assim vai indo.
**E SEMPRE QUE PRECISAR VENHA ATÉ NÓS, BRUTE, TIRAR SUAS DÚVIDAS**
