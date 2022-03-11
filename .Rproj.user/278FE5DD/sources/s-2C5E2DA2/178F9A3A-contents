library(dash)
library(dashCoreComponents)
library(dashHtmlComponents)
library(dashBootstrapComponents)
library(ggplot2)
library(plotly)

app <- Dash$new(external_stylesheets = dbcThemes$BOOTSTRAP)

msleep2 <- readr::read_csv(here::here('data', 'us_counties_processed.csv'))
msleep2 <- msleep2 %>% group_by(county) %>% summarise(percent_unemployed_CDC = mean(percent_unemployed_CDC))

app$layout(
  dbcContainer(
    list(
      dccGraph(id='plot-area'),
      dccDropdown(
        id='col-select',
        options = as.list(unique(msleep2$county)),
        value='Alachua')
    )
  )
)

app$callback(
  output('plot-area', 'figure'),
  list(input('col-select', 'value')),
  function(xcol) {
    msleep22 <- msleep2 %>%
      filter(county == xcol)
    p <- ggplot(msleep22) +
      aes(x = county,
          y = percent_unemployed_CDC) +
      geom_bar(stat="identity")
    ggplotly(p)
  }
)


app$run_server(debug = T)
app$run_server(host = '0.0.0.0')
