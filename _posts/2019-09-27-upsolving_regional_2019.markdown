# Upsolving Maratona regional ICPC 2019
<br />

Hora de alguém movimentar esse site aqui pra fazer valer a pena (manter site é caro demais para ninguem utilizar).  
Vou estar disponibilizando aqui um upsolving das questões que caíram na maratona regional de 2019.  
Vou estar disponibilizando também um código que solucione a questão, lembrando que o código não corresponde à melhor solução,
 além de que é no mínimo interessante a produção do próprio código, ou seja, olhe o código somente se você não foi capaz de
programar a própria solução (ou pra comparar também).  
Dito isso, aproveite a leitura

## Problema A
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


<details><summary>Solução em C++</summary>
    
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
    vector<circle> c;
    vector<vector<circle> > circles;
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
<br />

## Problema B
Para esse problema, nos é dado um vetor de entrada V, com N elementos, e é requerido que encontremos dentro desse vetor um valor que seja maior que o primeiro valor do vetor  
<br />
Podemos solucionar esse problema sem a necessidade de um vetor, testando os valores inseridos na entrada, otimizando o tempo gasto para rodar o algoritmo.  
<br />
Para isso, basta lermos o valor de N, o primeiro valor de V, e então para i = 2; i <= N, lemos os valores restantes e comparamos com o primeiro valor, gerando o resultado final a partir de uma variável booleana.

<details><summary>Solução em C++</summary>
 
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
