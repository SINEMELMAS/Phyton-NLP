# Phyton-NLP
To find summary of story and analysis it.
import spacy
from textblob import TextBlob
from collections import Counter

nlp = spacy.load("en_core_web_sm")

original_text = input("write a text:")
doc = nlp(original_text)
blob = TextBlob(original_text)
corrected_text = blob.correct()

print(f"Corrected text is: {corrected_text}")

summary = ' '.join([sent.text for sent in doc.sents][:3])
print(f"Summary: {summary}")

words = [token.text for token in doc if token.is_stop != True and token.is_punct != True]
word_freq = Counter(words)
keywords = word_freq.most_common(5)
print(f"Keywords: {keywords}")

sentiment = blob.sentiment
print(f"Sentiment - Polarity: {sentiment.polarity}, Subjectivity: {sentiment.subjectivity}")

entities = list(set([(ent.text, ent.label_) for ent in doc.ents]))

print("Named Entities:")
for entity in entities:
    print(f"{entity[0]} ({entity[1]})")
