# stanford-talk

Uses the [Stanford CoreNLP](http://nlp.stanford.edu/software/corenlp.shtml) to parse and annotate text.

## Usage

Experimental but basic usage is:

```clojure
(process-text "My name is Carin. I love cheese. I live in Cincinnati.")
```

It returns a data structure like:
```clojure
{:token-data
 ([{:sent-num 0, :token "My", :pos "PRP$", :net "O", :lemma "my", :sentiment "Neutral"}
   {:sent-num 0, :token "name", :pos "NN", :net "O", :lemma "name", :sentiment "Neutral"}
   {:sent-num 0, :token "is", :pos "VBZ", :net "O", :lemma "be", :sentiment "Neutral"}
   {:sent-num 0, :token "Carin", :pos "NNP", :net "PERSON", :lemma "Carin", :sentiment "Neutral"}
   {:sent-num 0, :token ".", :pos ".", :net "O", :lemma ".", :sentiment "Neutral"}]
  [{:sent-num 1, :token "I", :pos "PRP", :net "O", :lemma "I", :sentiment "Neutral"}
   {:sent-num 1, :token "love", :pos "VBP", :net "O", :lemma "love", :sentiment "Very positive"}
   {:sent-num 1, :token "cheese", :pos "NN", :net "O", :lemma "cheese", :sentiment "Neutral"}
   {:sent-num 1, :token ".", :pos ".", :net "O", :lemma ".", :sentiment "Neutral"}]
  [{:sent-num 2, :token "I", :pos "PRP", :net "O", :lemma "I", :sentiment "Neutral"}
   {:sent-num 2, :token "live", :pos "VBP", :net "O", :lemma "live", :sentiment "Neutral"}
   {:sent-num 2, :token "in", :pos "IN", :net "O", :lemma "in", :sentiment "Neutral"}
   {:sent-num 2, :token "Cincinnati", :pos "NNP", :net "LOCATION", :lemma "Cincinnati", :sentiment "Neutral"}
   {:sent-num 2, :token ".", :pos ".", :net "O", :lemma ".", :sentiment "Neutral"}]),
 :refs
 [[{:sent-num 0, :token "Carin", :gender "UNKNOWN", :mention-type "PROPER", :number "SINGULAR", :animacy "ANIMATE"}]
  [{:sent-num 0, :token "My", :gender "UNKNOWN", :mention-type "NOMINAL", :number "SINGULAR", :animacy "INANIMATE"}]
  [{:sent-num 0, :token "My", :gender "UNKNOWN", :mention-type "PRONOMINAL", :number "SINGULAR", :animacy "ANIMATE"}
   {:sent-num 1, :token "I", :gender "UNKNOWN", :mention-type "PRONOMINAL", :number "SINGULAR", :animacy "ANIMATE"}
   {:sent-num 2, :token "I", :gender "UNKNOWN", :mention-type "PRONOMINAL", :number "SINGULAR", :animacy "ANIMATE"}]
  [{:sent-num 2, :token "Cincinnati", :gender "NEUTRAL", :mention-type "PROPER", :number "SINGULAR", :animacy "INANIMATE"}]]}
```

where

* :text-data = The data associated with each word token
  * :sent-num = Sentence number
  * :token = Original text
  * :pos = Part of Speech tag.  [Guide for decoding](https://www.ling.upenn.edu/courses/Fall_2003/ling001/penn_treebank_pos.html)
  * :net = Named Entity Tag Annotation: PERSON, LOCATION, ORGANIZATION, MISC, MONEY, NUMBER, ORDINAL, PERCENT, DATE, TIME, DURATION, SET
  * :lemma = [lemma](https://simple.wikipedia.org/wiki/Lemma_(linguistics) for token
  * :sentiment = "Very negative", "Negative", "Neutral", "Positive", or "Very positive"
* :refs = The sentence mentions/references for token in sentences
  * :sent-num = Sentence number
  * :token = The word
  * :gender = Gender of the word if it can be determined
  * :mention-type = PRONOMINAL, NOMINAL, PROPER, LIST
  * :number =  SINGULAR, PLURAL, UNKNOWN
  * :animacy =  ANIMATE, INANIMATE, UNKNOWN (see [animacy](https://en.wikipedia.org/wiki/Animacy))

## License

Copyright © 2015 Carin Meier

Distributed under the Eclipse Public License either version 1.0 or (at
your option) any later version.
