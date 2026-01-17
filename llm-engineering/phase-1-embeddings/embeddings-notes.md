# Embeddings: Session Notes

What we covered in this session on embeddings.

---

## What is a Vector?

A vector is an ordered list of numbers that represents a position or direction.

- **1D**: Single number → point on a line
- **2D**: Two numbers `[3, 5]` → point on a grid, arrow from origin
- **3D**: Three numbers `[3, 5, 100]` → point in 3D space
- **384D**: 384 numbers → same concept, just can't visualize

**Physics definition:** A quantity with magnitude (size) and direction.

**Math definition:** An ordered list of numbers (n-tuple) that can be added and scaled.

The list of numbers encodes both direction (which way the arrow points) and magnitude (how long).

---

## What are Embeddings?

Embeddings represent meaning as vectors. A word's meaning becomes a point in high-dimensional space.

- "dog" → `[0.2, -0.5, 0.8, 0.1, ...]` (hundreds of numbers)
- "puppy" → `[0.21, -0.48, 0.79, 0.12, ...]` (similar numbers)

**Key insight:** Words with similar meanings end up with similar vectors (pointing in similar directions).

---

## How "Nearby" Works

Finding similar meanings = measuring distance between vectors.

**Cosine similarity** (most common):
- Measures the angle between two arrows
- Ignores length, just compares direction
- Returns -1 to 1:
  - **1** = identical direction (same meaning)
  - **0** = perpendicular (unrelated)
  - **-1** = opposite directions

```python
def cosine_similarity(a, b):
    dot_product = sum(x * y for x, y in zip(a, b))
    magnitude_a = sqrt(sum(x**2 for x in a))
    magnitude_b = sqrt(sum(x**2 for x in b))
    return dot_product / (magnitude_a * magnitude_b)
```

---

## How Embeddings are Learned

Embeddings are learned, not calculated by formula. They emerge from training.

### The Core Insight (Distributional Hypothesis)

"You shall know a word by the company it keeps."

Words that appear in similar contexts have similar meanings:
- "I took my ___ for a walk" → dog, puppy, hound all fit
- Words that fit the same blanks end up with similar vectors

### The Training Process

1. **Start:** Assign random vectors to every word (garbage numbers)
2. **Task:** Predict missing words from context ("The ___ barked loudly")
3. **Evaluate:** Model guesses wrong (at first)
4. **Nudge:** Adjust vectors slightly to improve the guess
5. **Repeat:** Billions of times across billions of sentences

After training, words that appeared in similar contexts have similar vectors.

### What's a "Nudge"? (Gradient Descent)

The model needs to know which direction to adjust each number.

**Calculus gives us the slope** - which way is "downhill" (less error).

1. Current vector: `[0.50, 0.30]`
2. Gradient (slope) says: "error increases if you go `[+0.1, -0.2]`"
3. Go opposite direction: `[-0.1, +0.2]`
4. New vector: `[0.49, 0.32]` → slightly less error

Repeat billions of times → vectors that make good predictions.

---

## What Do Dimensions Mean?

We don't fully know. Each dimension isn't a clean feature like "is_animal" or "size".

Dimensions are learned, not designed. Some research shows certain directions capture:
- Gender (king → queen similar to man → woman)
- Tense (walk → walked similar to run → ran)

But it's fuzzy. Meaning emerges from the combination of all dimensions.

**Analogy:** Like RGB for colors. No single number is "blueness" - it emerges from `[0, 50, 255]` together.

---

## Getting Embeddings (Practical)

### API Call

```python
from openai import OpenAI
client = OpenAI()

response = client.embeddings.create(
    input="dog",
    model="text-embedding-3-small"
)
vector = response.data[0].embedding  # 1536 numbers
```

### Local (Free)

```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')
vector = model.encode("dog")  # 384 numbers
```

### Common Models

| Provider | Model | Dimensions |
|----------|-------|------------|
| OpenAI | text-embedding-3-small | 1536 |
| OpenAI | text-embedding-3-large | 3072 |
| Local | all-MiniLM-L6-v2 | 384 |

---

## Semantic Search

Search by meaning, not keywords.

**Keyword search:** "dog" only finds documents with "dog"

**Semantic search:** "dog" finds "puppy", "canine", "golden retriever"

### How it Works

1. Convert query to vector
2. Compare to all stored document vectors (cosine similarity)
3. Return highest similarity matches

```python
def semantic_search(query, documents):
    query_vector = model.encode(query)
    similarities = [cosine_similarity(query_vector, doc_vec) for doc_vec in documents]
    return top_matches
```

This is the foundation of RAG (Retrieval Augmented Generation).

---

## Key Takeaways

1. **Embeddings = meaning as vectors** in high-dimensional space
2. **Similar meanings = nearby vectors** (small angle between arrows)
3. **Learned, not designed** - emerge from predicting words in context
4. **Gradient descent** - calculus tells us which way to nudge to reduce error
5. **Semantic search** - find by meaning, not keywords

---

## Resources

- Notebook: [embeddings-exploration.ipynb](embeddings-exploration.ipynb)
- Next: Build a semantic search tool (Phase 1 project)
