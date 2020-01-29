---
layout: post
title:  "Competitive Programmer Calouro's Guide - First Accepted"
date:   2020-01-29 15:00:00
img: calouros.jpg
description: Guia para o calouros sair com seu primeiro accepted.
---

# **Competitive Programmer Calouro's Guide**

Eai calouro. 

Este guia tem o objetivo de te adiantar algumas coisas sobre programação competitiva, e que, sabendo nada ou sabendo muito sobre programação, você saia daqui com seu primeiro **accepted**.

# Programming:

(carinhosamente abreviado para 'codar')

Se você já sabe os comandos básicos(input, operações matematicas e output) de alguma linguagem de programação (menos visualg) pode clicar [aqui](#competitive-programming) para pular esta parte. 

Esta seção vai te mostrar os comandos básicos para você fazer o seu primeiro código. Sem dúvida o mais rápido e fácil nesse momento é aprender Python. Antes de mais nada [instale python3 no seu computador](https://www.google.com/search?q=instalar+python) é importante adicionar ele às suas variáveis de ambiente, <font size=1> ou use um [compilador online](https://www.onlinegdb.com/) por enquanto</font>. Mas também colocarei o código em C para efeitos de comparação.

Hora de codar! Abra seu editor de texto, crie um arquivo `a.py`. Primeiro vamos aprender a dar um output, o famoso print. É complicado vá com calma:

Para printar palavras:<br>
`print("Ola  Mundo")`

Printar números:<br>
`print(10)`

Printar variáveis:<br>
`a = 5`<br>
`print(a)`

Printar váriaveis formatando a saída(o mais importante até aqui):<br>
`a = 5`<br>
`print('Ola mundo {}'.format(a))`

<img src="https://pics.conservativememes.com/declares-variables-when-learning-python-we-dont-do-that-here-41880532.png" title="Meme" width=300 height=300>

Para rodar seu código só ir até o terminal ou prompt de comando, ir até a [pasta](https://www.google.com/search?q=como+navegar+pelas+pastas+no+prompt+de+comando&oq) em que você criou o arquivo e dar o comando para executar `python3 a.py`.

Agora os comandos de entrada:

`a = input()`<br>
`a` será do tipo string, para fazer a converção quando você quer um número inteiro:<br>
`a = int(a)`<br>
ou diretamente na entrada:<br>
`a = int(input())`<br>

Continhas matemáticas:<br>
`a = 2`<br>
`b = a+a`<br>
Neste o `+` pode ser substituido por qualquer uma das outras operações(- , *, /)

Juntando tudo:
```python
a = int(input())
b = a+a
print("a = {}".format(b)) 
```
em C:

```C
#include <stdio.h>

int main(){
    int a; scanf("%i", &a);
    int b = a+a;
    printf("a = %i\n", b);
}
```
Esse é o básico que eu queria que você soubesse para passar para a próxima seção, e aplicar os conhecimentos de programação na programação competitiva. 

<img src="https://pvsmt99345.i.lithium.com/t5/image/serverpage/image-id/41242i1D8397BD21B07DA8/image-size/large?v=1.0&px=999" title="Meme" width=300 height=300>

# Competitive Programming:

Para falar de programação competitiva, primeiramente:

### ***JA FEZ UMA CONTA NO URI????!11***

URI é o online judge que a gente mais usa na UDESC, pelo menos no começo... E entrar na competição do ranking da udesc vai ser um bom insentivo.


## - Mas o que são online judges?


São corretores de código automáticos sem coração, olhos ou ouvidos. O que quero dizer é que eles não vão olhar seu código diretamente, não vão ver suas variáveis ou seus comentários chingando o judge.

    The only thing that matters is the output. (unknown,2020)

Vocẽ ja sabe printar, e a correção será feita comparando o que você printou com a resposta esperada, por isso a resposta deve ser exatamente como é pedida nos probleminhas.

<img src="https://pics.awwmemes.com/online-judge-when-i-submit-the-same-code-the-5th-60062139.png" title="Weiss" width=250 height=250>

## - Probleminhas:

Os problemas sempre são compostos por um enunsiado, uma explicação sobre a entrada que vai ser dada, sobre como a saida é esperada, e um input sample com a saida experada para ela, ajudando nos testes antes de dar o 
submit.

## - Hora do primeiro *submit*

*Submit* do inglês submeter, mandar. É quando você, no caso do URI, cola seu texto, manda para a correção, e torce pelo tão esperado accepted. O URI tem o problema 1001 solucionado em várias linguagens no site, mas espero que você faça seu próprio código para entender melhor.

Abra o problema [1001](https://www.urionlinejudge.com.br/judge/pt/problems/view/1001) veja o que é pedido e tente fazer seu código com o que você sabe.

E **hora do submit!**, teste seu código e pode mandar. Vá em submissões para ver a resposta recebida.

## - As respostas do Judge:

<font color=#0a0> **Acceped** </font>: Se você conseguiu essa resposta parabéns, você solucionou o problema - mas mesmo assim leia o que significam as outras respostas. Se não foi aceito faz parte, tanto que esse problema vale bastantes pontos, leia o significado das outras respostas para saber o que errou.

<font color=#660> **Presentation error** </font>: Um dos erros mais comuns no problema 1001, é quando você acerta as entradas mas não do jeito que foi pedido no problema. Quando, em C por exemplo esquece de pular linha (`\n`), isso é sempre uma coisa pedida nos problemas.

<font color=red> **Wrong anwser(%x)** </font>: Sim, resposta errada, você não fez o código esperado, tente consertar e achar testes que quebram sua solução. A porcentagem entre parenteses é quantas das resposta você errou.

<font color=#004fc5> **Time limit exeeded** </font>: É uma das coisas que torna os problemas mais dificeis mais dificeis, o seu código tem um tempo limite para executar e dar a resposta, geralmente 1s, e se passar disso terá o tempo limite exedido. É por causa desse erro que você vai ouvir muito falar em complexidade de código. 

<font color=#0AA> **Runtime error** </font>: Alguma coisa quebrou seu código durante a execução, uma divisão por zero, alguma coisa assim.

<font color=#e5af25> **Compilation error** </font>: Erro para compilar seu código (só acontece com linguagens que o código é compilado), provavelmente algo errado na sintaxe da linguagem. Se você fez um código em python e mandou em C é essa a resposta que vai ter.

# Pronto.

Agora que você já sabe o básico é só ir em frente, vendo os próximos problemas, saber mais sobre a linguagem, pesquisar como fazer alguma coisa é o que mais ajuda a aprender coisas específicas. Nos próximos problemas algumas coisas com números reais como formatação do print para esses números vai ser necessário, pesquise, aprenda, e assim vai indo.