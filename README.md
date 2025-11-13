# Data Visualization – Projectvoorstel

## Log mailverkeer

Mail Possemiers Philippe 16/10/2025

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
