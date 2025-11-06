```markdown
# Clothing Recommendation Workflow

This workflow recommends clothing based on the current weather conditions of a city provided by the user.

## Variables:

*   **CityName** (String): Stores the name of the city entered by the user.
*   **Temp** (String): Stores the temperature fetched from the web.
*   **weather** (String): Stores the weather description fetched from the web.
*   **Outfit** (String): Stores the recommended outfit based on temperature.
*   **RainGear** (String): Stores the recommendation for rain gear if applicable.

## Step-by-Step Process:

1.  **Get City Name from User**:
    *   An `Input Dialog` activity prompts the user to enter a city name.
    *   The input is stored in the `CityName` variable.

2.  **Fetch Weather Data**:
    *   A `NApplicationCard` activity is used to interact with a web browser (Chrome).
    *   Inside the `NApplicationCard`:
        *   A `NTypeInto` activity types a search query (e.g., "weather in [CityName] in fahrenheit") into the browser's search bar.
        *   A `NGetText` activity extracts the temperature from the webpage and stores it in the `Temp` variable.
        *   Another `NGetText` activity extracts the weather description (e.g., "Sunny", "Rain") from the webpage and stores it in the `weather` variable.

3.  **Analyze the Weather (Flowchart)**:
    *   A `Flowchart` named "Analyse The Weather" determines clothing recommendations.
    *   **Check if raining** (`FlowDecision`):
        *   Condition: `weather.ToLower.Contains("rain") or weather.ToLower.Contains("Showers") or weather.ToLower.Contains("thunderstorm")`
        *   If True:
            *   An `Assign` activity sets `RainGear` to "Bring An umbrella".
        *   If False:
            *   **Check if too cold** (`FlowDecision`):
                *   Condition: `Convert.ToInt32(Temp) < 40`
                *   If True:
                    *   An `Assign` activity sets `Outfit` to "It is very cold outside keep a jacket handy".
                *   If False:
                    *   **Check If Too Hot** (`FlowDecision`):
                        *   Condition: `Convert.ToInt32(Temp) > 75`
                        *   If True:
                            *   An `Assign` activity sets `Outfit` to "Weather is Sunny Wear a Tshirt, Shorts and a Hat".
                        *   If False:
                            *   An `Assign` activity sets `Outfit` to "weather is clear out side wear a jeans and shirt".

4.  **Display Recommendation**:
    *   A `Message Box` activity displays the final clothing recommendation, including temperature, outfit, and rain gear information (if applicable).
```