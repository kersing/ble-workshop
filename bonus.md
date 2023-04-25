# Bonus materiaal

Omdat de standaard ST BLE oplossing niet erg veilig is heb ik deze aangepast zodat er een passkey gevraagd wordt om te kunnen verbinden. Let op dat het gebruik van een vaste passkey ook niet als veilig beschouwd wordt. (Zie [Change Your BLE Passkey Like You Change Your Underwear](https://insinuator.net/2021/10/change-your-ble-passkey-like-you-change-your-underwear/) voor details hierover).

## Wijzigingen

Onderstaand een opsomming van de wijzigingen. Kijk voor de details vooral in de broncode, te vinden op [mijn github repository](https://github.com/kersing/ble-code), het gaat om st_passkey.

### Logging

De source is aangepast om alle gebruik van LOG_INFO en LOG_ERROR om te zetten naar printk. Daardoor kun je makkelijker met een terminal programma (PuTTY oid) de uitvoer volgen.

### Project definitie

In de prj.conf file zijn extra velden toegevoegd om authenticatie en versleuteling mogelijk te maken. Ook is het gebruik van een vaste passkey aangezet.

### Source code

In main.c zijn de includes aangevuld voor gebruik met authenticatie.

De registratie van de attributes is aangepast dat ze alleen benaderd mogen worden als authenticatie actief is.

Er zijn verschillende nieuwe callback functies toegevoegd ten behoeve van authenticatie.

Voor de ble stack actief gemaakt wordt, wordt de passkey aan de stack doorgegeven en worden de callbacks geregisteerd.

## Zelf proberen

Natuurlijk wil je deze versie ook zelf proberen. Download de source van github en maak de volgende aanpassingen:

- Verander in prj.conf de applicatie naam.
- Verander in main.c de DEVICE_PIN

Nu kun je bouwen en flashen.

## Onderzoeken

Als de beveiligde versie van de software loopt, start dan nRF explorer en connect met je module. Geef met opzet een foute code op.
Je zult nu zien dat je toch de tabel met attributen kun zien. Deze is niet beveiligd en altijd op te vragen.

Probeer nu een om de volgende characteristic te schrijven (druk op het pijlte omhoog, vul een waarde in, bijvoorbeeld 11, en verzend die). Gebeurt er wat op de module?

Verbreek de verbinding en 'connect' opnieuw. Geef nu wel de correcte code op en probeer dan nogmaals de waarde te schrijven. Kun je uitleggen waarom er nu (als het goed is) wel wat gebeurd? En welke regel in de code dat veroorzaakt?