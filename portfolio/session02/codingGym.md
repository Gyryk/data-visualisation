---
id: litvis

narrative-schemas:
  - ../../lectures/narrative-schemas/teaching.yml
---

@import "../../lectures/css/datavis.less"

<!-- Everything above this line should probably be left untouched. -->

# Coding Gym 2 : Lists

_These exercises are designed to help you build confidence programming with Elm. They assume no prior experience of coding in any language other than that arising from previous weeks of this module. This document is designed to be viewed in VSCode with litvis so you can add your own code blocks to answer each question._

## 2.1. Lists of items

In the previous gym you created functions that generated single values such as an integer, a floating point number or a String of text. We move on now to consider [lists of items](https://package.elm-lang.org/packages/elm/core/latest/List). Each item can again be a number, some text etc. but now we can create an ordered collection of them.

Lists are indicated with square brackets and items separated with commas. Lists can also be empty. For example:

```elm {l}
people : List String
people =
    [ "Ada Lovelace", "Alan Turing", "Jacques Bertin" ]


birthYears : List Int
birthYears =
    [ 1815, 1912, 1918 ]


todoList : List String
todoList =
    []
```

{(task|}

Create separate functions, each in their own code block, that display the following. Remember to include `elm {l r}` in each code block header so you can see the results. If created successfully, you should see the evaluation of each function appear in the preview window.

- the names of two cities you have visited and two you would like to visit
- the integers 70 to 75 inclusive.
- the [triangular numbers](https://en.wikipedia.org/wiki/Triangular_number) with one or two digits.
- The first 5 numbers in the sequence 1/1, 1/2, 1/3,... etc.
- The colours of the rainbow.
- A list of mammals that have eight legs.

{|task)}

```elm {l r}
visitedAndWishlistCities : List String
visitedAndWishlistCities =
    [ "Brussels", "Venice", "Cairo", "Jerash" ]
```

I have visited Brussels and Venice, and I would like to visit Cairo and Jerash.

```elm {l r}
seventyToSeventyFive : List Int
seventyToSeventyFive =
    [ 70, 71, 72, 73, 74, 75 ]
```

```elm {l r}
triangularNumbers : List Int
triangularNumbers =
    [ 1, 3, 6, 10, 15, 21, 28, 36, 45, 55, 66, 78, 91 ]
```

I started at 1 and kept adding the next whole number. I stopped at 91 because the next triangular number is 105, which has three digits.

```elm {l r}
firstFiveReciprocals : List Float
firstFiveReciprocals =
    [ 1 / 1, 1 / 2, 1 / 3, 1 / 4, 1 / 5 ]
```

```elm {l r}
rainbowColours : List String
rainbowColours =
    [ "Red", "Orange", "Yellow", "Green", "Blue", "Indigo", "Violet" ]
```

```elm {l r}
eightLeggedMammals : List String
eightLeggedMammals =
    []
```

I used an empty list because mammals do not normally have eight legs. `List String` tells Elm that any items in the list would be strings.

## 2.2. In-built functions to generate lists

Elm has a number of functions that make it easier to create lists. In particular [List.range](https://package.elm-lang.org/packages/elm/core/latest/List#range) for creating a range of integers; [List.repeat](https://package.elm-lang.org/packages/elm/core/latest/List#repeat) for creating a list of repeated items, the [cons operator `::`](<https://package.elm-lang.org/packages/elm/core/latest/List#(::)>) for adding an item to a list and the [++](https://package.elm-lang.org/packages/elm/core/latest/Basics#++) operator for combining two lists. For example:

```elm {l r}
firstTen : List Int
firstTen =
    List.range 1 10


fiveGoldRings : List String
fiveGoldRings =
    List.repeat 5 "gold ring"


newKidOnTheBlock : List String
newKidOnTheBlock =
    "New kid" :: [ "old kid", "another old kid" ]


oddsAndEvens : List Int
oddsAndEvens =
    [ 1, 3, 5, 7, 9 ] ++ [ 2, 4, 6, 8 ]
```

{(task|}

Choosing from the list-generating functions above, create separate functions to do the following:

- List the whole numbers (integers) 1992 to 2023 inclusive
- List the integers between -250 and -88 inclusive
- Add your own name added to this group of travellers: `[ "Ripley", "Vasquez", "Bishop", "Burke" ]`
- The word "dozen" repeated half a dozen times.
- Create a single list made up by combining a list of three animals, three vegetables and three minerals.

{|task)}

```elm {l r}
years1992To2023 : List Int
years1992To2023 =
    List.range 1992 2023
```

```elm {l r}
negativeIntegers : List Int
negativeIntegers =
    List.range -250 -88
```

`List.range` includes the starting and ending numbers. The first list has 32 items and the second has 163.

```elm {l r}
travellers : List String
travellers =
    "Girik" :: [ "Ripley", "Vasquez", "Bishop", "Burke" ]
```

```elm {l r}
halfDozenDozens : List String
halfDozenDozens =
    List.repeat 6 "dozen"
```

```elm {l r}
animalsVegetablesMinerals : List String
animalsVegetablesMinerals =
    [ "cat", "dog", "elephant" ]
        ++ [ "carrot", "broccoli", "spinach" ]
        ++ [ "quartz", "calcite", "gypsum" ]
```

I used strings for all nine items so I could put them in the same list.

## 2.3. Summarising Lists

Elm has some in-built functions that can summarise the contents of a list including [List.length](https://package.elm-lang.org/packages/elm/core/latest/List#length), [List.sum](https://package.elm-lang.org/packages/elm/core/latest/List#sum) and [List.product](https://package.elm-lang.org/packages/elm/core/latest/List#product). For example:

```elm {l r}
firstTenTotal : Int
firstTenTotal =
    List.sum (List.range 1 10)


numberOfAnimals : Int
numberOfAnimals =
    List.length [ "cat", "dog", "chicken" ]


power : Int
power =
    List.product [ 2, 3, 4 ]
```

{(task|}

Using the list-summarising functions above, create separate functions to calculate the following:

- The total of the integers from -250 to -88
- The number of items in the combined list `[] ++ [ "Ripley", "Vasquez", "Bishop", "Burke" ]`
- The mean (average) of all integers from -250 to -88
- 7 factorial (equivalent to `7 * 6 * 5 * 4 * 3 * 2 * 1`)

{|task)}

```elm {l r}
negativeIntegersTotal : Int
negativeIntegersTotal =
    List.sum negativeIntegers
```

The total is **-27,547**.

```elm {l r}
combinedListLength : Int
combinedListLength =
    List.length ([] ++ [ "Ripley", "Vasquez", "Bishop", "Burke" ])
```

The empty list adds nothing, so there are still **4** items.

```elm {l r}
negativeIntegersMean : Float
negativeIntegersMean =
    toFloat (List.sum negativeIntegers) / toFloat (List.length negativeIntegers)
```

I used `toFloat` on the total and the number of items so I could divide them using `/`. The average is **-169**, which is also halfway between -250 and -88.

```elm {l r}
sevenFactorial : Int
sevenFactorial =
    List.product (List.range 1 7)
```

Multiplying all seven integers gives **5,040**.

## 2.4 Tuples

Sometimes we might wish to operate on a very small collection of items rather than a list of unspecified length. For this we can use a [tuple](https://package.elm-lang.org/packages/elm/core/latest/Tuple) which can contain two or three items only. An unlike a list, the items do not need to be of the same type.

Tuples are indicated with round rather than square brackets. For example:

```elm {l r}
ada : ( String, Int )
ada =
    ( "Ada Lovelace", 1815 )
```

{(task|}

Create functions that return tuples or lists of tuples that represent:

- Your name and commuting time.
- A point in 3d space (requiring 3 coordinates)
- A list of 2d coordinates (i.e. each coordinate requiring a pair of coordinate values, but a number of them)

{|task)}

```elm {l r}
nameAndCommute : ( String, Int )
nameAndCommute =
    ( "Girik Agrawalla", 30 )
```

I used 30 minutes for my commute, the same as in my Session 1 coding gym.

```elm {l r}
pointIn3d : ( Float, Float, Float )
pointIn3d =
    ( 1.5, -2.0, 3.0 )
```

```elm {l r}
coordinatesIn2d : List ( Float, Float )
coordinatesIn2d =
    [ ( 0.0, 0.0 ), ( 1.5, 2.0 ), ( -3.0, 4.5 ), ( 2.0, -1.0 ) ]
```

Each pair gives the x and y coordinates of one point. Here both values are floats. My name and commute tuple uses a string and an integer, so a tuple can also hold different types.
