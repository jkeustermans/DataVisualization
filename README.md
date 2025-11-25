# Data Visualization – Projectvoorstel

# Inhoudsopgave
1. Logboek
    - Week 1
    - Week 2 (To Do)
    - Week 3 (To Do)
    - Week 4 (To Do)
    - Week 5 (To Do)
2. Projectvoorstel
3. Gebruikte Data-Sets
    - Consumptie Antibiotica
    - Bevolkingsdichtheid
    - 65 plussers
    - Activiteitsgraad
    - Gemiddeld inkomen per inwoner
    - Opleidingsniveau
    - TopoJSON
4. Gebruik AI en bronnen
5. Technisch/Implementatie
    - Opzet choropleth en TopoJSON
    - Kleurenblindhied
6. Initieel Projectvoorstel

## Logboek

### Week 1
Tijdens week 1 zijn de volgende zaken geïmplementeerd:
* Prototype van een kaartje die de gemeentes in België weergeeft
  * Algemeen
    * Het genereren van een Chloropeth was een onbekend aspect in het project. Alhoewel ik geen fundamentele problemen voorzag leek het me het veiligste om deze 'technical debt' naar voor te trekken in het ontwikkelproces. De last van het uitzoeken van deze techniciteit is (deels) opgelost.
  * Implementatie
    * Alle gemeentes van België worden afgebeeld via een Choropleth
    * De inkleuring berust voorlopig op mock-data
  * To Do/Optimalisaties
    * Beperken van het afbeelden van gemeentes tot het Vlaamse grondgebied
    * Opvullen met reële data afkomstig uit de data-sets
    * Kleurenweergave dient aangepast te worden zodat de kleuren onderscheiden kunnen blijven worden voor mensen die leiden aan een van de verschillende vormen van kleurenblindheid
* Prototype scatterplot
  * Algemeen
    * Ook hier is er geopteerd om de een prototype te implementeren omdat er (kort) diende uitgezocht te worden hoe een scatterplot via Seaborn geïmplementeerd diende te worden. Ook hiermee is een andere pure techniciteit van de baan
  * Implementatie
    * Er wordt gebruik gemaakt van de Seaborn library
    * De scatterplot is heel erg eenvoudig qua layout
    * Er wordt enkel mock-data getoond
  * To Do/Optimalisaties
    * Opvullen met reële data uit de data-sets
    * Opzoeken en toepassen layout verbeteringen puur vanuit data-visualisatie perspectief
      * Te gebruiken bron: Fundamentals of Data Visualization - A Primer on Making Informative and Compelling Figures (Clause O. Wilke, 2019)
* Data Ingestion van Individuele Data-Sets
  * Algemeen
    * Bedoeling was om een eerste versie van de code te schrijven voor het inladen van een enkelvoudige data-set, de gegevens te controleren en te transformeren. Op deze manier: 
      * Kunnen we er zeker van zijn dat de gegevens voldoen aan een minimaal aantal eisen voor de verdere verwerking. De bedoeling is om een aantal potentieel onvoorspelbare zaken uit te sluiten tijdens de verdere verwerking (vb. een gemeente waar een jaar aan data ontbreekt)
      * Maken we onderscheid tussen raw-data en een opgeschoonde (clean) data. Indien er later nog extra cleanup of transformaties dienen te gebeuren dan kan er altijd naar deze data-frame variable worden verwezen. We breiden de transformaties/cleanup dan uit in deze voorziene sectie terwijl we de variabele naam behouden. In onze verdere codebase is er dus geen impact
      * Wordt er een 'standaard structuur' voorzien in de notebook ter voorbereiding van het uitwerken van de Use Cases
  * Implementatie
    * Ingestion, Data-Quality checks en Transformation van data-set Bevolkingsdichtheid
    * Ingestion, Data-Quality checks en Transformation van data-set Antibiotica Consumptie
  * To Do/Optimalisaties
    * Eventuele verdere cleanup, checks en transformaties schrijven (afhankelijk van verdere noden)
* Implementatie Use Case 1: scatterplot van Bevolkingsdichtheid en Antibiotica Consumptie
  * Algemeen
    * Er worden hier 2 dimensies getoond en er worden hiervoor 2 aparte data-sets gekoppeld. Dit betekent dat we ons dienen te vergewissen van een aantal bijkomende controles zodat we zeker zijn dat de data-quality die betrekking heeft op de aspecten tussen de 2 data-sets voldoende gecontroleerd zijn
  * Implementatie
    * Extra controles voor invariants te checken tussen beide data-sets
    * Opzet scatterplot met mock-data
  * To Do/Optimalisaties
    * Verbeteren layout
    * Tonen reële data uit de data-sets
* Schrijven basis-documentatie

### Week 2
Tijdens week 2 zijn de volgende zaken geïmplementeerd:
* Algemeen
  * Afwerken van de eerste scatterplot met reële data & berekening pearson correlatie
  * Aligneren gemeentes van de data-csv files met de TopoJSON gemeentes
  * Herevaluatie visualisatie verband tussen 'Aandeel 65+' en 'Antibiotica consumptie'
* Implementatie
  * Aanpassing scatterplot Bevolkingsdichtheid en Antibiotica consumptie
    * Plotten van reële data uit de beide data-sets
    * Implementatie berekening Pearson correlatie-coëfficiënt en p-waarde (SciPy library)
  * Aanpassing Data Ingestion, cleanup en transformaties voor Bevolkingsdichtheid en Antibiotica-consumptie
    * Op voorhand filteren aan de hand van het werkingsjaar (op deze manier wordt de data-set vanaf het begin beperkt tot de relevante data)
    * Fusiegemeentes opsplitsen in aparte records zodat data-csv zo goed mogelijk afgestemd wordt op de TopoJSON data.
      * Reden: deze fusiegemeentes stonden als 1 record in de csv datasets en diende uitgepslitst te worden zodat deze ingekleurd konden worden op de kaart
    * Toevoegen extra deelgemeentes aan csv datasets. Deze deelgemeentes staan in de TopoJSON gedefinieerd maar niet in de csv datasets. De extra gemeentes zijn deelgemeentes van deze hoofdgemeentes en zullen de data van de hoofdgemeentes toegewezen krijgen.
      * Reden: omdat deze deelgemeentes niet gekend waren in de csv datasets maar wel in de TopoJSON, resulteerde dat in niet-ingekleurde delen van de kaart
    * Refactoring code, oa: definiëren van gezamenlijke code voor:
      * Scatterplot
      * Data transformaties bij inladen aparte data-sets
  * Analyse van anomalieën inzake CSV data-sets en TopoJSON
    * Vergelijken data-sets en uitleg Wikipedia (extra info inzake fusies)
    * Documenteren in Jupyter Notebook
  * Data Ingestion, cleanup en transformaties implementeren voor csv dataset 'aandeel 65+'
    * Deze keer geïmplementeerd met data-frames in combinatie met SQL
    * Reden: andere vorm van coderen dan rechtstreeks met RDD's te werken (leer-proces andere manier van implementeren)
  * Toevoegen scatterplot voor antibiotica consumptie en percentage 65+
    * Toont of er al dan niet een correlatie is tussen deze sets
    * Controles maken ook gebruik van data-frames icm. SQL ipv RDD's (leer-proces andere manier van implementeren)
  * Aanpassen inkleuring kaart met gemeentes om rekening te houden met kleurenblindheid
    * Reden: 8% vd mannen is kleurenblind en 0.5% vd vrouwen waardoor dit een significante groep vormt waar men best rekening mee houdt tijdens de visualisatie
    * Opmerking: ik heb voorlopig geen kleurenpallet gevonden dat rekening houdt met 'Rood-groen'-kleurenblindheid
  * Refactorings in de code (optimalisatie)
  * Herbekijken visualisatie-strategie inkleuren kaart (theoretisch)
    * Analyse
    * Kort documenteren van deze strategie
    * Voorlopig enkel rekening gehouden met Protanomalie/Protanopie (zie sectie 'Kleurenblindheid' voor meer info)
* To Do/Optimalisaties
  * Voorlopig worden de verschillen tussen de gemeentes in de csv data-sets en de TopoJSON weerspiegelt in een aantal constanten die vervolgens gebruikt worden in de verwerking van de alignering tussen de gemeentes van de csv data-sets en de TopoJSON. Een mogelijke optimalisatie is dat deze dynamisch bepaald zouden worden door de data-sets met mekaar te vergelijken.
  * Uitzoeken layout optimalisaties Scatterplots (bron: Fundamentals of Data Visualization)
  * Uitzoeken layout optimalisaties Choropleths (bron: Fundamentals of Data Visualization)
  * Analyse van correctheid van data-visualisatie voor verband 'aandeel 65+' en 'antbiotica consumptie' (eerste aanzet reeds gegeven - zie hierboven)

## Projectvoorstel
### Algemeen
* Stelling: gemeentes waar meer 65 plussers wonen zullen een hogere antibiotica consumptie vertonen
* Confounders:
  * Gemeentes met een hogere bevolkingsdichtheid gebruiken meer antibtiotica (hogere transmissie van bacteriën)
  * Gemeentes met een bevolking die gemiddeld een lagere SES (sociaal economische status) score heeft, zullen meer antibiotica gebruiken (slechtere hygiëne)
### Op te leveren artifacts
* Verschillende afbeeldingen
  * 3 ingekleurde kaarten van Vlaanderen
    * Correlatie aantal 65+ en consumptie antibiotica (aantal ddd)
    * Coëfficiënt sociaal economische status (SES) per gemeente
    * Bevolkingsdichtheid per gemeente
  * 3 scatterplots
    * Percentage 65+ en consumptie antibiotica
    * Bevolkingsdichteid en consumptie antibiotica
    * SES en consumptie antibiotica

### Definities
* Definitie Antibiotica consumptie
  * Aantal terugbetaalde DDD (standaard dagdosis) antibioticum per 1.000 rechthebbenden per dag tussen 1 juli van het jaar  en 30 juni van het volgende kalenderjaar (ambulant)
* Definitie Activiteitsgraad
  * De activiteitsgraad wordt berekend als het aandeel van de beroepsbevolking in de totale bevolking op arbeidsleeftijd (van 20 tot en met 64 jaar). 
  * Detail: bij de totale bevolking op arbeidsleeftijd (van 20 tot en met 64 jaar) maakt men een onderscheid tussen de niet-beroepsactieve bevolking en de beroepsbevolking op arbeidsleeftijd:
    * De niet-beroepsactieve bevolking bestaat uit die personen die niet werken, niet beschikbaar zijn voor een job  en/of niet actief op zoek zijn naar een job. 
    * De beroepsbevolking bestaat uit diegenen die aan het werk zijn (werkenden) en zij die beschikbaar zijn voor een job en actief op zoek naar werk (werkloze(n))

### Berekeningen
* Berekening SES
  * Voorstel: z-scores berekenen voor:
    * Gemiddeld Inkomen per inwoner (aantal euro)
    * Activiteitsgraad (Percentage van de bevolking dat aan de slag is)
    * Opleidingsgraad (onbekend, laag, midden, hoog)
      * Elke categorie (behalve onbekend) een getal geven (vb. 1, 2 en 3)
      * Daarna gemiddelde berekenen van alle gemeenten
      * Daarna z-score berekenen = (opleiding_graad_gemeente - gemiddelde_opleiding_graad_gemeente) / standaard afwijking
    * Daarna alle z-scores optellen = SES coëfficiënt

### Inkleuren kaartje
* Inkleuren kaart verband graad 65+ en ddd consumptie antibiotica
  * Defined daily dose = metriek die gebruikt wordt voor het monitoren van trends inzake antibiotica gebruik
  * Inkleuren per gemeente of er een correlatie is tussen aantal 65+ en aantal ddd consumpties per gemeente is of niet?
    * Initieel idee:
      * Uitwerking
        * Bereken z-score voor aantal 65 plussers      (bepaling schaling)
        * Bereken z-score voor aantal ddd consumpties  (bepaling schaling)
        * Als hoge 65+graad en hoog aantal ddd = correlatie
        * Als lage 65+graad en laag aantal ddd = correlatie
        * Als hoge 65+graad en laag aantal ddd = geen correlatie
        * Als lage 65+graad en hoog aantal ddd = geen correlatie
        * 2 kleuren: rood voor verband/correlatie en blauw voor geen verband
        * Gradatie berekenen: vermenigvuldigen z-scores (eventuele mogelijkheid)
      * Probleem:
        * Je kan geen correlatie voorzien per gemeente want je hebt maar 1 datapunt per gemeente
        * Wat wordt aanzien als grote verschillen tussen de Z-scores?
    * Status: in review
      * Alternatieven:
        * Bivariate choropleth map
          * X as wordt opgedeeld in vb. 3 stukken: laag,gemiddeld en hoog 65+ aandeel
          * Y as wordt opgedeeld in vb. 3 stukken: laag, gemiddeld, hoog
          * Men kan 3 x 3 matrix maken van alle combinaties
          * Elke combinatie krijgt een kleur
        * Regressiemodel
          * Je kan een enkelvoudige regressie doorvoeren maar de regressielijn geeft enkel het verband weer voor ALLE gemeentes en niet per gemeente
          * Als je per gemeente wil zien of deze 'afwijkend' is dan kan je dit aan de residu van het punt voor die gemeente bepalen
            * Residue(E(gemeente)) = E(gemeente) - Y(gemeente-voorspelling)
            * Als E(gemeente) > 0 = meer antibiotica geconsumueerd dan verwacht gegeven het aandeel 65+
            * Als E(gemeente) < 0 = minder antibiotica geconsumueerd dan verwacht gegeven het aandeel 65+
          * Dit kan je wél visualiseren
          * Wanneer is er sprake van een sterke afwijking?
            * Methode A: op basis van Z-score vh residu
              * Bereken Z(Egemeente) = (E(gemeente) - E(gemiddeld)) / standaardafwijking van E
              * Als |Z| > 2 dan zéér atypisch
              * Als |Z| = ongeveer 1 dan mild afwijkend
              * Als |Z| < 1 dan normaal gedrag
            * Methode B: op basis van absolute waarde vh residu
              * Men kan een drempel kiezen
              * Vb. top 10% meest positieve residuen = opvallend veel gebruik
              * Vb. top 10% meest negatieve residuen = opvallend weinig gebruik
              * Dit is een veel gebruikte aanpak in de gezondheidsgeografie
            * Methode C: ruimtelijke statistiek (Moran's I / GI*)
              * Enkel als je wil weten of deze ruimte een hotspot is in haar omgeving
              * Cluster berekeningen
                * High-High clusters = buurgemeentes en zichzelf hoog = echte hotspot
                * Low-Low cluster = structureel weinig gebruik
                * High-Low = uitschieter
                * Low-High = negatieve uitschieter
              * Dit lijkt me niet erg toepasbaar/relevant voor dit project
* Inkleuren kaart SES per gemeente
* Inkleuren kaart bevolkingsdichtheid per gemeente

### Scatterplots
* Graad 65+ en Antibiotica Consumptie
  * Graad van 65+: percentage van de bevolking in de gemeente
* Bevolkingsdichtheid (inw/km2) en Antibiotica Consumptie (Verhouding per 1000 rechthebbenden)
  * Bevolkingsdichteid = inwoners / vierkante km
* SES en Antibiotica Consumptie
  * SES = zelfberekende coëfficient aan de hand van activiteitsgraad, opleidingsniveau en gemiddeld inkomen per inwoner

## Gebruikte Data-Sets
Onderstaande data-sets bevatten gegevens voor elke Vlaamse gemeente inzake de aspecten die hieronder staan opgelijst. De content hieronder komt uit de link en is aangevuld met een schema die de data-structuur kort weergeeft (maakt het makkelijker voor de lezer).

### Consumptie Antibiotica
* Link: https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/antibioticumconsumptie
* Definitie: Aantal terugbetaalde DDD (standaard dagdosis) antibioticum per 1.000 rechthebbenden per dag tussen 1 juli van het jaar en 30 juni van het volgende kalenderjaar – ambulante praktijk
* Eenheid: dosissen
* Ratio: per 1000 rechthebbenden
* Teller: Aantal terugbetaalde dagdosissen
* Noemer: Aantal rechthebbenden
* Opmerking: De DDD (Defined Daily Dose) is een internationale meeteenheid gehanteerd door de wereldgezondheidsorganisatie (WHO) die toelaat het verbruik van diverse geneesmiddelen te vergelijken
* Schema
	* Gemeente
	* NIS-code
	* Indicator
	* Jaar
	* Verhouding per 1000 rechthebbenden

### Bevolkingsdichtheid
* Link: https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/bevolkingsdichtheid
* Definitie: aantal inwoners per vierkante kilometer
* Eenheid: personen
* Ratio: per vierkante kilometer
* Teller: aantal inwoners
* Noemer: totale oppervlakte
* Schema
	* Gemeente
	* NIS-code
	* Indicator
	* Jaar
	* Aantal inwoners
	* Totale oppervlakte
	* Dichtheid (inw/km2)

### 65 plussers
* Link: https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/65-plussers
* Eenheid: personen
* Ratio: procent
* Teller: Aantal inwoners van 65 jaar en ouder
* Noemer: Aantal inwoners 
* Opmerking:
	Het gaat om de volledige bevolking “de jure”. Dit is de bevolking zoals geregistreerd in de registers van de burgerlijke stand van de gemeenten. Het is de 
	som van het bevolkingsregister (Belgen woonachtig in een Belgische gemeente + vreemdelingen met permanente verblijfsvergunning), het vreemdelingenregister 
	(vreemdelingen met een tijdelijke verblijfsvergunning), het register van ambtenaren van de Europese Unie en het register van geprivilegieerde vreemdelingen 
	van de NATO of van SHAPE. Asielzoekers die ingeschreven zijn in het wachtregister horen NIET bij de bevolking “de jure” en zijn dus niet meegeteld in deze cijfers. 
	Worden eveneens niet meegeteld in de bevolking: Belgen in het buitenland (ingeschreven in de consulaire registers van de diplomatieke zendingen en consulaire 
	posten in het buitenland) en ambassadepersoneel en gevolg want zij zijn vrijgesteld. De bevolking de jure kan bijgevolg verschillen van de bevolking de facto. 
	Dit is de feitelijke bevolking, waartoe zowel personen ingeschreven in het wachtregister als ook niet bij de gemeente aangegeven personen inbegrepen zijn.
* Schema
	* Gemeente
	* NIS-code
	* Indicator
	* Jaar
	* Categorie
	* Aantal inwoners van 65 jaar en ouder
	* Aantal inwoners
	* Procent (%)

### Activiteitsgraad
* Link: https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/activiteitsgraad
* Definitie: De activiteitsgraad wordt berekend als het aandeel van de beroepsbevolking in de totale bevolking op arbeidsleeftijd (van 20 tot en met 64 jaar). Bij de totale bevolking op arbeidsleeftijd (van 20 tot en met 64 jaar) maakt men een onderscheid tussen de niet-beroepsactieve bevolking en de beroepsbevolking op arbeidsleeftijd. De niet-beroepsactieve bevolking bestaat uit die personen die niet werken, niet beschikbaar zijn voor een job en/of niet actief op zoek zijn naar een job. De beroepsbevolking bestaat uit diegenen die aan het werk zijn (werkenden) en zij die beschikbaar zijn voor een job en actief op zoek naar werk (werkloze(n))
* Eenheid: werkenden
* Ratio: procent
* Teller: beroepsbevolking van 20-64 jaar
* Noemer: aantal inwoners van 20 tot en met 64 jaar
* Schema
	* Gemeente
	* NIS-code
	* Indicator
	* Jaar
	* Beroepsbevolking van 20 tot en met 64 jaar
	* Aantal inwoners van 20 tot en met 64 jaar
	* Procent (%)

### Gemiddeld inkomen per inwoner
* Link: https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/gemiddeld-inkomen-inwoner
* Definitie: Gemiddeld netto belastbaar inkomen per inwoner. Het totale netto belastbaar inkomen bestaat uit alle netto inkomsten van alle inwoners min de aftrekbare uitgaven. Het netto belastbaar inkomen is de som van alle inkomsten uit onroerende goederen (huuropbrengsten en inkomsten uit woningen), inkomsten uit en opbrengsten van roerende goederen en kapitalen (dividenden, intresten…), beroepsinkomsten (wedden en lonen, ziekte-uitkeringen, werkloosheidsuitkeringen, (brug-)pensioenuitkeringen, winsten, baten, wedden van bedrijfsleiders en meewerkende echtgenoten, na aftrek van de beroepskosten) en diverse inkomsten, verminderd met de aftrekbare uitgaven (zoals kinderopvang, onderhoudsuitkeringen, giften…). Deze gegevens zijn gebaseerd op de aangiften in de personenbelasting die door de FOD Financiën aan Statbel worden aangeleverd. Het vermelde jaar is het inkomstenjaar, het jaar dus waarin de gegevens in de aangiften zijn "verdiend". Vanaf 2022 zijn ook de aangiften van de 15-17 jarigen mee opgenomen.
* Eenheid: euro
* Ratio: per inwoner
* Teller: Totaal netto belastbaar inkomen
* Noemer: Aantal inwoners
* Schema
	* Gemeente
	* NIS-code
	* Indicator
	* Jaar
	* Totaal netto belastbaar inkomen (in miljoen euro)
	* Aantal inwoners
	* Gemiddeld inkomen (in euro), per inwoner

### Opleidingsniveau
* Link: https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/scholingsgraad
* Definitie: Aandeel inwoners van 25 tot en met 64 jaar naar scholingsgraad. De scholingsgraad wordt ingedeeld in drie grote groepen aan de hand van het hoogst behaalde  diploma: laaggeschoolden (maximaal lager secundair onderwijs), middengeschoolden (secundair onderwijs afgewerkt of in het bezit van een einddiploma postsecundair niet-hoger onderwijs) en hooggeschoolden (diploma hoger onderwijs). Als er geen gegevens over de scholingsgraad gekend zijn, worden zij ondergebracht in de categorie ‘onbekend’.
* Eenheid: personen
* Ratio: procent
* Teller: Aantal inwoners van 25-64 jaar per scholingsgraad
* Noemer: Aantal inwoners van 25-64 jaar
* Schema
	* Gemeente
	* NIS-code
	* Indicator
	* Jaar
	* Scholingsgraad
	* Aantal inwoners van 25-64 jaar per scholingsgraad
	* Aantal inwoners van 25-64 jaar
	* Procent (%)

### TopoJSON
Verder wordt er een TopoJOSN gebruikt voor het inkleuren van het kaartje. Deze kan gevonden worden op de link: https://github.com/arneh61/Belgium-Map

## Gebruik AI en bronnen
Er werd/wordt tijdens de initiële fase en de ontwikkelingsfase van het project gebruik gemaakt van AI.
* Tijdens de initiële fase werd dit vooral gebruikt om een aantal statistische zaken af te wegen (oa. hoe kan ik een SES-score bepalen).
* Tijdens de ontwikkelingsfase is het gebruikt om bepaalde PySpark/Python zaken af te checken. Meestal is dit puur syntactisch gerelateerd. AI wordt soms ook gebruikt als klankbord inzake het bedenken van een oplossingsmethode voor een bepaald technisch probleem.
* De code die geschreven is is grotendeels manueel geschreven. Elke stukje code dat gegenereerd is door een LLM is manueel nagekeken en wordt volledig begrepen.
Verder wordt er gebruikt gemaakt van traditionele bronnen:
* Cursusmateriaal van het vak
* Boeken:
  * Fundamentals of Data Visualization - A Primer on Making Informative and Compelling Figures (Clause O. Wilke, 2019)
  * Data Analysis with Python and Spark (Jonathan Rioux, 2022)
  * Spark in Action 2nd edition (Jean-Georges Perrin, 2020)
* Artikels op het internet
* Wikipedia voor de fusie van de gemeentes te achterhalen
* Google Search

## Technisch/Implementatie

In deze sectie worden een aantal technische zaken besproken. Meestal draait het om technologieën of libraries die gebruikt zijn geweest en die een extra woordje uitleg vereisen om aan te tonen dat deze techniciteiten 'begrepen' worden. De zaken worden kort beschreven in bullet-points.

### Opzet choropleth en TopoJSON
* We hebben een TopoJSON file van de gemeentes van België
* Een TopoJSON heeft een specifieke structuur
```json
{
		"type":"Topology",
		"arcs":[ lijst van lijsten met arcs ],
		"transform":{
		  "scale":[
			 0.00004696985808298872,
			 0.000029667298308087575
		  ],
		  "translate":[
			 2.5553555488587563,
			 49.49721527099615
		  ]
	    },
		"objects":{
		  "BEL_adm4":{
			 "type":"GeometryCollection",
			 "geometries":[
				{
				   "arcs":[
					  [
						 0,
						 1,
						 2,
						 3,
						 4,
						 5,
						 6
					  ]
				   ],
				   "type":"Polygon",
				   "properties":{
					  "ID_0":23,
					  "ISO":"BEL",
					  "NAME_0":"Belgium",
					  "ID_1":1,
					  "NAME_1":"Bruxelles",
					  "ID_2":1,
					  "NAME_2":"Bruxelles",
					  "ID_3":1,
					  "NAME_3":"Brussel",
					  "ID_4":1,
					  "NAME_4":"Anderlecht",
					  "VARNAME_4":"",
					  "TYPE_4":"Commune",
					  "ENGTYPE_4":"Commune",
					  "NAME_3 - NEW":"ARR-BRUSSEL HOOFDSTAD",
					  "NAME_2 - NEW":"PRO-BRUSSEL",
					  "NAME_4 - NEW":"GEM-ANDERLECHT"
				   }
				},
				...
			}
		}
	}
```
* TopoJSON is variant op GeoJSON die de geometrie topologisch opslaagt (leidt tot kleinere dataset)
* Structuur van een TopoJSON:
  * Arc = lijst van punten die samen een lijn vormen
    * Eerste coördinaat is absoluut
    * De volgende zijn relatief tov de eerste coordinaat (vb. x eenheden naar links, y eenheden naar boven)
* objects - BEL_adm4
  * Hier staan de geometrieën (lijnen)
  * Een geometrie verwijst naar arcs door een index te specificeren
    * Voorbeeld: arcs: [1, 2, 4] staat voor: de veelhoek bestaat uit punten die verwijzen naar de algemene lijst van arcs (bovenaan het JSON document)
  * properties
    * Bevat de meta-data zoals de naam van de gemeente...
* Het deel waar we in geïnteresseerd zijn voor het tekenen van de kaart bevint zich onder het 'objects' attribute.
  * arcs: bevat alle arcs naar waar via een index naar verwezen zal worden (verwijzingen staan in de geometries sectie)
  * BEL_adm4.geometries.arcs: bevat getallen die indices vormen voor de globale arcs lijst
  * BEL_adm4.geometries.properties.NAME_4: geeft de naam weer van de gemeente
* Code uitleg
  * Voorbeelcode:
```python
folium.Choropleth(geo_data=topojson_data,
                      topojson='objects.BEL_adm4',
                      key_on='feature.properties.NAME_4',
                      data=df,
                      columns=['gemeente', 'aantal'],
                      fill_color='GnBu',
                      fill_opacity=0.7,
                      line_opacity=0.5).add_to(m)
```
  * topojson verwijst naar variabele die json content bevat die in het gemeente-geometrie bestand staat
  * key_on = verwijst naar het path in de TopoJSON structuur die de gemeente aangeeft en zal gerelateerd zijn aan de 1ste kolom in het columns attribute (dat ook de gemeente bevat)
  * data = bevat de (CSV) content met de voorbeeld data in (gemeente en aantal)
  * columns = geeft de naam van de kolommen aan in de data die de gemeente aanduiden die ingekleurd dient te worden samen met de kolomnaam die de waarde aangeeft voor die gemeente
  * fill_color, opacity,... = de layout configuratie

#### Gebruikte bronnen
* TopoJSON-based Choropleth Visualization using Folium (Yash Sanghvi, Aug 13, 2020). https://medium.com/tech-carnot/topojson-based-choropleth-visualization-using-folium-471113fa5964

### Kleurenblindheid

* Duiding:
  * Stoornissen
    * Protanomalie/Protanopie: L-kegels (rood) ontbreken/verminderd
    * Deuteranomalie/Deuteranopie: M-kegels (groen) ontbreken/verminderd
    * Tritanomalie/Tritanopie: S-kegels (blauw) ontbreken/verminderd
  * Soorten kleurenblindheid
    * Rood-groen kleurenblindheid (Protanomalie, Deuteranomalie, Protanopie, Deuteranopie)
    * Blauw-geel kleurenblindheid (Tritanomalie of Tritanoop)
    * Andere vormen van kleurenblindheid:
      * Achromatopsie:
        * Zeer zeldzaam
        * Kleurenkegels in het oog werken helemaal niet. Mensen zien enkel zwart, wit en grijstinten
      * Monochromatopsie
        * Zeer zeldzaam
        * Werkt maar één type kegeltje in het oog
        * Zeer slecht zicht en lichtschuwheid
    * Cijfers:
      * 8% van de mannen is kleurenblind
      * 0.5% van de vrouwen is kleurenblind
      * OOrzaak: erfelijk
  * Oplossing
    * Een oplossing die rekening houdt met alle vormen van kleurenblindheid lijkt een vrij ingewikkelde zaak te zijn.
    * In het project wordt enkel rekening gehouden met 'Rood-groen'-kleurenblindheid omdat hier nog kleurenpaletten voorhanden zijn die door het grootste deel van de bevolking erg goed leesbaar zijn. Wanneer er rekening zou dienen gehouden te worden met andere vormen van kleurenblindheid zal dit wellicht voor de overgrote meerderheid van de bevolking een minder goed leesbaar resultaat opleveren. Er is de voorkeur gegeven aan de meerderheid omdat de andere vormen van kleurenblindheid eerder zeldzaam zijn.
    * Men zou een oplossing kunnen aanreiken waar er via een widget gekozen kan worden tussen verschillende soorten weergave zodat elke groep zijn keuze kan maken.
#### Gebruikte bronnen
* AI: LLM
* Fundamentals of Data Visualization - A Primer on Making Informative and Compelling Figures (Clause O. Wilke, 2019)
* Oogartsen.nl: https://www.oogartsen.nl/glasvocht-netvlies/kleurenzien-en-blindheid/

## Initieel Projectvoorstel 

De beschrijving van het project hieronder vindt zijn oorsprong in mail-communicatie met de lector op 16/10/2025.

Beste

Naar aanleiding van uw vraag ivm. de uit te voeren opdracht voor het vak 'Data Visualization' overweeg ik om (een deel van) de volgende data-sets te gebruiken:

### Bron: Gemeente-Stadsmonitor Vlaanderen
- [Inwonersaantal](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/inwonersaantal)  
- [Netto inkomen per inwoner](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/gemiddeld-inkomen-inwoner)  
- [Kansarmoede in Vlaanderen](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/kansarmoede-index)  
- [Scholingsgraad](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/scholingsgraad)  
- [Bevolkingsdichtheid](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/bevolkingsdichtheid)  
- [Antibiotica consumptie](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/antibioticumconsumptie)  
- *(optioneel)* [Geluksgevoel](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/geluksgevoel)  
- *(optioneel)* [65-plussers](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/65-plussers)  
- *(optioneel)* [Intensiteit contacten](https://gemeente-stadsmonitor.vlaanderen.be/over-de-monitor/overzicht-indicatoren/intensiteit-van-contacten-detail)

### Bron: Intermutualistisch Agentschap (IMA)
- [IMA Databanken](https://atlas.ima-aim.be/databanken/)
- Aantal huisartsbezoeken, gebruik geneesmiddelen (antibiotica, antidepressiva, antipsychotica, ...)

---

## Concreet Scenario

Aangezien ik werkzaam ben aan de UA in een onderzoeksgroep die zich toespitst op resistentieproblematieken inzake antibioticagebruik, wil ik een aantal zaken hierover visualiseren.

### Doel
In eerste instantie wil ik enkele indicatoren visualiseren op gemeentelijk niveau op de kaart van Vlaanderen (via **Folium**):

- Totaal aantal inwoners  
- Percentage 65-plussers per gemeente  
- Aantal DDD’s (defined daily dose) antibiotica geconsumeerd per gemeente  

### Verwachting
Uit onderzoek blijkt dat ouderen meer antibiotica consumeren. Ik verwacht dit terug te zien in de visualisatie: gemeenten met meer 65-plussers zouden een hoger antibioticagebruik vertonen.

### Mogelijke Confounders
Er zijn echter een aantal factoren die dit beeld kunnen vertekenen:
- **Lagere Sociaal-Economische Status (SES):** wordt geassocieerd met slechtere gezondheid en dus mogelijk meer antibioticagebruik.  
- **Bevolkingsdichtheid:** hogere dichtheid kan leiden tot meer transmissie van infecties, en dus meer gebruik van antibiotica.  

Deze verbanden wil ik visualiseren via **scatterplots**.

### Berekening SES-coëfficiënt
De SES wordt doorgaans berekend op basis van inkomen, armoedecijfer en opleidingsgraad. Hiervoor gebruik ik bijkomende datasets (zie boven).

---

## Andere Mogelijke Onderzoeken

### 1. Luchtvervuiling en Antibioticagebruik
- Onderzoek: *“Short-Term Exposure to Ambient Air Pollution and Antimicrobial Use for Acute Respiratory Symptoms” (JAMA, 2024)*  
- Hypothese: meer fijn stof → meer luchtweginfecties → meer antibioticagebruik.  
- Helaas geen geschikte datasets gevonden.

### 2. Antibioticagebruik en Veebedrijven
- Hypothese: in gemeenten met meer veehouderij is mogelijk meer antibioticagebruik.  
- Relevante referenties:
  - *Risicoprofiel IP & AMR Zorgnetwerk Limburg (Nederland)*  
  - *Risicoprofiel antibioticaresistentie Noord-Brabant (Nederland)*  
- Geen bruikbare datasets beschikbaar → **niet geïmplementeerd**.

---

## Alternatieve Scenario’s

### 1. Geluksgevoel en Gebruik van Psychofarmaca
- Vergelijking tussen zelfgerapporteerd **geluksgevoel** en consumptie van **antidepressiva**, **antipsychotica**, ...  
- Data: zie bovenaan (geluksgevoel, psychofarmaca, inwoners).  
- Analyse:
  - Visualisatie van geluksgevoel op kaartniveau.  
  - Vergelijking met “harde” data (geneesmiddelgebruik).  
  - Doel: nagaan of er inconsistenties zijn tussen perceptie en werkelijkheid.

### 2. Ouderen, Sociale Contacten en Geluksgevoel
- **Onderzoeksvraag:** Is de oudere generatie socialer en draagt dat bij tot een hoger geluksgevoel?  
- **Opzet:** gemeenten met meer ouderen → meer sociale contacten → hoger geluksgevoel?  
- **Mogelijke confounders:** eenzaamheid en gezondheidsproblemen bij ouderen.

---

## Niet Weerhouden Data-Sets

Andere gevonden maar niet gebruikte datasets:

- [Verkiezingsuitslagen gemeentes 2024](https://www.vlaanderen.be/vlaanderen-kiest/resultaten)  
  - Interessant voor analyses rond stemgedrag, diversiteit, kansarmoede, sociale cohesie, criminaliteit.  
  - **Niet gebruikt wegens gevoeligheid van het onderwerp.**
- [Bruto sterftecijfer](https://statbel.fgov.be/nl/open-data/hvd-brutosterftecijfer)  
- [Verkeersongevallen 2024](https://statbel.fgov.be/nl/open-data/verkeersongevallen-2024)

---

## Concrete Planning

Het eerste scenario (**antibioticagebruik**) zal waarschijnlijk worden uitgewerkt.  
De bedoeling is niet om op academisch niveau te werken, maar om **duidelijke, verhelderende visualisaties** te maken.  

Mogelijke aanpassingen kunnen volgen als ik bijkomende interessante data vind, maar de **hoofdlijnen blijven stabiel.**

---

## Contact

Indien er nog vragen of opmerkingen zijn, hoor ik dat graag.

Vriendelijke groet
Jimmy Keustermans
