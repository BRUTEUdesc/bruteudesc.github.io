---
layout: post
title:  "Upsolving Maratona Regional ICPC 2019"
date:   2019-09-27 14:55:00
img: post3.jpg
description: Resolvendo probleminhas
---

# Upsolving Maratona regional ICPC 2019

Hora de alguém movimentar esse site aqui pra fazer valer a pena (manter site é caro demais para ninguem utilizar).
Me chamo João Vitor Fröhlich <a href="https://codeforces.com/profile/joaovitor01" style="color: green">(joaovitor01)</a> e estarei realizando aqui um upsolving das questões que caíram na maratona regional de 2019.  
Vou estar disponibilizando também um código que solucione a questão, lembrando que o código não corresponde à melhor solução, além de que é no mínimo interessante a produção do próprio código, ou seja, olhe o código somente se você não foi capaz de
programar a própria solução (ou pra comparar também).  
Cada problema terá um link para o problema na plataforma Uri Online Judge
Dito isso, aproveite a leitura

# Aquecimento

## Problema A

Teleférico

Solução disponivel na própria [prova](/docs/aquecimento_2019.pdf).

## Problema B

[Fatorial](https://www.urionlinejudge.com.br/judge/pt/problems/view/1936)

O problema se baseia em dado um valor $$N$$, descobrir qual a menor quantidade de $$k$$ fatorias são necessários tal que $$N = a! + b! + ... + z!$$, sendo $${a,b,...,z}$$ inteiros positivos menores que $$k$$.

Um valor $$N$$ pode ser descrito da forma $$N = a! + b! + c!$$
Sabemos que

$$\frac{N}{c!} = \frac{a!}{c!} + \frac{b!}{c!} + \frac{c!}{c!}$$

$$\frac{N}{c!} = \frac{a!}{c!} + \frac{b!}{c!} + 1$$

Se considerarmos como sendo divisão inteira temos

$$\frac{N}{c!} = 0 + 0 + 1$$

Isso nos mostra que se $$c!$$ pertencer a soma, $$\frac{N}{c!} == 1$$.

Então para minimizar $$k$$, precisamos adotar uma estratégia *greedy* começando por pegar os maiores valores até zerar $$N$$.

Por fim, realizamos uma operação modular em $$N$$ para retirar o fatorial da soma.
Com a finalidade de otimizar a consulta do fatorial, utilizamos a técnica de *programação dinâmica*.

### Solução em Python3
<details>


```python
def fats(x):
    ans = 1
    for i in range(2,x+1):
        ans *= i
    return ans

fat = [fats(i) for i in range(1,10)]

n = int(input())
ans = 0

for i in range(8,-1,-1):
    ans += n//fat[i]
    n %= fat[i]

print(ans)
```
</details>

## Problema C

[Nota Esquecida](/docs/aquecimento_2019.pdf)

Este problema consiste em descobrir $$B$$ tal que $$M = (A+B) / 2$$

Sabemos $$M$$ e $$A$$, então isolando $$B$$ obtemos

$$B = 2*M - A$$

### Solução em Python3
<details>


```python
A = int(input())
M = int(input())
B = 2*M - A

print(B)
```
</details>


# Prova Principal

## Problema A
[Arte Valiosa](https://www.urionlinejudge.com.br/judge/pt/problems/view/2962)  

O problema consiste em encontrar um caminho entre o canto inferior esquerdo e o canto superior direito de um retângulo, evitando
passar pela área dos sensores de presença, que possuem um raio r e um par de coordenadas (x,y).  
Para esse problema é interessante perceber as seguintes propriedades:  
* É possível passar entre dois círculos se e somente se eles não se interseccionam
* Um círculo impede a passagem da sala se:

  * As extremidades do círculo interseccionam as delimitantes do retângulo superior e inferior
  * As extremidades do círculo interseccionam as delimitantes do retângulo esquerda e direita
  * As extremidades do círculo interseccionam as delimitantes do retângulo esquerda e inferior
  * As extremidades do círculo interseccionam as delimitantes do retângulo direita e superior

Note que ao aplicar a primeira propriedade, é possível gerar um conjunto de circunferências de forma que as extremidades desse
conjunto serão dadas pelas:

* Extremidade mais a esquerda de todos os círculos do conjunto;
* Extremidade mais a direita de todos os círculos do conjunto;
* Extremidade mais superior de todos os círculos do conjunto;
* Extremidade mais inferior de todos os círculos do conjunto.

Assim, para solucionarmos o problema, basta armazenamos os conjuntos de circunferências em vetores e, em seguida, testarmos se
um conjunto de circunferências é capaz de impedir a passagem. Retornamos "N" caso um ou mais conjunto são capazes de impedir
a passagem pela sala, ou retornamos "S" caso contrário

### Solução em C++
<details>


```cpp
#include <bits/stdc++.h>
using namespace std;

struct point{
    int x, y;
    point () { x = y = 0; }
    point(int _x, int _y) : x(_x), y(_y) {}
};

double dist (point p1, point p2){
    return hypot(p1.x-p2.x, p1.y-p2.y);
}

struct circle{
    point c;
    int r;
    int idx;
    circle () { c = point(); r = 0; idx = 0; }
    circle(point _c, int _r, int _idx) : c(_c), r(_r), idx(_idx) {}
};

bool inter(circle c1, circle c2){
    return dist(c1.c, c2.c) <= c1.r+c2.r;
}

#define pb push_back

int main(int argc, char const *argv[]) {
    int n,m,k;
    int x,y,r;
    cin >> n >> m >> k;
    vector <circle> c;
    vector<vector <circle> > circles;
    for (int i = 0; i < k; i++){
        cin >> x >> y >> r;
        c.pb(circle(point(x,y),r,-1));
    }
    for (int i = 0; i < k; i++){
        for (int j = 0; j < k; j++){
            if (i == j) continue;
            if (inter(c[i],c[j])){
                if (c[i].idx != -1 || c[j].idx != -1){
                    if (c[i].idx == c[j].idx) continue;
                    else if (c[i].idx == -1 || c[j].idx == -1){
                        int idx;
                        if (c[i].idx == -1) {
                            idx = c[j].idx;
                            circles[idx].pb(c[i]);
                            c[i].idx = idx;
                        } else {
                            idx = c[i].idx;
                            circles[idx].pb(c[j]);
                            c[j].idx = idx;
                        }
                    } else {
                        int idx1 = c[i].idx, idx2 = c[j].idx;
                        for (int i = 0; i < circles[idx2].size(); i++){
                            circles[idx1].pb(circles[idx2][i]);
                            circles[idx2][i].idx = idx1;
                        }
                        circles[idx2] = vector<circle> ();
                    }
                } else {
                    int idx = circles.size();
                    c[i].idx = idx;
                    c[j].idx = idx;
                    circles.pb(vector<circle> ({c[i],c[j]}));
                }
            }
        }
        if (c[i].idx == -1){
            circles.pb(vector<circle> ({c[i]}));
        }
    }
    for (int i = 0; i < circles.size(); i++) {
        int minX = n+1, maxX = 0, minY = m+1, maxY = 0;
        for (int j = 0; j < circles[i].size(); j++){
            circle caux = circles[i][j];
            minX = min(minX, caux.c.x-caux.r);
            maxX = max(maxX, caux.c.x+caux.r);
            minY = min(minY, caux.c.y-caux.r);
            maxY = max(maxY, caux.c.y+caux.r);
        }
        if ((minX <= 0 && (maxX >= n || minY <= 0)) || (maxY >= m && (minY <= 0 || maxX >= n))){
            cout << "N" << endl;
            return 0;
        }
    }
    cout << "S" << endl;
    return 0;
}
```
</details>

## Problema B
[Bobo da Corte](https://www.urionlinejudge.com.br/judge/pt/problems/view/2963)


Para esse problema, nos é dado um vetor de entrada V, com N elementos, e é requerido que encontremos dentro desse vetor um valor que seja maior que o primeiro valor do vetor  

Podemos solucionar esse problema sem a necessidade de um vetor, testando os valores inseridos na entrada, otimizando o tempo gasto para rodar o algoritmo.  

Para isso, basta lermos o valor de N, o primeiro valor de V, e então para i = 2; i <= N, lemos os valores restantes e comparamos com o primeiro valor, gerando o resultado final a partir de uma variável booleana.

### Solução em C++
<details>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char const *argv[]) {
    int n, x, foo;
    cin >> n;
    cin >> foo;
    bool v = true;
    for (int i = 1; i < n; i++){
        cin >> x;
        if (x > foo){
            v = false;
        }
    }
    if (v) cout << "S" << endl;
    else cout << "N" << endl;
    return 0;
}
```

</details>

## Problema D
[Delação Premiada](https://www.urionlinejudge.com.br/judge/pt/problems/view/2965)

Nesse problema precisamos encontrar o maior número de mafiosos em uma hierarquia podendo saber os crimes de apenas K pessoas.

Note que como o topo da hierarquia sempre pertence ao nó 1, podemos facilmente modelar esse problema utilizando uma árvore, onde cada elemento possui um nó pai e uma profundidade.
Após a entrada de dados, precisamos encontrar a profundidade de todos os nós. Para isso, rodamos um DFS a partir do nó raiz da árvore.

Em seguida, com a profundidade de cada nó, precisamos encontrar quantas pessoas podem ser presas a partir de uma folha. Para isso, rodamos um DFS com DP em todos os nós, começando com os nós de menor profundidade e subindo a árvore, denotando para cada nó, o tamanho do caminho até a parte mais baixa da árvore. Perceba que caso um nó tenha 2 ou mais filhos, é interessante manter o nó cujo caminho seja maior. Os outros nós armazenaremos em um fila de prioridade.

Quando terminarmos de percorrer todos os nós, temos como resultado o tamanho do maior caminho até a parte mais baixa da árvore, enquanto os outros caminhos estarão armazenados de forma decrescente. Feito isso, basta agora pegar da fila K-1 elementos e somá-los com o resultado que ja tinhamos. Esse é o resultado que deve ser imprimido

### Solução em C++
<details>

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int> > adjList;
vector<pair<int, int> > r;
vector<int> parent;
vector<int> vis;
priority_queue<int> pq;

void busca_rank(int o){
    for (int i = 0; i < adjList[o].size(); i++){
        int idx = adjList[o][i];
        r[idx].first = r[o].first-1;
        busca_rank(idx);
    }
}

int dfs(int o){
    if (vis[o] != -1) return vis[o];
    int m = 0;
    for (int i = 0; i < adjList[o].size(); i++){
        int tam = dfs(adjList[o][i]);
        if (tam > m){
            if (m != 0) pq.push(m);
            m = tam;
        } else pq.push(tam);
    }
    vis[o] = m+1;
    return vis[o];
}

int main(int argc, char const *argv[]) {
    int n, k, x;
    cin >> n >> k;
    adjList.resize(n);
    vis.push_back(-1);
    r.push_back(make_pair(n,0));
    parent.push_back(-1);
    for (int i = 1; i < n; i++){
        vis.push_back(-1);
        r.push_back(make_pair(n,i));
        cin >> x;
        x--;
        parent.push_back(x);
        adjList[x].push_back(i);
    }
    busca_rank(0);
    sort(r.begin(), r.end());
    int res;
    for (int i = 0; i < n; i++){
        res = dfs(r[i].second);
    }
    for (int i = 0; i < k-1; i++){
        res += pq.top();
        pq.pop();
    }
    cout << res << endl;
    return 0;
}
```

</details>

## Problema H
[Hora da Corrida](https://www.urionlinejudge.com.br/judge/pt/problems/view/2968)

Nesse problema nos é fornecido o comprimento de uma volta (N) e o número de voltas (V) que serão percorridas, e precisamos fornecer a distância de cada 10% do trajeto até 90%.

A primeira coisa que precisamos fazer é encontrarmos a distância total do percurso $$dt = N*V$$

Após isso, basta fazer uma iteração de 1 a 9, imprimindo o resultado da operação

$$\sum_{i=1}^{9} \frac{dt}{0.1*i}$$  

### Solução em C++
<details>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int a,b,c;
    cin >> a >> b;
    c = a*b;
    printf("%d",(int)(ceil(c*0.1)));
    for (int i = 2; i < 10; i++){
        printf(" %d", (int)(ceil(c*(i/10.0))));
    }
    cout << endl;
    return 0;
}
```
</details>

## Problema M
[Maratona Brasileira de Comedores de Pipoca](https://www.urionlinejudge.com.br/judge/pt/problems/view/2973)

O problema consiste em encontrar um número [1,C] de subsequencias, onde a subsequencia que possua a maior soma tenha a soma de valor minimo

São fornecidos os dados de quantidade elementos da sequencia principal $$N$$, a quantidade máxima de subsequencias $$C$$ e quantas pipocas serão consumidas por segundo $$T$$. Também serão fornecidos $$N$$ valores, onde cada valor $$p_{i}$$ representa a quantidade de pipocas por elemento

Para resolvermos esse problema, iremos inicialmente testar um valor $$x = 2^{\log_2 \frac{M}{T}}$$, onde $$M$$ representa o elemento com maior quantidade de pipocas. Esse valor $$x$$ representa o valor máximo da soma de uma subsequência. Note que $$x = 2^{a}$$, $$a \in \mathbb{N}$$, com isso denotaremos uma variável $$aux = 2^{a-1}$$

Após obtermos $$x$$, encontraremos a quantidade de subsequências necessárias para obedecer ao valor $$x$$, que denotaremos $$contador$$.

Realizaremos agora uma implementação na forma de uma busca binária:
* Caso $$contador \leq C$$, calcularemos $$x = \frac{x-a}{2}$$ e armazenamos $$x$$ como resposta temporaria $$R$$.
* Caso contrário, utilizaremos duas abordagens diferentes:
  * Caso ainda não tenha acontecido $$contador \leq C$$, $$aux = x$$ e $$x = x*2$$
  * Caso contrario, denotaremos $$aux2 = \frac{x-a}{2}$$ e atribuiremos $$aux = x$$ e $$x = x+aux$$

Quando encerrarmos a busca binária basta imprimir o valor de $$R$$

### Solução em C++
<details>

```cpp
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char const *argv[]) {
    int n,c,t,x,m=0,mi,aux=1,ret;
    bool v = false;
    cin >> n >> c >> t;
    int s[n];
    for (int i = 0; i < n; i++){
        cin >> s[i];
        m = max(m,s[i]);
    }
    x = pow(2,(int) ceil(log2(m/t)));
    mi = x/2;
    while (aux != 0){
        int sa = 0;
        int cont = 0;
        for (int i = 0; i < n; i++){
            if (ceil(s[i]*1.0/t) > x || cont == c){
                cont = c+1;
                break;
            }
            if (ceil((double)(sa + s[i])/(t*1.0)) <= x){
                sa += s[i];
            } else {
                cont++;
                sa = s[i];
            }
        }
        cont++;
        aux = (x-mi)/2;
        if (cont <= c){
            ret = x;
            v = true;
            x -= aux;
        } else if (v){
            mi = x;
            x += aux;
        } else {
            aux = 1;
            mi = x;
            x = x*2;
        }
    }
    cout << ret << endl;
    return 0;
}
```
</details>

