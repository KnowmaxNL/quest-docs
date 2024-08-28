---
title: Quest identificatie
permalink: /concepts/quest-id
---

Alle [documenten](/topics/document-structure) in Knowmax Quest hebben een unieke identificatie. De identificatie is geschikt om als path-onderdeel in een URL gebruikt te worden. 

# Opbouw Quest identificatie
Ieder onderdeel binnen Knowmax Quest heeft de volgende opbouw:
```
documentid/documentlocatieid[versie]
```
Hierbij zijn de onderdelen "documentlocatieid" en "versie" optioneel. De documentid is het hele pad dat gevolgd wordt tot aan de root van het document.

# Huidige versie
Als geen versie is opgegeven, geldt de identificatie als een indentificatie naar de huidige [versie van het document](/topics/document-structure). Dat is de valide, online versie met het hoogste versienummer of de valide, online versie met expliciet de eigenschap **current** met waarde **true**. Indien meerdere documenten **current** markering hebben, zal het document met deze markering en het hoogste versienummer gebruikt worden.

# Syntax en restricties
* Alleen cijfers, letters en de volgende tekens zijn toegestaan: . - _ /
* Een Knowmax Quest Identificatie mag niet met een slash of punt beginnen en eindigen
* De slash wordt gebruikt als niveau-scheider
* In een geneste documentlocatiestructuur worden alle bovenliggende documentlocatieid's weergegeven
* De versie wordt tussen blokhaken [ ] geplaatst en kan direct achter de documentid of na de documentlocatiereeks geplaatst worden
* Als er geen versie is opgenomen, zal automatisch de huidige actieve versie worden opgevraagd
* Versie kan door middel van een geheel positief getal aangeduid worden, als datum of met de termen **first**, **last** en **current**. Voor een datum dient de notatiewijze jjjj-mm-dd gebruikt te worden

# Voorbeelden
Stel dat in Knowmax Quest alle documenten om praktische redenen ondergebracht zijn in kleurgroepen. De publicaties in zijn geheel hebben de prefix "pub" gevolgd door een uniek nummer. De documenten zijn opgebouwd uit paragrafen en bevatten vele versies. Mogelijke questidentificaties zijn in dit systeem:

```
1.       rood/pub23/6/6.1/6.1.3[4]
```
```
2.       rood/pub11/4/4.3
```
```
3.       geel/pub14[last]
```
```
4.       paars/pub15
```
```
5.       paars/pub17[first]
```
```
6.       oranje/pub234[2013-2-4]
```
```
7.       oranje/pub234[4]/hfd1/afbeelding1.png
```

Bovenstaande voorbeelden zullen de volgende onderdelen uit Knowmax Quest opvragen:

1. versie 4 van paragraaf 6.1.3 van pub23 uit kleurgroep rood;
2. de huidige actieve versie van paragraaf 4.3 van pub11 uit kleurgroep rood;
3. de laatste versie van pub14 uit kleurgroep geel (merk op dat dit niet de huidige actieve versie hoeft te zijn);
4. de huidige actieve versie van pub15 uit kleurgroep paars (merk op dat 6. dit niet de laatse versie [last] hoeft te zijn);
5. de eerste versie van pub17 (merk op dat dit niet versie [1] hoeft te zijn);
6. de versie van pub234 uit kleurgroep oranje zoals deze 4 februari 2013 geldig was.
7. de hfd1/afbeelding1.png uit versie van document oranje/pub234..

# Document alternatieven
Knowmax Quest biedt de mogelijkheid alternatieve onderdelen voor document(locaties) op te nemen. Zo kan aan een bepaalde publicatie bijvoorbeeld een PDF versie van het hele document zijn toegevoegd. Document alternatieven worden geïdentificeerd met een uniek label. Het label van een documentalternatief volgt na de identificatie van het document of het documentonderdeel waar het document alternatief onderdeel bij hoort en wordt voorafgegaan door **a~**. Voorbeeld:

```
docs/richtlijn/richtlijn1/a~documentalternative.pdf
```

In bovenstaande voorbeeld wordt het document alternatief met het label **documentalternative.pdf** dat hoort bij het document **docs/richtlijn/richtlijn1** aangeduid.

# Expliciete documentadressering
Bij het adresseren van een document(onderdeel) met een Quest identificatie zal altijd (een onderdeel van) een bepaalde versie worden opgevraagd. Om expliciet een document en niet een bepaalde versie te adresseren wordt het "!"-teken gebruikt.

```
doc/abc!
```

In bovenstaand voorbeeld wordt het document **doc/abc** opgevraagd en niet een bepaalde versie van dit document.
