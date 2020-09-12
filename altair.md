# Overview

## Bar Chart

``` python
bar_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="value",
    color="search_term"
)
```

## Line Chart

``` python
line_chart = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
)
```

## Scatter Chart

``` python
circles_chart = alt.Chart(lifecountries).mark_circle().encode(
    x='Country GDP',
    y=alt.Y('Life Expectancy',scale=alt.Scale(zero=False)),
    color='Continent',
    tooltip='country',
    size='size'
)
```

## Map Chart

``` python
temp = world_temp.groupby("city").mean().reset_index()

points = alt.Chart(temp).mark_circle().encode(
    latitude="lat",
    longitude="lon",
    color=alt.Color("mean(temp)",scale=alt.Scale(domain=[-30,10,40],range=["lightblue","orange","red"]))
)

# remote geojson data object
url = "https://raw.githubusercontent.com/datasets/geo-countries/master/data/countries.geojson"
data_geojson_remote = alt.Data(url=url, format=alt.DataFormat(property='features',type='json'))

# chart object
map = alt.Chart(data_geojson_remote).mark_geoshape(
    fill="lightgrey",
    stroke="white"
).encode(
).properties(
    
)

(map+points)

```


## Single selection

``` python
select_term = alt.selection(type="single",encodings=["x"])

trend_line = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
).transform_filter(
    select_term
)

trend_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="value",
    color="search_term",
    tooltip="search_term"
).properties(
    selection=select_term
)

trend_bar|trend_line
```

## Interval selection

``` python
select_date = alt.selection(type="interval",encodings=["x"])

trend_line = alt.Chart(trends).mark_line().encode(
    x="yearmonth(date):T",
    y="mean(value)",
    color="search_term"
).properties(
    selection=select_date
)

trend_bar = alt.Chart(trends).mark_bar().encode(
    x="search_term",
    y="value",
    color="search_term",
    tooltip="search_term"
).transform_filter(
    select_date
)

trend_bar|trend_line
```

## Horizontal compisition

```python
trend_bar|trend_line
```

## Vertical compisition

```python
trend_bar&trend_line

```
## Layer composition

```python
background+points
```
