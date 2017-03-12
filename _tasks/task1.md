---
layout: task
title: Zadanie 1
---
V tejto podstránke sa nachádzajú informácie o spôsobe vypracovania zadania. 

# Rozdelenie webovej stránky
Webová stránka je rozdelená na tieto podstránky: 
* **Domov** - na domovskej stránke sú zobrazené najnovšie príspevky z jednotlivých podstránok
* **Projekty** - podstránka pre projekty
* **Osobná galéria** - osobná galéria fotografií
* **Blog** - podstránka pre blogové príspevky
* **Webové publikovanie** - podstránka pre informácie o vypracovaných zadaniach

# Rozloženia
Vo webovej stránke sú použité rôzne rozloženia pre zobrazenie:
* **detailu fotografie** 
* **detailu projektu** 
* **príspevku** 
* **zadania** 
* **základnej štruktúry stránky** 

# Kolekcie
V zadaní sú použité tieto kolekcie: 
* **photos** - na vytvorenie galérie obrázkov
* **projects** - na správu projektov, na ktorých som pracoval
* **blog** - na publikovanie príspevkov do blogu

# Premenné

V rámci zadania boli použité tieto premenné:
* Kolekcia __photos__
	* *src_path* - zdrojová cesta k fotke
	* *title* - nadpis fotografie
	* *tookAt* - dátum vyhotovenia fotky
	* *place* - miesto vyhotovenia fotky
* Kolekcia __projects__
	* *title* - názov projektu
	* *date_from* - dátum od kedy projekt začal
	* *date_till* - dátum do kedy bol projekt vypracovávaný
	* *technologies* - technológie, ktoré boli pri projekte použité
	* *category* - kategória, do ktorej projekt zapadá - buď ngo (neziskové organizácie), school (školské) a work (pracovné), na základe tejto kategórie sú projekty zoskupené v zozname
	* *images*  - táto premenná je pole, ktoré môže obsahovať viaceré náhľady na projekt, pričom každý náhľad obsahuje zdrojovú cestu k obrázku a jeho popis
* Kolekcia __blog__
	* *title* - nadpis príspevku
	* *date* - dátum príspevku
* pri **podstránkach** je použitá premenná _menu_weight_, na základe ktorej sú zoradené podstránky v menu
* pri **include _backToLink.html_**  je použitá premenná *link* a *názov link-u*, ktorý má odkazaovať na zoznam položiek z konkrétnej položky
* pri **include _categoryEvaluation.html_** je použitá premenná *category* a *category_sk*
* pri **include _showMoreButton.html_** je použitá premenná *link* na určenie odkazu, ktorú stránkea sa má zobraziť

# Filtre a tagy

V zadaní používam tieto filtre a tagy: 
* *sort* - na zoradenie podstránok v menu, projektov podľa dátumu
* *reverse* - na opačné zoradenie položiek
* *group_by* - na zoskupenie projektov podľa kategórie
* *limit* - na limitovanie počtu zobrazených položiek pri iterovaní (napr. na zobrazenie len 3 projektov na úvodnej stránke)
* *date_to_string* - na konvertovanie dátumu na dátum s slovným vyjadrením mesiaca 
* *include* - na zahrnutie opakovaných sa častí webovej stránky - napr. _backToLink_ link na vrátenie sa na zoznam položiek, _categoryEvaluation.html_je akoby funckia, ktorá prekladá kategórie z premenných projektov na slovenské názvy (napr. ngo preloží ako neziskové organizácie)
* *for item in items* -  pri vytváraní menu, pri vytváraní zoznamu príspevkov v blogu, náhlade galérie a projektov, pri náhladoch projektu
* *assign* - na priradenie poľa do premennej, aby sme ju mohli na základe nejakej hodnoty zoradiť alebo zoskupiť a potom cez to pole prechádzať
* *if* - na zistenie, či je stránka aktuálne otvorená, aby sme ju v menu mohli odlíšiť od ostatných

# Plugin
V mojej webovej stránke je použitý plugin pre získanie nástenky používateľa na sociálnej sieti Twitter. To to je oficiálna stránka pluginu na [GitHub](https://github.com/rob-murray/jekyll-twitter-plugin). 


