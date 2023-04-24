# Installation instruction for OSX

## Zephyr (dit was het huiswerk)

Ga naar [Zephyr Project Getting Started](https://docs.zephyrproject.org/latest/develop/getting_started/index.html) en gebruik de instructies om de Zephyr omgeving te installeren.

## nRF Connect

Ga daarna naar [Nordic Semiconductor nRF tools download page](https://www.nordicsemi.com/Products/Development-tools/nrf-connect-for-desktop), klik op downloads (of scroll naar beneden), selecteer het juiste Operating System en download.

Open open de DMG file en installeer de software.

Ga nu naar de [Segger JLink website](https://www.segger.com/downloads/jlink/) en download the Universal Installer voor macOS. Installeer de software na download.

Open de 'nRF Connect for Desktop' applicatie en selecteer Install naast 'Bluetooth Low Energy'. Installeer de software.

Pak nu de Nordic nRF52480 dongle uit de verpakking en steek die in je laptop.

Start nu 'Bluetooth Low Energy'. Er verschijnt een melding om de software te installeren, doe dat. Zodra de software draait verschijnt er een venster waarin je links boven 'SELECT DEVICE' ziet staan. Klik op de pijl naar beneden en kies 'Open DFU Bootloader'.

Er verschijnt nu een venster met de melding dat het device geprogrammeerd moet worden. Klik op 'Yes'.

Als alles goed gaat verschijnt er in het rechter grijze vlak nu 'nRF5x' en in de linker kant kun je 'Start scan' selecteren. Start maar eens een scan en kijk hoeveel BLE devices er zichtbaar zijn. Vast een redelijk aantal met zoveel laptops, telefoons en smart watches.

## Wireshark

Met de BLE dongle (voorzien van de juiste firmware), kunnen we met Wireshark meekijken met BLE verkeer. Laten we de software hiervoor installeren.

Ga naar de [Wireshark Download pagina](https://www.wireshark.org/download.html) en download de installer voor macOS en installeer de software. Je hoeft geen van de eventueel meegeleverde capture drivers te installeren.

## Sniffer firmware

Om met de dongle te kunnen 'sniffen' moet er andere firmware geladen worden. Ga naar de (Nordic download pagina)[https://www.nordicsemi.com/Products/Development-tools/nRF-Sniffer-for-Bluetooth-LE/Download?lang=en#infotabs] scroll iets naar beneden en kies Downloads. Download nu nrf_sniffer_for_bluetooth_le_4.1.1.zip. Pak het bestand uit na downloaden.

Voor het updaten van de dongle gebruiken we de nRF Connect for Desktop software, start die op en kies 'Install' naast 'Programmer'. Als de installatie klaar is open dan de programmer.

Klik op de pijl naar beneden bij 'SELECT DEVICE' en kies de dongle. Als die niet zichtbaar is of er een foutmelding verschijnt, druk dan op de reset knop. De reset ligt plat op de PCB en moet je indrukken vanaf de korte kant richting de laptop.

Kies nu 'Add file' en blader naar de 'hex' folder bij de net uitgepakte bestanden. Kies bestand 'sniffer_nrf52480dongle_nrf52480_4.1.1.hex'. Klik op 'Write' om het bestand op de dongle te programmeren. De dongle wordt nu verzenden van de data automatisch gereboot, je kunt de foutmelding over 'Failed to detect device' negeren. Sluit de nRF software.

## BLE modules aan Wireshark toevoegen

Om Wireshark met BLE te laten werken moeten we nog een paar stappen zetten. Open eerst een terminal window in de extcap folder van de eerder uitgepakte zip. Run daar 'pip install -r requirements.txt'.

Nu moeten we de bestanden op de correcte plaats zetten. Start daarvoor Wireshark, ga naar 'Help', 'About Wireshark' en kies het tabblad 'Folders'. Dubbelklik op 'Personal Extcap Path' en laat de directory aanmaken. Kopieer nu de inhoud (met sub folders) van de extcap folder uit de zip hier naar toe.

Open een commando prompt in de folder en run 'nrf_sniffer_ble.sh --extcap-interfaces'. Als het goed gegaan is staat 'nRF sniffer for Bluetooth' in de uitvoer.

Ga terug naar het 'About Wireshark' venster in de tab 'Folders' en dubbelklik 'Personal configuration'. Kopieer nu de folder 'Profile_nRF_Sniffer_Bluetooth_LE' (niet alleen de inhoud, de folder zelf met alles erin) uit de uitgepakte ZIP naar de folder 'profiles'

Sluit 'Wireshark' en start 'm opnieuw op. Ga naar 'Edit', 'Configuration Profiles'. Selecteer 'Profile_nRF_Sniffer_Bluetooh_LE' en klik op 'OK'.

Ga naar 'Capture' en kies 'Start'. Je moet nu verkeer binnen zien komen.

## Klaar op de laptop

Hiermee zijn we klaar met het installeren op de laptop.