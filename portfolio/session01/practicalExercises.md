---
id: litvis

narrative-schemas:
  - ../../lectures/narrative-schemas/teaching.yml

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest
---

@import "../../lectures/css/datavis.less"

```elm {l=hidden}
import Tidy exposing (..)
import VegaLite exposing (..)
```

<!-- Everything above this line should probably be left untouched. -->

# Session 1: Practical Exercises

{(task|}

Use this document as a place to add your answers to the week's practical exercises.

{|task)}

## Q.2 Datavis Evaluation

I chose Alvin Chang's [30 minutes with a stranger](https://pudding.cool/2025/06/hello-stranger/) from Nathan Yau's [Best Data Visualization Projects of 2025](https://flowingdata.com/2025/12/31/best-data-visualization-2025/).

1. **Complex data:** It shows the participants, their demographics and how they felt. I think showing individual people alongside the overall patterns makes the differences easier to understand than a table would.
2. **Connections and comparisons:** It pairs people and compares how they felt before, during and after talking. This makes it easier to see how individual experiences fit into the overall results.
3. **Interaction:** You can click on a person to find out more about them. This lets you explore individual cases. However, most of the experience still follows the order of the story.
4. **Narrative:** It takes you through the conversation from start to finish, explaining the results as you go. This makes the changes easier to follow, although the examples shown may not represent everyone in the dataset.
5. **Aesthetic response:** I think the human figures make the data easier to relate to and encourage you to keep reading. A standard chart would probably be better for comparing exact numbers.

Overall, I think it works well because it connects the numbers to individual people, while still showing the bigger picture.

## Q.3 Bicycle Hires Visualization

The months go along the x-axis and the number of hires goes on the y-axis. The bars start at zero so that their heights can be compared fairly.

```elm {l v}
bikehireBarchart : Spec
bikehireBarchart =
    let
        data =
            dataFromUrl "https://gicentre.github.io/data/bicycleHiresLondon.csv"

        enc =
            encoding
                << position X [ pName "Month", pTemporal ]
                << position Y [ pName "NumberOfHires", pQuant ]
    in
    toVegaLite [ width 640, data [], enc [], bar [] ]
```

The [dataset](https://gicentre.github.io/data/bicycleHiresLondon.csv) has 194 months, from July 2010 to August 2026, as checked on 13 October 2026. It now covers more years than the example in the lecture notes.

The main pattern is that more bikes are hired in summer and fewer in winter. July 2022 has the most hires at **1,315,801**. July 2010 has a much smaller total, but it is right at the start of the data, so I would not treat it as a normal month. The totals also depend on how many days are in each month, so they do not directly tell us the daily hire rate.

## Q.4 Creating a Scatterplot

I used a scatterplot to compare the number of hires with the average time a bike was hired for. Each circle is one month, with the number of hires on the x-axis and the average duration in minutes on the y-axis. This makes it easier to see whether the two are related and which months stand out.

```elm {l v}
bikehireScatterplot : Spec
bikehireScatterplot =
    let
        data =
            dataFromUrl "https://gicentre.github.io/data/bicycleHiresLondon.csv"

        enc =
            encoding
                << position X
                    [ pName "NumberOfHires"
                    , pQuant
                    , pAxis [ axTitle "Number of hires per month", axFormat ",.0f" ]
                    ]
                << position Y
                    [ pName "AvHireTime"
                    , pQuant
                    , pAxis [ axTitle "Average hire duration (minutes)" ]
                    ]
    in
    toVegaLite
        [ title "London bicycle hires: volume and duration" []
        , width 640
        , height 320
        , data []
        , enc []
        , circle [ maOpacity 0.6, maSize 45 ]
        ]
```

Many of the months have an average duration of around 15 to 25 minutes, even though the number of hires varies quite a lot. More hires do not always mean longer journeys. **April 2020** stands out at **36 minutes** with **591,294** hires. **May 2020** has a similar average of **35 minutes**, but **1,121,435** hires. These are monthly averages, so they do not show how much individual trips vary.

## Q.5 Data Challenge

I wanted to show **how support for joining the EU, staying out and giving no answer changed over time**, as well as how the polls differed from each other.

The [polling dataset](https://gicentre.github.io/data/euPolls3.json) has 183 polls from February 2020 to September 2023, with three answers for each poll. This means the chart shows opinions during that period, rather than current opinions.

```elm {l v}
euPollingChart : Spec
euPollingChart =
    let
        data =
            dataFromUrl "https://gicentre.github.io/data/euPolls3.json"

        trans =
            transform
                << calculateAs "toDate(slice(datum.Date, 0, 10))" "PollDate"

        enc =
            encoding
                << position X
                    [ pName "PollDate"
                    , pTemporal
                    , pAxis [ axTitle "Poll date", axFormat "%b %Y", axTickCount (niTickCount 6) ]
                    ]
                << position Y
                    [ pName "Percent"
                    , pQuant
                    , pScale [ scDomain (doNums [ 0, 100 ]) ]
                    , pAxis [ axTitle "Respondents (%)" ]
                    ]
                << color
                    [ mName "Answer"
                    , mNominal
                    , mScale
                        [ scDomain (doStrs [ "Join", "Stay out", "no answer / don't know" ])
                        , scRange (raStrs [ "#0072B2", "#D55E00", "#666666" ])
                        ]
                    , mLegend [ leTitle "Response", leLabelLimit 200 ]
                    ]
    in
    toVegaLite
        [ title "UK attitudes towards joining the EU, 2020–2023" []
        , width 640
        , height 320
        , data []
        , trans []
        , enc []
        , circle [ maOpacity 0.55, maSize 35 ]
        ]
```

**Why I used this design:** I put the date on the x-axis and the percentage on the y-axis, using different colours for the three answers. I used circles instead of joining the results with lines because the polls come from different pollsters. Joining them could make unrelated results look like one continuous trend. I made the circles partly transparent so that overlapping points are easier to see. The y-axis goes from 0 to 100% so that the percentages have a clear scale.

The dates are not all written in the same format. I used `slice` to keep the `YYYY-MM-DD` part and `toDate` to turn it into a date so that they all display correctly. Source: [Vega expression documentation](https://vega.github.io/vega/docs/expressions/).

**What the chart shows:** Join and Stay out are fairly close in 2020–2021, but by 2023 Join is usually higher. There are still differences between polls. On 15 September 2023, Deltapoll has **49% Join, 38% Stay out and 13% no answer / don't know**, while Omnisis has **50%, 31% and 19%**. Kantar has **39% no answer / don't know** on 4 September, showing how much the undecided group can vary between polls.

This makes it easier to compare the overall pattern and spot unusual results. However, it does not explain why opinions changed. The pollsters may use different samples, wording or methods. The data also does not include sample sizes or margins of error, so I cannot show confidence intervals or weight the results by sample size.

## Q.6 Design Challenge

_Add a link to a photo of your design sketch._
