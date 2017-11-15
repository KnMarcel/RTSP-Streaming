# Aufgabenstellung RTSP-Streaming
Die Aufgaben beziehen sich auf den Beleg Videostreaming für das Modul Internettechnologien 2.

## Aufgaben

### 1. Client
Ergänzen Sie die Klasse Client entsprechend der in der Projektbeschreibung und den Kommentaren im Quelltext gegebenen Hinweisen.

### 2. Server
Ergänzen Sie die Klasse RTPpacket entsprechend der in der Projektbeschreibung und den Kommentaren im Quelltext gegebenen Hinweisen.

### 3. RTSP-Methoden
Ergänzen Sie die RTSP-Methoden OPTIONS und DESCRIBE anhand der Beispiele aus RFC 2326, RFC 2327 und RFC 5109. Es ist ausreichend, sich bei DESCRIBE auf das Beispielvideo zu beziehen.

### 4. Simulation von Paketverlusten
Simulieren Sie Paketverluste und eine variable Verzögerung im Netz, indem Sie am Sender eine wahlweise Unterdrückung von zu sendenden Paketen vornehmen. Diese Unterdrückung von Paketen sollte zufällig und mit einstellbarer Paketverlustwahrscheinlichkeit über das GUI erfolgen. Beispiel: der Wert 0,1 bedeutet, es werden im Mittel 10% der zu übertragenen Pakete unterdrückt.

### 5. Anzeige von Statistiken am Client
Um die simulierten Netzwerkeigenschaften prüfen zu können und die Leistungsfähigkeit der später zu integrierenden Fehlerschutzcodes einschätzen zu können, ist eine Statistikanzeige notwendig.
Folgende Werte sollten mindestens am Client angezeigt werden:
1. Anzahl erhaltener/verlorener Medienpakete + prozentuale Angabe
2. Anzahl korrigierter/unkorrigierbarer Medienpakete
3. Die Anzeige sollte bis zum Ende des Videos sekündlich aktualisiert werden und dann auf dem Gesamtstand stehen bleiben.

Mit dem ersten Punkt kann die Qualität der Verbindung eingeschätzt werden und mit dem zweiten Punkt die Leistungsfähigkeit des FEC-Verfahrens.
Machen Sie sich Gedanken über weitere zu überwachende Parameter.


### 6. Implementierung des FEC-Schutzes
Implementieren Sie einen FEC-Schutz mittels Parity-Check-Code (XOR mit k = 2...20, p = 1). Der Parameter sollte am Server einstellbar sein (GUI / Kommandozeile) Der Server mit FEC-Schutz soll kompatibel zu Clients ohne FEC-Verfahren sein! Nutzen Sie dazu das Feld Payloadtype des RTP-Headers (PT=127 für FEC-Pakete).
Sie können sich bei der Implementierung an RFC 5109 orientieren, dies ist aber keine Pflicht. Sie sollten aber das Dokument zumindest lesen.

Implementierung Sie FEC über nachfolgende Schritte:
1. Nutzung einer separaten Klasse FECpacket für das FEC-Handling für Sender und Empfänger, siehe Ausführungen weiter unten
2. Serverseitige Implementierung des XOR-FEC. Nach Auswertung des PT (26) sollte der Client nach wir vor regulär funktionieren.
3. Entwurf der Architektur der Paket- und Bildverarbeitung im Client
4. Eingangspuffer im Client implementieren (Größe ca. 1-2 s)
5. FEC-Korrektur im Client implementieren

Ändern Sie die vorhandenen Klassen nur soweit **nötig**. Halten Sie die Struktur einfach und überschaubar. Nutzen Sie Threads nur wenn dies notwendig ist und Sie die Nebenwirkungen (Blockierungen, Race-Condition) kennen. Bei einer durchdachten Implementierung benötigen Sie keine Threads.


#### Architekturvorschlag
t.b.d.

#### Parameterwahl
Finden Sie den optimalen Wert für k bei einer Kanalverlustrate von 10%. Optimal bedeutet in
diesem Fall eine subjektiv zufriedenstellende Bildqualität bei geringstmöglicher Redundanz.

#### Dokumentation
Dokumentieren Sie Ihr Projekt. Beschreiben Sie die Architektur Ihrer Implementierung anhand
sinnvoller Softwarebeschreibungsmethoden (Klassendiagramm, Zustandsdiagramm, etc.). Eine
Quellcodekommentierung ist dazu nicht ausreichend!


## Literatur
* Real Time Streaming Protocol (RTSP)                   [RFC 2326](http://www.ietf.org/rfc/rfc2326.txt)
* SDP: Session Description Protocol                     [RFC2327](http://www.ietf.org/rfc/rfc2327.txt)
* RTP: A Transport Protocol for Real-Time Applications  [RFC 3550](http://www.ietf.org/rfc/rfc3550.txt)
* RTP Payload Format for JPEG-compressed Video          [RFC 2435](http://www.ietf.org/rfc/rfc2435.txt)
* RTP Profile for Audio and Video Conferences with Minimal Control  [RFC 3551](http://www.ietf.org/rfc/rfc3551.txt)
* RTP Payload Format for Generic Forward Error Correction  [RFC 5109](http://www.ietf.org/rfc/rfc5109.txt)
* Reed-Solomon Forward Error Correction (FEC) Schemes   [RFC 5510](http://www.ietf.org/rfc/rfc5510.txt)