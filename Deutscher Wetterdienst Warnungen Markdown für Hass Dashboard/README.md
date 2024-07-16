## INFO FÜR DIESEN ORDNER


Füge den Markdown bei hass ein, in dem du ein "Markdown pannel" selectierst.
Copy und paste denn Test in HAss ein, Andere denn text so dass sie deine Celle ID besitzt


[Download der Cellen ID Liste](https://www.dwd.de/DE/leistungen/opendata/help/warnungen/cap_warncellids_csv.csv?__blob=publicationFile&v=6) 

.csv kann mit MS excel und oder LibreOffice Calc geöfnet werden. Dannach einfach nach deinem Ort suchen und ID Kopieren

[Quelle des Markdowns + Video erklärung + Wetterwarn Karte](https://youtu.be/yYK5giUO19E?si=SEKdgYRtJgSTcggH)


```
# Deine City heir ---------(Diese zeile Nicht copieren)

{% set current_count = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_current_warning_level", "warning_count") %}
{% set advance_count = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_advance_warning_level", "warning_count") %}
{% if ((current_count == 0 or current_count == None) and (advance_count == 0 or advance_count == None)) %}
  **<font color=#44739e>Keine Warnungen</font>**
{% else %}
  {% for i in range(current_count) %}
    {% set headline = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_current_warning_level", "warning_" ~ loop.index ~ "_headline") %}
    {% set description = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_current_warning_level", "warning_" ~ loop.index ~ "_description") %}
    {% set level = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_current_warning_level", "warning_" ~ loop.index ~ "_level") %}
    {% set time_start = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_current_warning_level", "warning_" ~ loop.index ~ "_start") | as_timestamp %}
    {% set weekday_start = time_start | timestamp_custom("%w", True) | int %}
    {% set time_end = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_current_warning_level", "warning_" ~ loop.index ~ "_end") | as_timestamp %}
    {% set weekday_end = time_end | timestamp_custom("%w", True) | int %}
**<font color=#fdd835>{{ headline }}</font>**     
*<font color=gray>{{ ['Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag','Sonntag'][weekday_start-1] ~ ", " ~ time_start | timestamp_custom("%H:%M") ~ " - " ~ ['Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag','Sonntag'][weekday_end-1] ~ ", " ~ time_end | timestamp_custom("%H:%M") }}</font>*
    {{ description|trim }}
    {% if not loop.last %}
***
    {% endif %}
  {% endfor %}
  {% if ((current_count != 0) and (advance_count != 0)) %}{% endif %}
  {% for i in range(advance_count) %}
    {% set headline = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_advance_warning_level", "warning_" ~ loop.index ~ "_headline") %}
    {% set description = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_advance_warning_level", "warning_" ~ loop.index ~ "_description") %}
    {% set level = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_advance_warning_level", "warning_" ~ loop.index ~ "_level") %}
    {% set time_start = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_advance_warning_level", "warning_" ~ loop.index ~ "_start") | as_timestamp%}
    {% set weekday_start = time_start | timestamp_custom("%w", True) | int %}
    {% set time_end = state_attr("sensor.dwd_weather_warnings_{MACH_DEINE_CELL_ID_HEIR_REIN})_advance_warning_level", "warning_" ~ loop.index ~ "_end") | as_timestamp %}
    {% set weekday_end = time_end | timestamp_custom("%w", True) | int %}
**<font color=#fdd835>{{ headline }}</font>**
*<font color=gray>{{ ['Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag','Sonntag'][weekday_start-1] ~ ", " ~ time_start | timestamp_custom("%H:%M") ~ " - " ~ ['Montag','Dienstag','Mittwoch','Donnerstag','Freitag','Samstag','Sonntag'][weekday_end-1] ~ ", " ~ time_end | timestamp_custom("%H:%M") }}</font>*
    {{ description|trim }}
    {% if not loop.last %}
***
    {% endif %}
  {% endfor %}
{% endif %}
```
