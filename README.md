# Code-Similarity-Measurement
This is a code similarity measurement system made by group2.
## 1. System Overview
This system is a tool designed to measure code similarity by integrating lexical analysis, Abstract Syntax Tree (AST) analysis, and a Winnowing-based algorithm. Users can select two Python code files through a graphical user interface (GUI), and the system calculates the following similarity metrics:
1. Combined Similarity: A weighted score combining Token similarity and AST similarity.
2. Winnowing Similarity: A text fingerprinting algorithm based on K-grams and sliding windows.
3. Inter-file Similarity: The similarity of File 1 to File 2 and vice versa.
## 2. Similarity Measurement Methods
1. Token Analysis
The system uses the Pygments library to perform lexical analysis, breaking the code into tokens. Each token is mapped to a single-character category based on its type.
(1) Token Classification: 
Each token is assigned a category based on its type.
Tokens that do not belong to predefined categories are ignored.
(2) Block Creation: 
The code is divided into logical blocks, each containing multiple tokens.
Each block records its tokens and positional information (row and column numbers).
(3)Block Similarity Calculation: 
The SequenceMatcher from difflib is used to compare token sequences or raw strings of two blocks to calculate their similarity
(4)Overall Similarity Scoring: 
The overall Token similarity is computed as the proportion of blocks with similarity scores above a threshold.

2. Abstract Syntax Tree Analysis
The system uses the ast module to parse the code's Abstract Syntax Tree (AST) and extract structural features like function definitions, class definitions, loops, and conditional statements.
(1)AST Parsing: 
The ast.parse method is used to parse the code into an AST. If parsing fails, an empty set is returned.
(2)Feature Extraction: 
The ASTVisitor class traverses the AST and records node types as features.
(3)Similarity Calculation: 
The Jaccard similarity between the feature sets of two codes is calculated

3. Winnowing Algorithm
(1)Text Preprocessing:
The code is treated as plain text and divided into substrings of length K (K-grams).
Default K=5.
(2)Hash Calculation:
A hash value is computed for each K-gram, generating a hash list.
(3)Sliding Window: 
A sliding window of length window_size is applied to the hash list. 
Default window_size = 4.
(4)Minimum Hash Selection: 
The smallest hash value in each sliding window is selected as a fingerprint.
A new fingerprint is recorded only if it differs from the previous one.
(5)Fingerprint Set Comparison: 
The Jaccard similarity of the fingerprint sets of two codes is computed.

## 3. Combined Similarity Calculation
The system combines Token similarity and AST similarity to compute the overall similarity.Users can adjust these weights to modify the contribution of each method in the final combined similarity score.

## 4. Graphical User Interface
1. File Selection:
Users can select two files using the "Browse" button;
The file paths are displayed in corresponding input fields.

2. Parameter Configuration:
Users can set the similarity threshold, with a default value of 0.9.

3. Similarity Analysis:
Clicking the "Analyze Similarity" button starts the similarity calculation.

4. Result Display:
Combined Similarity
Winnowing Similarity
Inter-file similarity scores



