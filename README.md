# LeetCode 3300 - Minimum Element After Replacement With Digit Sum

## 📝 Descrição do Problema

O problema solicita que, dado um array de números inteiros chamado `nums`, você substitua cada elemento desse array pela **soma de seus dígitos**. Após realizar essa substituição para todos os elementos, o objetivo é encontrar e retornar o **menor (mínimo) elemento** resultante.

### Exemplos de Entrada e Saída

| Entrada (`nums`) | Processamento (Soma dos Dígitos) | Saída |
| --- | --- | --- |
| `[10, 12, 13, 14]` | `[1+0, 1+2, 1+3, 1+4]` $\rightarrow$ `[1, 3, 4, 5]` | **1** |
| `[1, 2, 3, 4]` | `[1, 2, 3, 4]` $\rightarrow$ `[1, 2, 3, 4]` | **1** |
| `[999, 19, 199]` | `[9+9+9, 1+9, 1+9+9]` $\rightarrow$ `[27, 10, 19]` | **10** |

---

## 💡 Abordagem Algorítmica

Para resolver o problema de forma eficiente sem gastar memória extra, a solução adota uma estratégia direta em dois passos principais para cada número do array:

1. **Separação Matemática de Dígitos:** Em vez de converter o número para texto (o que seria mais lento), usamos operadores aritméticos dentro de um loop `while`:
* `temp % 10`: Isola o último dígito do número (ex: `199 % 10 = 9`).
* `temp /= 10`: Remove o último dígito do número de forma inteira (ex: `199 / 10 = 19`).


2. **Atualização do Mínimo Global:** Usamos uma variável acumuladora iniciada com o maior valor inteiro possível (`Integer.MAX_VALUE`). À medida que calculamos a soma dos dígitos de cada número, comparamos com o menor valor encontrado até o momento e o atualizamos se a nova soma for menor.

---

## 💻 Código em Java

```java
class Solution {
    public int minElement(int[] nums) {
        // Inicializa com o maior valor possível para garantir a primeira substituição
        int minSum = Integer.MAX_VALUE; 

        // Percorre cada número dentro do array fornecido
        for (int num : nums) {
            int currentSum = 0;
            int temp = num;
            
            // Loop para extrair e somar os dígitos de 'num'
            while (temp > 0) {
                currentSum += temp % 10; // Adiciona o último dígito à soma
                temp /= 10;              // Remove o último dígito do número
            }
            
            // Verifica se a soma dos dígitos atual é a menor encontrada até agora
            if (currentSum < minSum) {
                minSum = currentSum;
            }
        }
        
        // Retorna o menor valor obtido após todas as reduções
        return minSum;
    }
}

```

---

## 📊 Análise de Complexidade

* **Complexidade de Tempo:** $O(N \times K)$, onde $N$ é o número de elementos no array e $K$ é a quantidade de dígitos do maior número. De acordo com as restrições do problema, os números vão no máximo até $10^4$ (possuem no máximo 5 dígitos), portanto $K \le 5$. Isso torna o tempo de execução praticamente linear: **$O(N)$**.
* **Complexidade de Espaço:** **$O(1)$** (Espaço Constante). O algoritmo não cria estruturas de dados adicionais (como listas ou arrays novos), utilizando apenas algumas variáveis primitivas na memória.

---

## 🛠️ Requisitos de Execução

* **Linguagem:** Java 8 ou superior.
* **Ambiente:** Qualquer IDE Java (Eclipse, IntelliJ, VS Code) ou diretamente no juiz online do LeetCode.
