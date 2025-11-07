Data Capturing Bot Workflow

This project automates Excel data entry into both web and desktop applications using UiPath. Both workflows are executed in parallel from the main file.

How To Create
---------------------------------------------------------

Step 1: Create Project

Open UiPath Studio.

Click on Process → select Blank Process.

Name the project as DataCapturingBot.

Choose a folder location and click Create.

Step 2: Create WebDataCapturingBot.xaml

In the Project panel, right-click the project and select Add → New Sequence.

Name it WebDataCapturingBot.xaml.

Drag and drop a Read Range activity.

Select the Excel file path from your local system.

Create a DataTable variable named dtInputData to store the Excel data.

Drag a Use Application or Browser activity and open the target web page where you want to enter data.

Inside it, drag a For Each Row in DataTable activity and select dtInputData.

Inside the loop:
a. Use Type Into activity to fill text fields such as Name and Email.
b. Add an If activity to handle the Gender radio button.

Condition: row("Gender").ToString.ToLower = "male"

Then: Click Male option

Else: Click Female option
c. Use Select Item activity for dropdown fields and set the value as row("City").ToString.
d. Use Click activity to click on the Submit button.

Save and run to test the workflow.

Step 3: Create DesktopDataCapturingBot.xaml

In the Project panel, add another new Sequence named DesktopDataCapturingBot.xaml.

Add a Read Range activity to read Excel data.

Select the Excel file path and store the data in dtDesktopData variable.

Add a Use Application or Browser activity and indicate the desktop application window.

Inside it, drag a For Each Row in DataTable activity and select dtDesktopData.

Inside the loop:
a. Use Type Into activity to enter data in text boxes.
b. Add an If activity to handle gender options.

Condition: row("Gender").ToString.ToLower = "male"

Then: Click Male option

Else: Click Female option
c. Use Select Item activity for dropdown fields like row("Department").ToString.
d. Use Click activity to press the Submit or Save button.

Save and test the workflow to ensure correct data entry.

Step 4: Configure Main.xaml to Run Both Workflows

Open Main.xaml file (the default workflow).

Drag and drop a Parallel activity.

Inside the Parallel activity:
a. Add the first Invoke Workflow File activity and select WebDataCapturingBot.xaml.
b. Add the second Invoke Workflow File activity and select DesktopDataCapturingBot.xaml.

Click Debug or Run to see both workflows executing simultaneously.

Step 5: Connect Project to GitHub

Create a new repository in GitHub and name it DataCapturingBot.

In UiPath Studio, go to Home → Team → GIT → Init Repository.

Add the remote URL of your GitHub repository.

Click Commit and Push to upload your project files.

Verify that the following files are uploaded:

Main.xaml

WebDataCapturingBot.xaml

DesktopDataCapturingBot.xaml

project.json

.gitignore

Output

The bot reads data from Excel.

It enters data into both web and desktop applications.

It fills text boxes, selects dropdowns, and handles radio buttons dynamically.

Both workflows run in parallel from the main file.

The entire project is version-controlled in GitHub.

Summary

This project demonstrates how to:

Read data from Excel files.

Automate both web and desktop form filling.

Execute multiple workflows in parallel.

Use conditional logic for handling gender and dropdowns.

Connect and manage UiPath projects with GitHub.
