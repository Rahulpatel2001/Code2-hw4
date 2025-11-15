# Code2-hw4
Rahul kuduru 700763240

import spacy
This imports the spaCy NLP library, which provides tokenization, entity recognition, POS tagging, and more.
You must install spaCy before running this (pip install spacy).

def run_ner_and_pronoun_check(text: str):
Creates a function named run_ner_and_pronoun_check.
It accepts one argument: text, which is the sentence you want to analyze.

nlp = spacy.load("en_core_web_sm")
Loads the small English model.
This model contains:
Tokenizer
POS tagger
Named Entity Recognizer
This step is required before any spaCy processing.

doc = nlp(text)
Runs the entire spaCy pipeline on the input text.
The result doc contains:
Tokens
POS tags
Named entities
Lemmas
You can loop through doc to analyze the sentence.

print("Named Entities:")
if doc.ents:
    for ent in doc.ents:
        print(f" - {ent.text} [{ent.label_}]")
doc.ents gives a list of all detected named entities (people, organizations, places, products, etc.).
ent.text → the actual text of the entity
ent.label_ → the category/type (e.g., PERSON, ORG, GPE, PRODUCT)
Example:
Chris [PERSON]
Alex [PERSON]
Apple [ORG]
California [GPE]
iPhone [PRODUCT]

pronouns = {"he", "she", "they"}
Creates a set of pronouns.
The code will check if any of these appear in the text.
Lowercase is used because the check is case-insensitive.

detected = [token.text for token in doc if token.text.lower() in pronouns]
Loops through every token (word) in the text.
Converts each token to lowercase (token.text.lower()).
Checks if it's in the pronoun set.
If yes, it adds that pronoun to the list detected.

example:
detected = ["He"]

if detected:
    print("\nWarning: Possible pronoun ambiguity detected!")
    print("Detected pronouns:", ", ".join(detected))
If the text contains “he”, “she”, or “they”, ambiguity may exist.

Ambiguity means:
The pronoun might refer to multiple different people.
Example:
"He told him…"
→ There is no clear way to know if “He” is Chris or Alex.

Output:
Warning: Possible pronoun ambiguity detected!
Detected pronouns: He

Example input
text = "Chris met Alex at Apple headquarters in California. He told him about the new iPhone launch."
Your test sentence.
Contains people, organizations, products, and one ambiguous pronoun.

run_ner_and_pronoun_check(text)
Calls the function.
Runs NER + pronoun check.
Prints both results.
