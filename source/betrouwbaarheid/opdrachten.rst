(opdrachten bij betrouwbaarheid)


Foutdetecterende codes
======================

**Opdracht**:
ga na of je app voor internet-bankieren deze gegevens (bankrekeningnummer en betalingskenmerk) ook controleert,
en op tijd een foutmelding geeft (voordat je een overschrijving naar een verkeerde rekening doet).

**Opdracht***: hoe kun je het betalingskenmerk 1234-5678-9012-3456 veranderen in een geldig betalingskenmerk -
door alleen het eerste cijfer te veranderen?

**Opdracht**: schrijf een programma voor het controleren van de geldigheid van een BSN (burger service nummer).
Zie: https://nl.wikipedia.org/wiki/Elfproef.
Een BSN bestaat uit 9 cijfers; deze cijfers worden achtereenvolgend vermenigvuldigd met 9, 8, 7, ..., 3, 2, -1(!).
De som van deze getallen moet dan deelbaar zijn door 11 ("elfproef").

**Opdracht**: laad een groot bestand (bijvoorbeeld een Raspbian-distributie),
en controleer de daarbij gegeven SHA-256 code om te controleren of je het bestand correct ontvangen hebt.

**Vraag**: de SHA-256 code ontvang je via een veilig kanaal: via het HTTPS-protocol;
is het dan ook nodig om het bestand zelf via een veilig kanaal te versturen?

**Vraag**: je kunt deze hash-code gebruiken om te controleren of een bericht (bestand) zonder fouten overgestuurd is;
welke andere communicatieproblemen kun je hiermee oplossen?

**Vraag**: wat is "best effort" communicatie?

A) de meest betrouwbare communicatie;
B) communicatie zonder ontvangstgarantie;

Bericht van ontvangst
=====================

**Vraag**.
Welke van de communicatievormen die je gebruikt bieden de mogelijkheid tot bevestiging van ontvangst?
Wanneer maak je daarvan gebruik?

**Opdracht**.
Als Alice steeds moet wachten op een ontvangsbevestiging van Bob voordat ze een volgend bericht naar Bob kan sturen,
levert dit veel vertraging op: voor elk bericht is dan tenminste tweemaal de latency van de verbinding Alice-Bob nodig.
Een handiger aanpak is als Alice alvast het volgende bericht kan sturen, terwijl ze nog wacht op het vorige.
In dat geval moet Alice aan een ontvangstbevestiging kunnen zien voor welk bericht dit bedoeld is.
De berichten en de ACKs voorzien we daarom van een volgnummer.


+-----------+------------------+-------------+
| Alice     |                  | Bob         |
+===========+==================+=============+
|           | -- bericht 0 --> |             |
+-----------+------------------+-------------+
|           | -- bericht 1 --> |             |
+-----------+------------------+-------------+
|           | <- ACK 0 ---     |             |
+-----------+------------------+-------------+
|           | -- bericht 2 --> |             |
+-----------+------------------+-------------+
|           | <- ACK 1 ---     |             |
+-----------+------------------+-------------+
|           | -- bericht 3 --> |             |
+-----------+------------------+-------------+
|  timeout  | ... geen ACK2... |             |
+-----------+------------------+-------------+
|           |                  |             |
+-----------+------------------+-------------+

Maak de tabel af.

**Opdracht**.
Als de verbinding tussen Alice en Bob toch niet voor andere doeleinden gebruikt wordt,
dan kan Alice een bericht steeds herhalen totdat ze een ACK van Bob gekregen heeft.
En Bob kan een ACK steeds herhalen totdat hij een volgend bericht van Alice gekregen heeft.
In dit geval hebben we ook weer volgnummers van berichten en ACKs nodig -
maar we kunnen deze beperken tot 1 bit
(Alternating Bit Protocol, zie https://nl.wikipedia.org/wiki/Alternating_bit_protocol)

Maak de onderstaande tabel af, waarbij bericht 0 goed aankomt bij Bob, en bericht 1 niet.

+-----------+------------------+-------------+
| Alice     |                  | Bob         |
+===========+==================+=============+
|           | -- bericht 0 --> |             |
+-----------+------------------+-------------+
|           | -- bericht 0 --> |             |
+-----------+------------------+-------------+
|           | <- ACK 0 ---     |             |
+-----------+------------------+-------------+
|           | -- bericht 1 --> |             |
+-----------+------------------+-------------+
|           | <- ACK 0 ---     |             |
+-----------+------------------+-------------+
|           |                  |             |
+-----------+------------------+-------------+
|           |                  |             |
+-----------+------------------+-------------+
|           |                  |             |
+-----------+------------------+-------------+

Foutherstellende codes
======================

Bij het voorbeeld van de (7,4) Hamming code:

**Vraag**: wat gebeurt er als een pariteitsbit zelf fout is?

**Vraag**: welk bit is fout als de groep van p1 en p2 een pariteitsfout aangeven - en p3 niet?
