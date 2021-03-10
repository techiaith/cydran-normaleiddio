[English Below](#normalisation-component)

# Cydran Normaleiddio
Cydran arbrofol ar gyfer normaleiddio testunau Cymraeg yw hon.

Mae'r gydran yn seiliedig ar spaCy, a bydd angen gosod y feddalwedd honno ynghyd â'r pecyn iaith Cymraeg er mwyn iddo weithio.

Mae'r gydran yn gweithio drwy ddefnyddio eithriadau tocyneiddio spaCy i ddarparu 'norm', neu un ffurf gyson, mewn sefyllfaeodd lle caiff ffurfiau gwahanol eu harddel, er enghraifft drwy newid pob 'ydi' i 'ydy' fel mai'r sillafiad hwnnw a geir yn gyson yn y testun ar gyfer y gair hwnnw.

Gall hyn gynnwys:

* amrywiadau orgraffyddol cydnabyddedig e.e. normaleiddio **ydi** i **ydy**
* amrywiadau llafar e.e. normaleiddio **isio**,**ishe** etc. i **eisiau**
* dadgollnodi e.e. normaleiddio **cer'ed** i **cerdded**, **'rioed** i **erioed**, a **cynta'** i **cyntaf**

Dyma rai brawddegau amrywiol sy'n enghreifftio'r gydran ar waith:

* poeni 'falla bod wbath arall wyt ti, 'lly?  
  *poeni efallai bod rhywbeth arall wyt ti, felly?*

* ydi 'cos ma' hi am raddio 'leni  
  *ydi achos ma' hi am raddio eleni*

* o's 'ishe gadael 'biti deg, 'falle?
  *oes eisiau gadael ambeutu deg, efallai?*



Dyma'r cod ar gyfer cynhyrchu'r enghreifftiau hyn gan ddefnyddio spaCy:

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
Mae'r gydran normaleiddio yn weddol syml ac ni all wahaniaethu ar sail cyd-destun rhwng geirffurfiau sy'n gallu golygu mwy nag un peth. Ceir llawer o eirffurfiau amwys mewn Cymreag llafar. Dyma rai enghreifftiau:
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
Mae angen rhagor o ymchwil arnom i ddeall yn well pa fath o normaleiddio sy'n briodol ar gyfer y Gymraeg, ac a yw hi'n briodol cynnwys sawl math gwahanol o normaleiddio o fewn y run gydran.

Dyma rai enghreifftiau o fathau gwahnol o normaleiddio:

* Normaleiddio Tafodiaith (mofyn/isio/eisiau), (fo/fe/ef/efe), (llaeth/llefrith)
* Normaleiddio Cywair? (rydw/rwyf/yr ydwyf), (ti,chdi)
* Normlaeiddio Colli Geiriau ([fy] 'nghath i)
* Normaleiddio Termau (meicroffon/microffon), (firws,feirws)

Ar hyn o bryd, mae'r gydran yn cynnwys cymysgedd o'r uchod, ond efallai nad yw hynny'n cyd-fynd gyda phob defnydd a ragwelir.

### Mae creadigrwydd y Cymry yn ddiderfyn
Does dim modd darogan pob ffurf lafar bosib, felly rhaid defnyddio'r gydran hon yn briodol ac yn ofalus, gan ychwanegu ati yn ôl yr angen. 

## Casgliadau
Cydran gychwynnol yw hon, ac fe obeithiwn y bydd ei rhyddhau yn agor trafodaeth ehanach ar y defnydd a'r disgwyliadau o gydrannau normaleiddio er mwyn llywio gwaith datblygu'r dyfodol.

# Normalisation Component
This is an experimental normalisation component for the normalisation of Welsh-language texts.

It is based on spaCy, and the requires that the software and the Welsh language package be installed for it to work.

