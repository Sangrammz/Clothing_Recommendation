Data Capturing Bot Workflow

This UiPath project automates data entry from Excel into both web and desktop applications and runs both workflows in parallel from the main file.

Variables:

dtInputData (DataTable) – Stores web form data read from Excel
dtDesktopData (DataTable) – Stores desktop form data read from Excel
row (DataRow) – Represents each data row during iteration
Gender (String) – Stores “Male” or “Female” value from dataset
City / Department (String) – Stores dropdown selection values

Step-by-Step Process

How To Create Project
-------------------------------------------------


Open UiPath Studio → Choose Blank Process → Name it DataCapturingBot
Click Create to open the main project

Create WebDataCapturingBot.xaml
Add a new Sequence and name it WebDataCapturingBot.xaml
Add a Read Range activity to read Excel data and store it in variable dtInputData
Add a Use Application/Browser activity to open the target web page
Add a For Each Row in DataTable activity and select dtInputData
Inside the loop
– Use Type Into to fill form fields like Name, Email, etc.
– Add an If activity
Condition: row("Gender").ToString.ToLower = "male"
Then: Click Male radio button
Else: Click Female radio button
– Use Select Item to choose dropdown value from row("City").ToString
– Use Click activity to press the Submit button
Save and Debug or Run the workflow

Create DesktopDataCapturingBot.xaml
Add another new Sequence named DesktopDataCapturingBot.xaml
Add Read Range activity to read Excel data into dtDesktopData
Add Use Application/Browser activity and indicate your desktop app window
Add For Each Row in DataTable activity to loop through dtDesktopData
Inside the loop
– Use Type Into to fill data fields
– Use If activity for gender selection
Condition: row("Gender").ToString.ToLower = "male"
Then: Click Male option
Else: Click Female option
– Use Select Item for dropdowns such as row("Department").ToString
– Use Click to submit the form
Save and Run to confirm automation works correctly

Configure Main.xaml for Parallel Execution
Open Main.xaml (default workflow)
Drag and drop a Parallel activity
Inside the Parallel
– Add first Invoke Workflow File → select WebDataCapturingBot.xaml
– Add second Invoke Workflow File → select DesktopDataCapturingBot.xaml
Run or Debug to see both workflows executing simultaneously

Connect Project to GitHub
Create a new repository on GitHub named DataCapturingBot
In UiPath Studio, go to Home → Team → GIT → Init Repository
Add the remote URL of your GitHub repository
Click Commit and Push to upload files

Expected GitHub Folder Structure:
DataCapturingBot
│
├── Main.xaml
├── WebDataCapturingBot.xaml
├── DesktopDataCapturingBot.xaml
├── project.json
└── .gitignore

Output

• Reads data from Excel
• Enters data into both web and desktop applications
• Handles text fields, dropdowns, and radio buttons dynamically
• Runs both workflows in parallel from Main.xaml
• Connected with GitHub for version control
