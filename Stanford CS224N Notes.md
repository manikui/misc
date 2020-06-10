# Stanford CS224N: NLP with Deep Learning

## Lecture 1
- We want to represent the meaning of a word
    - Meaning: the idea that is represented by a word, signifier vs. signified
- Usable meaning in a computer: use WordNet, a thesaurus containing lists of synonym sets and hypernyms ("is a" relationships): ```from ntlk.corpus import wordnet```
    - Problems: great as a resource but missing nuance (proficient as a synonym for good), missing new meanings of words (slang), subjective, requires human labor, can't compute word similarity as it has fixed synonym sets
- Traditional NLP: we regard words as just words, discrete symbols - a localist representation where words are represented as one-hot vectors
    - Language has a lot of vocabulary: huge vector dimension
    - We want to understand relationships in the meaning of words e.g. search for "Seattle motel" should match with "Seattle hotel" $\rightarrow$ traditional NLP would have these two vectors as orthogonal, no natural notion of similarity when you have one-hot vectors
        - Could rely on WordNet's list of synonyms but this could fail due to incompleteness or size
    - Solution: learn to encode similarity in the vectors themselves
- Representing words by their **context**: distributional semantics
    - A word's meaning is given by the words that frequently appear close-by
    - If you can explain what context is correct for a certain word, then you understand the meaning of the word
    - When a word $w$ appears in a text, its context is the set of words that appear nearby within a fixed-size window
    - Use the many contexts of $w$ to build up a representation of $w$
- Word vectors: instead of having spare one-hot vectors, we will build dense vectors for each word, chosen so that it is similar to vectors of words that appear in similar contexts - a distribution representation. It will be of a smaller dimension
- Word2vec algorithm: a framework for leaning word vectors
    - We have a large corpus of text. Every word in a fixed vocabulary is represented by a vector. Go through each position $t$ in the text, which has a center word $c$ and context ("outside") words around it $o$
    - Use the similarity of the word vectors for $c$ and $o$ to calculate $P(o | c)$. Keep adjusting the word vectors to maximize this probability
    - Eventually you'll get a word vectors space with distance as a measure of similarity
    - Likelihood $L(\theta) = \Pi_{t = 1}^T \Pi_{-m \leq j \leq m; j \neq 0} P(w_{t + J} | w_t; \theta)$
    - Objective function $J(\theta) = -\dfrac{1}{T} \sum_{t = 1}^T \sum_{-m \leq j \leq m; j \neq 0} \log P(w_{t+j}|w_t; \theta)$
    - Calculate $P(w_{t+j}|w_t; \theta)$ using two vectors per word: $v_w$ when $w$ is the center word and $u_w$ when $w$ is a context word
    - For a center word $c$ and a context word $o$: $P(o|c) = \dfrac{\exp(u_o^Tv_c)}{\sum_{w \in V} \exp(u_w^Tv_c)}$, an example of the softmax function that maps arbitrary values $x_i$ to a probability distribution $p_i$
    - $u_o^Tv_c$ is a measure of similarity between $o$ and $c$ where larger dot product means more similarity and thus larger probability
    - $\sum_{w \in V} \exp(u_w^Tv_c)$ normalizes over entire vocabulary to give probability distribution
    - Optimize using $\theta = \left [v_{\text{aardvark}}, ..., v_{\text{zebra}}, u_{\text{aardvark}}, ..., y_{\text{zebra}} \right ]$. Thus, $\theta \in \mathbb{R}^{2dV}$ for $d$-dimensional vectors and $V$ words
    - $\dfrac{\partial}{\partial v_c} \log P(o | c) = u_o - \sum_{x = 1}^V P(x | c) u_x = u_o - E[x | c]$

## Lecture 2
- Word vector space also has a notion of vector composition, or analogy: "king" vector - "man" vector + "woman" vector = "queen" vector $\rightarrow$ king:man as is queen:woman; australia:beer as is france:champange
- Word2vec aims to provide a reasonably high probability estimate to all words that occur in the context
- Word2vec maximizes objective function by putting similar words nearby in space
- Need to use stochasitc gradient descent as the objective is a function of all windows in the corpus, making it expensive to compute
    - Take a minibatch of words from the corpus and compute the gradient on those
    - End up with a sparse gradient vector as you are only selecting a few words from the entire corpus at each iteration
        - Solution: either use sparse matrix updates to only update certain rows of full embedding matrices U and V, or keep around a hash for word vectors
- Can also capture co-occurence counts: fill a co-occurence matrix X using a window around each word type (word token - fruits instead of a specific fruit), counting up the number of times each word appears within that window
    - X is symmetric and sparse
    - Can measure similarity directly using the counts
    - Problems: X becomes huge with vocabulary increases, sparsity
    - Solution: low rank approximation using SVD that preserves most of the information
- Evaluating word vectors: intrinsic vs. extrinsic
    - Intrinsic: are you guessing the right part of speech? Are you returning the correct synonyms? Evaluation on a specific/intermediate subtask, fast to compute, helps to understand that system
    - Extrinsic: evaluation on a real task (some application that human beings use like web search or phone dialogue), can take a long time to compute accuracy, unclear if the subsystem is the problem or its interaction or other subsystems
- Intrinsic word vector evaluation
    - Word vector analogies: a:b :: c:?
    - Word vector distances and their correlation with human judgements
    - Evaluation word sense: the different contexts and meanings of a word: cluster word windows around words, retrain with each word assigned to multiple different clusters
        - Different sense of a word reside in a linear superposition (weighted sum) in different word embeddings
        - $v_{\text{pike}} = \alpha_1 v_{\text{pike}, 1} + \alpha_2 v_{\text{pike}, 2}$
        - Where $\alpha_i = \dfrac{f_i}{\sum_{j}f_j}$ for frequency $f$

## Lecture 3
- Softmax Classifier: $P(y|x) = \dfrac{\exp(W_y x)}{\sum_c \exp(W_c x)}$
    - Essentially 2 steps: Take the ith row of $W$ and multiply that row with $x$ for all classes, then apply the softmax function with the normalization $\sum_c \exp(W_c x)$ to get a probability
- For each training example $(x, y)$, our objective is to maximize the probability of the correct class $y$
    - Corresponds to: $\max P(y|x) = \max \log(P(y|x)) = \min - \log(P(y|x))$
- Cross entropy loss: for true probability distribution $p$ and computed probability distribution $q$, $H(p, q) = - \sum_c P(c) \log(q(c))$
    - The true probability distribution for some point takes the form: $p = [0, ..., 0, 1, 0, ..., 0]$. Thus, plugging this into the cross-entropy loss yields a single non-zero term: the negative log probability of the true class
    - $H(p, q) = -\log P(y|x)$
- NLP deep learning:
    - Learn both weights $W$ and word vectors $x$
    - Learn both conventional parameters and word representations
    - The word vectors re-represent one-hot vectors - move them around in an intermediate layer vector space
- The loss function directs what the intermediate hidden variables should be, so as to do a good job at predicting the targest for the next layer, etc.
- Neural networks require non-linear functions like sigmoid as with just linear functions, the networks can't model anything more than a linear transformation
    - With more layers and non-linear functions, neural nets can approximate more complex functions
- Named Entity Recognition (NER): finding and classifying names in text (organizations, places, people)
    - Predict entities by classifying words in context (like Word2vec) and then within those extracted entities, combine them into subsequences
        - Problems: boundaries of entity, hard to know if something is an entity ("Future School"), class of unknown/novel entity
- We want to build classifiers of language that work inside a context window of neighboring words
    - Simple solution: average the word vectors in a window and then classify the average vector
        - Problem: loses position information
    - Another solution: train softmax classifier to classify a center word by taking the concatenation of word vectors surrounding it in a window
        - Treat all windows without a named entity in its center as "corrupt"
        - Want a system that returns a high score if there is a named entity at the center 
        - All the neural net does is return an unnormalized score for all combinations of concatenated word vectors
        - The middle layer in the neural net learns non-linear interactions between the input word vectors
        - Whole neural net: $x$ (input: concatenation of word vectors) $\rightarrow h = f(Wx + b) \rightarrow s = u^Th$
        - Example gradient: $\dfrac{\partial s}{\partial b} = \dfrac{\partial s}{\partial h} \dfrac{\partial h}{\partial z} \dfrac{\partial z}{\partial b}= h^T \text{diag}(f'(z)) I = h^T \circ f'(z)$ 
        - Similarly, $\dfrac{\partial s}{\partial W} = \dfrac{\partial s}{\partial h} \dfrac{\partial h}{\partial z} \dfrac{\partial z}{\partial W}$. The first two terms in the chain rule are the same
        - We consider this repetition of gradients as the local error signal $\delta$, the computations in the neural net that are above where $W$ and $b$ are
        - Just compute error signal once, reuse when computing lower-level partial derivatives
        - $\delta = \dfrac{\partial s}{\partial h} \dfrac{\partial h}{\partial z} = h^T \circ f'(z)$
        - Thus: $\dfrac{\partial s}{\partial W} = \dfrac{\partial s}{\partial h} \dfrac{\partial h}{\partial z} \dfrac{\partial z}{\partial W}= \delta \dfrac{\partial z}{\partial W} = \delta^T x^T$

## Lecture 4


