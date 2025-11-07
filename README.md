

This project Take City Input As User Input and check the temprature and type of wether and recomend cloths according to that

How To Create
---------------------------------------------------------

Step 1: Create the Project

Open UiPath Studio.

Click Process → Blank Process.

Name it ClothingRecommendationBot → choose location → Click Create.

Step 2: Add Main Workflow

In the Project panel, right-click the project → Add → New Sequence.

Name it Main.xaml.

Open Main.xaml — this will be the main automation workflow.

Step 3: Define Variables

Create variables in the sequence:
CityName (String)
Temp (String)
weather (String)
Outfit (String)
RainGear (String)

Step 4: Get City Name from User

Add an Input Dialog activity.

Prompt: "Enter city name".

Store the result in CityName.

Step 5: Open Browser and Search Weather

Add a Use Application/Browser activity and point it to your browser (or use Open Browser with a blank page).

Inside the browser scope, add a Type Into activity.

Type the search query: "weather in " + CityName + " in fahrenheit" into the search bar and send Enter.

Add a short Delay (1–2 seconds) to allow the page to load.

Step 6: Extract Temperature and Weather Description

Use Get Text (or NGetText if using modern activities) to scrape the temperature element from the results page and store it in Temp.

Use another Get Text to scrape the weather description (e.g., Sunny, Rain) and store it in weather.

Trim and normalize extracted values if needed:
Temp = Temp.Replace("°", "").Trim()
weather = weather.Trim().ToLower()

Step 7: Create Flowchart for Analysis

Add a Flowchart activity and name it AnalyseTheWeather.

Add a FlowDecision to check for rain:
Condition: weather.Contains("rain") Or weather.Contains("showers") Or weather.Contains("thunderstorm")

If True (raining):
Assign RainGear = "Bring an umbrella"
Continue to final outfit decision or directly to display (you may still set Outfit based on Temp)

If False (not raining):
Add a FlowDecision to check if very cold:
Condition: Convert.ToInt32(Temp) < 40
If True:
Assign Outfit = "It is very cold outside keep a jacket handy"
Continue to display
If False:
Add a FlowDecision to check if too hot:
Condition: Convert.ToInt32(Temp) > 75
If True:
Assign Outfit = "Weather is Sunny Wear a T-shirt, Shorts and a Hat"
If False:
Assign Outfit = "Weather is clear outside wear jeans and a shirt"

Step 8: Combine RainGear and Outfit

After flowchart decisions, ensure RainGear has a value when applicable (set to empty string "" if not raining).

Build the final recommendation string:
recommendation = "City: " + CityName + Environment.NewLine +
"Temperature: " + Temp + "°F" + Environment.NewLine +
"Condition: " + weather + Environment.NewLine +
"Outfit: " + Outfit + (If(String.IsNullOrWhiteSpace(RainGear), "", Environment.NewLine + "Rain Gear: " + RainGear))

Step 9: Display Recommendation

Add a Message Box activity.

Set the text to recommendation to show the user the full suggestion.

Step 10: Debug and Run

Save all files.

Click Debug File or Run File.

Enter a sample city when prompted, observe browser scraping, and verify the recommendation shown in the message box.

If the page selectors fail, re-indicate elements or add delays; adjust text parsing for different weather result formats.

Step 11: Optional Improvements

Add exception handling around browser scraping (Try Catch) to handle navigation or selector failures.

Add validation to ensure Temp parses to integer safely (use Int32.TryParse and default behavior if parsing fails).

Use assets or config file for user preferences (temperature units, outfit text variations).

Replace browser scraping with a weather API call (Http Request) for more reliable structured data if desired.

Step 12: Save and Add to GitHub

Save the project.

Initialize Git in UiPath Studio (Home → Team → GIT → Init Repository).

Commit and push the project to your GitHub repository for version control.
