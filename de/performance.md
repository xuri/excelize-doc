# Leistung

Die folgenden Leistungsdaten zeigen die Ausführungszeit und die Speichernutzung für Arbeitsblätter mit der Größe `N` Zeilen x `50` Spalten mit einer 50/50-Mischung aus Zeichenfolgen und Zahlen. Die Zahlen stammen von einer beliebigen Maschine mittlerer Reichweite (Betriebssystem: macOS Catalina Version 10.15.7, CPU: 3.4 GHz Intel Core i5, RAM: 16 GB, 2400 MHz DDR4, Festplatte: 1 TB, Go-Version: `go1.15.2 darwin/amd64`, Commit: [`9316028`](https://github.com/360EntSecGroup-Skylar/excelize/tree/93160287bb7fa6479c73ee031b5ed771972a17a8)). Specific figures will vary from machine to machine but the trends should be the same.

<table>
    <tr>
        <th>Typ</th>
        <th>Zeilen</th>
        <th>Säulen</th>
        <th>Zeit (s)</th>
        <th>Erinnerung (MB)</th>
    </tr>
    <tr>
        <td rowspan="10">Zellenwert einstellen</td>
        <td>200</td>
        <td>50</td>
        <td>0.018</td>
        <td>2</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>0.033</td>
        <td>2</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>0.060</td>
        <td>4</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>0.119</td>
        <td>11</td>
    </tr>
    <tr>
        <td>3200</td>
        <td>50</td>
        <td>0.240</td>
        <td>22</td>
    </tr>
    <tr>
        <td>6400</td>
        <td>50</td>
        <td>0.458</td>
        <td>44</td>
    </tr>
    <tr>
        <td>12800</td>
        <td>50</td>
        <td>0.960</td>
        <td>46</td>
    </tr>
    <tr>
        <td>25600</td>
        <td>50</td>
        <td>1.973</td>
        <td>49</td>
    </tr>
    <tr>
        <td>52100</td>
        <td>50</td>
        <td>4.044</td>
        <td>67</td>
    </tr>
    <tr>
        <td>102400</td>
        <td>50</td>
        <td>7.791</td>
        <td>131</td>
    </tr>
    <tr>
        <td rowspan="1">Diagramm hinzufügen</td>
        <td>200</td>
        <td>50</td>
        <td>8.77</td>
        <td>156</td>
    </tr>
    <tr>
        <td rowspan="4">Stellen Sie HyperLink ein</td>
        <td>200</td>
        <td>50</td>
        <td>1.08</td>
        <td>9</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>1.12</td>
        <td>9</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>16.9</td>
        <td>31</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>0.59</td>
        <td>63</td>
    </tr>
    <tr>
        <td rowspan="4">Bild einfügen</td>
        <td>200</td>
        <td>50</td>
        <td>1,57</td>
        <td>47</td>
    </tr>
    <tr>
        <td>400</td>
        <td>50</td>
        <td>5.01</td>
        <td>94</td>
    </tr>
    <tr>
        <td>800</td>
        <td>50</td>
        <td>18.56</td>
        <td>188</td>
    </tr>
    <tr>
        <td>1600</td>
        <td>50</td>
        <td>74</td>
        <td>374</td>
    </tr>
</table>

## Leistungsvergleich ähnlicher Bibliotheken

Die folgende Grafik zeigt den Leistungsvergleich der Klartextmatrix der Generation `102400*50` durch die wichtigsten Open-Source-Excel-Bibliotheken unter Personal Computer (Betriebssystem: macOS Catalina Version 10.15.7, CPU: 3,4 GHz Intel Core i5, RAM: 16 GB) 2400 MHz DDR4, Festplatte: 1 TB), einschließlich Go, Python, Java, PHP und NodeJS.

<p align="center"><img width="688" src="https://xuri.me/wp-content/uploads/2016/08/excelize-golang-library-for-reading-and-writing-xlsx-files-3.png" alt="Leistungsvergleich ähnlicher Bibliotheken"></p>
