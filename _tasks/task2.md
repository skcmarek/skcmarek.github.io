---
layout: task
title: Zadanie 2
---
Predmetom zadania 2 bolo pretvorenie bakalárksej práce zo súčasného formátu (v mojom prípade LaTeX) na formát DocBook. 

Pri vypracovaní zadania som použil tieto DocBook elementy: 

* **bookinfo** - na zapísanie metadát k bakalárskej práci, ktoré sú pri výstupe použité na titulnú stranu a anotáciu
* **abstract** -  na zapísanie anotácie v angličtine a slovenčine
* **para** - na zapísanie textu do odsekov
* **chapter** - na členenie do kapitol a podkapitol
* **emphasis** - na zvýraznenie textu kurzívov
* **emphasis s atribútom role="strong"** - na zvýraznenie textu
* **programlisting** - na ukážku HMTL štruktúry
* **itemizedlist** - na členenie textu do odrážok
* **xref** - na odkazy na iné časti dok. alebo na referencie na literatúru
* **indexterm** - na indexovanie dokumentu
* **footnote** - na poznámku pod čiarou
* **bibliogrpahy** - na vytvorenie bibliografie
* **mediaobject - imageobject - imagedata** -na vloženie obrázkov
* **indexterm** - na vytvorenie registru pojmov

Pre bibliografické odkazy som použil nasledovnú štruktúru: 

```xml
	<biblioentry id="">
	   <authorgroup>
	       <author></author> 
	       <author></author> 
	   </authorgroup>
	   <title></title>
	   <isbn></isbn>
	   <publisher>
	      <publishername>/publishername>
	   </publisher>
	   <edition></edition> 
	   <pubdate></pubdate>
	</biblioentry>
```

Pre metádáta na úvodnej stránke boli do šablóny **book.titlepage.before.version** pridané bloky pre študijný program, miesto vypracovania, študijný odbor a dátum. 

Pre problémy s rozdelením slova Bratislava na titulnej strane, bola v thesis.xsl prekrytá šablóna book.titlepage.before.recto s nastavením atribútu bloku _hyphenate="false"_


Obsah som vygeneroval pre jednotlivé kapitoly a obrázky. Aby nástroj generoval aj obsah figúr musel som upraviť parameter v súbore **thesis.xls**:

```xml
	<xsl:param name="generate.toc">
		book      title,toc,figure
	</xsl:param>
```



