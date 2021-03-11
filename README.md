[English Below](#normalisation-component)

# Cydran Normaleiddio
Cydran arbrofol ar gyfer normaleiddio testunau Cymraeg yw hon.

Mae'r gydran yn seiliedig ar spaCy, a bydd angen gosod y feddalwedd honno ynghyd â'r pecyn iaith Cymraeg er mwyn iddo weithio.

Mae'r gydran yn gweithio drwy ddefnyddio eithriadau tocyneiddio spaCy i ddarparu 'norm', neu un ffurf gyson, mewn sefyllfaoedd lle caiff ffurfiau gwahanol eu harddel, er enghraifft drwy newid pob 'ydi' i 'ydy' fel mai'r sillafiad hwnnw a geir yn gyson yn y testun ar gyfer y gair hwnnw.

Gall hyn gynnwys:

* amrywiadau orgraffyddol cydnabyddedig e.e. normaleiddio **ydi** i **ydy**
* amrywiadau llafar e.e. normaleiddio **isio**,**ishe** etc. i **eisiau**
* dadgollnodi e.e. normaleiddio **cer'ed** i **cerdded**, **'rioed** i **erioed**, a **cynta'** i **cyntaf**

Dyma rai brawddegau amrywiol sy'n enghreifftio'r gydran ar waith:

* poeni 'falla bod wbath arall wyt ti, 'lly?  
  *poeni efallai bod rhywbeth arall wyt ti, felly?*

* ydi 'cos ma' hi am raddio 'leni  
  *ydy achos ma' hi am raddio eleni*

* o's 'ishe gadael 'biti deg, 'falle?
  *oes eisiau gadael ambeutu deg, efallai?*

## Gosod
1. Gosodwch y fersiwn ddiweddaru o spaCy 2 (e.e. `pip install spacy==2.3.5`)
2. Gosodwch y pecyn iaith rydym wedi'i ddatblygu ar gyfer spaCy o https://github.com/techiaith/spacy-lang-cy
3. Disodlwch y ffeil `tokenizer_exceptions.py` a geir yn y ffolder `cy` rydych chi newydd ei osod gyda'r un o'r enw yn y storfa hon


## Defnyddio
Dyma'r cod ar gyfer cynhyrchu'r enghreifftiau uchod gan ddefnyddio spaCy:

```
import spacy

def retokenize_norms(doc):
    retokenized_str = ""
    for token in doc:
        if " " in token.text_with_ws:
            retokenized_str = retokenized_str + token.norm_ + " "
        else:
            retokenized_str = retokenized_str + token.norm_
    return retokenized_str
    
nlp = spacy.blank("cy")

texts = ["poeni 'falla bod wbath arall wyt ti, 'lly?",
         "ydi 'cos ma' hi am raddio 'leni",
         "o's 'ishe gadael 'biti deg, 'falle?"]
            
for text in texts:
    doc = nlp(text)
    normalized_text = retokenize_norms(doc)
    
    print (doc.text)
    print (retokenize_norms(doc))
    print ("------------------------------------------")
```

## Rhai Ystyriaethau
### Problem geirffurfiau amwys
Mae'r gydran normaleiddio yn weddol syml ac ni all wahaniaethu ar sail cyd-destun rhwng geirffurfiau sy'n gallu golygu mwy nag un peth. Ceir llawer o eirffurfiau amwys mewn Cymraeg llafar. Dyma rai enghreifftiau:
* 'da (gyda/rydym)
* 'di (wedi, ydi)
* 'na (yna, dyna)
* 'ma (yma, dyma)
* 'se (tasai/petasai)
* sgen (does gen/oes gen)

Gan  mai ar sail tocynnau unigol yn unig y mae'r gydran yn gweithio, nid oes modd defnyddio cyd-destun ehangach y geirffurf i'w normaleiddio yn briodol.

Y datrysiad gorau ar gyfer geirffurfiau amwys fyddai anodi digon o destunau llafar sy'n eu cynnwys, ac yna hyfforddi model sy'n gallu gwahaniaethu rhyngddynt, neu eu tagio'n wahanol fel bod modd gwneud.

Serch hynny, mae hyn yn gam pwysig tuag at hynny. 

### Beth ddylid ei normaleiddio a pa ffurf ddylai fod ar y norm?
Mae angen rhagor o ymchwil arnom i ddeall yn well pa fath o normaleiddio sy'n briodol ar gyfer y Gymraeg, ac a yw hi'n briodol cynnwys sawl math gwahanol o normaleiddio o fewn yr un gydran.

Dyma rai enghreifftiau o fathau gwahanol o normaleiddio:

* Normaleiddio Tafodiaith (mofyn/isio/eisiau), (fo/fe/ef/efe), (llaeth/llefrith)
* Normaleiddio Cywair? (rydw/rwyf/yr ydwyf), (ti,chdi)
* Normaleiddio Colli Geiriau ([fy] 'nghath i)
* Normaleiddio Termau (meicroffon/microffon), (firws,feirws)

Ar hyn o bryd, mae'r gydran yn cynnwys cymysgedd o'r uchod, ond efallai nad yw hynny'n cyd-fynd gyda phob defnydd a ragwelir.

### Mae cryn amrywiaeth o ran ffurfiau anffurfiol
Does dim modd darogan pob ffurf lafar bosib, felly rhaid defnyddio'r gydran hon yn briodol ac yn ofalus, gan ychwanegu ati yn ôl yr angen. 

## Casgliadau
Cydran gychwynnol yw hon, ac fe obeithiwn y bydd ei rhyddhau yn agor trafodaeth ehangach ar y defnydd a'r disgwyliadau o gydrannau normaleiddio er mwyn llywio gwaith datblygu'r dyfodol.

# Normalisation Component
This is an experimental normalisation component for the normalisation of Welsh-language texts.

The normalisation compenent is based on spaCy, and the software and the Welsh language package will both need to be installed for it to work.

The component works by using spaCy tokenisation exceptions to provide a 'norm', or one consistent form, in situations where different forms are adopted, for example by changing each 'ydi' to 'ydy' so that spelling is consitant in the text for that word.

This may include:
* recognized orthographic variations e.g. normalisiation of **ydi** to **ydy**
* verbal variations e.g. normalisiation of **isio**,**ishe** etc. to **eisiau**
* deapostrophising e.g. Normalisiation of **cer'ed** to **cerdded**, **'rioed** to **erioed**, and **cynta'** to **cyntaf**

Here are some miscellaneous sentences that exemplify the component in action:
* poeni 'falla bod wbath arall wyt ti, 'lly?  
  *poeni efallai bod rhywbeth arall wyt ti, felly?*

* ydi 'cos ma' hi am raddio 'leni  
  *ydy achos ma' hi am raddio eleni*

* o's 'ishe gadael 'biti deg, 'falle?
  *oes eisiau gadael ambeutu deg, efallai?*
  
## Installation
1. Install the latest version of spaCy 2 (e.e. `pip install spacy==2.3.5`)
2. Install the Welsh language pack that we have developed for spaCy, found here: https://github.com/techiaith/spacy-lang-cy
3. Replace the `tokenizer_exceptions.py` file in the  `cy` ffolder that you've just placed in spaCy with the one with same name from this repository

## Usage
Here is the code for producing the above examples using spaCy:

```
import spacy

def retokenize_norms(doc):
    retokenized_str = ""
    for token in doc:
        if " " in token.text_with_ws:
            retokenized_str = retokenized_str + token.norm_ + " "
        else:
            retokenized_str = retokenized_str + token.norm_
    return retokenized_str
    
nlp = spacy.blank("cy")

texts = ["poeni 'falla bod wbath arall wyt ti, 'lly?",
         "ydi 'cos ma' hi am raddio 'leni",
         "o's 'ishe gadael 'biti deg, 'falle?"]
            
for text in texts:
    doc = nlp(text)
    normalized_text = retokenize_norms(doc)
    
    print (doc.text)
    print (retokenize_norms(doc))
    print ("------------------------------------------")
```

## Some Considerations
### The problem of ambiguous wordforms

The normalisation component is fairly straightforward and cannot use context to distinguish between wordforms that may correspond to more than one thing. There are many ambiguous words in spoken Welsh. Here are some examples:

* 'da (gyda/rydym)
* 'di (wedi, ydi)
* 'na (yna, dyna)
* 'ma (yma, dyma)
* 'se (tasai/petasai)
* sgen (does gen/oes gen)

As the component only works on a single token basis, it is not possible to use the wider context of the wordform to appropriately normalise it.

The most appropriate solution for dealing with ambiguous wordforms would be to annotate enough texts containing those forms, and then train a model that can distinguish between them, or tag them differently to aid disambiguation. This is an important step towards that goal.

### What should be normalised and what form should the norm take?
We need further research to better understand what type of normalisation is appropriate for the Welsh language, and whether it is appropriate to include several different types of normalisation within the same component.

Here are some examples of different types of normalisation:

* Normalisiation of Dialect (mofyn/isio/eisiau), (fo/fe/ef/efe), (llaeth/llefrith)
* Normalisiation of Register? (rydw/rwyf/yr ydwyf), (ti,chdi)
* Normalisiation of Word Loss ([fy] 'nghath i)
* Normalisiation of Terms (meicroffon/microffon), (firws,feirws)

At present, the component contains a mixture of the above, but this may not coincide with all anticipated uses.

### There is great variety of different colloquial forms
It is not possible to predict all possible colloquial forms, so this component must be used appropriately and carefully, and should be added to as necessary.

## Conclusions
This is an initial fersion of this component. We hope that its release will open a broader discussion on the use and expectations of normalisation components to inform future development.

