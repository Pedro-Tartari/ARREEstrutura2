# Metódos de Ordenação
## Sumário
________________________

 - Conceito
 - [Bubble](#bublle-sort) 
 - [Selection](#selection-sort) 
 - [Insertion](#insertion-sort)
 - [Quick](#quick-sort)
 - [Comparações](#comparações)
 - [Resultado](#resultado)
&nbsp;


## Conceito
___

Em alguns casos é necessário ordenar uma lista de números ou objetos, nesses casos nem sempre é possível ou viável criar um metodo do zero, dessa forma podemos nos inspirar ou mesmo utilizar alguns métodos de ordenação já difundidos.
Essa organização pode ser Interna (quando os dados a serem ordenados estão na memória principal) ou Externa (quando os dados a serem ordenados necessitam de armazenamento em memória auxiliar como por exemplo o disco HD).
Os metodos mais utilizados são citados abaixo: 

&nbsp;


## Bubble Sort
___________
O Bubble irá pegar o conteúdo e arrumá-lo de forma crescente, fazendo uma verificação entre pares de números, se o da esquerda for maior que o da direita esse deve mudar de “casa” . Esse tipo de verificação deve ser feita toda vez que houver troca de valores e se seguir até todos chegarem na ordem correta, mesmo que tenha que fazer diversas vezes o trajeto, exemplo [5,3,2] -> [3,5,2]. No caso, a pior ordem possível é estarem os números maiores por primeiro pois assim terá uma quantidade maior de laços e a melhor é obviamente os números em ordem crescente.

```java
public static void main(String args[]){
	
	for(i = 0; i<5; i++){
		for(int j = 0; j<4; j++){
			if(vet[j] > vet[j + 1]){
				aux = vet[j];
				vet[j] = vet[j+1];
				vet[j+1] = aux;
	}   }   }   }
```

Exemplo:
1. Array desorganizado [5,3,2,1,4]
2. Com o código o programa irá selecionar o primeiro e fazer a verificação com o segundo, se for maior troca de posição, assim sucessivamente.
3. [5,3,2,1,4] → [3,5,2,1,4] → [3,2,5,1,4]→ [3,2,1,5,4]→[3,2,1,4,5] 
4. Dessa forma completa a primeira verificação, agora será feito em todos itens até chegar na ordem crescente. 
5. No fim terá uma última verificação de validação.
&nbsp;


## Selection Sort
_____________

Ao contrário do Bubble onde a verificação irá selecionar dois intervalos, este irá buscar nos arrays o menor número assim o selecionando e colocando como o primeiro da ordem. Após esse processo faz um loop agora ignorando o primeiro número e buscando o próximo menor. 
Sua desvantagem com grandes quantidade de números visto que terá a verificação a cada loop.  


```Java
for (int i = 0; i < vetor.length - 1; i++) {
            menor = vetor[i];
            indiceMenor = i;

            for (int j = i + 1; j < vetor.length; j++){
                if (vetor[j] < menor){
                    menor = vetor[j];
                    indiceMenor = j;
                }
            }
            vetor[indiceMenor] = vetor[i];
            vetor[i] = menor;
        }
```

Exemplo:
1. Array desorganizado [4,3,5,1,2]
2. Selecionamos no primeiro loop o menor valor e jogamos ele para a esquerda.
3. [4,3,5,1,2] → [1,4,3,5,2]
4. Com isso passamos para o próximo loop, onde ignoramos o número 1, em nosso exemplo, e buscaremos o próximo menor número que no caso é o 2, assim por diante. 
5. [1,4,3,5,2] → [1,2,4,3,5] // [1,2,4,3,5] → [1,2,3,4,5] 
&nbsp;


## Insertion Sort
___
Muito semelhante com o Selection Sort, entretanto ao fazer a sua verificação ele irá selecionar uma “chave”,  essa chave deve ser comparada ao item à sua esquerda, caso seja menor que ele, acaba por mudar de posição senão permanece onde está assim encerrando o uso daquele chave selecionada. Igual sua parceira, não é ideal para uma quantidade grande de objetos.

```Java
for (i=2; i<=tam; i++){
    x = vet[i];
    j=i-1;
    vet[0] = x; 
    while (x < vet[j]){
        vet[j+1] = vet[j];
        j--;
    }
    vet[j+1] = x;
}
```
Exemplo:
1. Array desorganizado [2,3,5,1,4]
2. Selecionamos o menor item da sequência, que no caso é o "1". Posteriormente comparamos ele com o item da esquerda, se for menor assume a posição.
3. [2,3,(5,1),4] → [2,3,1,5,4]
4. Após a verificação iremos comparar o 1 com o objeto a esquerda novamente até não puder mais mover. 
5. [2,(3,1),5,4] → [2,1,3,5,4] // [(2,1),3,5,4] → [1,2,3,5,4]
6. Assim concluímos o loop da primeira verificação, agora faremos mais um teste buscando outro número, no caso será o "4".
7. [1,2,3,(5,4)] → [1,2,3,4,5]
8. No fim temos a organização do array.

&nbsp;


## Quick Sort
____

No modo Quick Sort trabalhamos com a divisão e conquista dos números, sendo assim precisamos escolher dentro do array, na ponta mais a direita de preferência, o pivô que irá ser o centro de reorganização. Após isso iremos pegar todos números menores que o pivô e colocá-los a esquerda e a direita os maiores não importando sua ordem, dessa forma podemos organizar separadamente cada um dos segmentos ao escolhemos novamente o item mais a direita fazendo uma nova verificação interna, No final ao “juntarmos” estão organizados na ordem correta. 

```Java
public void quickSort(int arr[], int begin, int end) {
    if (begin < end) {
        int partitionIndex = partition(arr, begin, end);

        quickSort(arr, begin, partitionIndex-1);
        quickSort(arr, partitionIndex+1, end);
    }
}

private int partition(int arr[], int begin, int end) {
    int pivot = arr[end];
    int i = (begin-1);

    for (int j = begin; j < end; j++) {
        if (arr[j] <= pivot) {
            i++;

            int swapTemp = arr[i];
            arr[i] = arr[j];
            arr[j] = swapTemp;
        }
    }

    int swapTemp = arr[i+1];
    arr[i+1] = arr[end];
    arr[end] = swapTemp;

    return i+1;
}
```

Exemplo:
1. Array desorganizado [9, 7, 5, 11, 12, 2, 3, 10, 6]
2. Escolhemos o número mais a direita, posteriormente organizando menores e maiores a esquerda e direita respectivamente. 
3. [5, 2, 3, 6, 12, 7, 14, 9, 10, 11]
4. Agora temos dois “subconjuntos” - [(5, 2, 3), 6, (12, 7, 14, 9, 10, 11)]
5. Devemos organizá-los da mesma forma.
[2, 3, 5] //  6 // [7, 9, 10, 11, 12, 14]
6. Assim ao final temos a organização.
[2, 3, 5, 6, 7, 9, 10, 11, 12, 14]

&nbsp;
## Comparações
___

#### Lista ordenada em ordem **crescente**:

| Tipo | Velocidade | Comparações| Movimentos |
| ------ | ------ | -----| ---|
| Bubble | 0,0988 | 5050 |0 |
| Selection | 0,0602 | 4950 |297|
| Insertion | 0,0038 | 99 |198|
| Quick | 0,0141 | 606] |189|

#### Lista ordenada em ordem **decrescente**.
| Tipo | Velocidade | Comparações| Movimentos |
| ------ | ------ | -----| ---|
Bubble |	0,2045	|5050	|14850|
Selection |	0,0750|	4950|	297|
Insertion |	0,1173|	99|	5148|
Quick 	|0,0147	|610	|336|


#### Lista desordenada com números **aleatórios**.
| Tipo | Velocidade | Comparações| Movimentos |
| ------ | ------ | -----| ---|
Bubble |	0,1596|	5050|	6777|
Selection |	0,0698|	4950|	297|
Insertion |	0,0570|	99|	2457|
Quick |	0,0314|	897|	576|

>>Tabelas pegas em [DevMedia](https://www.devmedia.com.br/algoritmos-de-ordenacao-analise-e-comparacao/28261)

&nbsp;

### Resultado
Podemos notar que cada um dos tipos de organizações citados tem suas desvantagens e vantagens que podem variar dependedo da quantidade vericações, inserções etc.
Dito isso em minha visão quem ganha o posto de mais rápida no comparativo é a Quicksort devido a sua versatilidade independente dos meio testados, seu único detalhe é a escolha do pivo que pode acabar por atrapalhar na execução da organição.
