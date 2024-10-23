# Trie

## 208. Implement Trie (Prefix Tree)

### Problem
A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

Trie() Initializes the trie object.
void insert(String word) Inserts the string word into the trie.
boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

### Pseudocode and explanation

A Trie, or prefix tree, is an efficient data structure for storing and searching strings. Here's how we can implement it:

1. Create a TrieNode class:
   - Each node will have:
     - An array or map to store child nodes (one for each possible character)
     - A boolean to mark if it's the end of a word

2. Implement the Trie class with the following methods:

   a. insert(word):
      - Start from the root
      - For each character in the word:
        - If the character doesn't exist, create a new node
        - Move to the next node
      - Mark the last node as the end of a word

   b. search(word):
      - Start from the root
      - For each character in the word:
        - If the character doesn't exist, return false
        - Move to the next node
      - Return true if the last node is marked as the end of a word

   c. startsWith(prefix):
      - Start from the root
      - For each character in the prefix:
        - If the character doesn't exist, return false
        - Move to the next node
      - Return true (we've found all characters of the prefix)

Pseudocode:

``` python
Class Trie:
    def __init__(self):
        self.root = {}

    def insert(self, word):
        node = self.root
        for char in word:
            if char not in node:
                node[char] = {}
            node = node[char]
        node['$'] = True

    def search(self, word):
        node = self.root
        for char in word:
            if char not in node:
                return False
            node = node[char]
        return '$' in node 

    def startsWith(self, prefix):
        node = self.root
        for char in prefix:
            if char not in node:
                return False
            node = node[char]
        return True
```
