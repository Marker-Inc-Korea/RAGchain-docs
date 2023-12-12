# REDE Search Detector

This class is implementation of REDE, the method for detect knowledge-seeking turn in few-shot setting.
It means, you can detect search (retrieve) intent in dialogues with only few knowledge-seeking turn dialogues.
It contains train function for your custom model, and inference function for detect knowledge-seeking turn.
You will need non-knowledge seeking turn dialogues and few knowledge-seeking turn dialogues.
The detail of this method is described in [paper](https://arxiv.org/pdf/2109.08820.pdf). 
Or you can read [Korean Blog](https://velog.io/@vkehfdl1/Towards-Zero-and-Few-shot-Knowledge-seeking-Turn-Detection-in-Task-orientated-Dialogue-Systems) about it.


# How to Use

## Train

You have to prepare non-knowledge seeking turn dialogues and few knowledge-seeking turn dialogues.
Then, you can find representation formation and train density estimation. Finally, you can find threshold for detect knowledge-seeking turn using validation data.
You need to input [GaussianMixtureModel](https://scikit-learn.org/stable/modules/generated/sklearn.mixture.GaussianMixture.html) from scikit-learn for training density estimation. You can save this model for further inference.

```python
knowledge_seeking_sentences = ['your sentences']
non_knowledge_seeking_sentences = ['your sentences']

detector = RedeSearchDetector()
detector.find_representation_transform(knowledge_seeking_sentences)
detector.train_density_estimation(GaussianMixture(n_components=1), non_knowledge_seeking_sentences)

valid_knowledge_seeking_sentences = ['your sentences']
valid_non_knowledge_seeking_sentences = ['your sentences']
threshold = detector.find_threshold(valid_knowledge_seeking_sentences, valid_non_knowledge_seeking_sentences)
```

## Inference

After training, you can use inference function for detect knowledge-seeking turn like below.

```python
results = detector.detect(['your sentences'])
```

If result is True, it means knowledge-seeking turn. Otherwise, it means non-knowledge-seeking turn.

## Evaluate

You can evaluate your model with two methods. First, put your own test data. Second, use [DSTC11-Track5](https://github.com/alexa/dstc11-track5) dataset using `SearchDetectorEvaluator` instance.

### 1. Put your own test data
```python
test_knowledge_seeking_sentences = ['your sentences']
test_non_knowledge_seeking_sentences = ['your sentences']

precision, recall, f1 = detector.evaluate(test_knowledge_seeking_sentences, test_non_knowledge_seeking_sentences)
```
You can get precision, recall, f1 score by using your own test dataset.

### 2. Use DSTC11-Track5 dataset
```python
evaluator = SearchDetectorEvaluator(detector)
precision, recall, f1 = evaluator.evaluate()
```

You can also get precision, recall, f1 score by using DSTC11-Track5 dataset. 
DSTC11-Track5 dataset is about hotel and restaurant reservation dialogue dataset. Thus, it is not great benchmark for out-of-domain dataset other than hotel and restaurant reservation dialogues.
So, we recommend to use `train` function at `SearchDetectorEvaluator` instance for training with DSTC11-Track5 dataset.
Then, you might get great result.
