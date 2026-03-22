Databron: https://denhaag.dataplatform.nl/#/data/1ffa4758-d143-4d78-b510-a713ab8365df

"Beschrijving: Meldingen van burgers in de openbare ruimte. De data wordt sinds januari 2024 door de betreffende afdeling niet meer geleverd. De bestanden bevatten dus historische gegevens van vóór die datum. De shape en geojson bestanden bevatten de meldingen waarvan de locatie is aangeduid met behulp van het dichtstbijzijnde adres, waarvan de coördinaten bekend zijn. Dit betreft ongeveer 80% van het totaal aantal meldingen. De meldingen gaan tot ongeveer 3 jaar terug. Het csv bestand bevat alle meldingen, ook die zonder exacte locatie aanduiding, en gaat terug tot 1 januari 2013. Hiervan is het percentage meldingen met coordinaten ongeveer 60%."

# Eerste dataverkenning

# Importeer de benodigde Python‑packages


```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import plotly.express as px
```

# Laad de data en bekijk de eerste vijf rijen van de dataset


```python
df = pd.read_csv('meldingen_.csv', low_memory=False)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>WKT</th>
      <th>ogc_fid</th>
      <th>zaaknummer</th>
      <th>zaaktype</th>
      <th>niveau1</th>
      <th>niveau2</th>
      <th>niveau3</th>
      <th>niveau4</th>
      <th>stadsdeel</th>
      <th>registrdat</th>
      <th>...</th>
      <th>huisletter</th>
      <th>toevoeging</th>
      <th>wijk</th>
      <th>buurt</th>
      <th>afdeling</th>
      <th>oplossing</th>
      <th>counter</th>
      <th>objectid</th>
      <th>xcoord</th>
      <th>ycoord</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MULTIPOINT ((76375.119 453365.016))</td>
      <td>1</td>
      <td>734187</td>
      <td>Melding Openbare Ruimte</td>
      <td>Riolering, Water en Constructies</td>
      <td>Riool</td>
      <td>huisaansluiting</td>
      <td>kan niet lozen</td>
      <td>Loosduinen</td>
      <td>2016-07-01T12:28:35</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Waldeck</td>
      <td>Nieuw Waldeck</td>
      <td>Riolering</td>
      <td>Opgelost</td>
      <td>186</td>
      <td>186</td>
      <td>76375.119</td>
      <td>453365.016</td>
    </tr>
    <tr>
      <th>1</th>
      <td>MULTIPOINT ((85510.15 451385.08))</td>
      <td>2</td>
      <td>734191</td>
      <td>Melding Openbare Ruimte</td>
      <td>Afval</td>
      <td>Verzamelcontainer</td>
      <td>Restafval</td>
      <td>Vol</td>
      <td>Leidschenveen-Ypenburg</td>
      <td>2016-07-01T12:34:42</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Ypenburg</td>
      <td>Morgenweide</td>
      <td>HMS</td>
      <td>NaN</td>
      <td>189</td>
      <td>189</td>
      <td>85510.150</td>
      <td>451385.080</td>
    </tr>
    <tr>
      <th>2</th>
      <td>MULTIPOINT ((76401.81 452015.138))</td>
      <td>3</td>
      <td>734194</td>
      <td>Melding Openbare Ruimte</td>
      <td>Afval</td>
      <td>Zwerfvuil</td>
      <td>Op openbare weg</td>
      <td>NaN</td>
      <td>Loosduinen</td>
      <td>2016-07-01T12:39:57</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Loosduinen</td>
      <td>Houtwijk</td>
      <td>Straten-serviceploeg</td>
      <td>Wordt meegenomen in gepland onderhoud</td>
      <td>191</td>
      <td>191</td>
      <td>76401.810</td>
      <td>452015.138</td>
    </tr>
    <tr>
      <th>3</th>
      <td>MULTIPOINT ((78874.023 456134.274))</td>
      <td>4</td>
      <td>734195</td>
      <td>Melding Openbare Ruimte</td>
      <td>Afval</td>
      <td>Inzameling huisvuil</td>
      <td>Huisvuilzak</td>
      <td>Niet opgehaald</td>
      <td>Scheveningen</td>
      <td>2016-07-01T12:40:00</td>
      <td>...</td>
      <td>A</td>
      <td>NaN</td>
      <td>Geuzen- en Statenkwartier</td>
      <td>Statenkwartier</td>
      <td>HMS</td>
      <td>NaN</td>
      <td>193</td>
      <td>193</td>
      <td>78874.025</td>
      <td>456134.278</td>
    </tr>
    <tr>
      <th>4</th>
      <td>MULTIPOINT ((80003.281 455564.21))</td>
      <td>5</td>
      <td>734196</td>
      <td>Melding Openbare Ruimte</td>
      <td>Straten en straatmeubilair</td>
      <td>Anti-parkeerpaal/ Hagenaartje</td>
      <td>Verwijderen</td>
      <td>NaN</td>
      <td>Centrum</td>
      <td>2016-07-01T12:40:02</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Zeeheldenkwartier</td>
      <td>Zeeheldenkwartier</td>
      <td>Wegbeheer Centrum</td>
      <td>Informatie verstrekt</td>
      <td>195</td>
      <td>195</td>
      <td>80003.281</td>
      <td>455564.210</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 29 columns</p>
</div>



Laten we de kolomnamen bekijken


```python
df.columns
```




    Index(['WKT', 'ogc_fid', 'zaaknummer', 'zaaktype', 'niveau1', 'niveau2',
           'niveau3', 'niveau4', 'stadsdeel', 'registrdat', 'verlengen',
           'vervaldat', 'afgerondop', 'binnenkmst', 'prioriteit', 'externstat',
           'internstat', 'straat', 'huisnummer', 'huisletter', 'toevoeging',
           'wijk', 'buurt', 'afdeling', 'oplossing', 'counter', 'objectid',
           'xcoord', 'ycoord'],
          dtype='object')



Laten we het aantal meldingen bekijken


```python
len(df)
```




    468553



We zien in totaal 468.553 meldingen. Laten we kijken van welk jaar tot welk jaar deze meldingen lopen.


```python
df['registrdat'].value_counts().sort_index()
```




    registrdat
    2016-07-01T01:26:58    1
    2016-07-01T07:25:51    1
    2016-07-01T07:45:21    1
    2016-07-01T08:04:30    1
    2016-07-01T08:06:03    1
                          ..
    2024-01-15T11:38:25    1
    2024-01-16T18:37:47    1
    2024-01-17T15:55:33    1
    2024-01-18T12:22:00    1
    2024-01-18T16:09:00    1
    Name: count, Length: 467376, dtype: int64



We zien dat de registraties lopen van 2016 tot en met 2024. Laten we een nieuwe kolom aanmaken zodat we de data per jaar kunnen bekijken en groeperen.


```python
print(df.dtypes)
```

    WKT            object
    ogc_fid         int64
    zaaknummer      int64
    zaaktype       object
    niveau1        object
    niveau2        object
    niveau3        object
    niveau4        object
    stadsdeel      object
    registrdat     object
    verlengen      object
    vervaldat      object
    afgerondop     object
    binnenkmst     object
    prioriteit     object
    externstat     object
    internstat     object
    straat         object
    huisnummer      int64
    huisletter     object
    toevoeging     object
    wijk           object
    buurt          object
    afdeling       object
    oplossing      object
    counter         int64
    objectid        int64
    xcoord        float64
    ycoord        float64
    dtype: object
    


```python
df["registrdat"] = pd.to_datetime(df["registrdat"])

print(df["registrdat"].dtype) 
```

    datetime64[ns]
    


```python
df["jaar"] = df["registrdat"].dt.year
df["jaar"].head()
```




    0    2016
    1    2016
    2    2016
    3    2016
    4    2016
    Name: jaar, dtype: int32



_______________________________

# Hoeveel meldingen zijn er per jaar geregistreerd?



```python
counts_per_year = df.groupby("jaar").size().rename_axis('jaar').reset_index(name='het aantal meldingen')
print(counts_per_year)
```

       jaar  het aantal meldingen
    0  2016                 20451
    1  2017                 46715
    2  2018                 64062
    3  2019                 72814
    4  2020                 92810
    5  2021                 88304
    6  2022                 42417
    7  2023                 40930
    8  2024                    50
    

**Interactieve figuur**


```python
fig = px.bar(
counts_per_year,
    x="jaar",
    y="het aantal meldingen",
    title="Welk jaar heeft het hoogste aantal meldingen?", color = 'jaar',
    hover_data=counts_per_year.columns  
)

fig.show()
```


<div>                            <div id="238e5e4b-0856-4827-abd1-1eb0684774da" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("238e5e4b-0856-4827-abd1-1eb0684774da")) {                    Plotly.newPlot(                        "238e5e4b-0856-4827-abd1-1eb0684774da",                        [{"alignmentgroup":"True","hovertemplate":"jaar=%{marker.color}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"","marker":{"color":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"coloraxis":"coloraxis","pattern":{"shape":""}},"name":"","offsetgroup":"","orientation":"v","showlegend":false,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[20451,46715,64062,72814,92810,88304,42417,40930,50],"yaxis":"y"}],                        {"barmode":"relative","coloraxis":{"colorbar":{"title":{"text":"jaar"}},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"legend":{"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Welk jaar heeft het hoogste aantal meldingen?"},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"jaar"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"het aantal meldingen"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('238e5e4b-0856-4827-abd1-1eb0684774da');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


2020 en 2021 waren de jaren met de hoogste aantal meldingen

# Hoe zijn de meldingen ingediend?


```python
df['binnenkmst'].value_counts().rename_axis('manier').reset_index(name='het aantal meldingen')

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>manier</th>
      <th>het aantal meldingen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>formulier met geo-inf</td>
      <td>258596</td>
    </tr>
    <tr>
      <th>1</th>
      <td>BuitenBeter</td>
      <td>99694</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Telefoon</td>
      <td>79122</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Web formulier</td>
      <td>12903</td>
    </tr>
    <tr>
      <th>4</th>
      <td>E-mail</td>
      <td>5788</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Interne Melding</td>
      <td>4804</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Social Media</td>
      <td>4016</td>
    </tr>
    <tr>
      <th>7</th>
      <td>App melding</td>
      <td>1273</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Andere meldingen app</td>
      <td>1160</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Verbeterdebuurt</td>
      <td>1076</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Balie</td>
      <td>48</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Brief</td>
      <td>40</td>
    </tr>
    <tr>
      <th>12</th>
      <td>E-mail Ombudsman</td>
      <td>18</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Fietsersbond</td>
      <td>8</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Mobiel formulier</td>
      <td>5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Brief (regio/6 weken)</td>
      <td>1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Post (buiten regio HL)</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python

counts = (
    df.groupby(["jaar", "binnenkmst"])
    .size()
    .rename("het aantal meldingen")
    .reset_index(name='het aantal meldingen')
)



counts_sorted = counts.sort_values("het aantal meldingen", ascending=False)

counts_sorted.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>jaar</th>
      <th>binnenkmst</th>
      <th>het aantal meldingen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>72</th>
      <td>2020</td>
      <td>formulier met geo-inf</td>
      <td>50680</td>
    </tr>
    <tr>
      <th>84</th>
      <td>2021</td>
      <td>formulier met geo-inf</td>
      <td>45678</td>
    </tr>
    <tr>
      <th>98</th>
      <td>2023</td>
      <td>formulier met geo-inf</td>
      <td>40553</td>
    </tr>
    <tr>
      <th>95</th>
      <td>2022</td>
      <td>formulier met geo-inf</td>
      <td>36324</td>
    </tr>
    <tr>
      <th>58</th>
      <td>2019</td>
      <td>formulier met geo-inf</td>
      <td>34985</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2018</td>
      <td>formulier met geo-inf</td>
      <td>30062</td>
    </tr>
    <tr>
      <th>76</th>
      <td>2021</td>
      <td>BuitenBeter</td>
      <td>26063</td>
    </tr>
    <tr>
      <th>63</th>
      <td>2020</td>
      <td>BuitenBeter</td>
      <td>21968</td>
    </tr>
    <tr>
      <th>49</th>
      <td>2019</td>
      <td>BuitenBeter</td>
      <td>19433</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2017</td>
      <td>Telefoon</td>
      <td>16616</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig = px.bar(
    counts,
    x="jaar",
    y="het aantal meldingen",
    color="binnenkmst",
    title="Aantal meldingen per manier van binnenkomst per jaar",
    barmode="group"
)

fig.show()
```


<div>                            <div id="fa463e43-e7c1-46b7-84bd-8acf2da48792" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("fa463e43-e7c1-46b7-84bd-8acf2da48792")) {                    Plotly.newPlot(                        "fa463e43-e7c1-46b7-84bd-8acf2da48792",                        [{"alignmentgroup":"True","hovertemplate":"binnenkmst=Andere meldingen app<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Andere meldingen app","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Andere meldingen app","offsetgroup":"Andere meldingen app","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[4,225,634,75,184,35,3],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=App melding<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"App melding","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"App melding","offsetgroup":"App melding","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[26,2,146,559,70,454,16],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Balie<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Balie","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Balie","offsetgroup":"Balie","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[1,6,10,22,4,2,3],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Brief<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Brief","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Brief","offsetgroup":"Brief","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020],"xaxis":"x","y":[4,24,3,6,3],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=BuitenBeter<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"BuitenBeter","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"BuitenBeter","offsetgroup":"BuitenBeter","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[3792,10556,14004,19433,21968,26063,3878],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=E-mail<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"E-mail","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"E-mail","offsetgroup":"E-mail","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023],"xaxis":"x","y":[850,1777,911,502,859,670,218,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=E-mail Ombudsman<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"E-mail Ombudsman","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"E-mail Ombudsman","offsetgroup":"E-mail Ombudsman","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2020,2021],"xaxis":"x","y":[6,7,2,2,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Fietsersbond<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Fietsersbond","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Fietsersbond","offsetgroup":"Fietsersbond","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2020],"xaxis":"x","y":[3,2,2,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Interne Melding<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Interne Melding","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Interne Melding","offsetgroup":"Interne Melding","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[653,1575,834,531,595,541,75],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Social Media<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Social Media","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Social Media","offsetgroup":"Social Media","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[404,1319,806,852,412,216,7],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Telefoon<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Telefoon","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Telefoon","offsetgroup":"Telefoon","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[7889,16616,13701,12812,14784,11826,1494],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Verbeterdebuurt<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Verbeterdebuurt","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Verbeterdebuurt","offsetgroup":"Verbeterdebuurt","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[72,119,239,369,194,75,8],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Web formulier<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Web formulier","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Web formulier","offsetgroup":"Web formulier","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023],"xaxis":"x","y":[549,419,2706,2665,3054,2743,391,376],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=formulier met geo-inf<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"formulier met geo-inf","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"formulier met geo-inf","offsetgroup":"formulier met geo-inf","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[6198,14066,30062,34985,50680,45678,36324,40553,50],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Brief (regio/6 weken)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Brief (regio/6 weken)","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Brief (regio/6 weken)","offsetgroup":"Brief (regio/6 weken)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2017],"xaxis":"x","y":[1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Mobiel formulier<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Mobiel formulier","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Mobiel formulier","offsetgroup":"Mobiel formulier","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2017,2018,2019],"xaxis":"x","y":[1,2,2],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"binnenkmst=Post (buiten regio HL)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Post (buiten regio HL)","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Post (buiten regio HL)","offsetgroup":"Post (buiten regio HL)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2019],"xaxis":"x","y":[1],"yaxis":"y"}],                        {"barmode":"group","legend":{"title":{"text":"binnenkmst"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Aantal meldingen per manier van binnenkomst per jaar"},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"jaar"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"het aantal meldingen"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('fa463e43-e7c1-46b7-84bd-8acf2da48792');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


Het formulier met geo‑informatie was de meest gebruikte manier van meldingen indienen. In 2023 bleken meldingen alleen via het formulier met geo‑informatie en het webformulier te zijn ingediend.

Wat is er aan de hand?


```python
counts_per_year_per_issue = (
    df.groupby(["jaar", "niveau1"])
    .size()
    .rename_axis(["jaar", "kwesties"])
    .reset_index(name="het aantal meldingen")
)

print(counts_per_year_per_issue)
```

        jaar                                    kwesties  het aantal meldingen
    0   2016                                       Afval                 11469
    1   2016                      Bedrijven/ evenementen                    66
    2   2016     Graffiti/ posters/ stickers verwijderen                   207
    3   2016                                       Groen                  1444
    4   2016                  Onveilige verkeerssituatie                   219
    ..   ...                                         ...                   ...
    95  2024                                    Parkeren                     4
    96  2024            Riolering, Water en Constructies                    19
    97  2024                                Speelterrein                     1
    98  2024                  Straten en straatmeubilair                     5
    99  2024  Verkeerslichten/ borden/ straatverlichting                    14
    
    [100 rows x 3 columns]
    


```python
fig = px.bar(
  counts_per_year_per_issue,
    x="jaar",
    y="het aantal meldingen",
    color="kwesties",
    title="Aantal meldingen per kwestie per jaar",
    barmode="group"
)

fig.show()
```


<div>                            <div id="2e97ad2f-3814-4542-af20-ffe73b481239" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("2e97ad2f-3814-4542-af20-ffe73b481239")) {                    Plotly.newPlot(                        "2e97ad2f-3814-4542-af20-ffe73b481239",                        [{"alignmentgroup":"True","hovertemplate":"kwesties=Afval<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Afval","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Afval","offsetgroup":"Afval","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022],"xaxis":"x","y":[11469,27449,32973,34390,50982,44659,214],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Bedrijven/ evenementen<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Bedrijven/ evenementen","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Bedrijven/ evenementen","offsetgroup":"Bedrijven/ evenementen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023],"xaxis":"x","y":[66,109,159,249,273,216,48,30],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Graffiti/ posters/ stickers verwijderen<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Graffiti/ posters/ stickers verwijderen","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Graffiti/ posters/ stickers verwijderen","offsetgroup":"Graffiti/ posters/ stickers verwijderen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023],"xaxis":"x","y":[207,470,574,942,1002,965,1134,1124],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Groen<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Groen","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Groen","offsetgroup":"Groen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[1444,3479,4103,5102,6413,5817,4936,5655,2],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Onveilige verkeerssituatie<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Onveilige verkeerssituatie","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Onveilige verkeerssituatie","offsetgroup":"Onveilige verkeerssituatie","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[219,494,1263,1603,2251,1755,1479,1652,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Parkeren<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Parkeren","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Parkeren","offsetgroup":"Parkeren","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[406,802,1253,1692,2380,1862,1822,1554,4],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Riolering, Water en Constructies<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Riolering, Water en Constructies","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Riolering, Water en Constructies","offsetgroup":"Riolering, Water en Constructies","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[918,2044,1756,1992,2283,2337,1959,2559,19],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Speelterrein<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Speelterrein","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Speelterrein","offsetgroup":"Speelterrein","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[143,294,467,513,763,729,675,608,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Straten en straatmeubilair<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Straten en straatmeubilair","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Straten en straatmeubilair","offsetgroup":"Straten en straatmeubilair","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[3391,7138,9239,10701,9847,10400,11798,10396,5],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Verkeerslichten/ borden/ straatverlichting<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Verkeerslichten/ borden/ straatverlichting","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Verkeerslichten/ borden/ straatverlichting","offsetgroup":"Verkeerslichten/ borden/ straatverlichting","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[2188,4436,6433,6831,7640,7821,8034,7864,14],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Achtergelaten voertuig/ fiets<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Achtergelaten voertuig/ fiets","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Achtergelaten voertuig/ fiets","offsetgroup":"Achtergelaten voertuig/ fiets","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[4189,6227,6500,9430,9800,9390,4],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Afvalbakken<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Afvalbakken","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Afvalbakken","offsetgroup":"Afvalbakken","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2018],"xaxis":"x","y":[3],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"kwesties=Dieren en hondenpoep<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Dieren en hondenpoep","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Dieren en hondenpoep","offsetgroup":"Dieren en hondenpoep","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2018,2019,2020,2021,2022,2023],"xaxis":"x","y":[1649,2572,2474,2313,518,98],"yaxis":"y"}],                        {"barmode":"group","legend":{"title":{"text":"kwesties"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Aantal meldingen per kwestie per jaar"},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"jaar"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"het aantal meldingen"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('2e97ad2f-3814-4542-af20-ffe73b481239');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


De meeste meldingen blijken afval‑gerelateerd te zijn.

# Oplossingstatus


```python
df['oplossing'].value_counts().rename_axis('status').reset_index(name='het aantal meldingen')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>status</th>
      <th>het aantal meldingen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Handhavingsorganisatie oplossing</td>
      <td>82619</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Wordt meegenomen in gepland onderhoud</td>
      <td>63380</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Informatie verstrekt</td>
      <td>56670</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Opgelost</td>
      <td>51624</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Wordt verder behandeld in GISIB (OVL)</td>
      <td>22973</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Afgewezen</td>
      <td>8611</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Wordt verder behandeld in HPS (R&amp;W)</td>
      <td>4773</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wordt verder behandeld in Viadesk (R&amp;W)</td>
      <td>3953</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Wordt verder behandeld in Vera+ (VM)</td>
      <td>1507</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Wordt verder behandeld in OVIN (OVL)</td>
      <td>727</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Straten-serviceploeg</td>
      <td>359</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Wordt verder behandeld in BWT4All (Graffiti)</td>
      <td>131</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Wordt verder behandeld in MPM (MenV)</td>
      <td>123</td>
    </tr>
  </tbody>
</table>
</div>




```python

counts_oplossing = (
    df.groupby(["jaar", "oplossing"])
    .size()
    .rename("het aantal meldingen")
    .reset_index(name='het aantal meldingen')
)



counts_sorted_oplossing = counts_oplossing.sort_values("het aantal meldingen", ascending=False)

counts_sorted_oplossing.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>jaar</th>
      <th>oplossing</th>
      <th>het aantal meldingen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>48</th>
      <td>2020</td>
      <td>Handhavingsorganisatie oplossing</td>
      <td>15538</td>
    </tr>
    <tr>
      <th>60</th>
      <td>2021</td>
      <td>Handhavingsorganisatie oplossing</td>
      <td>14820</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2019</td>
      <td>Handhavingsorganisatie oplossing</td>
      <td>12670</td>
    </tr>
    <tr>
      <th>88</th>
      <td>2023</td>
      <td>Wordt meegenomen in gepland onderhoud</td>
      <td>11654</td>
    </tr>
    <tr>
      <th>76</th>
      <td>2022</td>
      <td>Wordt meegenomen in gepland onderhoud</td>
      <td>11609</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2018</td>
      <td>Handhavingsorganisatie oplossing</td>
      <td>11466</td>
    </tr>
    <tr>
      <th>50</th>
      <td>2020</td>
      <td>Opgelost</td>
      <td>10071</td>
    </tr>
    <tr>
      <th>38</th>
      <td>2019</td>
      <td>Opgelost</td>
      <td>9906</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2017</td>
      <td>Handhavingsorganisatie oplossing</td>
      <td>9784</td>
    </tr>
    <tr>
      <th>49</th>
      <td>2020</td>
      <td>Informatie verstrekt</td>
      <td>9522</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig = px.bar(
    counts_sorted_oplossing,
    x="jaar",
    y="het aantal meldingen",
    color="oplossing",
    title="Oplossingstatus per jaar",
    barmode="group"
)

fig.show()
```


<div>                            <div id="02564708-8fea-4a35-b000-66d33cacbd61" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("02564708-8fea-4a35-b000-66d33cacbd61")) {                    Plotly.newPlot(                        "02564708-8fea-4a35-b000-66d33cacbd61",                        [{"alignmentgroup":"True","hovertemplate":"oplossing=Handhavingsorganisatie oplossing<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Handhavingsorganisatie oplossing","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Handhavingsorganisatie oplossing","offsetgroup":"Handhavingsorganisatie oplossing","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2020,2021,2019,2018,2017,2022,2023,2016],"xaxis":"x","y":[15538,14820,12670,11466,9784,7662,6655,4024],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt meegenomen in gepland onderhoud<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt meegenomen in gepland onderhoud","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Wordt meegenomen in gepland onderhoud","offsetgroup":"Wordt meegenomen in gepland onderhoud","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2023,2022,2021,2018,2020,2019,2017,2016],"xaxis":"x","y":[11654,11609,8885,8274,7680,7670,5137,2471],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Opgelost<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Opgelost","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Opgelost","offsetgroup":"Opgelost","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2020,2019,2017,2021,2018,2016,2022,2023],"xaxis":"x","y":[10071,9906,8793,7691,7681,4373,1917,1192],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Informatie verstrekt<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Informatie verstrekt","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Informatie verstrekt","offsetgroup":"Informatie verstrekt","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2020,2021,2019,2018,2017,2023,2022,2016,2024],"xaxis":"x","y":[9522,9305,9211,8315,6249,6122,5680,2245,21],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in GISIB (OVL)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in GISIB (OVL)","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Wordt verder behandeld in GISIB (OVL)","offsetgroup":"Wordt verder behandeld in GISIB (OVL)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2022,2023,2020,2019,2021,2018,2017,2016,2024],"xaxis":"x","y":[3653,3546,3521,3479,3263,3160,1696,647,8],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Afgewezen<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Afgewezen","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Afgewezen","offsetgroup":"Afgewezen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2020,2018,2019,2021,2023,2022,2017,2016,2024],"xaxis":"x","y":[1521,1413,1375,1356,882,752,706,605,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in Viadesk (R&W)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in Viadesk (R&W)","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Wordt verder behandeld in Viadesk (R&W)","offsetgroup":"Wordt verder behandeld in Viadesk (R&W)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2023,2020,2019,2021,2022,2018,2017,2016,2024],"xaxis":"x","y":[993,753,650,615,421,343,168,9,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in HPS (R&W)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in HPS (R&W)","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Wordt verder behandeld in HPS (R&W)","offsetgroup":"Wordt verder behandeld in HPS (R&W)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2021,2020,2019,2022,2018,2023,2017,2016,2024],"xaxis":"x","y":[880,821,688,637,611,533,462,140,1],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in OVIN (OVL)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in OVIN (OVL)","marker":{"color":"#FF97FF","pattern":{"shape":""}},"name":"Wordt verder behandeld in OVIN (OVL)","offsetgroup":"Wordt verder behandeld in OVIN (OVL)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016],"xaxis":"x","y":[727],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in Vera+ (VM)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in Vera+ (VM)","marker":{"color":"#FECB52","pattern":{"shape":""}},"name":"Wordt verder behandeld in Vera+ (VM)","offsetgroup":"Wordt verder behandeld in Vera+ (VM)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2023,2019,2018,2020,2022,2021,2017,2016],"xaxis":"x","y":[375,215,213,212,199,184,68,41],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Straten-serviceploeg<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Straten-serviceploeg","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Straten-serviceploeg","offsetgroup":"Straten-serviceploeg","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2019,2020,2022,2023,2021,2018],"xaxis":"x","y":[192,118,18,18,11,2],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in BWT4All (Graffiti)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in BWT4All (Graffiti)","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Wordt verder behandeld in BWT4All (Graffiti)","offsetgroup":"Wordt verder behandeld in BWT4All (Graffiti)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2017,2021,2018,2022,2020,2023,2019,2016],"xaxis":"x","y":[48,28,20,9,9,8,5,4],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"oplossing=Wordt verder behandeld in MPM (MenV)<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Wordt verder behandeld in MPM (MenV)","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Wordt verder behandeld in MPM (MenV)","offsetgroup":"Wordt verder behandeld in MPM (MenV)","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2022,2021,2023,2018,2017,2019,2020,2016],"xaxis":"x","y":[45,19,15,12,11,11,8,2],"yaxis":"y"}],                        {"barmode":"group","legend":{"title":{"text":"oplossing"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Oplossingstatus per jaar"},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"jaar"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"het aantal meldingen"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('02564708-8fea-4a35-b000-66d33cacbd61');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


De oplossing wordt in de meeste gevallen door de handhavingsorganisatie verleend.

# Welk stadsdeel heeft het hoogste aantal meldingen? Interactieve figuur:


```python
df['stadsdeel'].value_counts().rename_axis('stads_deel').reset_index(name='het aantal meldingen')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>stads_deel</th>
      <th>het aantal meldingen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Escamp</td>
      <td>99316</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Centrum</td>
      <td>91480</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Segbroek</td>
      <td>57405</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Scheveningen</td>
      <td>53477</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Loosduinen</td>
      <td>47535</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Laak</td>
      <td>38391</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Haagse Hout</td>
      <td>37933</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Leidschenveen-Ypenburg</td>
      <td>36547</td>
    </tr>
  </tbody>
</table>
</div>




```python
stads_deel = df['stadsdeel'].value_counts().rename_axis('stads_deel').reset_index(name='het aantal meldingen')
```


```python
stads_deel_hoge_meldingen = stads_deel.iloc[:5].copy()
```


```python
fig = px.bar(
    stads_deel_hoge_meldingen,
    x="stads_deel",
    y="het aantal meldingen",
    title="Welk stadsdeel heeft het hoogste aantal meldingen?",color="stads_deel",                              
    color_discrete_sequence=["red", "orange", "yellow", "grey", "purple"],
    hover_data=stads_deel_hoge_meldingen.columns  
)
```


```python
fig.show()
```


<div>                            <div id="29d7dfdd-c54e-4e36-a165-5ea82e24f42e" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("29d7dfdd-c54e-4e36-a165-5ea82e24f42e")) {                    Plotly.newPlot(                        "29d7dfdd-c54e-4e36-a165-5ea82e24f42e",                        [{"alignmentgroup":"True","hovertemplate":"stads_deel=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Escamp","marker":{"color":"red","pattern":{"shape":""}},"name":"Escamp","offsetgroup":"Escamp","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["Escamp"],"xaxis":"x","y":[99316],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"stads_deel=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Centrum","marker":{"color":"orange","pattern":{"shape":""}},"name":"Centrum","offsetgroup":"Centrum","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["Centrum"],"xaxis":"x","y":[91480],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"stads_deel=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Segbroek","marker":{"color":"yellow","pattern":{"shape":""}},"name":"Segbroek","offsetgroup":"Segbroek","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["Segbroek"],"xaxis":"x","y":[57405],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"stads_deel=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Scheveningen","marker":{"color":"grey","pattern":{"shape":""}},"name":"Scheveningen","offsetgroup":"Scheveningen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["Scheveningen"],"xaxis":"x","y":[53477],"yaxis":"y"},{"alignmentgroup":"True","hovertemplate":"stads_deel=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Loosduinen","marker":{"color":"purple","pattern":{"shape":""}},"name":"Loosduinen","offsetgroup":"Loosduinen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":["Loosduinen"],"xaxis":"x","y":[47535],"yaxis":"y"}],                        {"barmode":"relative","legend":{"title":{"text":"stads_deel"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Welk stadsdeel heeft het hoogste aantal meldingen?"},"xaxis":{"anchor":"y","categoryarray":["Escamp","Centrum","Segbroek","Scheveningen","Loosduinen"],"categoryorder":"array","domain":[0.0,1.0],"title":{"text":"stads_deel"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"het aantal meldingen"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('29d7dfdd-c54e-4e36-a165-5ea82e24f42e');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


per jaar:


```python

counts_deel = (
    df.groupby(["jaar", "stadsdeel"])
    .size()
    .rename("het aantal meldingen")
    .reset_index(name='het aantal meldingen')
)



counts_sorted_deel = counts_deel.sort_values("het aantal meldingen", ascending=False)

counts_sorted_deel.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>jaar</th>
      <th>stadsdeel</th>
      <th>het aantal meldingen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33</th>
      <td>2020</td>
      <td>Escamp</td>
      <td>20497</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2021</td>
      <td>Escamp</td>
      <td>18761</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2021</td>
      <td>Centrum</td>
      <td>17211</td>
    </tr>
    <tr>
      <th>32</th>
      <td>2020</td>
      <td>Centrum</td>
      <td>17017</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2019</td>
      <td>Escamp</td>
      <td>15330</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2019</td>
      <td>Centrum</td>
      <td>14048</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2018</td>
      <td>Escamp</td>
      <td>13691</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2018</td>
      <td>Centrum</td>
      <td>12909</td>
    </tr>
    <tr>
      <th>47</th>
      <td>2021</td>
      <td>Segbroek</td>
      <td>11614</td>
    </tr>
    <tr>
      <th>39</th>
      <td>2020</td>
      <td>Segbroek</td>
      <td>11286</td>
    </tr>
  </tbody>
</table>
</div>




```python
counts_sorted_deel["stadsdeel"].value_counts()
```




    stadsdeel
    Escamp                    9
    Centrum                   9
    Segbroek                  9
    Scheveningen              9
    Loosduinen                9
    Laak                      9
    Haagse Hout               9
    Leidschenveen-Ypenburg    9
    Name: count, dtype: int64




```python
fig = px.bar(
    counts_deel,
    x="jaar",
    y="het aantal meldingen",
    color="stadsdeel",
    title="Welk stadsdeel heeft het hoogste aantal meldingen?",  barmode="group",                          
 
    hover_data=counts_deel.columns  
)

fig.show()
```


<div>                            <div id="ad5fb420-6667-4da9-a653-45031763fd88" class="plotly-graph-div" style="height:525px; width:100%;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("ad5fb420-6667-4da9-a653-45031763fd88")) {                    Plotly.newPlot(                        "ad5fb420-6667-4da9-a653-45031763fd88",                        [{"alignmentgroup":"True","customdata":[["Centrum"],["Centrum"],["Centrum"],["Centrum"],["Centrum"],["Centrum"],["Centrum"],["Centrum"],["Centrum"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Centrum","marker":{"color":"#636efa","pattern":{"shape":""}},"name":"Centrum","offsetgroup":"Centrum","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[4375,9702,12909,14048,17017,17211,8019,8191,8],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Escamp"],["Escamp"],["Escamp"],["Escamp"],["Escamp"],["Escamp"],["Escamp"],["Escamp"],["Escamp"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Escamp","marker":{"color":"#EF553B","pattern":{"shape":""}},"name":"Escamp","offsetgroup":"Escamp","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[4603,10439,13691,15330,20497,18761,8071,7918,6],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Haagse Hout"],["Haagse Hout"],["Haagse Hout"],["Haagse Hout"],["Haagse Hout"],["Haagse Hout"],["Haagse Hout"],["Haagse Hout"],["Haagse Hout"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Haagse Hout","marker":{"color":"#00cc96","pattern":{"shape":""}},"name":"Haagse Hout","offsetgroup":"Haagse Hout","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[1786,3736,4942,6415,7589,6163,3849,3447,6],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Laak"],["Laak"],["Laak"],["Laak"],["Laak"],["Laak"],["Laak"],["Laak"],["Laak"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Laak","marker":{"color":"#ab63fa","pattern":{"shape":""}},"name":"Laak","offsetgroup":"Laak","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[1652,3768,4844,5787,8545,8693,2727,2372,3],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"],["Leidschenveen-Ypenburg"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Leidschenveen-Ypenburg","marker":{"color":"#FFA15A","pattern":{"shape":""}},"name":"Leidschenveen-Ypenburg","offsetgroup":"Leidschenveen-Ypenburg","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[1434,3577,5159,5647,6972,6329,3855,3568,6],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Loosduinen"],["Loosduinen"],["Loosduinen"],["Loosduinen"],["Loosduinen"],["Loosduinen"],["Loosduinen"],["Loosduinen"],["Loosduinen"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Loosduinen","marker":{"color":"#19d3f3","pattern":{"shape":""}},"name":"Loosduinen","offsetgroup":"Loosduinen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[1841,4465,5822,6549,8689,9310,5340,5513,6],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Scheveningen"],["Scheveningen"],["Scheveningen"],["Scheveningen"],["Scheveningen"],["Scheveningen"],["Scheveningen"],["Scheveningen"],["Scheveningen"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Scheveningen","marker":{"color":"#FF6692","pattern":{"shape":""}},"name":"Scheveningen","offsetgroup":"Scheveningen","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[2142,5058,6892,8652,10523,9947,5224,5035,4],"yaxis":"y"},{"alignmentgroup":"True","customdata":[["Segbroek"],["Segbroek"],["Segbroek"],["Segbroek"],["Segbroek"],["Segbroek"],["Segbroek"],["Segbroek"],["Segbroek"]],"hovertemplate":"stadsdeel=%{customdata[0]}<br>jaar=%{x}<br>het aantal meldingen=%{y}<extra></extra>","legendgroup":"Segbroek","marker":{"color":"#B6E880","pattern":{"shape":""}},"name":"Segbroek","offsetgroup":"Segbroek","orientation":"v","showlegend":true,"textposition":"auto","type":"bar","x":[2016,2017,2018,2019,2020,2021,2022,2023,2024],"xaxis":"x","y":[2518,5464,7473,8984,11286,11614,5229,4826,11],"yaxis":"y"}],                        {"barmode":"group","legend":{"title":{"text":"stadsdeel"},"tracegroupgap":0},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Welk stadsdeel heeft het hoogste aantal meldingen?"},"xaxis":{"anchor":"y","domain":[0.0,1.0],"title":{"text":"jaar"}},"yaxis":{"anchor":"x","domain":[0.0,1.0],"title":{"text":"het aantal meldingen"}}},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('ad5fb420-6667-4da9-a653-45031763fd88');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>


Escamp en Centrum lijken de stadsdelen met de hoogste aantal meldingen te zijn.

# Bubble map:


```python
df_clean = df.dropna(subset=["stadsdeel"])
counts_deel = (
    df_clean
    .groupby(["jaar", "stadsdeel"])
    .size()
    .rename("het aantal meldingen")
    .reset_index(name='het aantal meldingen')
)

```


```python
stadsdeel_coords = pd.DataFrame({
    "stadsdeel": [
        "Centrum",
        "Escamp",
        "Segbroek",
        "Scheveningen",
        "Loosduinen",
        "Laak",
        "Haagse Hout",
        "Leidschenveen-Ypenburg"
    ],
    "lat": [
        52.0707,
        52.0609,
        52.0450,
        52.0900,
        52.0400,
        52.0650,
        52.0500,
        52.0900
    ],
    "lon": [
        4.3126,
        4.3600,
        4.3300,
        4.2100,
        4.2700,
        4.3250,
        4.3400,
        4.3800
    ]
})

counts_geo = counts_deel.merge(stadsdeel_coords, on="stadsdeel", how="inner")

if counts_geo.empty:
    print("ERROR: counts_geo is empty → check stadsdeel names match exactly!")
    print("stadsdeel unique in counts_deel:")
    print(counts_deel["stadsdeel"].unique())
else:
   
    fig = px.scatter_mapbox(
        counts_geo,
        lat="lat",
        lon="lon",
        size="het aantal meldingen",
        color="het aantal meldingen",
        color_continuous_scale="Blues",
        hover_name="stadsdeel",
        hover_data=["het aantal meldingen", "jaar"],
        zoom=9,
        mapbox_style="open-street-map",
        title="Aantal meldingen per stadsdeel (Den Haag)"
    )

    fig.update_layout(
        margin={"r":0, "t":40, "l":0, "b":0},
        coloraxis_colorbar=dict(title="Aantal meldingen"),
        width=900, height=600
    )

    fig.show()

```


<div>                            <div id="3060bbb6-1271-42c5-9aca-92a3d91d7bf0" class="plotly-graph-div" style="height:600px; width:900px;"></div>            <script type="text/javascript">                require(["plotly"], function(Plotly) {                    window.PLOTLYENV=window.PLOTLYENV || {};                                    if (document.getElementById("3060bbb6-1271-42c5-9aca-92a3d91d7bf0")) {                    Plotly.newPlot(                        "3060bbb6-1271-42c5-9aca-92a3d91d7bf0",                        [{"customdata":[[4375,2016],[9702,2017],[12909,2018],[14048,2019],[17017,2020],[17211,2021],[8019,2022],[8191,2023],[8,2024],[4603,2016],[10439,2017],[13691,2018],[15330,2019],[20497,2020],[18761,2021],[8071,2022],[7918,2023],[6,2024],[1786,2016],[3736,2017],[4942,2018],[6415,2019],[7589,2020],[6163,2021],[3849,2022],[3447,2023],[6,2024],[1652,2016],[3768,2017],[4844,2018],[5787,2019],[8545,2020],[8693,2021],[2727,2022],[2372,2023],[3,2024],[1434,2016],[3577,2017],[5159,2018],[5647,2019],[6972,2020],[6329,2021],[3855,2022],[3568,2023],[6,2024],[1841,2016],[4465,2017],[5822,2018],[6549,2019],[8689,2020],[9310,2021],[5340,2022],[5513,2023],[6,2024],[2142,2016],[5058,2017],[6892,2018],[8652,2019],[10523,2020],[9947,2021],[5224,2022],[5035,2023],[4,2024],[2518,2016],[5464,2017],[7473,2018],[8984,2019],[11286,2020],[11614,2021],[5229,2022],[4826,2023],[11,2024]],"hovertemplate":"<b>%{hovertext}</b><br><br>het aantal meldingen=%{marker.color}<br>lat=%{lat}<br>lon=%{lon}<br>jaar=%{customdata[1]}<extra></extra>","hovertext":["Centrum","Centrum","Centrum","Centrum","Centrum","Centrum","Centrum","Centrum","Centrum","Escamp","Escamp","Escamp","Escamp","Escamp","Escamp","Escamp","Escamp","Escamp","Haagse Hout","Haagse Hout","Haagse Hout","Haagse Hout","Haagse Hout","Haagse Hout","Haagse Hout","Haagse Hout","Haagse Hout","Laak","Laak","Laak","Laak","Laak","Laak","Laak","Laak","Laak","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Leidschenveen-Ypenburg","Loosduinen","Loosduinen","Loosduinen","Loosduinen","Loosduinen","Loosduinen","Loosduinen","Loosduinen","Loosduinen","Scheveningen","Scheveningen","Scheveningen","Scheveningen","Scheveningen","Scheveningen","Scheveningen","Scheveningen","Scheveningen","Segbroek","Segbroek","Segbroek","Segbroek","Segbroek","Segbroek","Segbroek","Segbroek","Segbroek"],"lat":[52.0707,52.0707,52.0707,52.0707,52.0707,52.0707,52.0707,52.0707,52.0707,52.0609,52.0609,52.0609,52.0609,52.0609,52.0609,52.0609,52.0609,52.0609,52.05,52.05,52.05,52.05,52.05,52.05,52.05,52.05,52.05,52.065,52.065,52.065,52.065,52.065,52.065,52.065,52.065,52.065,52.09,52.09,52.09,52.09,52.09,52.09,52.09,52.09,52.09,52.04,52.04,52.04,52.04,52.04,52.04,52.04,52.04,52.04,52.09,52.09,52.09,52.09,52.09,52.09,52.09,52.09,52.09,52.045,52.045,52.045,52.045,52.045,52.045,52.045,52.045,52.045],"legendgroup":"","lon":[4.3126,4.3126,4.3126,4.3126,4.3126,4.3126,4.3126,4.3126,4.3126,4.36,4.36,4.36,4.36,4.36,4.36,4.36,4.36,4.36,4.34,4.34,4.34,4.34,4.34,4.34,4.34,4.34,4.34,4.325,4.325,4.325,4.325,4.325,4.325,4.325,4.325,4.325,4.38,4.38,4.38,4.38,4.38,4.38,4.38,4.38,4.38,4.27,4.27,4.27,4.27,4.27,4.27,4.27,4.27,4.27,4.21,4.21,4.21,4.21,4.21,4.21,4.21,4.21,4.21,4.33,4.33,4.33,4.33,4.33,4.33,4.33,4.33,4.33],"marker":{"color":[4375,9702,12909,14048,17017,17211,8019,8191,8,4603,10439,13691,15330,20497,18761,8071,7918,6,1786,3736,4942,6415,7589,6163,3849,3447,6,1652,3768,4844,5787,8545,8693,2727,2372,3,1434,3577,5159,5647,6972,6329,3855,3568,6,1841,4465,5822,6549,8689,9310,5340,5513,6,2142,5058,6892,8652,10523,9947,5224,5035,4,2518,5464,7473,8984,11286,11614,5229,4826,11],"coloraxis":"coloraxis","size":[4375,9702,12909,14048,17017,17211,8019,8191,8,4603,10439,13691,15330,20497,18761,8071,7918,6,1786,3736,4942,6415,7589,6163,3849,3447,6,1652,3768,4844,5787,8545,8693,2727,2372,3,1434,3577,5159,5647,6972,6329,3855,3568,6,1841,4465,5822,6549,8689,9310,5340,5513,6,2142,5058,6892,8652,10523,9947,5224,5035,4,2518,5464,7473,8984,11286,11614,5229,4826,11],"sizemode":"area","sizeref":51.2425},"mode":"markers","name":"","showlegend":false,"subplot":"mapbox","type":"scattermapbox"}],                        {"coloraxis":{"colorbar":{"title":{"text":"Aantal meldingen"}},"colorscale":[[0.0,"rgb(247,251,255)"],[0.125,"rgb(222,235,247)"],[0.25,"rgb(198,219,239)"],[0.375,"rgb(158,202,225)"],[0.5,"rgb(107,174,214)"],[0.625,"rgb(66,146,198)"],[0.75,"rgb(33,113,181)"],[0.875,"rgb(8,81,156)"],[1.0,"rgb(8,48,107)"]]},"height":600,"legend":{"itemsizing":"constant","tracegroupgap":0},"mapbox":{"center":{"lat":52.063950000000006,"lon":4.315949999999999},"domain":{"x":[0.0,1.0],"y":[0.0,1.0]},"style":"open-street-map","zoom":9},"margin":{"b":0,"l":0,"r":0,"t":40},"template":{"data":{"bar":[{"error_x":{"color":"#2a3f5f"},"error_y":{"color":"#2a3f5f"},"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"bar"}],"barpolar":[{"marker":{"line":{"color":"#E5ECF6","width":0.5},"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"barpolar"}],"carpet":[{"aaxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"baxis":{"endlinecolor":"#2a3f5f","gridcolor":"white","linecolor":"white","minorgridcolor":"white","startlinecolor":"#2a3f5f"},"type":"carpet"}],"choropleth":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"choropleth"}],"contour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"contour"}],"contourcarpet":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"contourcarpet"}],"heatmap":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmap"}],"heatmapgl":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"heatmapgl"}],"histogram":[{"marker":{"pattern":{"fillmode":"overlay","size":10,"solidity":0.2}},"type":"histogram"}],"histogram2d":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2d"}],"histogram2dcontour":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"histogram2dcontour"}],"mesh3d":[{"colorbar":{"outlinewidth":0,"ticks":""},"type":"mesh3d"}],"parcoords":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"parcoords"}],"pie":[{"automargin":true,"type":"pie"}],"scatter":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter"}],"scatter3d":[{"line":{"colorbar":{"outlinewidth":0,"ticks":""}},"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatter3d"}],"scattercarpet":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattercarpet"}],"scattergeo":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergeo"}],"scattergl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattergl"}],"scattermapbox":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scattermapbox"}],"scatterpolar":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolar"}],"scatterpolargl":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterpolargl"}],"scatterternary":[{"marker":{"colorbar":{"outlinewidth":0,"ticks":""}},"type":"scatterternary"}],"surface":[{"colorbar":{"outlinewidth":0,"ticks":""},"colorscale":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"type":"surface"}],"table":[{"cells":{"fill":{"color":"#EBF0F8"},"line":{"color":"white"}},"header":{"fill":{"color":"#C8D4E3"},"line":{"color":"white"}},"type":"table"}]},"layout":{"annotationdefaults":{"arrowcolor":"#2a3f5f","arrowhead":0,"arrowwidth":1},"autotypenumbers":"strict","coloraxis":{"colorbar":{"outlinewidth":0,"ticks":""}},"colorscale":{"diverging":[[0,"#8e0152"],[0.1,"#c51b7d"],[0.2,"#de77ae"],[0.3,"#f1b6da"],[0.4,"#fde0ef"],[0.5,"#f7f7f7"],[0.6,"#e6f5d0"],[0.7,"#b8e186"],[0.8,"#7fbc41"],[0.9,"#4d9221"],[1,"#276419"]],"sequential":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]],"sequentialminus":[[0.0,"#0d0887"],[0.1111111111111111,"#46039f"],[0.2222222222222222,"#7201a8"],[0.3333333333333333,"#9c179e"],[0.4444444444444444,"#bd3786"],[0.5555555555555556,"#d8576b"],[0.6666666666666666,"#ed7953"],[0.7777777777777778,"#fb9f3a"],[0.8888888888888888,"#fdca26"],[1.0,"#f0f921"]]},"colorway":["#636efa","#EF553B","#00cc96","#ab63fa","#FFA15A","#19d3f3","#FF6692","#B6E880","#FF97FF","#FECB52"],"font":{"color":"#2a3f5f"},"geo":{"bgcolor":"white","lakecolor":"white","landcolor":"#E5ECF6","showlakes":true,"showland":true,"subunitcolor":"white"},"hoverlabel":{"align":"left"},"hovermode":"closest","mapbox":{"style":"light"},"paper_bgcolor":"white","plot_bgcolor":"#E5ECF6","polar":{"angularaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","radialaxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"scene":{"xaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"yaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"},"zaxis":{"backgroundcolor":"#E5ECF6","gridcolor":"white","gridwidth":2,"linecolor":"white","showbackground":true,"ticks":"","zerolinecolor":"white"}},"shapedefaults":{"line":{"color":"#2a3f5f"}},"ternary":{"aaxis":{"gridcolor":"white","linecolor":"white","ticks":""},"baxis":{"gridcolor":"white","linecolor":"white","ticks":""},"bgcolor":"#E5ECF6","caxis":{"gridcolor":"white","linecolor":"white","ticks":""}},"title":{"x":0.05},"xaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2},"yaxis":{"automargin":true,"gridcolor":"white","linecolor":"white","ticks":"","title":{"standoff":15},"zerolinecolor":"white","zerolinewidth":2}}},"title":{"text":"Aantal meldingen per stadsdeel (Den Haag)"},"width":900},                        {"responsive": true}                    ).then(function(){

var gd = document.getElementById('3060bbb6-1271-42c5-9aca-92a3d91d7bf0');
var x = new MutationObserver(function (mutations, observer) {{
        var display = window.getComputedStyle(gd).display;
        if (!display || display === 'none') {{
            console.log([gd, 'removed!']);
            Plotly.purge(gd);
            observer.disconnect();
        }}
}});

// Listen for the removal of the full notebook cells
var notebookContainer = gd.closest('#notebook-container');
if (notebookContainer) {{
    x.observe(notebookContainer, {childList: true});
}}

// Listen for the clearing of the current output cell
var outputEl = gd.closest('.output');
if (outputEl) {{
    x.observe(outputEl, {childList: true});
}}

                        })                };                });            </script>        </div>

