---
layout: post
title:  "Upsolving Codeforces Round 481"
date:   2020-02-19 15:45:00
img: cf.png
description: Resolvendo probleminhas
---

# Upsolving Codeforces Round 481

Após não terminar o post sobre o Upsolving da Regional 2019, decidi vim aqui agora fazer um upsolving completo, dessa vez de um contest que rolou no [Codeforces](https://www.codeforces.com).

Eu, <a href="https://codeforces.com/profile/joaovitor01" style="color: green">joaovitor01</a> (assim que puder eu mudo esse handle), simulei esse [contest div3](https://codeforces.com/contest/978) e, superando minhas expectativas, quase resolvi todos os problemas durante as 2 horas e meia que me eram disponibilizadas, sendo que o último problema eu fui submeter 5 minutos depois. Minha conclusão com isso não é que o contest era fácil, mas era mais o meu estilo, já que o outro div3 que eu terminei de resolver eu levei aproximadamente uma semana, e tive algumas (muitas) complicações.

Acho que quase valeria a pena comentar sobre o codeforces aqui, mas vou deixar isso para uma postagem mais adiante, onde vou falar de alguns judges interessantes para treinar a programação competitiva.

Vale lembrar que eu recomendo tentar realizar o contest antes de conferir esse upsolving, caso você nunca tenha visto esse contest antes e, caso você fique preso em algum problema, pode dar uma conferida aqui, naquele mesmo esquema de ver primeiro a solução escrita e se isso não for suficiente olhar o código para conseguir alguma base.

Sem mais enrolação, bora pro upsolving.

## Problema A

Nesse problema recebemos um vetor $$a$$ com $$n$$ elementos e nos é pedido para removermos os elementos duplicados, deixando apenas a ocorrência mais à direita do elemento.

Limites do problema:
* $$1 \leq$$ $$n$$ $$\leq 50$$
* $$1 \leq$$ $$a_i$$ $$\leq 1000$$

### Solução

Perceba que os limites do problema são pequenos, logo existem muitas abordagens capazes de resolver o problema. Uma das possíveis abordagens é a seguinte.

Como queremos o elemento mais a direita, percorremos o vetor $$a$$ da direita para a esquerda processando os elementos da seguinte forma:

* Caso o elemento não esteja marcado:
    * Inserimos o elemento em um outro vetor $$b$$;
    * Marcamos o elemento.
* Caso o elemento esteja marcado:
    * Ignoramos o elemento.

Após processar todos os elementos, teremos como resposta $$\mid b \mid$$ e o vetor $$b$$.

### Solução em C++

<details>
```cpp
#include <bits/stdc++.h>
using namespace std;
map<int,bool> vis;

int main(int argc, char const *argv[]) {
    int n; cin >> n;
    int v[n];
    vector<int> nv;
    for (int i = 0; i < n; i++){
        cin >> v[i];
    }
    for (int i = n-1; i>= 0; i--){
        if (!vis[v[i]]){
            nv.push_back(v[i]);
            vis[v[i]] = true;
        }
    }
    cout << nv.size() << endl;
    cout << nv[nv.size()-1];
    for (int i = nv.size()-2; i >= 0 ; i--){
        cout << " " << nv[i];
    }
    cout << endl;
    return 0;
}
```
</details>


## Problema B

O problema consiste em: dado uma string $$s$$ de tamanho $$n$$, verificar quantas letras devem ser removidas tal que não exista a substring "xxx" em $$s$$, tal que o número de remoções seja mínimo.

Limites do problema:
* $$1 \leq$$ $$n$$ $$\leq 100$$

### Solução

Nesse problema só nos interessam as substrings de $$s$$ que contenham apenas o caracter 'x'. Portanto, basta percorrer $$s$$ buscando as substrings interessantes.

Perceba também que devemos remover caracters de substrings $$aux$$ tal que $$\mid aux$$$$\mid \geq 3$$, de tal forma que $$\mid aux$$$$\mid$$ passe a ser $$= 2$$.

Assim, para cada substring $$aux$$, com $$\mid aux$$$$\mid \geq 3$$, o resultado deverá ser incrementado em $$\mid aux\mid - 2$$.

### Solução em C++

<details>
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char const *argv[]) {
    int n; cin >> n;
    string s; cin >> s;
    int cnt = 0, rm = 0;
    for (int i = 0; i < n; i++){
        if (s[i] == 'x') cnt++;
        else {
            if (cnt > 2)
                rm += cnt-2;
            cnt = 0;
        }
    }
    if (cnt > 2)
        rm += cnt-2;
    cnt = 0;
    cout << rm << endl;
    return 0;
}
```
</details>

## Problema C

Nesse problema, existem $$n$$ dormitórios, numerados de $$1$$ a $$n$$, tal que em cada dormitório $$i$$ existem $$a_i$$ quartos, numerados de $$1$$ a $$a_i$$. Um carteiro precisa entregar cartas a esses quartos, onde cada carta está numerada de $$1$$ a $$a_1 + a_2 + ... + a_n$$, onde os quartos do primeiro dormitório vêm primeiro, depois os quartos do segundo dormitório e assim por diante.

O problema é: dado um conjunto de $$m$$ cartas, definir o dormitório e o quarto onde cada carta deve ser entregue.

Limites do problema:
* $$ 1 \leq n$$,$$m \leq 2 \cdot 10^5 $$
* $$ 1 \leq$$ $$a_i$$ $$\leq 10^{10}$$
* $$ 1 \leq b_j\leq$$ $$\sum_{i=1}^{n} a_i$$ $$\mid$$ $$b$$ é dado em ordem crescente

### Solução

A primeira coisa a se perceber aqui são os limites do problema. O número de dormitórios e carta é relativamente, logo uma solução linear para cada carta não solucionará o problema no tempo proposto, sendo necessário uma solução em $$\Theta(log$$ $$n)$$ ou $$\Theta(1)$$. Outro limite para ter atenção é o valor de $$b_i$$, que pode chegar a $$10^{11}$$, o suficiente para gerar overflow em alguns tipos de variáveis, como o $$int$$ em C.

A solução que vou apresentar executa em $$\Theta(n+m)$$ e passa "tranquilamente" no tempo. Aproveitando o fato que as cartas já estão ordenadas, vamos processar cada uma da seguinte forma:

Os dormitórios percorridos pela carta anterior não precisam ser percorridos de novo, assim, partindo do dormitório atual, basta encontrar o dormitório $$x$$ tal que $$(\sum_{i=1}^{x-1} a_i)+1$$ $$\leq$$ $$b_j \leq sum_{i=1}^{x} a_i$$, e o quarto $$y = (\sum_{i=1}^{x} a_i) - b_j$$.

Como são muitas entradas e saídas, recomendo o uso de fast I/O.

### Solução em C++

<details>
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char const *argv[]) {
    long long n, m; cin >> n >> m;
    long long a[n+1];
    a[0] = 0;
    long long x;
    for (long long i = 1; i <= n; i++){
        scanf("%lld", &x);
        a[i] = a[i-1]+x;
    }
    long long d = 1;
    for (long long i = 0; i < m; i++){
        scanf("%lld", &x);
        while (x > a[d]) d++;
        printf("%lld %lld\n", d, x-a[d-1]);
    }
    return 0;
}
```
</details>

## Problema D

Dada uma sequência $$b$$ de números inteiros, onde cada elemento $$b$$ pode:
* Ser incrementado em 1;
* Ter seu valor mantido;
* Ser diminuido em 1.

O problema consiste em encontrar uma sequência aritmética a partir da sequência $$b$$, podendo realizar aquela operação acima apenas uma vez por elemento.

Obs.: uma sequência $$a[a_1,a_2,...,a_n]$$ é chamada aritmética se e somente se $$\forall i \mid 1\leq i\leq n, a_{i+1}-a_i = r$$.

Limites do problema:
* $$1 \leq$$ $$n$$ $$\leq 10^5$$
* $$1 \leq$$ $$b_i$$ $$\leq 10^9$$

### Solução em C++

<details>
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(int argc, char const *argv[]) {
    int n; cin >> n;
    vector<int> v(n);
    for (int i = 0; i < n; i++){
        cin >> v[i];
    }
    bool ve,va = false;
    vector<int> aux = v;
    int cnt,m = n;
    for (int i = -1; i <= 1; i++){
        aux[0] = v[0]+i;
        for (int j = -1; j <= 1; j++){
            ve = true;
            aux[1] = v[1]+j;
            cnt = abs(i)+abs(j);
            int diff = aux[1]-aux[0];
            for (int k = 2; k < n; k++){
                int diff2 = v[k]-aux[k-1];
                if (diff2-diff == 1){
                    aux[k] = v[k]-1;
                    cnt++;
                } else if (diff2-diff == 0){
                    aux[k] = v[k];
                } else if (diff2-diff == -1){
                    aux[k] = v[k]+1;
                    cnt++;
                } else {
                    ve = false;
                    break;
                }
            }
            if (ve){
                m = min(m,cnt);
                va = true;
            }
        }
    }
    if (va) cout << m << endl;
    else cout << -1 << endl;
    return 0;
}
```
</details>

## Problema E

Nesse problema nos são fornecidos dois inteiros $$n$$ e $$w$$, representando respectivamente o número de paradas de ônibus e a capacidade do ônibus. Em seguida, são fornecidos $$n$$ números, onde

$$\forall a_i$$ $$\epsilon$$ $$a$$; $$a_i$$ corresponde à mudança registrada após a parada de ônibus

Com esses dados, o problema nos pede para computarmos quantas capacidades diferentes o ônibus poderia ter no início da contagem.

Limites do problema:
* $$1 \leq$$ $$n$$ $$\leq 1000$$
* $$1 \leq$$ $$w$$ $$\leq 10^9$$
* $$-10^6 \leq$$ $$a_i$$ $$\leq 10^6$$

### Solução em C++

<details>
```cpp
#include <bits/stdc++.h>
using namespace std;

#define INF 0x3f3f3f3f

int main(int argc, char const *argv[]) {
    long long n, w; cin >> n >> w;
    long long pre[n+1];
    long long x;
    long long mi = INF;
    long long ma = 0;
    pre[0] = 0;
    for (long long i = 1; i <= n; i++){
        scanf("%lld", &x);
        pre[i] = pre[i-1]+x;
        ma = max(ma,pre[i]);
        mi = min(mi,pre[i]);
    }
    if (mi < -w || ma > w) cout << 0 << endl;
    else {
        long long cnt = w+1;
        if (mi < 0){
            cnt += mi;
        }
        if (ma > 0){
            cnt -= ma;
        }
        cout << max(cnt,(long long)0) << endl;
    }
    return 0;
}
```
</details>

## Problema F

### Solução em C++

<details>
```cpp
#include <bits/stdc++.h>
using namespace std;

typedef pair<int,int> ii;
map<int,int> cnt;
int p[200005];
int cntp[200005];

int main(int argc, char const *argv[]) {
    int n,k; cin >> n >> k;
    int x,y;
    vector<ii> prog;
    for (int i = 0; i < n; i++){
        scanf("%d", &x);
        p[i] = x;
        cnt[x]++;
    }
    int aux = 0, aux2 = 0;
    for (auto c : cnt){
        cnt[c.first] = aux + aux2;
        aux2 += aux;
        aux = c.second;
    }
    for (int i = 0; i < k; i++){
        scanf("%d %d", &x, &y);
        x--;y--;
        if (p[x] > p[y]) cntp[x]++;
        else if (p[y] > p[x]) cntp[y]++;
    }
    cout << cnt[p[0]]-cntp[0];
    for (int i = 1; i < n; i++){
        cout << " " << cnt[p[i]]-cntp[i];
    }
    cout << endl;
    return 0;
}
```
</details>

## Problema G

### Solução em C++
<details>

```cpp
#include <bits/stdc++.h>
using namespace std;

typedef pair<int,int> ii;
map<pair<int,int>,int > p;
vector<int> es[105];
map<int,int> e;

int main(int argc, char const *argv[]) {
    int n, m; cin >> n >> m;
    int s,d,c;
    int exams[105];
    for (int i = 0; i < m; i++){
        cin >> s >> d >> c;
        p[{s,i}] = d;
        es[s].push_back(i);
        exams[d] = c;
        e[d] = i;
    }
    int schedule[n];
    priority_queue<int, vector<int>, greater<int> > exam;
    priority_queue<int, vector<int>, greater<int> > pexam;
    for (int i = 1; i <= n; i++){
        if (es[i].size() > 0){
            for (int j = 0; j < es[i].size(); j++){
                exam.push(p[{i,es[i][j]}]);
            }
        }
        if (pexam.size() > 0 && pexam.top() == i){
            schedule[i-1] = m+1;
            pexam.pop();
            continue;
        } else if (exam.size() > 0){
            d = exam.top();
            if (i == d) {
                cout << -1 << endl;
                return 0;
            }
            exams[d]--;
            schedule[i-1] = e[d]+1;
            if (exams[d] == 0) {
                pexam.push(d);
                exam.pop();
            }
        } else {
            schedule[i-1] = 0;
        }
    }
    cout << schedule[0];
    for (int i = 1; i < n; i++){
        cout << " " << schedule[i];
    }
    cout << endl;
    return 0;
}
```
</details>
