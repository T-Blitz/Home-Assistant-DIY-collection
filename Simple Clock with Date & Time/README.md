# Simple Clock with Date & Time for your HASS Dasboard

![Screenshot from 2024-07-10 15-00-08](https://github.com/T-Blitz/Home-Assistant-DIY-collection/assets/103434881/3276e64f-392b-4af0-8aae-fa02b74db6a2)
> If you use AM/PM, for some weird reason, then it should be automatically set by hass

### Time.Sensor
Go to Settings -> Devices & services -> Helpers -> + Create Helper<br/>
Select "Date and or time" give it the name "Time" ad make sure only time is selected at the bottom.<br/>

### TEMPLATE part
Go to Settings -> Devices & services -> Helpers -> + Create Helper
"Select Template a sensor" (not the binary one), then past the follwing code part in to the "State template*" field <br/>
Make sure to give it a simple name ("Full_Date" in this example):<br/>
```
{{ now().day }}
{{ ['Monday','Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday'][now().weekday()] }}
{{ ['January-01','February-02','March-03','April-04','May-05','June-06','July-07','August-0','September-09','October-10','November-11','December-12'][now().month-1] }}
{{ now().year }}
```
Now you have Template sensor for the Date.<br/>

### Image Element

Now go to your Dashboard and add a new "Image Element" card<br/>
past the following code in the code field:<br/>

```
show_state: true
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
  - entity: sensor.full_date
    style:
      color: var(--primary-text-color)
      font-size: 200%
      left: 50%
      top: 80%
    type: state-label
```
Save the card and now you should have a Simple Clock with Date and time on your Dashboard.<br/>
Enjoy.
