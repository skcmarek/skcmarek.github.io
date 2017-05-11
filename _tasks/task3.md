--- 
layout: task 
title: Zadanie 3         
--- 
Cieľom tretieho zadania bolo vytvoriť možnosť vytvorenia prezentácie cez XML a vygenerovaním jej výstupu do formátu HTML a PDF. Medzi jednotlivé body zadania patrilo: 
 
* vytvoriť opis typu dokumentu - pre moje zadanie som si vybral variantu DTD 
* vytvoriť ukážkovú prezentáciu - použil som už vytvorenú prezentáciu na iný predmet, pretože spĺňala demonštračné kritéria 
* navrhnutie základných transformácií XSL 
* konverzia na XHTML - na generovanie xml prezentácie do HTML bol použitý Saxon vo verzii PE 9 
* konverzia na PDF - na generovanie FO bol použitý SAXON vo verzii PE 9, na generovanie PDF bol použitý procesor XEP 
 
V nasledujúcej časti sa nachádza popis DTD dokumentu:  
 
```xml 
<!ELEMENT slides (slide+)> 
<!ELEMENT slide ( (header,content) | (introSec) | (header,text)| (header,unordered) | (header,ordered) | (header,imageSec) | (header, codeSec))*> 
 
<!ELEMENT content EMPTY> 
 
<!ELEMENT introSec (title, author, org?)> 
<!ELEMENT title (#PCDATA)> 
<!ELEMENT author (#PCDATA)> 
<!ELEMENT org (#PCDATA)> 
 
<!ELEMENT header (#PCDATA)> 
 
<!ELEMENT text (para+)> 
<!ELEMENT para (#PCDATA|bold)*> 
 
<!ELEMENT unordered (items)> 
<!ELEMENT ordered (items)> 
<!ELEMENT items (item+)> 
<!ELEMENT item (#PCDATA|bold)*> 
 
 
<!ELEMENT imageSec (image, desc)> 
<!ELEMENT image (#PCDATA)> 
 
<!ELEMENT codeSec (code, desc)> 
<!ELEMENT code (#PCDATA)> 
 
<!ELEMENT desc (#PCDATA)> 
 
<!ELEMENT bold (#PCDATA)> 
 
<!ATTLIST image src CDATA #REQUIRED> 
<!ATTLIST slides font CDATA #IMPLIED> 
<!ATTLIST slides color CDATA #IMPLIED> 
<!ATTLIST slides fontColor CDATA #IMPLIED> 
``` 
 
 
* **slides** - celá prezentácia sa nachádza v elemente slides, ktorý obsahuje viacero elementov **slide** 
* **slide** - v týchto elelemntoch sa nachádzajú jednotlivé slide-y prezentácie. Môžu obsahovať viacero elementov, ktoré definujú typ slide-u. Všetky slide-y majú header, okrem slide-u introSec, a sekciu, do ktorej je možné vkladať konkrétny typ obsahu slide-u.  
* **introSec** - tento element slúži na definovanie úvodného slide-u prezentácie. Nemá **header**, pretože má element **title**, ktorý slúži na definovanie názvu prezentácie, čím je **header** v tomto prípade zbytočný. Ďalej obsahuje elementy **author** na definovanie autora prezentácie a nepovinný **org**, ktorý definuje organizáciu prezentácie 
* **header** - slúži na definovanie nadpisu slide-u 
* **text** - táto sekcia slúži na zadefinovanie slide-u, ktorý obsahuje text. **text** obsahuje element **para**, ktorý slúži na oddelenie odsekov textu.  
* **unordered** - táto sekcia slúži na zadefinovanie slide-u, ktorý obsahuje zoznam s odrážkami, jednotlivé odrážky sa nachádzajú v **items** a definovanie konrétnej odrážky s textom je možné **item**, kotrú **items** obsahuje 
* **orderd** - rovnaký princíp ako **undordered**, no v tomto prípade je zoznam očíslovaný 
* **imageSec** - slide s obrázkom a popisom. Obsahuje **image**, kde sa nastavuje obrázok cez atribút **src** a **desc***, ktorý obsahuje popis obrázka 
* **codeSec** - slide s ukážkou kódu. Obsahuje **code**, ktorý slúži na nastavenie ukážky kódu a **desc** na popis ukážky 
* **bold** - tento element obsahujú viaceré elementy a slúži na zvýraznenie obsahu 
* **atribúty**  
        - **src** - obsahuje cestu k obrázku v elemente **image** 
        - **font** - obsahuje typ písma celej prezentácie 
        - **color** - obsahuje farbu pozadia celej prezentácie 
        - **colorFont** - obsahuje farbu písma celej prezentácie 
 
 
Možnosti prezentácie (tie, ktoré nie su spomenuté pri opise DTD): 
* je nastavená tak, že každý slide je vygenerovaný do zvlášť súboru 
* je možné vygenerovať obsah prezentácie cez element ```html <content/> ``` 
* v prezentácií je možné sa navigovať medzi jednotlivými slide-ami prostredníctvom odkazov *next* a *previous* 
* prezentácia zobrazuje číslo slide-u a celkový počet slide-ov 
* do vstupného súboru je možné vložiť ukážkový kód programovacieho jazyka, ktorý bude v pôvodnom formátovaný zobrazený v ráme slide-u 
* na začiatku je možné cez atribúty do elementu slides nastaviť písmo, farbu pozadia a farbu písma celej prezentácie 
 
Transformácia do HTML: 
* generovanie súborov je vyriešené prostredníctvom  ```xml <xsl:result-document> ```, v ktorom podľa pozície slide-u v strome slide-ov názov výstupného html dokumentu so slide-om 
* na začiatku sú nastavená farba a písmo podľa vstupných atribútov cez ```xml <xsl:attribute name="style"> `` 
* jednotlivé slide-y a ich sekcie sú spracovávané podľa nasledujúcej ukážky:  
 
```xml 
<xsl:template match="slides/slide"> 
  <div id="slide"> 
    <xsl:apply-templates select="header"/> 
    <xsl:apply-templates select="content"/> 
    <xsl:apply-templates select="introSec"/> 
    .... 
 </div> 
 </xsl:template>  
``` 
 
* obsah je generovaný tak, že sa zoberú všetky nadpisy slide-ov, na základe pozície slidov sú vygenerované odkazy pre jeho jednotlivé časti 
* značky *ďalej* a *späť* sú generované na základe pozície aktuálneho slide-u, ak je možné prepnúť do ďaľšieho alebo predchádzajúceho slide-u 
* pre vygenerovanie pätičky každej prezentácie, v ktorej sú informácie o stranách je použité volanie na šablónu, do parametra je nastavená aktuálna pozícia elementa:  
 
```xml 
<xsl:call-template name="footer"> 
      <xsl:with-param name="position" select="count(./preceding-sibling::*)+1"/> 
</xsl:call-template> 
``` 
 
Tranformácia do PDF  
* transformácia funguje na rovnakom princípe ako transformácia do HTML 
* pri transformácií je potrebné najskôr ztransformovať vstupné xml do xml súboru, obsahujúceho Formatting Objects, na základe ktorých je vytvorené PDF 
* členenie textu do zoznamov je robené zavolaním šablóny:  
 
```xml 
 
 <xsl:call-template name="list"> 
      <xsl:with-param name="elements" select="items/item"/> 
      <xsl:with-param name="bullet">bullet char</xsl:with-param> 
      <xsl:with-param name="number" select="false()"/> 
  </xsl:call-template> 
 
``` 
- v parametroch sú nastavené položky, z ktorých ideme robiť zoznam, značka odrážky a tiež hodnota, ktorá slúži na definovanie, či ide o odrážkový zoznam alebo číslovaný. Týmto sme dosiahli to, aby sa pri vytváraní transformácií do zoznamov nemuseli písať transformácie zvlášť 
 
 
 
 