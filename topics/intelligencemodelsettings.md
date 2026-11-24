---
title: ⚙️ Instellingen intelligentiemodellen
permalink: /topics/intelligencemodelsettings
category: Onderwerpen
order: 14
---

Een intelligentiemodel heeft naast de algemene modelconfiguratie een optioneel veld `SettingsJson`. Dit veld bevat instellingen die specifiek zijn voor het gebruik van het model binnen Knowmax Quest. In de beheerclient kunnen beheerders deze instellingen met een formulier bewerken of de ruwe JSON aanpassen.

Dit topic beschrijft de eigenschappen van `IntelligenceModelSettings`. Voor de algemene configuratie van een intelligentiemodel, zie de pagina over [intelligentie modellen](/topics/intelligencemodels).

## Bewerken en opslaan

De editor groepeert de velden in de tabbladen **Algemeen**, **Systeemberichten**, **Ondersteuning**, **Bijlagen**, **Compressie** en **Ruwe JSON**. De formulierweergave en JSON-weergave werken met hetzelfde instellingenobject.

De JSON gebruikt camelCase-eigenschappen en enumwaarden als strings. De server deserialiseert `SettingsJson` naar `IntelligenceModelSettings`; lege of ontbrekende JSON-inhoud is toegestaan. Niet-lege JSON moet deserialiseerbaar zijn. De server controleert daarmee de JSON-structuur en bekende eigenschapstypen, maar dit is geen volledige controle of alle getallen en combinaties inhoudelijk passend zijn voor het gekozen AI-model.

De editor schrijft `conversationDepth` en `threshold` altijd weg. Optionele velden zonder waarde worden doorgaans weggelaten; lege `systemChatMessages` worden niet opgeslagen. Als `supports` expliciet als lege array is opgeslagen (`[]`), betekent dat dat geen van de opgesomde mogelijkheden is ingeschakeld. Wordt `supports` weggelaten of op `null` gezet, dan gelden de standaardwaarden in de tabel hieronder.

> **Let op bij nieuwe modellen:** de beheerclient maakt een nieuw model standaard aan met `{"conversationDepth":30}`. Als `SettingsJson` ontbreekt of de algemene instellingen niet zijn opgegeven, is de backendstandaard voor `conversationDepth` 10. De standaardwaarde van `threshold` is in beide gevallen 600.000 tekens.

## Algemene instellingen

| JSON-eigenschap | Type | Betekenis | Standaard / gedrag |
|---|---|---|---|
| `sequence` | getal, optioneel | Volgnummer voor de sorteervolgorde van intelligentiemodellen in lijsten. | Niet ingesteld; Quest past geen eigen waarde toe. |
| `conversationDepth` | geheel getal | Maximumaantal gebruikersvragen in een gesprek. Zodra de limiet wordt overschreden, moet een nieuw gesprek worden gestart. | Backend: `10`. De beheerclient vult bij een nieuw model standaard `30` in. |
| `threshold` | geheel getal | Maximale invoerbudget in tekens voor gesprekstekst en, bij Document Insight, geëxtraheerde documentinhoud. Stem dit af op het contextvenster van het model en reserveer ruimte voor systeeminstructies en antwoord. | `600000`. Voor Document Insight wordt 75% van deze waarde als grens voor documentinhoud gebruikt. |
| `defaultReasoningEffort` | enum, optioneel | Standaard redeneerinspanning wanneer een verzoek zelf geen niveau opgeeft. | Niet ingesteld; de AI-laag gebruikt dan haar eigen standaard. Mogelijke waarden: `Minimal`, `Low`, `Medium`. Werkt alleen wanneer `ReasoningEffort` is ingeschakeld bij `supports`. |

`threshold` is een karakterbudget en geen exacte tokenlimiet. De tekst van bestandsbijlagen heeft een afzonderlijk budget via `attachments.maxTextLength`; bijlagen worden niet van `threshold` afgetrokken. Binaire/native bijlagen, zoals afbeeldingen en native verwerkte PDF's, tellen niet als geëxtraheerde tekst. Het model verwerkt zulke bestanden wel met zijn eigen multimodale capaciteit.

## Systeemberichten

`systemChatMessages` is een optionele array met extra systeeminstructies die op modelniveau aan de chatberichten worden toegevoegd. Een bericht heeft deze eigenschappen:

| Eigenschap | Type | Betekenis | Standaard / gedrag |
|---|---|---|---|
| `message` | string | De inhoud van de systeeminstructie. Lege berichten worden niet toegevoegd aan de prompt. | Verplicht voor een bruikbare instructie. |
| `position` | `Before` of `After` | Positie ten opzichte van het laatste gebruikersbericht in de chatgeschiedenis. | `Before`. |
| `target` | `DocumentInsight` of `Research`, optioneel | Bepaalt voor welke functie het bericht wordt gebruikt. | Niet ingesteld: toepassen op zowel Document Insight als Research. |

De volgorde van de array blijft behouden binnen de berichten die vóór, respectievelijk ná het laatste gebruikersbericht worden ingevoegd. Gebruik deze instelling voor algemene modelinstructies die niet in applicatieprompts thuishoren.

## Ondersteunde functies

`supports` is een array met de functies waarvoor het model in Knowmax Quest beschikbaar mag zijn. De waarden zijn:

| Waarde | Betekenis | Standaard wanneer `supports` ontbreekt |
|---|---|---|
| `DocumentInsight` | Model mag worden gebruikt voor Knowmax Quest Document Insight. | Aan |
| `Research` | Model mag worden gebruikt voor Knowmax Quest Research. | Aan |
| `Math` | Model is geschikt voor wiskundige bewerkingen. | Uit |
| `ReasoningEffort` | Model accepteert een instelling voor redeneerinspanning. Maakt het gebruik van `defaultReasoningEffort` mogelijk als het verzoek zelf geen niveau opgeeft. | Uit |
| `Attachments` | Model mag bestandsbijlagen in gebruikersberichten verwerken. De limieten en toegestane bestandstypen staan onder `attachments`. | Uit |

Als `supports` een waarde bevat, is die functie ingeschakeld. Wanneer de array expliciet aanwezig is, maar een functie ontbreekt, is die functie uitgeschakeld. Laat het veld weg om de standaardinstellingen te gebruiken.

## Bijlagen

De `attachments`-sectie stelt limieten en verwerkingskeuzes in voor bestanden die bij gebruikersberichten worden meegestuurd. Deze instellingen worden alleen gebruikt wanneer `Attachments` in `supports` is ingeschakeld.

| JSON-eigenschap | Type | Betekenis | Standaard |
|---|---|---|---|
| `maxFiles` | geheel getal | Maximumaantal bestanden per gebruikersbericht. | `5` |
| `maxFileSize` | geheel getal, bytes | Maximale omvang van één bestand. De editor toont deze instelling in MiB (1 MiB = 1.048.576 bytes). | `1048576` bytes (1 MiB) |
| `maxTextLength` | geheel getal, tekens | Maximumaantal tekens van bijlagetekst dat als tekst in de prompt mag worden opgenomen. Dit is een afzonderlijk quotum en telt niet mee in `threshold`. | `3000000` |
| `allowedContentTypes` | array van MIME-typen | MIME-typen die bijlagen mogen hebben. De editor biedt keuzes voor de standaardtypen hieronder. | `image/png`, `image/jpeg`, `image/gif`, `image/webp`, `application/pdf`, `text/plain`, `text/markdown` |
| `pdfMode` | enum | Manier waarop PDF-bestanden naar het model worden gestuurd. | `Native` |
| `attachmentReplayWindow` | geheel getal | Aantal meest recente gebruikersbeurten waarvan opgeslagen bijlagen volledig opnieuw aan het model worden meegestuurd. Oudere bijlagen krijgen een lichte verwijzing en kunnen op verzoek worden opgehaald. | `3` |

`pdfMode` kent twee waarden:

- `Native`: verstuur de PDF als bestand naar het model. Dit is de standaard en vereist een model dat native PDF-invoer ondersteunt. De PDF wordt niet eerst door Quest naar tekst omgezet.
- `ExtractText`: extraheer tekst uit de PDF en stuur die tekst naar het model. Gebruik dit als terugvaloptie voor modellen zonder native PDF-ondersteuning. De geëxtraheerde tekst telt mee voor `maxTextLength`.

Het maximale totale aantal bytes per gebruikersbericht is geen aparte instelling: Quest berekent dit als `maxFiles × maxFileSize`. Tekst- en Markdownbijlagen worden als tekst in de prompt opgenomen. Daardoor kan de feitelijke tekengrens voor die bestanden lager zijn dan de maximale bestandsgrootte. Stel de limieten af op het contextvenster en de multimodale mogelijkheden van het model.

## Gesprekscompressie

`compression` bepaalt of en wanneer oudere delen van een lang gesprek worden samengevat voordat de chatgeschiedenis opnieuw aan het model wordt aangeboden.

| JSON-eigenschap | Type | Betekenis | Standaard |
|---|---|---|---|
| `enabled` | boolean | Schakelt compressie in of uit. | `true` |
| `turnThreshold` | geheel getal | Compressie wordt geactiveerd wanneer het aantal gebruikersbeurten deze grens overschrijdt. | `20` |
| `characterThreshold` | geheel getal | Compressie wordt geactiveerd wanneer de geschatte tekengrootte van de gesprekstekst deze grens overschrijdt. | `60000` |
| `retainedTurns` | geheel getal | Aantal meest recente beurten dat ongewijzigd behouden blijft; oudere beurten kunnen worden samengevat. | `6` |

Compressie wordt geactiveerd zodra ten minste één van de ingestelde drempels wordt overschreden. De bewaarde gespreksberichten en bijlagen worden niet verwijderd of gewijzigd: alleen de geschiedenis die voor een verzoek aan het model wordt aangeboden, wordt verkort. De samenvatting wordt hergebruikt voor volgende verzoeken. Het bijlage-herhalingsvenster is onafhankelijk van `retainedTurns` en wordt met `attachments.attachmentReplayWindow` ingesteld.

Zorg ervoor dat `retainedTurns` lager is dan `turnThreshold`; anders zou de beurtendrempel geen oudere beurten opleveren om samen te vatten. Als de ingestelde waarde gelijk is aan of groter is dan `turnThreshold`, begrenst Quest `retainedTurns` tijdens runtime tot één minder dan `turnThreshold` en schrijft het een waarschuwing naar het log.

## Voorbeeld

Onderstaand voorbeeld laat alle onderdelen zien. Weggelaten optionele waarden gebruiken de genoemde standaardwaarden.

```json
{
	"sequence": 1,
	"conversationDepth": 30,
	"threshold": 600000,
	"defaultReasoningEffort": "Medium",
	"systemChatMessages": [
		{
			"message": "Antwoord beknopt en verwijs naar relevante bronnen.",
			"position": "Before",
			"target": "Research"
		},
		{
			"message": "Gebruik begrijpelijke taal.",
			"position": "After"
		}
	],
	"supports": [
		"DocumentInsight",
		"Research",
		"ReasoningEffort",
		"Attachments"
	],
	"attachments": {
		"maxFiles": 5,
		"maxFileSize": 1048576,
		"maxTextLength": 3000000,
		"allowedContentTypes": [
			"image/png",
			"image/jpeg",
			"image/gif",
			"image/webp",
			"application/pdf",
			"text/plain",
			"text/markdown"
		],
		"pdfMode": "Native",
		"attachmentReplayWindow": 3
	},
	"compression": {
		"enabled": true,
		"turnThreshold": 20,
		"characterThreshold": 60000,
		"retainedTurns": 6
	}
}
```
