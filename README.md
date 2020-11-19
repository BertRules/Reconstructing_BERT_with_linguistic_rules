# Reconstructing_BERT_with_linguistic_rules


## Load Data
you can load the data with the following python code:
```
import json
import glob
path = '\\example_folder\\' # replace with data folder
filenames = glob.glob(path+"*.json")
data = dict()
for filename in filenames:
    key = filename.split('\\')[-1].split('.json')[0]
        data[key] = json.load(open(filename,'r'))
```

## Data Description
The predicted token labels (BIO labeling schema) of BERT for aspect term and sentiment term detection are given by:
```
laptop_BERT_predictions_aspect.json
restaurant_BERT_predictions_aspect.json
laptop_BERT_predictions_sentiment.json
restaurant_BERT_predictions_sentiment.json
```

The labels of NLP building blocks for tags are given by:
```
laptop_NE.json
laptop_POS.json
laptop_SYNSET.json
restaurant_NE.json
restaurant_POS.json
restaurant_SYNSET.json
```

The labels of NLP building blocks for relations are given by:
```
laptop_COREF.json
laptop_DEP.json
laptop_PROX.json
laptop_SRL.json
restaurant_COREF.json
restaurant_DEP.json
restaurant_PROX.json
restaurant_SRL.json
```

The labels of aspect terms and sentiment terms based on the rules of the first iteration of rule extraction are given by:
```
laptop_ASP.json
restaurant_ASP.json
laptop_SENT.json
restaurant_SENT.json
```

The tokens of the considered sentences are given by
```
laptop_tokens.json
# Note: Due to licence restrictions, the tokens for restaurants (restaurant_tokens.json) cannot be provided.
```

## Data Example
By the following short example, we want to illustrate the mappings between the data of tokens, BERT's predictions and labels of NLP building blocks and of classes from the first iteration of rule extraction.

Consider the tokens of the 19-th sentence of the laptop dataset:
```
>>> data['laptop_tokens']['19']
['On', 'top', 'of', 'all', ',', 'its', 'pricey', '.']
# The 6-th token in this sentence is 'pricey' (note that the index starts at 0 -> data['laptop_tokens']['19'][0] = 'On')
```

The predictions of BERT for these tokens can be found by
```
>>> data['laptop_BERT_predictions_sentiment']['19']
['O', 'O', 'O', 'O', 'O', 'O', 'B', 'O']
# The 6-th token 'pricey' is predicted as 'B' by BERT (indicating the "B"eginning token of a sentiment term)
```

The POS tag labels for these tokens can be found by
```
>>> data['laptop_POS']['19']
['POS_IN', 'POS_NN', 'POS_IN', 'POS_DT', 'POS_,', 'POS_PRP$', 'POS_JJ', 'POS_.']
# The 6-th token 'pricey' has POS tag label 'JJ' (indicating an adjective)
```

The DEP relation labels for these tokens can be found by
```
>>> data['laptop_DEP']['19']
[{'DEP_case': {'id_tok_1': 0, 'id_tok_2': 1}},
 {'DEP_obl': {'id_tok_1': 1, 'id_tok_2': 6}},
  {'DEP_case': {'id_tok_1': 2, 'id_tok_2': 3}},
  {'DEP_nmod': {'id_tok_1': 3, 'id_tok_2': 1}},
  {'DEP_punct': {'id_tok_1': 4, 'id_tok_2': 6}},
  {'DEP_nmod:poss': {'id_tok_1': 5, 'id_tok_2': 6}},
  {'DEP_root': {'id_tok_1': 6, 'id_tok_2': -1}},
  {'DEP_punct': {'id_tok_1': 7, 'id_tok_2': 6}}]
# For example, the 6-th token 'pricey' has the DEP relation label 'nmod:poss' to the 5-th token 'its'
```

The DEP relation labels for these tokens can be found by
```
>>> data['laptop_SENT']['19']
['OP_O', 'OP_O', 'OP_O', 'OP_O', 'OP_O', 'OP_O', 'OP_A', 'OP_O']
# The 6-th token 'pricey' has sentiment term label 'A' (indicating a sentiment term; 'O' indicates no sentiment term)
```


