---
layout: post
title:  "Desenvolvendo um protótipo de autojudge próprio para C/C++"
date:   2019-10-10 10:25:00
img: post3.jpg
description: Criando um auto-judge próprio
---

# Desenvolvendo um autojudge para C/C++

Enquanto esse upsolving da Sub-Regional 2019 ICPC vem sendo feito, vamos falar sobre outros assuntos.  

Vou mostrar aqui então uma ferramenta que eu estou usando para trabalhar no
upsolving. Trata-se de um autojudge que eu criei para auxiliar em problemas
que estavam dando resposta errada.

Como a plataforma URI Online Judge não disponibiliza os casos de testes que
são utilizados para testar o codigo, fui levado a procurar pelas entradas
e saidas da prova, que foram encontradas [aqui](http://maratona.ime.usp.br/primfase19/provas/competicao/competicao_tests.tar.bz2)

Baseado na forma como as entradas e saidas estão dispostas no arquivo comprimido,
pensei em uma forma de testar meu código em todas as entradas, comparar com as
saidas e mostrar o tempo de execução.  

A solução foi feita em shell script em um computador com Ubuntu 18.04.  
A arquitetura da execução foi feita da seguinte forma:

* Diretorio do problema/
  * script.sh
  * programa_compilado
  * input/
  * output/

Note que as pastas input/ e output/ são as mesmas que foram extraidas  
O programa_compilado é o executavel do codigo em C/C++  
O arquivo script.sh será um shell script com um código semelhante ao código abaixo,
que retorna caso de teste, tempo de execução, avaliação da resposta e mostra
qual a resposta correta e qual foi a resposta retornada pelo código:

```shell
#!/bin/bash

PROBLEMA=(letraProblema)
LIMITE=(qtdProblemas)
for ((i=1; i <= $LIMITE; i++))
do
	echo Teste: $i
	echo
	echo Tempo de execucao:
	ANSWER=$(time ./main < input/$PROBLEMA_$i)
	echo
	WAITED=$(cat output/$PROBLEMA_$i)
	if [ $WAITED -eq $ANSWER ]
	then
		echo Resposta Correta
	else
		echo Resposta Errada
		echo Esperava $WAITED, encontrou $ANSWER
	fi
	echo
	echo
done
```

Antes de executar o código, lembre-se de inserir valores para as variáveis
PROBLEMA e LIMITE.  



É isso, com esse código se torna um pouco mais facil resolver problemas que
estejam dando problemas, desde que exista as entradas e saidas dos problemas.

**João Vitor Fröhlich** ([codeforces](https://codeforces.com/profile/joaovitor01))
