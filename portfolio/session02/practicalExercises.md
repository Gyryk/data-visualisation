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

# Session 2: Practical Exercises

{(task|}

Use this document as a place to add your answers to the week's practical exercises.

{|task)}

## Q.1 Evaluating Design Approaches

### Corum: See, Think, Design, Produce

I would start with a few rough ideas and then choose **three different designs** to work on. This gives me enough to compare without spending too much time on one idea. The [Five Design-Sheets method](https://fds-design.github.io/) follows a similar process, with one sheet for ideas, three for different designs and one for the final design.

I agree that having a clear idea helps when explaining something through a chart. It makes it easier for the reader to understand the point. However, if I am still exploring the data, I might not know what the main message is yet. I would want to be able to change my idea as I learn more.

I think Corum means that showing numbers alone is not always enough. A chart should help the reader understand why they matter. Counts are still useful, and a chart can help people find patterns for themselves. A personal diary can also be meaningful to its owner even if it is not interesting to everyone else.

In Bloom's cognitive domain, this fits understanding, analysing and evaluating, rather than just remembering. Making different designs also involves creating. In the affective domain, a chart might get someone to respond or care about an issue, although it will not always change how they behave.

Source: [Jonathan Corum's talk](https://style.org/stdp3/) and the [Session 2 notes](../../lectures/session02/README.md#3-see-think-design-produce).

### Train-delay scarf

I think the scarf is a data visualization because its coloured rows show train delays. Sara Weber shared her mother's work. [Source](https://www.theguardian.com/world/2019/jan/14/german-train-delay-scarf-ebay-commute).

It fits data humanism because it connects the numbers to someone's daily life. Making the scarf by hand also shows the time and effort behind it. I think it connects to feminist visualization because it shows a commuter's own experience, which might get lost in the railway's overall statistics. However, it only shows one person's journeys, so it cannot tell us how reliable the whole network is.

### Dear Data and personal visualization

[Dear Data](https://www.dear-data.com/theproject) used weekly personal observations and drawings sent as postcards, with keys explaining how to read them. I think this fits Corum's point because the drawings do more than show a count. The topics and notes help the other person understand something about the maker's life.

With personal visualization, the person collecting the data may also make and read the chart. They might choose their own definitions, such as what counts as a distraction. Recording things can also make them notice more about their habits. The aim might be to reflect or connect with someone, rather than compare exact values. However, I would still explain how the data was collected and whether anything was missed.

### Data ink, non-data ink and chart junk

In the [food graphic from the lecture](https://staff.city.ac.uk/~jwo/datavis2023b/session02/images/tnsFood.png), the bar lengths, percentages and sizes of the fruit sections show the data. The labels, explanations and sources help the reader understand it. The yellow background and details such as the fruit's seeds and skin do not show any extra data.

I would consider much of the fruit decoration chart junk if the aim is to compare the numbers accurately. It takes attention away from the percentages, and the seeds could look like they mean something. However, the food theme might make people more interested in reading it. I would keep the labels and use a simpler chart if comparing values was the main task.

### BBC migration map: lie factor

The [BBC graphic from the lecture](https://staff.city.ac.uk/~jwo/datavis2023b/session02/images/migration.png) uses circles to show the number of migrants. I would compare the change in **circle area** with the change in the count, because readers see the whole circle.

The middle and largest circles in the legend are about 84 and 144 pixels across. I used 45 for the 40–50 group and **assumed 85** for the more-than-80 group:

$$
\text{Lie factor} \approx
\frac{(144/84)^2 - 1}{85/45 - 1}
\approx 2.18.
$$

Using these assumptions, the increase in circle area exaggerates the increase in the count by about **2.2 times**. This is only an estimate because the legend gives ranges and I measured the circles from a screenshot. I would need the actual counts and sizing rule for an exact answer. If a circle's diameter doubles, its area becomes four times as large. I would scale the area to the count to avoid exaggerating the difference. The overlapping circles also make the map harder to read.

### Accessible heat lane makeover

I think the [accessible makeover](https://www.smashingmagazine.com/2022/07/accessibility-first-approach-chart-visual-design/) follows Tufte's ideas by keeping the chart compact and making patterns easier to see. This also helps when putting several charts next to each other. The [gallery example](../../gallery/bars.md#accessible-heatlane-chart) removes the border and vertical axis but keeps the legend so the reader knows what the marks mean.

However, it also adds useful detail. Both colour and height show frequency ranges, and the dark ends make the marks easier to see. Removing these details just to reduce ink could make the chart harder to use. Grouping the counts into ranges saves space but hides some differences. I would use this design to compare overall patterns in a small space, and a normal histogram if exact counts mattered more.

### Choosing a framework for a task

| Approach                 | Example user task                                   | How it helps                                                  |
| ------------------------ | --------------------------------------------------- | ------------------------------------------------------------- |
| Corum's iterative design | Understand a trend                                  | Try different sketches and use the data to decide what works. |
| Data humanism            | Think about a daily routine                         | Connect the numbers to someone's experience.                  |
| Tufte's minimalism       | Compare how many films fall in each rating range    | Remove distractions but keep useful labels and scales.        |
| Visualization algebra    | Check whether a chart changes when the data changes | Check that the visual changes match the data changes.         |

I see explanation as showing a finding, analysis as looking for patterns, reflection as thinking about what the data means personally, and artistic expression as using data to express an idea or feeling. A chart can do more than one of these, but I would decide what the reader needs to do before choosing the design.

For visualization algebra, I would use these examples:

- **Hallucinator:** Changing the order of the data rows changes which overlapping points are visible, even though the values are the same.
- **Confuser:** Different values get the same colour, hiding a difference that matters for the task.
- **Jumbler:** Colours have no clear order, so it is hard to follow an increase in the values.
- **Misleader:** Charts use different scales, making very different values look the same size.
- **Distractor:** Details such as the fruit seeds take attention away from the data. The notes use _confuser_ for a design that hides meaningful differences between datasets.

## Q.2 Creating a Minimalist Tufte Visualization

I made two documents so I can compare the original histogram with my simpler line chart:

1. [defaultHistogram.md](defaultHistogram.md) contains the chart from the exercise.
2. [minimalistHistogram.md](minimalistHistogram.md) uses a line to connect the counts at the middle of each rating range. It also explains what works and what could be improved.

Both documents load the same movie data directly, so I can preview either one on its own.
