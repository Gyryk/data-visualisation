---
id: litvis

elm:
  dependencies:
    gicentre/elm-vegalite: latest
---

@import "../../lectures/css/datavis.less"

```elm {l=hidden}
import VegaLite exposing (..)
```

## A minimalist IMDb line chart

I used Tufte's ideas to simplify the [original histogram](defaultHistogram.md). I used a line to show how the number of films changes across the rating ranges. The line joins the counts at the middle of each range. This is called a frequency polygon.

```elm {l v}
minimalistLineChart : Spec
minimalistLineChart =
    let
        data =
            dataFromUrl "https://vega.github.io/vega-lite/data/movies.json" []

        cfg =
            configure
                << configuration (coView [ vicoStroke Nothing ])
                << configuration
                    (coAxis
                        [ axcoDomain False
                        , axcoTicks False
                        , axcoLabelAngle 0
                        ]
                    )

        trans =
            transform
                << filter (fiExpr "isValid(datum['IMDB Rating'])")
                << binAs [] "IMDB Rating" "ratingBin"
                << aggregate [ opAs opCount "" "filmCount" ] [ "ratingBin", "ratingBin_end" ]
                << calculateAs "(datum.ratingBin + datum.ratingBin_end) / 2" "ratingMidpoint"

        enc =
            encoding
                << position X
                    [ pName "ratingMidpoint"
                    , pQuant
                    , pScale [ scDomain (doNums [ 0, 10 ]) ]
                    , pAxis [ axTitle "IMDb rating (0–10)", axGrid False ]
                    ]
                << position Y
                    [ pName "filmCount"
                    , pQuant
                    , pScale [ scZero True ]
                    , pAxis
                        [ axTitle "Number of films"
                        , axFormat ",.0f"
                        , axTickCount (niTickCount 5)
                        , axGrid False
                        ]
                    ]
    in
    toVegaLite
        [ title "Distribution of IMDb ratings in the movie sample" []
        , width 500
        , height 300
        , cfg []
        , data
        , trans []
        , enc []
        , line [ maColor "#4b5563", maStrokeWidth 2 ]
        ]
```

**What works:** I used one grey line and removed the colour legend. I think this makes the overall pattern easier to follow. I also removed the border, grid and tick marks to reduce non-data ink. I kept the title, axis labels and numbers so the reader can still understand the chart. The y-axis starts at zero to give the counts a clear scale. The x-axis goes from 0 to 10 to show the full rating scale, and I kept all the films with a rating.

**What could be improved:** Without grid lines, it is harder to estimate the number of films in each range. A few light lines might help. The line connects grouped counts, so its height between the midpoints does not show an exact count for that rating. Bars make the width of each range clearer. I would also try different bin widths to see how much they change the pattern. The chart is wide enough for horizontal labels, but it might need resizing on a smaller screen.

The main pattern is that middle-to-high ratings are more common than very low or very high ratings. This only describes the films in this dataset. The filter leaves out films with missing ratings.

**Visualization algebra:** Changing the order of the films should not change the chart, so this should avoid a hallucinator. Moving a film's rating into another bin should lower the line at one midpoint and raise it at the other. However, a rating can change within the same bin without affecting the chart. I think that is fine for comparing ranges, but it would be a confuser if I needed to compare exact ratings. Keeping the rating scale fixed and starting the count axis at zero also helps avoid misleading comparisons.
