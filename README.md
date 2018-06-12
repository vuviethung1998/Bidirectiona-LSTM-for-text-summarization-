# Bidirectiona-LSTM-for-text-summarization-
A bidirectional encoder-decoder LSTM neural network is trained for text summarization on the cnn/dailymail dataset.

The unprocessed dataset can be downloaded [here](https://cs.nyu.edu/~kcho/DMQA/)

## 1) Word embeddings
Word2vec algorithm [skipgram](https://papers.nips.cc/paper/5021-distributed-representations-of-words-and-phrases-and-their-compositionality.pdf) is used for the encoder input sequence. This is achieved by training a shallow neural network to ro predict context words given a current word. after training the hidden layer is used as the embedding layer. embedding size was kept at 128. skipgram was pre-trained on both the articles and golden summary words.
![Skip-gram model](https://github.com/DeepsMoseli/Bidirectiona-LSTM-for-text-summarization-/blob/master/skip-gram.jpg)

For the decoder input and output, one hot encoding of the summary words was used. vocabulary size was initialy 50k but reduced to 30k due to memory constraints. one hot encoding was also to allow addition of attention layer later. 

## 2) Encoder - decoder LSTM
We use a unidirectional encoder lstm  with state size = 128, dropout=0.2 and a tanh activation.
The Decoder is a bidirectional lstm with size = 128, droput = 0.2 and a softmax ativation.
![BiEnDeLSTM Network](https://github.com/DeepsMoseli/Bidirectiona-LSTM-for-text-summarization-/blob/master/BiEnDeLstm_preview.jpeg)

## 3) Attention Layer
An attention layer between the encoder and decoder over the source sequence's hidden states. as the skipgram embedding and the one-hot vector sizes arent the same, pca over embedding to allow multiplication with one-hot vectors to get attention weights and vectors. final prediction of output word in decoder sequence is done by the attention layer. It helps allow the decoder individual encoder state information. *(forgive the figure below if unclear or messy)* 
![BiEnDeLSTM + Attention mechanism](https://github.com/DeepsMoseli/Bidirectiona-LSTM-for-text-summarization-/blob/master/BiEnDeLstmAttention.jpg)

## 4) Training

## 5) Results

# References
1. Bahdanau, Dzmitry, Kyunghyun Cho, and Yoshua Bengio. [Neural machine translation by jointly learning to align and translate](https://arxiv.org/abs/1409.0473)
2. Zixiang Ding, Rui Xia, Jianfei Yu, Xiang Li and Jian Yang. [Densely Connected Bidirectional LSTM with Applications to Sentence Classification](https://arxiv.org/abs/1802.00889)
