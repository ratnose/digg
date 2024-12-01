Att kontrollera ett publikt API
De automatiska testerna* ska vara på den nivå att de ska kunna köras med en periodicitet, så vi snabbt kan upptäcka att API inte svarar eller fungerar som tänkt.

Jag är en testare som är helt övertygad om att tester* och automatiska tester* är två olika saker och båda behvövs för olika saker.
Automatisk tester* är när vi vet vad vi ska få för svar och sätter upp något som kontrollerar att vi får det svaret. 
Det här är det enklaste sättet att automatisera tester* av vad man bygger baserat på kraven. 
Jag skulle dock vilja hävda att detta är ett dyrt sätt att utveckla på. Kostnaden är tid och att inte slösa resurser på onödiga automatiska tester.
För misnta kodändring, måste även testerna ändras...

Jag börjar att läsa in mig på vad det är som ska undersökas.
Sedan stänger ute allt som kan störa mig under 30 min.
Under dessa 30 minuter fokuserar jag på att testa det vi byggt, jag skriver ner precis allt jag hittar, buggar, funderingar och undringar, under denna tid värdesätter jag inte det jag hittar. Tänk brainstorming.

Efter övningen går jag genom och värdesätter allt jag hittat. Jag pratar med de personer som jag behöver prata med efteråt. Buggar i koden, buggar i kraven, buggar i det automatiska testerna*.
Om jag inte förstår varför ett visst beteende uppsått. sättar jag mig med de personer som behövs för att ta reda på vad det är jag sett.
Ex. Det var efter en sådan session jag hittade att det lånesysteme vi byggde avrundade för snävt i början av processen, vilket fick konsekvensker långt senare. 

Det är under dessa sessioner som jag hittat det konstigaste buggarna. Många gånger helt omöjligt att automatisera fram. Och partesta... wow säger jag bara.

Således charmtrollet2 publikt API.
Jag skulle vilja använda mig av Robot Framework.
Istället för att skriva tester på flera olika sätt i olika ramverk.
Får vi skriva tester på samma sätt, i samma ramverk.
Alltså kan jag mha Robot skriva tester för både publiktAPI och frontend.
Vi kan då snabbt komma djupare med ett ramverk än att hålla på med flera olika.
Robot är byggt i Python och du kan skriva tester i Python (är open source).
Men jag skulle gärna se att vi automatiser mha Cucumber och Gherkin.
Det vi kommer bygga ut med tiden är de sk keywords för Gherkin, desto länge vi kommer det arbtet desto mer och snabbare kommer vi kunna skriva testfall som täcker större delar produkten.

Jag tror ni, som jag skulle inse magin att skriva kraven enligt Cucumber dokument formattering. Sedan lägga dokumentet i en mapp, som sedan plockas upp och körs som ett automatisk test. Sista jag jobbade så här, lät vi systemet köra Gherkin testerna på natten och på morgonen när vi kom fanns resultatet i form av bubblor på en skärm. Lunget på morgonen när det bara var gröna bubblor.

Ett exempel:
*** Settings ***
Resource        Digg_keywords.resource

*** Test Cases ***
Test PuliktAPI With BDD Syntax
    Given PubiktAPI Is Running
    When we add a user using json
    Then The Result Should be the json with an "id"

    Given PubiktAPI Is Running
    When we want to be able to limit and divide into pages
    And we add "page 0" and "size 10"
    Then The Result Should be list with 10 users spanning over 0 pages

    Given that digg-front is running
    #Detta får att koppla mot en datafil med 100-tals användare om man vill det
    When the user enters <name> in "name"
    And the user enters <address> in "adress"
    And the user enters <phone> in "phone"
    And the user enters <email> in "email"
    And the user pushes the button "Create"
    Then the system should return the "id" of the new user
    Then all values should be removed  

    Exapmples:
    	| name | address | phone | email |
    	| Mattias Hedman | Ekvägen 19 | 0706102529 | mattias.hedman@me.com |
    	| Kalle Anka | Ankeborgsvägen 12 | 0705556565 | kalle@anka.anka |

Test digg-frontend With BDD Syntax
    Given that digg-front is running
    When the user enters an "id"
    And pushed the button "Delete"
    Then if the id is found
    Then all values should be removed

    Given that digg-front is running
    When the user enters an "id"
    And pushed the button "Delete"
    Then if the id is not found
    Then a "error message 1" should be displayed above the "Delete" button


* Jag vill skilja på automatiska tester och tester.
Krasst skulle jag vilja kalla dom autmatiska kontroller och undersökande tester.
Det som automatiska kontroller möjligör att frigöra tid så människan kan få excellera på det den är bra på. Tänka utanför boxen sas.