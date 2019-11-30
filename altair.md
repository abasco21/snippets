# Altair code

## Histogram

``` python

histo_brain=alt.Chart(brain_body).mark_bar().encode(
    x=alt.X('Brain Weight',bin=alt.Bin(maxbins=20)),
    y="count()"
)
``` 

## Barra
``` python
bar_trends=alt.Chart(trends).mark_bar().encode(
    x='search_term',
    y='mean(value)',
    color='search_term'
)
```

## Line
``` python
  line_trends=alt.Chart(trends).mark_line().encode(
      x=alt.X("date:T",timeUnit="year"),
      y="mean(value)",
      color="search_term"
  )
```

## Scatter
``` python
  scatter_body_brain=alt.Chart(brain_body).mark_circle().encode(
      x='Brain Weight',
      y='Body Weight',
      color=alt.value("#123456")
  ).properties(
      width=800
  )

```
## Concatenation
``` python
bar_trends|line_trends
(bar_trends|line_trends).save("selector.html")
```

## Above
``` python
bar_trends & line_trends
```

## Both
``` python
bar_trends + line_trends
```

## selection single
``` python
select_term = alt.selection_single(encodings=["x"])

line_trends=alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="year"),
    y="mean(value)",
    color="search_term"
).transform_filter(select_term)

bar_trends=alt.Chart(trends).mark_bar().encode(
    x='search_term',
    y='mean(value)',
    color='search_term'
).properties(
    selection=select_term
)
```

## Selection interval
``` python
select_zoom = alt.selection_interval(encodings=["x"])

line_trends = alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="mean(value)",
    color="search_term"
).properties(
    height=200
).transform_filter(
    select_zoom
)

line_trends_small = alt.Chart(trends).mark_line().encode(
    x=alt.X("date:T",timeUnit="yearmonth"),
    y="mean(value)",
    color="search_term"
).properties(
    height=50,
    selection=select_zoom
)

(line_trends&line_trends_small).save("zoom.html")
```
