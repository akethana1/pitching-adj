We provide PitcherOptimize, an app and model that attempts to investigate and define the best situation i.e. defense, park) for a pitcher. 

A user inputs a pitcher, team, and ballpark, and will get a comparison of the predicted BABIP relative to the current situation, as well as the top predicted combinations for the pitcher.

To do this, we leverage defensive-independent pitching predictors(k%, hard hit% etc.) and zonal defensive skill (OAA by side of infield, outfield, position etc.). We leverage park adjustment rolling averages from Statcast to account for park factors.

finalproject/finalproject.rmd is where all of the code is located.

We generate the raw_pitcher data using:
```{r}
raw_pitchers <- fg_pitcher_leaders(
  startseason = "2025",
  endseason = "2025",
  stats = "pit",
  lg = "all",
  qual = "30",
  ind = "1"
)

write_csv(raw_pitchers, "raw_pitcher_fangraphs_2024.csv")
```

We follow similar processes with defensive information, and preprocess the dataaset to account for all three components mentioned above.

We fit a glm based off of such predictors, and define helper functions below to generate comparisons and find the best situations. 

We leave an example with Logan Webb for the user to try.

We also define a Shiny server for the user to input any combination they would like, and experiment with all sorts of combinations. 


