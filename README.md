<h1>I2C-Treiber für ROBO Pro</h1>

Das I²C-Protokoll [1] wird auch von den fischertechnik-Controllern TX und TXT unterstützt. In der fischertechnik-Programmierumgebung ROBO Pro gibt es seit 2012 einen 
Lese- und einen Schreibbefehl, über den I²C-Sensoren angesprochen werden können [2]. Der TX kann über die 5V-Stromversorgung des Busses problemlos Aktoren mit mehreren 
hundert mA Strombedarf versorgen. Der Anschluss an die sechspolige EXT2-Buchse gelingt sehr einfach mit einem Adapter oder mit Jumper-Kabeln.

Der TXT hingegen verwendet eine 3,3V-Logik und stellt an seinem Bus keine stabile Stromversorgung bereit. Mit einem Level Shifter und einem Spannungswandler (9V oder 5V 
auf 3,3V) lassen sich die Sensoren an beiden Controllern betreiben. Im Folgenden werden einige I²C-Sensoren mit passenden ROBO Pro-Treibern vorgestellt. Die Treiber enthalten
eine ausführliche Dokumentation (bei den Unterprogrammen unter "Beschreibung") und ein Beispielprogramm, mit dem Treiber und Sensor getestet werden können.

<h2>Nunchuk</h2>

Für die Spielekonsole WII gibt es ein zweites Steuergerät, den WII Nunchuk. Der darin verbaute 3D-Beschleunigungssensor (+/-3g), der Joystick und die beiden Tasten werden 
über das I²C-Protokoll ausgelesen. Mit einem einfachen Adapter kann der Nunchuk auch an den TX(T) angeschlossen werden [3] - für den TX sollte der Adapter über einen Level
Shifter verfügen, da der Nunchuk eine 3,3V Betriebsspannung erwartet [4]. Adapter mit (z.B. seeedstudio) und ohne Level Shifter (z.B. DFRobot) gibt es für wenige Euro. 
Den Nunchuk gibt es sogar mit einer kabellosen IR-Verbindung; damit kann der Nunchuk als Bewegungs-Fernsteuerung für fischertechnik-Modelle genutzt werden. Mit ca. 10 € ist
er zudem deutlich günstiger als ein Breadboard mit einem vergleichbaren Bewegungssensor.

<ul>
<li>ROBO Pro-Treiber Nunchuk (TX/TXT): Accelerometer-Nunchuk v2.1.zip
</ul>

<h2>Farbsensoren</h2>

Die Farbsensoren von fischertechnik liefern einen Helligkeitswert zurück, aus dem sich die Farbe "ableiten" lässt. Allerdings sind die Sensoren äußerst anfällig für Störlicht;
das ist in sehr vielen fischertechnik-Modellen ein Ärgernis: Die Auswertung benötigt Zeit und die Farberkennung erfordert einen abgeschirmten "Messpunkt". 
Hochwertigere Farbsensoren sind da deutlich robuster - und ermöglichen eine schnellere, weniger Störlicht anfällige und verlässlichere Farbbestimmung. 
Für zwei dieser Sensoren - den TCS34725 von TAOS, der sowohl mit 3,3V als auch mit 5V betrieben werden kann, und den 3,3V-Sensor ISL29125 von Intersil - gibt es Breadboards,
die den Anschluss an einen I²C-Bus sehr erleichtern. Eine ausführliche Beschreibung der Funktionsweise der beiden Sensoren und der zugehörigen ROBO Pro-Treiber findet sich in 
[5], die Datenblätter unter [6, 7].

<ul>
<li>ROBO Pro-Treiber TCS34725 (TX/TXT): Color-TCS34725 v1.2.zip
<li>ROBO Pro-Treiber ISL29125 (TXT): Color-ISL29125 v1.1.zip
</ul>

<h2>Kompass-Sensoren</h2>

Ein für viele Anwendungen (wie z. B. selbstständig fahrende Roboter) wichtiger Sensor, der im fischertechnik-Programm fehlt, ist ein Kompass-Sensor. Inzwischen gibt es sehr 
viele günstige und genaue Kompass-Sensoren mit I²C-Schnittstelle, die sich über ein Breadboard am TX oder TXT anschließen lassen. Eine ganze Familie von Kompass-Sensoren stammt
von Honeywell; beispielhaft gibt es bereits einen ROBO Pro-Treiber für den HMC6352. Ein sehr verbreiteter I²C-Kompass-Sensor ist der CMPS10 von Devantech, der außer der 
Himmelsrichtung auch Pitch und Roll (die Neigung in zwei Richtungen) angeben kann. Beide Sensoren werden mit 5V betrieben und lassen sich direkt am TX, mit Level Shifter und 
Spannungswandler auch am TXT nutzen. Eine ausführliche Beschreibung findet sich in [8], die zugehörigen Datenblätter in [9, 10]. Der Nachfolger CMPS11 von Devantech (der den
Sensorbaustein LSM9DS0 von ST Microelectronics verwendet) kann mit 3,6-5V betrieben werden; dasselbe gilt für den jüngsten, den CMPS14 (der den Bosch-Sensor BMO080 verwendet).

<ul>
<li>ROBO Pro-Treiber HMC6351 (TX): Compass-HMC6352 v1.2.zip
<li>ROBO Pro-Treiber CMPS10 (TX): Compass-CMPS10 v1.3.zip
<li>ROBO Pro-Treiber CMPS11 (TX/TXT): Compass-CMPS11 v1.0.zip
<li>ROBO Pro-Treiber CMPS14 (TX/TXT): Compass-CMPS14 v1.0.zip
</ul>

<h2>Real-Time Clock</h2>

In vielen Programmen ist eine korrekte Zeit - oder zumindest ein korrekter Timer - von großer Bedeutung. Um nicht auf die (wegen diverser Interrupts und anderer Effekte oft
ungenauen) Timer des TX Controllers zurückgreifen zu müssen, ist eine Echtzeituhr (Real-Time Clock, RTC), die von einem eigenständigen IC gesteuert und einer eigenen 
Stromquelle gespeist wird, oft eine gute Lösung. Vor allem zwei I²C-RTC-ICs haben eine große Verbreitung: die DS1307 und die DS3231, beide von Dallas Semiconductors.
Von Sparkfun bzw. Adafruit (DS1307) und von macetech (DS3231, 2.3-5.5 V, ChronoDot) gibt es jeweils ein passendes Breadboard. Beide Sensoren können direkt an den TX 
angeschlossenwerden; der DS3231 erlaubt auch einen Betrieb am TXT ohne Level Shifter und, wegen des geringen Stromverbrauchs von < 0,9 mA, sogar ohne externe Stromversorgung.
Eine ausführliche Beschreibung beider Sensoren und Beispielanwendungen findet sich in [11], die Datenblätter und technische Hinweise unter [12-14]. 
(Der TXT bietet in ROBO Pro inzwischen einen Zugriff auf seine Echtzeituhr.)

<ul>
<li>ROBO Pro-Treiber DS1307 (TX): RealTimeClock-DS1307 v1.3.zip
<li>ROBO Pro-Treiber DS3231 (TX/TXT): RealTimeClock-DS3231 v1.3.zip
</ul>

<h2>Temperatur- und Drucksensor</h2>

Eine einigermaßen genaue Bestimmung der Temperatur ist mit den fischertechnik-Temperatursensoren nicht möglich. Da helfen nur präzise Temperatursensoren. Auch die Sensoren,
die bpsw. in der RTC DS3231 verbaut sind, sind mit +/-3°C zu ungenau. Der Temperatursensor MCP9808 spielt da in einer anderen Liga: Eine Auflösung von 0,0625°C bei einer
Genauigkeit von +/-0,25°C. Der Sensor kann sowohl mit 3,3V als auch mit 5V betrieben werden; da sein Strombedarf bei 0,2-0,4mA liegt, lässt er sich auch problemlos direkt am
EXT-Port des TXT anschließen. Eine detaillierte Beschreibung des Sensors findet sich unter [15], das Datenblatt unter [16].

Einige hochpräzise Temperatursensoren erhält man zusammen mit einem Drucksensor - dazu zählt z. B. die Familie der Bosch-BMP-Sensoren (BMP085, BMP180 und BMP280). Derm BMP280
erreicht eine Auflösung von 0,0003°C und eine Genauigkeit von 0,01°C. Von Adafruit gibt es Breakout-Boards, die zugleich einen Level Shifter auf 3,3V-Logik enthalten, sodass
der Sensor sowohl am TX als auch am TXT genutzt werden kann (einzige Einschränkung: Beim TX funktioniert der Treiber, wahrscheinlich wegen der aufwändigen 
Fließkommaoperationen, nur im Online-Mode). Details zum Sensor und einer Beschreibung des Treibers finden sich unter [36], das Datenblatt unter [37].

<ul>
<li>ROBO Pro-Treiber MCP9808 (TX/TXT): Thermometer-MCP9808 v1.2.zip
<li>ROBO Pro-Treiber BMP280 (TX/TXT): Pressure-BMP280 v1.0.zip
</ul>

<h2>Ultraschall-Sensoren</h2>

Abstandsmessungen sind für viele Anwendungen wichtig. fischertechnik ermöglicht das mit einem Ultraschallsensor, der den Abstand eines Objekts in cm zurückliefert. 
Mit ca. 35 € ist der Sensor nicht ganz billig, und er belegt einen Messeingang am TX/TXT. Über den I²C-Bus lassen sich weitere Ultraschallsensoren anschließen, die außerdem
flexible Einstellungsmöglichkeiten bieten (maximaler Abstand, Verstärkungsfaktor des Signals etc.). Einer dieser Sensoren ist der SRF08 von Devantech, der außerdem einen 
Helligkeitssensor mitbringt (mit dem sich bspw. bei einem Fahrzeug bei einbrechender Dunkelheit automatisch die Beleuchtung einstellen lässt). Der SRF08 benötigt eine 
5V-Betriebsspannung; da er in der Spitze bis zu 275 mA Strom zieht, benötigt er am TXT einen Level Shifter und eine separate Spannungsversorung. Am TX kann er direkt betrieben
werden. Ausführlich beschrieben ist der Sensor in [17], Details finden sich im Datenblatt [18]. Ein weiterer interessanter Ultraschall-Sensor von Devantech ist der SRF02,
der nur einen "Schalltrichter" zum Senden und Empfangen benötigt - und auch den Abstand zu einem Fremdsignal bestimmen kann. Ihn gibt es bereits für ca. 15 €. 
Auch dieser Sensor benötigt eine 5V-Betriebsspannung; er kann direkt an den TX angeschlossen werden. Der Sensor ist ebenfalls in [17] beschrieben, Details finden sich im 
Datenblatt [19].

<ul>
<li>ROBO Pro-Treiber SRF08 (TX): Ultraschall-SRF08 v1.1.zip
<li>ROBO Pro-Treiber SRF02 (TX): Ultraschall-SRF02 v2.0.zip
</ul>

<h2>IR-Abstandssensoren</h2>

Die Abstandsmessung mit Ultraschall-Sensoren ist ungenau, denn durch die große Streuung der Ultraschall-Signale kommt es zu Reflexionen von Gegenständen am Rande des 
Trichters, und der Sensor kann nicht unterscheiden, ob diese Objekte sich unmittelbar vor oder seitlich vom Sensor befinden. Präziser sind Laser- oder Infrarot-Sensoren, 
die den Abstand aus den unterschiedlichen Laufzeiten einfallender Reflexionen berechnen. Die Messmethode beschränkt diese Sensoren jedoch auf kurze Distanzen (1-200 mm). 
Die Vishay-Sensoren VCNL4000 und VCNL4010 verfügen außerdem über einen Licht-Sensor, der die Beleuchtungsstärke (also den auf einer Fläche gegebener Größe auftreffenden 
Lichtstrom) in Lux misst (Lumen/m²).

<ul>
<li>ROBO Pro-Treiber VCNL4000 (TX/TXT):
<li>ROBO Pro-Treiber VCNL4010 (TX/TXT):
</ul>

<h2>Multiplexer</h2>

Auf einem I²C-Bus können theoretisch ca. 120 verschiedene Aktoren und Sensoren angesprochen werden. Allerdings gibt es einige Sensoren, die mit fester I²C-Adresse geliefert 
werden; in diesem Fall kann an demselben Bus nur einer dieser Sensoren betreiben werden. Manchmal kollidieren auch die Adressen unterschiedlicher Sensoren, weil diese mit 
derselben Adresse oder demselben einstellbaren Adressbereich ausgeliefert werden. Einen Ausweg bietet ein Multiplexer, der wie eine "Weiche" auf mehrere I²C-Busse verzweigt. 
Dazu muss der Master lediglich erst im Multiplexer den richtigen Kanal wählen und dann das I²C-Kommando an den auf diesem Kanal angeschlossenen Sensor senden. Der TCA9548A 
(von Texas Instruments) ist ein solcher 8-Kanal-Multiplexer, mit dem bis zu acht Sensoren oder Aktoren mit derselben I²C-Adresse über denselben I²C-Bus vom Master adressiert 
werden können. Er kommt mit Betriebsspannungen von 1,65-5,5V klar und kann wg. des geringen Stromverbrauchs (<0,1 mA) sowohl am EXT-Anschluss des TX als auch des TXT ohne 
Level Shifter oder separate Stromversorgung direkt angeschlossen werden. Der Sensor und das Adafruit-Breadboard werden ausführlich in [20] besprochen; Details finden sich im 
Datenblatt des Sensors [21].

<ul>
<li>ROBO Pro-Treiber Multiplexer TCA9548A (TX/TXT): Multiplexer-TCA9548A v1.0.zip
</ul>

<h2>I/O-Expander</h2>

Reichen die (digitalen) Ein- und Ausgänge des TX/TXT nicht aus, können mit einem GPIO-Expander weitere I/O-Ports über die I²C-Schnittstelle ausgelesen bzw. beschrieben werden. 
Die Ursprünge des GPIO-Expanders PCF8574 mit acht digitalen I/O-Ports von NXP reicht bis zum Jahr 1989 zurück. Die aktuelle Version des Microchip beherrscht den I²C-Fast-Mode 
(400 kHz) und kann wahlweise mit 3,3 oder 5V betrieben werden. Das Breadboard kann daher ohne Level Shifter sowohl am TX als auch am TXT eingesetzt werden. Die 
Default-I²C-Adresse 0x20 kann durch Jumper in sieben weitere Adressen (0x21-0x27) geändert werden; damit können an einem I²C-Bus (ohne Multiplexer) mit acht PCF8574-Boards 
insgesamt 64 I/O-Ports angesteuert werden. Eine Anwendung für den PCF8574 ist die Auswertung von Keypads. Der I²C-Treiber enthält eine Funktion, die ein solches 3x4-Tastenfeld 
auswertet.

<ul>
<li>ROBO Pro-Treiber PCF8574 (TX/TXT, inkl. Keypad): IO-Expander PCF8574 v1.1.zip
</ul>

<h2>LED-Displays</h2>

In vielen Modellen ist die Anzeige von Daten (Messergebnisse, Zeiten, Datum etc.) hilfreich oder sogar wichtig. Die Displays von TX und TXT sind da oft keine gute Wahl, da 
der Controller oft an einer schlecht einsehbaren Stelle verbaut ist. LED-Displays, die über das I²C-Protokoll angesteuert werden können, sind da eine attraktive Alternative. 
Ein solches vierstelliges 7-Segment-Display wird von Sparkfun in unterschiedlichen Farben angeboten. Es verträgt Betriebsspannungen von 2,4-5,5V und kann daher sowohl am TX 
als auch am TXT ohne Level Sifter betrieben werden. Das Display hat einen maximalen Strombedarf von 7,9mA (bei 3,3V) bzw. 14,1mA (bei 5V); am TXT sollte es also mit einer 
separaten 3,3V-Stromzufuhr betrieben werden. Das Display ist ausführlich in [22] beschrieben; alle technischen Angaben finden sich im Wiki von Sparkfun [23].

Von Adafruit gibt es (ebenfalls in fünf unterschiedlichen Farben) 7-Segment-LED-Module, die mit 2 cm Höhe etwas größer und deutlich heller sind. Außerdem bietet Adafruit ein 
vierstelliges 14-Segment-LED-Display, mit dem sich alpha-numerische Zeichen darstellen lassen; auch das in unterschiedlichen Farben (allerdings ohne Doppelpunkt). Sie werden 
von einem mit 5V betriebenen HT16K33 (Holtek) gesteuert. Am TX können sie unmittelbar angeschlossen werden; für den Betrieb am TXT benötigt man Level Shifter und 
5V-Stromzufuhr. Eine ausführliche Beschreibung des Moduls findet sich in [24], Details zum HT16K33 im Datenblatt [25].

Schließlich gibt es noch ein vierstelliges 7-Segment-LED-Display von Conrad (5V), das direkt mit dem TX-Kabel angeschlossen werden kann. Es hat leider einen hohen
Stromverbrauch (bis 350 mA), beherrscht nur den I²C Standard Mode (100 kHz), existiert nur in einer LED-Farbe (hellrot) und ist mit ca. 25 € kein Schnäppchen. Dafür können 
vier verschiedene I²C-Adressen ganz einfach mit einem Jumper auf der Rückseite des Display eingestellt werden. Eine ausführliche Beschreibung findet sich in [26].

<ul>
<li>ROBO Pro-Treiber S7SD (TX/TXT): LED-S7SD v1.2.zip
<li>ROBO Pro-Treiber A7SD (TX): LED-A7SD v1.1.zip
<li>ROBO Pro-Treiber A14SD (TX): LED-A14SD v1.1.zip
<li>ROBO Pro-Treiber SAA1064 (TX): LED-SAA1064 v2.0.zip
</ul>

<h2>LC-Displays</h2>

Für die Ausgabe von Texten sind LC-Displays die richtige Wahl. Wenn das Display des TX/TXT dafür nicht geeignet ist (zu klein, zu dunkel, Controller im Modell verbaut etc.), 
dann sind zweizeilige, via I²C ansteuerbare LC-Displays eine attraktive Alternative. Meist gibt es sie in Blau oder Grün, jeweils mit Hintergrundbeleuchtung, zwei- bis 
vierzeilig und mit 16-20 Zeichen pro Zeile. für den TX ist das LCD05 von Devantech eine sehr leistungsfähige Option - 4x20 Zeichen und sehr flexible Kommandos, I²C Fast Mode 
(400 kHz) und 5V Vcc. Außerdem lässt sich an diesem Display direkt ein 12-Tasten-Keypad anschließen und auswerten. Beschrieben ist das Display ausführlich in [28], mehr im 
Datenblatt [29]. 

Ebenfalls eine gute Wahl ist das vierzeilige 80-Zeichen-Display LCD2004 (großer Bruder des LCD1602 mit zwei Zeilen und 32 Zeichen), das ebenfalls einen 5V-Anschluss benötigt.
Die Helligkeitsregelung erfolgt mechanisch über ein Poti auf der Rückseite, es unterstützt den I²C Standard Mode (100 kHz) und ist ebenfalls als grünes und blaues Display 
lieferbar. Es verwendet den HD44780 von Hitachi [32], gesteuert über einen PCF8574T von NXP. Eine Beschreibung des Displays findet sich in [28].

<ul>
<li>ROBO Pro-Treiber LCD05 mit Keypad (TX): LCD-LCD05 v2.4.zip
<li>ROBO Pro-Treiber LCD05 (TX, inkl. Keypad): Keypad-LCD05 v1.1.zip
<li>ROBO Pro-Treiber LCD2004 (TX): LCD-LCD2004 v2.0.zip
</ul>

<h2>LED-Spielereien</h2>

Neben LED-Displays gibt es auch andere LED-Anzeigen, die via I²C angesteuert werden können. Eine ist die LED-RGB-Diode BinkM mit 18 programmierten Skripts, die via I²C 
gestartet werden können; siehe Datenblatt von ThingM Labs [30]. Sie lässt sich sowohl am TX als auch am TXT betreiben, da die Betriebsspannung Vcc bei 3-5,5V liegen darf.

<ul>
<li>ROBO Pro-Treiber LED-BlinkM (TX/TXT): LED-BlinkM v1.1.zip
</ul>

<h2>Servo-Driver</h2>

Die fischertechnik-Controller TX und TXT verfügen über keine Möglichkeit, den fischertechnik-Servo anzusteuern - das geht allein über das IR- bzw. BT-Fernsteuerungsmodul. 
Von Adafruit gibt es jedoch einen Servo Driver, der die Ansteuerung von 16 Servos mit 12-bit-PWM-Signalen erlaubt - und über das I²C-Protokoll angesprochen wird. 
Es verwendet den LED-Driver-IC PCA9685, der eine feine 12-Bit-Ansteuerung der LED/Servo-Ausgänge erlaubt (0-4095) und eine Frequenzvoreinstellung (hier: 50-60 Hz)
ermöglicht [31, 33]. Das Board ist auf eine Spannung von 2,3-5,5V ausgelegt und kann daher direkt am TX und am TXT betrieben werden. Es kostet ca. 15 €. 

Wichtig: für den Betrieb der Servos benötigt man eine separate Stromversorgung von 4,8-6 V (erhältlich über einen Spannungswandler 9V -> 6V direkt vom TX(T)). 
Beim Betrieb am TXT sollte man außerdem die I²C-Stromversorgung des Servo Driver über einen Spannungswandler 9V -> 3,3V realisieren, da das Board bis zu 10 mA Strom ziehen 
kann - zu viel für den Vcc-Anschluss am EXT-Stecker. Getestet wurden Board und Treiber mit dem fischertechnik-Servo und einem DGServo S05NF STD. Eine ausführliche Erläuterung
mit Beispielprogramm (Steuerung eines Servos mit IR-Fernsteuerung und TXT als Empfänger) findet sich in [34].

<ul>
<li>ROBO Pro-Treiber Servodriver-PCA9685: Servodriver-PCA9685 v1.1.zip
</ul>

<h2>GPS-Sensor</h2>

Es gibt bisher nicht viele  Breadboards mit GPS-Sensoren, die via I²C angesprochen werden können. Eines ist das Navigatron-Board mit einem GTPA010 von Flytron, dass mit 10 Hz 
zudem über eine sehr schnelle Positionsbestimmung berfügt. Es kann außerdem bis zu 16 Wegpunkte speichern und an diesen entlang navigieren. Mit einer Genauigkeit von unter
3m ist der GPS-Sensor hinreichend präzise, um bspw. ein fischertechnik-Fahrzeug zu einem vorgegebenen Punkt navigieren zu lassen. Eine ausführliche Beschreibung des Treibers 
findet sich in [35].

<ul>
<li>ROBO Pro-Treiber GPS-GTPA010: GPS-GTPA010 v1.1.zip
</ul>

<h2>Gyro- und Beschleunigungssensoren</h2>

2018 brachte fischertechnik den "Kombisensor" auf den Markt, einen I²C-IMU (Inertial Measurement Unit) von Bosch mit der Typbezeichnung BMX055, der einen Gyro-, 
Beschleunigungs- und Kompasssensor umfasst. fischertechnik liefert dazu einen ROBO Pro-Treiber aus, der allerdings einige Fehler enthält und nicht alle Funktionen des 
Bosch-Sensors nutzt. Eine ausführliche Beschreibung des Sensors findet sich in [40, 41].

<ul>
<li>ROBO Pro-Treiber Kombisensor BMX055: Kombisensor-BMX055 v2.0.zip
</ul>

<h2>Quellen</h2>

<br>[1] NXP: I²C-bus specification and user manual UM10204, Rev. 4 vom 13.02.2012.
<br>[2] Dirk Fox: I²C mit TX und Robo Pro - Teil 1: Grundlagen. ft:pedia 3/2012, S. 32-37.
<br>[3] Dirk Fox: Wii-Nunchuk steuert fischertechnik-Modelle. c't Hardware Hacks 1/2013, S. 64-69.
<br>[4] Dirk Fox: I²C mit dem TX(T) - Teil 4: Nunchuk-Fernsteuerung. ft:pedia 2/2013, S. 41-49.
<br>[5] Dirk Fox: I²C mit dem TX(T) - Teil 13: Farbsensor. ft:pedia 1/2016, S. 79-89.
<br>[6] ams (TAOS): TCS3472 Color Light to digital Converter with IR Filter. Datasheet, TAOS135, August 2012.
<br>[7] Intersil: Digital Red, Green and Blue Color Light Sensor with IR Blocking Filter. Datasheet ISL29125, 15.01.2016.
<br>[8] Dirk Fox: I²C mit dem TX(T) - Teil 10: Kompass-Sensoren. ft:pedia 2/2014, S. 57-64.
<br>[9] Honeywell: 2-Axis Compass with Algorithms HMC6352. Datasheet, 2009.
<br>[10] Devantech: CMPS10 - Tilt Compensated Compass Module.
<br>[11] Dirk Fox: I²C mit dem TX(T) - Teil 7: Real Time Clock. ft:pedia 4/2013, S. 28-34.
<br>[12] Dallas Semiconductors: DS1307 64 x 8 Serial Real-Time Clock. Datasheet, Rev. 5, February 2008.
<br>[13] Maxim Integrated: DS3231 Extremely Accurate I²C-Integrated RTC/TCXO/Crystal. Datasheet, Rev. 9, January 2013.
<br>[14] Macetech: Chronodot Dokumentation.
<br>[15] Dirk Fox: I²C mit dem TX(T) - Teil 12: Temperatursensor. ft:pedia 4/2015, S. 44-48.
<br>[16] Microchip Technology Inc.: Maximum Accuracy Digital Temperature Sensor MCP9808. Datasheet, 02.08.2011.
<br>[17] Dirk Fox: I²C mit dem TX(T) - Teil 8: Ultraschall-Sensor. ft:pedia 4/2013, S. 35-40.
<br>[18] Robot-Electronics: SRF08 Ultra sonic range finder. Technical Documentation.
<br>[19] Robot-Electronics: SRF02 Ultra sonic range finder. Technical Documentation.
<br>[20] Georg Stiegler: I²C mit dem TX(T) - Teil 5: Multiplexer. ft:pedia 2/2013, S. 50-52.
<br>[21] Texas Instruments: TCA9548A Low-Voltage 8-Channel I2C Switch with Reset, Datasheet, Rev. F, November 2016.
<br>[22] Dirk Fox: I²C mit dem TX(T) - Teil 14: LED-Display (2). ft:pedia 4/2016, S. 84-89.
<br>[23] Sparkfun: Serial 7-Segment Display Datasheet. github.com.
<br>[24] Dirk Fox: I²C mit dem dem TX(T) - Teil 15: LED-Display (3). ft:pedia 1/2017, S. 86-91.
<br>[25] Holtek: RAM Mapping 16*8 LED Controller Driver with keyscan HT16K33. Datasheet, Rev. 1.10, 16.05.2011.
<br>[26] Dirk Fox: I²C mit dem TX - Teil 2: LED-Display. ft:pedia 4/2012, S. 32-37.
<br>[27] Philips Semiconductors: SAA1064: 4-digit LED-driver with I2C-Bus interface. Data Sheet, Feb. 1991.
<br>[28] Dirk Fox: I²C mit dem TX(T) - Teil 9: LC-Displays. ft:pedia 1/2014, S. 47-57.
<br>[29] Robot Electronics: LCD05 - I²C/Serial LCD. Technical Dokumentation.
<br>[30] Thingm Labs: BlinkM Datasheet. 11.05.2011.
<br>[31] Christian Bergschneider, Stefan Fuss: Alternative Controller (3): Der ftPi - ein Motor Shield für den TX(T). ft:pedia 2/2016, S. 68-72.
<br>[32] Hitachi: HD44780U (LCD-II) - Dot Matrix Liquid Crystal Display Controller/Driver. Datasheet, Rev. 0.0, 9/1999.
<br>[33] NXP Semiconductors: PCA 9685 16-channel 12-bit PWM Fm+ I²C-bus LED controller. Product Data Sheet, Rev. 4, 16.04.2015.
<br>[34] Dirk Fox: I²C mit dem TX(T) - Teil 16: Servo Driver. ft:pedia 2/2017, S. 41-47.
<br>[35] Dirk Fox: I²C mit dem TX - Teil 6: GPS-Sensor. ft:pedia 3/2013, S. 54-62.
<br>[36] Dirk Fox: I²C mit dem TX(T) - Teil 17: Luftdruck- und Temperatursensor (2). ft:pedia 1/2019, S. 64-70.
<br>[37] Bosch Sensortec: BMP280 Digital Pressure Sensor. Data Sheet, v1.19, 08.01.2018.
<br>[38] NXP Semiconductors: PCF8574/A Remote 8-bit I/O expander for I2C-bus with interrupt, Product Data Sheet, Rev. 3, 03.06.2013.
<br>[39] Dirk Fox: I²C mit dem TX(T) - Teil 18: Keypads und I/O-Erweiterungen. ft:pedia 2/2019, S. 46-51.
<br>[40] Dirk Fox: Experimente mit dem Kombisensor. ft:pedia 3/2021, S. 78-91.
<br>[41] Dirk Fox: Experimente mit dem Kombisensor - Teil 2. ft:pedia 4/2021, S. 75-83.
