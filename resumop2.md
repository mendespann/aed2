# 1. Métodos de Pesquisa

### Introdução

> A informação é dividida em registros

> Cada registro possui uma chave para ser
> usada na pesquisa

**CONCEITOS BÁSICOS**

- tabela: arquivo de índices
- arquivo: tabela de valores de funções

Como escolher o método de pesquisa mais adequado:

- Observar quantidade dos dados envolvidos
- Se o arquivo estar sujeito a inserções e retiradas frequentes

**Dicionário** é um tipo abstrato de dados
com as operações:

1. Inicializa
2. Pesquisa
3. Insere
4. Retira

**MÉTODOS DE PESQUISA**

Pesquisa sequencial (ou linear)

- Aplica-se tanto a dados ordenados quanto a dados não ordenados

Pesquisa binária

- Aplica-se somente a dados ordenados
- Vetores, Árvores
- Problema: a ordenação freqüentemente leva muito mais tempo do que a busca

Pesquisa direta com hashing

- Acesso à chave em tempo O(1)

### Pesquisa Sequencial

É o método mais simples e pode ser aplicado a dados ordenados ou não ordenados.

Consiste em percorrer o vetor ou lista de dados e comparar cada elemento com a chave de busca.

É um método custoso, pois requer n comparações no pior caso. O(N)

**CÓDIGO:**

```c
int busca_sequencial(int v[], int n, int chave_busca){
  int i;
    for(i = 0; i<n; i++){
      if( v[i] == chave_busca){
        return i;}}
  return -1;
}
```

### Pesquisa Sequencial Ordenada

- É um aprimoramento da pesquisa sequencial que aproveita a ordenação dos dados.

- Se a chave de busca for menor que o valor em uma posição do vetor, podemos concluir que ela não estará no restante do vetor, evitando a necessidade de percorrer todo o vetor.

- Apresenta uma complexidade linear no pior caso. O(N)

**CÓDIGO:**

```c
int busca_sequencial_ordenada(int v[], int n, int chave_busca) {
    int i;
    for (i = 0; i < n; i++) {
        if (v[i] == chave_busca) {
            return i; // chave_busca encontrada
        } else if (v[i] > chave_busca) {
            return -1; // interrompe busca
        }
    }
    return -1; // chave_busca não encontrada
}

```

### Pesquisa binária

- É uma estratégia de busca mais eficiente quando os dados estão ordenados. Divide o vetor ao meio a cada passo e compara o elemento do meio com a chave de busca.
- Com base nessa comparação, reduz o intervalo de busca pela metade. Esse processo é repetido até encontrar o elemento ou chegar ao fim do vetor.

- A pesquisa binária tem uma complexidade logarítmica O(log n), sendo muito mais rápida do que a pesquisa sequencial ordenada.

```c
int buscaBinaria(int v[], int inicio, int fim, int alvo) {
    if (fim >= inicio) {
        int meio = inicio + (fim - inicio) / 2;
        if (v[meio] == alvo) {
            return meio;  // Retorna o índice onde o elemento foi encontrado
        }
        if (v[meio] > alvo) {
            return buscaBinaria(v, inicio, meio - 1, alvo);
        }
        return buscaBinaria(v, meio + 1, fim, alvo);
    }

    return -1;  // Retorna -1 se o elemento não for encontrado
}

```

# 2. Árvore

As árvores são estruturas de dados capazes de representar o relacionamento hierárquico entre diversas informações.

### Definições:

Definições:

- **Árvore**: conjunto finito de nós e ramificações.
- **Nó**: representa uma informação e seus relacionamentos.
- **Subárvore**: árvore formada por nós descendentes de um nó.
- **Raiz**: nó especialmente designado que é o ponto de partida da árvore.
- **Pai, filho, irmão, avô**: relação entre nós.
- **Grau de um nó**: número de subárvores desse nó.
- **Nó folha**: nó sem descendentes.
- **Nó não folha**: nó com pelo menos um descendente.
- **Grau da árvore**: maior grau entre seus nós.
- **Altura de um nó**: maior caminho do nó até um de seus descendentes.
- **Altura da árvore**: altura do nó raiz.
- **Árvore Ordenada**: Os filhos de cada nó estão ordenados (assume-seordenação da esquerda para a direita)

Exercício: dado essa árvore fuleira

```
     A
    / \
   B   C
      /|\
     D E F
       / \
      G   H

```

Claro! Aqui está a versão com cada linha grifada em Markdown:

1. **Quantas subárvores contém TA?** 2 subárvores.
2. **Quais os nós são folhas?** B, D, G, H
3. **Quais nós são internos?** A, C, E, F
4. **Qual o grau de cada nó?** Grau representa o número de conexões de cada nó, logo:

- Grau 0: B, G, H, D
- Grau 1: E, F
- Grau 2: A
- Grau 3: C

5. **Qual o grau da árvore?**
   O grau da árvore é 3, que é o maior.

6. **Dê o nível e altura do nó F?** Nível vai de 0 até 3, partindo da primeira camada. Logo, o nível de F é 2. Sua altura em relação ao nó folha de maior nível é 1.

# 3. Árvore Binaria

### Definições

- Árvore Binária: O grau de cada nó é menor ou igual a dois, com subárvores esquerda e direita.
- Árvore Binária: Conjunto finito de elementos que é vazio ou composto por três conjuntos disjuntos: raiz, subárvore esquerda e subárvore direita.
- Árvore Binária Ordenada: Os filhos de cada nó interno são ordenados, com pelo menos um filho em cada nó.

### Tipos de Árvores Binárias

- Degenerada: Nesse tipo de árvore binária, todos os nós possuem apenas um filho ou nenhum filho. Isso significa que o grau de saída de todos os nós é no máximo 1. Uma árvore degenerada é essencialmente uma sequência linear de nós.

```
    A
     \
      B
       \
        C
         \
          D
```

- Completa: Uma árvore binária completa é aquela em que todos os níveis da árvore, exceto possivelmente o último, estão completamente preenchidos, e todos os nós do último nível são o mais à esquerda possível. Isso significa que todos os nós têm grau de saída 2, exceto talvez os nós do último nível, que podem ter apenas um filho à esquerda.

```
       A
     /   \
    B     C
   / \   / \
  D   E F   G


```

- Balanceada: Uma árvore binária balanceada é aquela em que a maioria dos nós possui grau de saída 2. Embora possa haver nós com grau de saída 1 ou nenhum filho, a maior parte dos nós terá exatamente dois filhos. A altura da árvore é mantida minimizada, proporcionando um equilíbrio entre os ramos esquerdo e direito da árvore.

```
       A
     /   \
    B    C
   /    / \
  D    F   G

```

_Vantagens_

- Otimização de alocação de memóri
- Mais fáceis de manipular
- Implementação de operações é muito simplificada

_Desvantagens_

- Necessidade de balanceamento
- Sensível a ordem de inserção

### Representação em C

```C
typedef struct {
    int info;
    tipo_no *esq;
    tipo_no *dir;
} tipo_no;


typedef struct {
    char info;
    tipo_no *esq;
    tipo_no *dir;
    tipo_no *pai;
} tipo_no;


// Estrutura do dicionário para Árvore Binária em C
typedef int TipoChave;

typedef struct Registro{
    TipoChave Chave;
} Registro;

typedef struct No *Apontador;

typedef struct No {
    Registro Reg;
    Apontador Esq, Dir;
} No;

typedef Apontador TipoDicionario;

// Árvore Binária em C
void Inicializa(Apontador *Dicionario){
    *Dicionario = NULL;
}

int Vazio(Apontador *Dicionario){
    return (*Dicionario == NULL);
}

```

### Percurso de uma árvore

Percurso de uma Árvore:

**Percurso Pré-fixado**

1. Visitar raiz
2. Percorrer subárvore da esquerda
3. Percorrer subárvore da direita

**Percurso Central (em ordem)**

1. Percorrer subárvore da esquerda
2. Visitar raiz
3. Percorrer subárvore da direita

**Percurso Pós-fixado**

1. Percorrer subárvore da esquerda
2. Percorrer subárvore da direita
3. Visitar raiz

### Árvore Binária de Pesquisa

Propriedade chave: valor de um nó
Valores menores: sempre na subárvore da esquerda
Valores maiores: sempre na subárvore da direita

Ou seja, facilita a busca porque sempre compara a partir da raiz e sabe para onde ir.

### Propriedades

Tempo de pesquisa é proporcional à altura da árvore

- Árvore binária balanceada tem Tempo O (log N)
- Árvore binária degenerada tem Tempo O (N)

### Operação de Inserção

Algoritmo

1. Realiza busca pelo valor X
2. Busca termina no nó Y (se X não está na árvore)
3. Se X < Y, inserir nova folha X como uma
   subárvore da esquerda de Y
4. Se X > Y, inserir nova folha X como uma
   subárvore da direita de Y

Complexidade: O(log N) – somente para árvores balanceadas.
Inserções podem desbalancear a árvore.

### Operação de Remoção

Algoritmo

1. Realizar busca por valor X
2. Se X for uma folha, remover X
3. Senão // precisa remover nó interno
   - Trocar X com o maior valor Y na sub-árvore da esquerda OU
   - Trocar X com o menor valor Z na sub-árvore da direita

Complexidade: O(log N) – somente para árvores balanceadas.
Remoções podem desbalancear a árvore.

### Código ÁRVORE BINÁRIA

```C
#include <stdio.h>
#include <stdlib.h>

// Definição da estrutura do nó da árvore
struct Node {
    int chave;
    struct Node* esquerda;
    struct Node* direita;
};

// Função para criar um novo nó
struct Node* criarNo(int chave) {
    struct Node* novoNo = (struct Node*)malloc(sizeof(struct Node));
    novoNo->chave = chave;
    novoNo->esquerda = NULL;
    novoNo->direita = NULL;
    return novoNo;
}

// Função para inserir um nó na árvore
struct Node* inserirNo(struct Node* raiz, int chave) {
    // Se a árvore estiver vazia, cria um novo nó e o retorna como raiz
    if (raiz == NULL)
        return criarNo(chave);

    // Caso contrário, percorre a árvore para encontrar a posição correta
    if (chave < raiz->chave)
        raiz->esquerda = inserirNo(raiz->esquerda, chave);
    else if (chave > raiz->chave)
        raiz->direita = inserirNo(raiz->direita, chave);

    // Retorna a raiz sem alterações
    return raiz;
}

// Função para realizar uma busca na árvore
struct Node* buscarNo(struct Node* raiz, int chave) {
    // Caso a chave seja encontrada ou a árvore esteja vazia, retorna o nó atual
    if (raiz == NULL || raiz->chave == chave)
        return raiz;

    // Se a chave for menor que a chave do nó atual, busca na subárvore esquerda
    if (chave < raiz->chave)
        return buscarNo(raiz->esquerda, chave);

    // Se a chave for maior que a chave do nó atual, busca na subárvore direita
    return buscarNo(raiz->direita, chave);
}

```

# 4. Árvore Balanceada (AVL)

- Uma das vantagens no uso de árvores é que o
  processo de busca na mesma é muito mais rápido
  do que em listas encadeadas

As árvores AVL são uma variação das árvores binárias de busca que possuem um mecanismo de balanceamento automático.

Uma árvore AVL é uma árvore de busca balanceada, na qual a altura das subárvores esquerda e direita de cada nó difere em no máximo 1. Isso garante que as operações de inserção, remoção e pesquisa na árvore AVL ocorram em tempo O(log N).

### Fator de Balanceamento

- Para definir o balanceamento, é utilizado o fator de balanceamento (FB):

FB(v) = hE(v) – hD(v) onde:

- FB(v) é o fator de balanceamento para o nó
- hE(v) é a altura da subárvore da esquerda
- hD(v) é a altura da subárvore da direita

* -1 = subárvore direita é mais alta
* 0 = subárvores esquerda e direita com mesma altura
* +1 = subárvore esquerda é mais alta

Se a árvore não estiver balanceada é necessário
fazer seu rebalanceamento por meio de rotações

- Rotação simples ou rotação dupla

### CÓDIGO

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct Node {
    int chave;
    struct Node* esquerda;
    struct Node* direita;
    int altura;
} Node;

// Função para obter a altura de um nó
int altura(Node* n) {
    if (n == NULL)
        return 0;
    return n->altura;
}

// Função para obter o máximo entre dois números
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Função para criar um novo nó com uma chave dada
Node* criarNo(int chave) {
    Node* novoNo = (Node*)malloc(sizeof(Node));
    novoNo->chave = chave;
    novoNo->esquerda = NULL;
    novoNo->direita = NULL;
    novoNo->altura = 1; // Um novo nó é sempre inserido como folha
    return novoNo;
}

// Função para realizar uma rotação simples à direita
Node* rotacaoDireita(Node* y) {
    Node* x = y->esquerda;
    Node* T2 = x->direita;

    // Realiza a rotação
    x->direita = y;
    y->esquerda = T2;

    // Atualiza as alturas
    y->altura = max(altura(y->esquerda), altura(y->direita)) + 1;
    x->altura = max(altura(x->esquerda), altura(x->direita)) + 1;

    return x;
}

// Função para realizar uma rotação simples à esquerda
Node* rotacaoEsquerda(Node* x) {
    Node* y = x->direita;
    Node* T2 = y->esquerda;

    // Realiza a rotação
    y->esquerda = x;
    x->direita = T2;

    // Atualiza as alturas
    x->altura = max(altura(x->esquerda), altura(x->direita)) + 1;
    y->altura = max(altura(y->esquerda), altura(y->direita)) + 1;

    return y;
}

// Função para obter o fator de balanceamento de um nó
int fatorBalanceamento(Node* n) {
    if (n == NULL)
        return 0;
    return altura(n->esquerda) - altura(n->direita);
}

// Função para inserir um nó em uma árvore AVL
Node* inserir(Node* no, int chave) {
    // Realiza a inserção normal de uma árvore de pesquisa binária
    if (no == NULL)
        return criarNo(chave);

    if (chave < no->chave)
        no->esquerda = inserir(no->esquerda, chave);
    else if (chave > no->chave)
        no->direita = inserir(no->direita, chave);
    else // Chaves iguais não são permitidas em árvores AVL
        return no;

    // Atualiza a altura do nó atual
    no->altura = 1 + max(altura(no->esquerda), altura(no->direita));

    // Verifica o fator de balanceamento do nó para determinar a rotação necessária
    int balanceamento = fatorBalanceamento(no);

    // Caso de rotação esquerda-esquerda
    if (balanceamento > 1 && chave < no->esquerda->chave)
        return rotacaoDireita(no);

    // Caso de rotação direita-direita
    if (balanceamento < -1 && chave > no->direita->chave)
        return rotacaoEsquerda(no);

    // Caso de rotação esquerda-direita
    if (balanceamento > 1 && chave > no->esquerda->chave) {
        no->esquerda = rotacaoEsquerda(no->esquerda);
        return rotacaoDireita(no);
    }

    // Caso de rotação direita-esquerda
    if (balanceamento < -1 && chave < no->direita->chave) {
        no->direita = rotacaoDireita(no->direita);
        return rotacaoEsquerda(no);
    }

    return no;
}

// Função para imprimir a árvore AVL em ordem
void imprimirArvore(Node* raiz) {
    if (raiz != NULL) {
        imprimirArvore(raiz->esquerda);
        printf("%d ", raiz->chave);
        imprimirArvore(raiz->direita);
    }
}
```

# 5. Árvore Rubro Negra

### DEFINIÇÕES

Uma árvore rubro-negra é uma árvore de busca binária,
logo segue todas as regras:

- todo nó da sub-árvore esquerda de um nó p tem chave
  menor que a chave de p;
- todo nó da sub-árvore direita de um nó p tem chave maior
  que a chave de p.

### REGRAS

- Regra 1: Um nó é vermelho ou é preto
- Regra 2: A raiz é preta
- Regra 3: Toda folha (NULL) é preta
- Regra 4: Se um nó é vermelho então ambos os seus filhos são
  pretos
- Regra 5: Para cada nó p, todos os caminhos desde p até as
  folhas contêm o mesmo número de nós pretos

### Para que essa porra de regra???

Restringindo a maneira que os nós podem ser coloridos do caminho da raíz até qualquer uma das suas folhas, as
árvores rubro-negras:

- Garantem que nenhum dos caminhos será maior que 2x o
  comprimento de qualquer outro
- Garantem que a árvore é aproximadamente balanceada

- As operações de Busca, Mínimo, Máximo, Sucessor e
  Predecessor podem ser efetuadas em tempo O(lg(n))

### Remoção

DIFERNTES CASOS:

| Caso | Nó a ser removido | sucessor |
| ---- | ----------------- | -------- |
| 1    | Vermelho          | Vermelho |
| 2    | Preto             | Vermelho |
| 3    | Preto             | Preto    |
| 4    | Vermelho          | Preto    |

Caso 1 - O nó a ser removido z é vermelho e possui 0 ou 1 filho: Remova o nó diretamente
O nó a ser removido z é vermelho e suc, sucessor de z
também é vermelho: Nada a ser feito

Caso 2 - O nó a ser removido z é preto e suc, sucessor de z é vermelho. Pinte sucessor de preto

Caso 3 -

O problema do duplo preto ocorre quando retiramos um nó
preto
• O duplo preto nada mais é do que uma forma de
compensar a falta do nó removido na altura de preto da
árvore
• Existem 4 casos a tratar caso o nó suc a ser removido for
preto

### AVL vs Rubro Negra

- Na teoria ambas tem a mesma complexidade de inserção, remoção e busca (O(lg n))
- Na prática a árvore AVL é mais rápida para buscas e mais
  lenta para inserção e remoção
- As árvores AVL são mais rigidamente balanceadas do que as árvores rubro-negras, o que permite uma operação de busca mais rápida mas também copromete o desempenho das operações de modificação

Quando usar AVL ou Rubro Negra?

AVL: mais operações de busca

RUBRO NEGRA: mais operações de modificações como inserção e remoção.

### CÓDIGO

```C
#include <stdio.h>
#include <stdlib.h>

enum Cor {VERMELHO, PRETO};

typedef struct No {
    int chave;
    enum Cor cor;
    struct No *esquerda, *direita, *pai;
} No;

No* criarNo(int chave) {
    No* no = (No*)malloc(sizeof(No));
    no->chave = chave;
    no->cor = VERMELHO;
    no->esquerda = NULL;
    no->direita = NULL;
    no->pai = NULL;
    return no;
}

void trocarCores(No* x, No* y) {
    enum Cor temp;
    temp = x->cor;
    x->cor = y->cor;
    y->cor = temp;
}

void rotacaoEsquerda(No** raiz, No* x) {
    No* y = x->direita;
    x->direita = y->esquerda;

    if (y->esquerda != NULL)
        y->esquerda->pai = x;

    y->pai = x->pai;

    if (x->pai == NULL)
        *raiz = y;
    else if (x == x->pai->esquerda)
        x->pai->esquerda = y;
    else
        x->pai->direita = y;

    y->esquerda = x;
    x->pai = y;
}

void rotacaoDireita(No** raiz, No* x) {
    No* y = x->esquerda;
    x->esquerda = y->direita;

    if (y->direita != NULL)
        y->direita->pai = x;

    y->pai = x->pai;

    if (x->pai == NULL)
        *raiz = y;
    else if (x == x->pai->esquerda)
        x->pai->esquerda = y;
    else
        x->pai->direita = y;

    y->direita = x;
    x->pai = y;
}

void balancearInsercao(No** raiz, No* novo) {
    No* pai = NULL;
    No* avo = NULL;

    while ((novo != *raiz) && (novo->cor != PRETO) && (novo->pai->cor == VERMELHO)) {
        pai = novo->pai;
        avo = novo->pai->pai;

        if (pai == avo->esquerda) {
            No* tio = avo->direita;

            if (tio != NULL && tio->cor == VERMELHO) {
                avo->cor = VERMELHO;
                pai->cor = PRETO;
                tio->cor = PRETO;
                novo = avo;
            } else {
                if (novo == pai->direita) {
                    rotacaoEsquerda(raiz, pai);
                    novo = pai;
                    pai = novo->pai;
                }

                rotacaoDireita(raiz, avo);
                trocarCores(pai, avo);
                novo = pai;
            }
        } else {
            No* tio = avo->esquerda;

            if (tio != NULL && tio->cor == VERMELHO) {
                avo->cor = VERMELHO;
                pai->cor = PRETO;
                tio->cor = PRETO;
                novo = avo;
            } else {
                if (novo == pai->esquerda) {
                    rotacaoDireita(raiz, pai);
                    novo = pai;
                    pai = novo->pai;
                }

                rotacaoEsquerda(raiz, avo);
                trocarCores(pai, avo);
                novo = pai;
            }
        }
    }

    (*raiz)->cor = PRETO;
}

void inserir(No** raiz, int chave) {
    No* novo = criarNo(chave);

    No* atual = *raiz;
    No* anterior = NULL;

    while (atual != NULL) {
        anterior = atual;

        if (chave < atual->chave)
            atual = atual->esquerda;
        else if (chave > atual->chave)
            atual = atual->direita;
        else {
            free(novo);
            return;
        }
    }

    novo->pai = anterior;

    if (anterior == NULL)
        *raiz = novo;
    else if (chave < anterior->chave)
        anterior->esquerda = novo;
    else
        anterior->direita = novo;

    balancearInsercao(raiz, novo);
}

void imprimirArvore(No* raiz) {
    if (raiz != NULL) {
        imprimirArvore(raiz->esquerda);
        printf("%d ", raiz->chave);
        imprimirArvore(raiz->direita);
    }
}

int main() {
    No* raiz = NULL;

    inserir(&raiz, 10);
    inserir(&raiz, 20);
    inserir(&raiz, 30);
    inserir(&raiz, 40);
    inserir(&raiz, 50);

    imprimirArvore(raiz);

    return 0;
}
```

### Algoritmo da Árvore Rubro-Negra

O algoritmo da árvore rubro-negra é uma estrutura de dados balanceada que segue algumas regras para garantir o equilíbrio da árvore e melhorar o desempenho de operações como inserção, exclusão e busca. Vou explicar o algoritmo passo a passo:

1. A árvore rubro-negra segue algumas regras para manter o equilíbrio e garantir que nenhuma operação tenha um tempo de execução muito ruim. As principais regras são:
   - Todo nó é vermelho ou preto.
   - A raiz da árvore é sempre preta.
   - Se um nó é vermelho, seus filhos devem ser pretos.
   - Toda folha NULL é preta, e não é representada
   - Todo caminho da raiz até uma folha deve ter o mesmo número de nós pretos.

## Inserção na Árvore Rubro-Negra

Aqui estão os passos para inserir um novo nó na árvore rubro-negra:

1. Inserir o novo nó na árvore, inicialmente colorido como vermelho.
2. Verificar e corrigir possíveis violações às regras da árvore.
3. Se o nó inserido for a raiz, colori-lo de preto.
4. Caso contrário, tratar as seguintes situações:
   - Caso 1: O pai do nó inserido é preto.
   - Caso 2: O pai e o tio (irmão do pai) são vermelhos.
   - Caso 3: O pai é vermelho, mas o tio é preto ou inexistente.
     - Caso 3a: O nó inserido é filho direito do pai e o pai é filho esquerdo do avô.
     - Caso 3b: O nó inserido é filho esquerdo do pai e o pai é filho direito do avô.

Após realizar as rotações e trocas de cores necessárias, a árvore estará balanceada novamente.

Esse é o processo básico de inserção em uma árvore rubro-negra. Ao seguir esses passos, garantimos que a árvore permaneça balanceada e que as violações às regras sejam corrigidas.

# 6. Hashing

## Tabela Hash

- É uma generalização da ideia de array

Por que espalhar os elementos melhora a busca?

- A tabela permite associar valores a chaves

**chave:** parte da informação que compõe o elemento a ser inserido ou buscado na tabela

**valor** é a posição (índice) onde o elemento se encontra no array que define a tabela

### Vantagens

- Alta eficiência na operação de busca
- Implementação simples

### Desvantagens

- Colisões podem ocorrer, afetando o desempenho
- Alto custo para recuperar os elementos da tabela
  ordenados pela chave
- O pior caso é O(N), sendo N o tamanho da tabela

### Hashing: etapas da pesquisa

1. Armazena um conjunto de elementos em um vetor

2. Duas etapas:

- Computar o valor da função
  hashing, a qual transforma a chave de pesquisa em um
  endereço da tabela
- Lidar com colisões

### Definições

_Função de Hashing_
(Função de Transformação)

- Calcula a posição a partir de uma chave escolhida a partir dos dados manipulados

_Mapeamento_

- Associação de cada objeto de um tipo a uma chave, permitindo a indexação.

_Escolha do tamanho da tabela_

OBJETIVO: encontrar um tamanho que minimize a quantidade de posições não utilizadas e a quantidade de colisões.

_Colisões_
Devido ao fato de existirem mais chaves que posições, é comum que várias chaves sejam mapeadas na mesma posição. Quando isto ocorre, dizemos que houve uma _colisão._

_Hashing Imperfeito_

- Para duas chaves diferentes a saída da função de hashing é a mesma posição na tabela

- Ou seja, podem ocorrer colisões das chaves

_Hashing Perfeito_

- Nunca ocorre colisão

Mundo real: Independente da função de hashing utilizada, a mesma vai retornar a mesma posição para duas chaves diferentes: colisão!

### Técnicas de Tratamento de Colisões

_Endereçamento aberto_

Os elementos são armazenados na própria tabela hash

No endereçamento aberto, quando uma nova chave é mapeada para uma posição já ocupada, uma nova posição é indicada para esta chave

- Sondagem Linear

Se uma chave colidir com outra já presente na tabela, ela é inserida na próxima posição vazia, seguindo a sondagem linear.

### EXEMPLO DE CÓDIGO TAD

```C

// Exemplo Aluno
struct aluno {
    int mat;
    char nome[81];
    char turma;
    char email[41];
};

typedef struct aluno Aluno;
#define N 127
typedef Aluno* Hash[N]; // vetor de ponteiros para a estrutura aluno

int hash(int mat) { // função hashing
    return (mat % N);
}

/* na operação de busca, procuramos a ocorrência do elemento a partir do índice mapeado pela função hash */
Aluno* hsh_busca(Hash tab, int mat) {
    int h = hash(mat);
    while (tab[h] != NULL) {
        if (tab[h]->mat == mat)
            return tab[h];
        h = (h + 1) % N;
    }
    return NULL;
}

/* inserção */
Aluno* hsh_insere(Hash tab, int mat, char* n, char* e, char* t) {
    int h = hash(mat);
    while (tab[h] != NULL) {
        if (tab[h]->mat == mat)
            break;
        h = (h + 1) % N;
    }
    if (tab[h] == NULL) { // não achou o elemento
        tab[h] = (Aluno*) malloc(sizeof(Aluno));
        tab[h]->mat = mat;
    }
    // atribui/modifica informação
    strcpy(tab[h]->nome, n);
    strcpy(tab[h]->email, e);
    tab[h]->turma = *t;
    return tab[h];
}

```

Endereçamento por sondagem linear tem problemas, porque vai colocando um do lado do outro, deveria ter um espalhamento, dificultanto a busca.

- Sondagem Quadrática

Tenta espalhar os elementos utilizando uma equação do segundo grau (pqp n aguento mais)

Resolve o problema de agrupamento primárioPorém, gera outro problema conhecido como agrupamento secundário. Todas as chaves que produzam a mesma posição inicial também produzem as mesmas posições na sondagem quadrática

- Hash Duplo

Outra política de endereçamento aberto é o chamado hash duplo: ao invés de incrementar a posição de 1, uma função auxiliar é utilizada para calcular o incremento. Esta função também leva em conta o valor da chave.

_Vantagens_

- Maior número de posições na tabela para a mesma quantidade de memória usada no encadeamento separado
- A memória utilizada para armazenar os ponteiros da lista encadeada no encadeamento separado pode ser aqui usada para aumentar o tamanho da tabela, diminuindo o número de colisões
- Busca é realizada dentro da própria tabela Recuperação mais rápida de elementos
- Voltada para aplicações com restrições de memória Ao invés de acessarmos ponteiros extras,
  calculamos a sequência de posições a serem
  armazenadas

_Desvantagens_

- Maior esforço de processamento no cálculo das posições
- Esse esforço maior se deve ao fato de que, quando uma colisão ocorre, devemos calcular uma nova posição da tabela
- Colisões sucessivas

- Lista Encadeada

Nesta estratégia, a posição de inserção não muda, logo, todos devem ser inseridos na mesma posição, por meio de uma lista ligada

Tem uma lista pra cada posicao
Gasta mais memória

# Considerações Finais

| Estrutura de Dados      | Vantagens                                                                                          | Desvantagens                                                                 | Complexidade de Tempo (Caso Médio) | Complexidade de Tempo (Pior Caso) |
| ----------------------- | -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------- | --------------------------------- |
| Tabela Hash             | - Acesso rápido aos elementos, Alta eficiência no custo de pesquisa, Simplicidade de implementação | - Colisões podem ocorrer, afetando o desempenho Pior caso é O(n) muinto ruim | O(1)                               | O(n)                              |
| Árvore Binária de Busca | - Ordenação automática dos elementos                                                               | - Pode ficar desbalanceada, levando a pior desempenho                        | O(log n)                           | O(n)                              |
| Árvore AVL              | - Mantém o balanceamento automático                                                                | - Requer operações adicionais para manter o balanceamento                    | O(log n)                           | O(log n)                          |
| Árvore Rubro-Negra      | - Mantém o balanceamento automático                                                                | - Requer operações adicionais para manter o balanceamento                    | O(log n)                           | O(log n)                          |

### MIL LINHAS JÁ DE RESUMO

Hash

- Excelente para acesso direto
- Pobre para acesso seqüencial
  Lista
- Excelente para acesso seqüencial
- Pobre para acesso direto

Árvore binária

- Bom compromisso entre acesso direto e seqüencial

E vetor ordenado?

- Mantê-lo ordenado tem custo O(N)
