# German version

![Screenshot from 2024-07-09 17-20-21](https://github.com/T-Blitz/Home-Assistant-DIY-collection/assets/103434881/59c52854-260c-49bb-9662-ab0ec2273333)


### Zeit Sensor
Gehe in Hass zu den Einstellungen -> Geräte & Dienste -> + Integration Hinzufugen
Erstelle such fü "Datum und/oder Uhrzeit erstellen" 
gehe sicher dass du nur "Uhrzeit" ausgewhält ist.
### TEMPLATE part

Gehe in Hass zu den Einstellungen -> Geräte & Dienste -> Helfer -> HELFER ERSTELLEN
Wähle "Template" und dann "einen Sensor" (nicht den binären)
Sätze einen guten Namen (Voll-Datum in diesen Beispiel) und Kopiere folgendes in den "Zustandstemplate*":

```
{{ now().day }} 
{{ ['Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag','Sonntag'][now().weekday()] }} 
{{ ['Januar-01','Februar-02','März-03','April-04','Mai-05','Juni-06','Juli-07','August-0','September-09','Oktober-10','November-11','Dezember-12'][now().month-1] }} 
{{ now().year }} 
```
Nun hast du ein Template das die wie im beispiel Bild dass Datum anzeight.

### Bildelement

Nun erstelle ein neues Bildelement aud dein Dasboard hinzu un füge folgenden Code ein:

```show_state: true
show_name: true
camera_view: auto
type: picture-elements
image: >-
  data:image/svg+xml,%3Csvg%20width%3D%22300%22%20height%3D%22130%22%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%2F%3E
elements:
  - entity: sensor.time
    style:
      color: var(--accent-color)
      font-size: 600%
      left: 50%
      top: 45%
    type: state-label
  - entity: sensor.voll_datum
    style:
      color: var(--primary-text-color)
      font-size: 200%
      left: 50%
      top: 80%
    type: state-label
```
Speichere es und nun soltest du eine Uhr In HASS haben.
