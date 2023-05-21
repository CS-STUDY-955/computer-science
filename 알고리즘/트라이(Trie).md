# 트라이

- 문자열을 저장하고 효율적으로 탐색하기 위한 자료구조
- Trie라는 이름은 re<b>trie</b>val(검색)에서 유래됨

![trie-data-structure](https://static.javatpoint.com/ds/images/trie-data-structure.png)

- 문자열의 문자가 각 노드에 저장되어 있고, 루트부터 자식들을 따라가며 생성되는 문자열이 자료구조에 저장되어 있음
- 저장된 단어의 마지막 문자에 단어의 끝을 표시하는 변수를 추가해 단어의 끝을 구분할 수 있음
- 자동완성 기능, 사전 검색 등 문자열을 탐색하는데에 특화되어있음
- 특히 접두사(prefix)와 관련된 작업에 효과적임

<br>

## Trie 구현

- 노드 구현

```java
// 알파벳 소문자 기준
class Node {
    Node[] children;
    boolean isEndOfWord;

    public Node() {
        children = new Node[26]; // 알파벳 소문자에 대한 자식 노드 배열
        isEndOfWord = false; // 단어의 끝인지 나타내는 플래그
    }

    public boolean containsKey(char ch) {
        return children[ch - 'a'] != null;
    }

    public Node get(char ch) {
        return children[ch - 'a'];
    }

    public void put(char ch, Node node) {
        children[ch - 'a'] = node;
    }
}
```

<br>

- Trie 구현

```java
class Trie {
    Node root;

    public Trie() {
        this.root = new Node();
    }

    // 문자열의 각 단어를 가져와 현재 트리에 존재하는지 검사
    // 없다면 자식노드를 새로 만들어 자식으로 삽입
    public void insert(String word) {
        Node node = this.root; // 항상 루트노드에서 시작
        for (char ch : word.toCharArray()) {
            if (!node.containsKey(ch)) {
                node.put(ch, new Node());
            }
            node = node.get(ch);
        }
        node.isEndOfWord = true;
    }

    // 특정 문자열 검색
    public boolean search(String word) {
        Node node = searchPrefix(word);
        return node != null && node.isEndOfWord;
    }

    // 특정 접두사로 시작하는 문자열이 있는지 확인
    public boolean startsWith(String prefix) {
        Node node = searchPrefix(prefix);
        return node != null;
    }

    private Node searchPrefix(String prefix) {
        Node node = root;
        for (char ch : prefix.toCharArray()) {
            if (!node.containsKey(ch)) {
                return null;
            }
            node = node.get(ch);
        }
        return node;
    }
}
```

## 예시 코드

```java
public static void main(String[] args) {
		Trie trie = new Trie();

		trie.insert("ball");
		trie.insert("bat");
		trie.insert("bear");
		trie.insert("bell");
		trie.insert("bore");
		trie.insert("stack");
		trie.insert("stock");
		trie.insert("stardust");

		System.out.println(trie.search("stick")); // false
		System.out.println(trie.search("stock")); // true
		System.out.println(trie.search("star")); // false
		System.out.println(trie.startsWith("star")); // true
}
```

<br>

## 시간 복잡도

제일 긴 문자열의 길이 L, 총 문자열들의 수를 M이라 할 때

- 생성 시간 복잡도: O(LM)
- 탐색 시간 복잡도: O(L)

<br>

## 장점

- 효율적인 문자열 검색
  - 접두사의 검색을 효율적으로 수행함
  - 문자열 길이와 관계 없이 일관된 시간 복잡도를 가짐
  - 검색 속도가 매우 빠름
- 자동완성
  - 트라이는 특정 접두사로 시작하는 모든 문자열을 찾을 수 있기 때문에 사용자가 입력하는 동안 트라이를 탐색하여 가능한 단어를 제안할 수 있음

<br>

## 단점

- 공간 복잡도

  - 각 노드에서 자식들에 대한 포인터들을 배열로 모두 저장하고 있어 메모리 측면에서 비효율적일 수 있음

<br>

- 참고자료

  - [TWpower's Tech Blog](https://twpower.github.io/187-trie-concept-and-basic-problem)
  - [[자료구조] 트라이 (Trie)](https://velog.io/@kimdukbae/%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%ED%8A%B8%EB%9D%BC%EC%9D%B4-Trie)
  - [Trie Data Structure - javatpoint](https://www.javatpoint.com/trie-data-structure)
  - [[Algorithm] Trie를 Java로 구현해보자!](https://codingnojam.tistory.com/40)

  <br>

- 관련 문제(백준)
  - [5052번: 전화번호 목록](https://www.acmicpc.net/problem/5052)
