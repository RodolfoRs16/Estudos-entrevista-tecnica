# Pedras Preciosas - Solução em Java

Este README explica **passo a passo** o raciocínio e o código que resolve o desafio **Pedras Preciosas** do HackerRank.  
O objetivo é mostrar como encontramos o número de "elementos preciosos" (letras que aparecem em todas as pedras).

---

## 📖 Problema (resumido)
- Temos `N` pedras, cada uma representada por uma string de letras minúsculas (`a-z`).  
- Um "elemento precioso" é uma letra que aparece **em todas as pedras ao menos uma vez**.  
- A saída deve ser o **número de elementos preciosos**.

Exemplo:
Entrada:
3
abcdde
baccd
eeabg

Saída:
2

Explicação: apenas `a` e `b` aparecem em todas as pedras.

---

## 💡 Ideia da Solução
O problema é resolvido como uma **interseção de conjuntos**:

1. Pegamos as letras da **primeira pedra** e guardamos em um `Set<Character>`.  
   Esse conjunto é nosso **balde inicial** de candidatos.  
2. Para cada nova pedra:
   - Criamos um conjunto com suas letras.  
   - Aplicamos `retainAll`, que faz a **interseção**: mantém apenas as letras que também estão nessa nova pedra.  
3. No final, o conjunto contém somente as letras que aparecem em todas as pedras.  
4. O tamanho do conjunto (`.size()`) é a resposta.

---

## 📜 Código
```java
import java.util.*;

public class Solution {
    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = Integer.parseInt(sc.nextLine());

        Set<Character> comuns = new HashSet<>();
        for (char c : sc.nextLine().toCharArray()) {
            comuns.add(c);
        }

        for (int i = 1; i < n; i++) {
            String pedra = sc.nextLine();
            Set<Character> atual = new HashSet<>();
            for (char c : pedra.toCharArray()) {
                atual.add(c);
            }
            comuns.retainAll(atual);
        }

        System.out.println(comuns.size());
    }
}
Linha a linha

import java.util.*;
Diz ao Java que vamos usar classes utilitárias do pacote java.util, como Scanner, Set e HashSet.

public class Solution {
Define a classe pública chamada Solution. O HackerRank espera esse nome.

public static void main(String[] args) throws Exception {
Ponto de entrada do programa (onde ele começa a rodar). O throws Exception aqui é só para simplificar casos de erro — não é essencial para essa solução.

Scanner sc = new Scanner(System.in);
Cria um leitor de entrada. Ele vai “ler” o que o juiz do HackerRank envia como input (como se fosse digitado no teclado).

int n = Integer.parseInt(sc.nextLine());
Lê uma linha de texto e converte para número inteiro. É o N, a quantidade de pedras.

Usamos nextLine() para evitar problemas de quebra de linha (é mais seguro do que nextInt() nesse contexto).

Set<Character> comuns = new HashSet<>();
Cria um conjunto de caracteres chamado comuns. Conjunto não aceita duplicatas — perfeito para letras que podem se repetir na mesma pedra.

for (char c : sc.nextLine().toCharArray()) {
Lê a primeira pedra (uma string) e a transforma em um array de caracteres para podermos percorrer letra por letra.

comuns.add(c);
Adiciona cada letra da primeira pedra ao conjunto comuns.

Se a letra aparecer repetida (ex.: “d” duas vezes), o Set guarda só uma vez.

for (int i = 1; i < n; i++) {
Começa um laço para processar as outras pedras (da 2ª até a N-ésima).

Por isso começa em 1 (a 1ª já tratamos).

String pedra = sc.nextLine();
Lê a string da pedra atual.

Set<Character> atual = new HashSet<>();
Cria um conjunto atual com as letras dessa pedra.

for (char c : pedra.toCharArray()) {
Percorre cada letra da pedra atual.

atual.add(c);
Coloca a letra no conjunto atual (de novo, sem duplicatas).

comuns.retainAll(atual);
Ponto-chave: faz a interseção entre comuns e atual.

“Reter tudo que também está em atual”.

Na prática, remove de comuns as letras que não aparecem na pedra atual.

Depois de passar por todas as pedras, comuns fica só com as letras que apareceram em todas.

System.out.println(comuns.size());
Imprime a quantidade de letras que sobraram em comuns. Esse número é exatamente a resposta pedida.

} (fecha o main)

} (fecha a classe)

Metáfora rápida (para leigo)

Imagine que a 1ª pedra enche um balde com as letras que ela tem.

Cada nova pedra vira um “filtro”: só passa pelo filtro o que ela também tem.

No fim dos filtros, o que ficou no balde são as letras que todas as pedras tinham.
