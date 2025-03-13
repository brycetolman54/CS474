# Transformers

- The whole idea of a large language model (LLM) is to predict the next word given a sequence of words

- Let's talk about embeddings. These were around before transformers to help us represent words
    - We want a way to represent words that helps us see how similar they are
    - We could do something like a huge vector with one hot encoding
        - The problem is that we can't really find out about the similarity between two things
    - If we represent the words as vectors in however many dimensions as we want, we can then dot product to find the similarity, and do operations to get new words from vectors we already have
- We need our model to transform our embeddings to account for context
    - We do this for a fixed number of steps (the number of times that we redo the attention in our network)
    - We do attention in each layer to update our embedding

## Self attention

- There are three vectors that come from our initial embedding:
    - The <b>Value</b> is simply a linear transformation: $v_n = \beta_v + \Omega_v \x_n$ (no ReLU)
    - The inputs are $N$ words, and there are $N$ outputs that are weighted sums of the attention of each word multiplied by its value
        - These attentions and weights are different for each word because each is different and cares differently about the words around it (their context)
        - For the attention, we have to calculate the <b>Queries</b> and <b>Keys</b>, which are just a linear transformation like that of the <b>Values</b>
            - How do we use the <b>Queries</b> and <b>Keys</b> to get attention?
                - take the dot product of the two and pass them through a softmax for all the words
                - So, this tells us how similar we are to a specific word in the context compared to all the other words in the context
        - After we have found out from the Q and K how much each word cares about each other word, we just multiply the V by this dot-product output to get a new representation
        - We do this with different heads to get multiple outputs of the new V, which we then push into a MLP to combine them in some useful way to represent all the information gathered by all the heads in one new V vector
        - For the dot-product, we can scale the outputs before doing the softmax by dividing them by the square root of the dimensionality
            - This keeps things from getting too large, and works empirically, with no theoretical explanation as of yet
- Positional encoding is important too
    - We know that order is important, so we need to account for it.
    - We just add a vector to the original embedding that uniquely encodes the order
    - We add this to the Q, K, and V vectors


# Flavors of Transformers

- There are different ways to use these transformers

## Encoder (BERT)

- The whole purpose of this is to find a good embedding, that is the product that we are interested in
- We get it to create these embeddings by masking some of the input words and having it predict the probability of those masked words
- Once we have it making good embeddings, we add a new head that looks at those embeddings and does what we want it to
    - Sentiment analysis, entity recognition, etc.

## Decoder (GPT3)

- This is just the latter part, what we talked about above
- Even though we are not doing Encoding-Decoding, we have to do some sort of embedding in order to get vectors we can pass through the model
    - We don't care about making great embeddings, so we don't care what the embeddings we use look like
- We take the embeddings, do all of that above, get out a probability distribution and sample from that to get the next output
    - We add that to the input, then go again until we are done.

## Encoder-Decoder (Machine Translation)

- Where as we have Q and K and V be the same for auto-regression in Decoders, we do something different here
    - We want to generate language according to the other language that we are translating from
    - We make the keys come from the embeddings of the first language (to translate from) (from the Encoder)
    - We make the queries come from the language that we are translating to (from the Decoder)
