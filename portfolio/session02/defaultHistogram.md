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

## Default histogram

This is the chart from the exercise. It loads the movie data directly.

```elm {l v}
histogram : Spec
histogram =
    let
        data =
            dataFromUrl "https://vega.github.io/vega-lite/data/movies.json" []

        enc =
            encoding
                << position X [ pName "IMDB Rating", pBin [] ]
                << position Y [ pAggregate opCount ]
                << color [ mName "IMDB Rating", mOrdinal ]
    in
    toVegaLite [ data, enc [], bar [] ]
```

The bars show how many films fall into each rating range. Colour also shows the original rating, which splits the bars into coloured sections and creates a long legend. I think this makes it harder to focus on comparing the total bar heights.

I made a [simpler version](minimalistHistogram.md) to compare with this chart.
