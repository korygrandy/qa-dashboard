Acme Co - QA Metrics Dashboard
This repository contains a simple, interactive HTML dashboard designed to visualize Quality Assurance (QA) automation metrics for various testing teams within Sammons Financial Group. It provides a quick overview of automation coverage, tracks progress against planned automation, and highlights potential data inconsistencies.

✨ Features
Overall Automation Coverage: Displays total automated tests and tests planned for automation across all teams, with an aggregated progress bar.
Team-Specific Metrics: Provides detailed automation metrics for individual teams (CSM, Imaging, Phoenix, Ace), including their total tests, planned automation, and current automated count.
Dynamic Test Type Breakdown: Each team card features a collapsible section to show a granular breakdown of automated tests by type (Unit, Functional, API, Regression, etc.), complete with individual progress bars.

Intuitive Color Coding:
Progress Bars: Green (>80% automated), Yellow (>60% & <=80% automated), Red (<=60% automated).
Team Cards: Background color changes based on the team's overall automation coverage (Green, Yellow, Red).

Data Consistency Warnings:
An overall warning appears if "Total Tests Currently Automated" exceeds "Tests Planned for Automation."
Team-specific warnings are displayed if the sum of automated tests from individual test types does not match the team's reported "Tests Automated" figure from the CSV input.
CSV Data Input: Easily update all dashboard metrics by pasting new CSV data directly into a provided text area.
Print Functionality: A dedicated button to print the dashboard, optimized for a clean print layout (hides input/export sections).
Developer Readme: Built-in section within the dashboard itself provides detailed instructions for developers on configuration and regression testing.

🚀 How to Use
Viewing the Dashboard
Clone the repository:
git clone https://github.com/korygrandy/qa-dashboard.git


Navigate to the project directory:
cd qa-metrics-dashboard


Open index.html: Simply open the index.html file in your preferred web browser.
The dashboard will load with either hardcoded default data or randomly generated data, depending on the LOAD_FROM_HARDCODED_ON_STARTUP configuration (see Developer Information below).
Updating Dashboard Data
The dashboard is designed to be updated by pasting CSV (Comma Separated Values) content directly into a text area.
Prepare your CSV data:
Your CSV file must have exactly two columns: Metric and Value.
Example data structure:
Metric,Value
PlannedToAutomate,880
CSM_Total,200
CSM_PlannedToAutomate,180
CSM_Automated,117
CSM_Unit_Total,40
CSM_Unit_PlannedToAutomate,35
CSM_Unit_Automated,20
# ... and so on for all teams and test types


Important: The _Automated value for each team (e.g., CSM_Automated) should represent the sum of the automated counts of its constituent test types (e.g., CSM_Unit_Automated, CSM_Functional_Automated, etc.). The dashboard will calculate this sum internally and compare it to the provided CSM_Automated value to trigger a "Roll-up Warning" if there's a mismatch.
Exporting from Excel: In Excel, go to File > Save As > Browse, then select "CSV (Comma delimited) (*.csv)" from the "Save as type" dropdown. Open the saved .csv file with a simple text editor (like Notepad or VS Code) and copy its entire content.
Paste and Load:
Scroll down to the "Update Data via CSV" section on the dashboard.
Paste your copied CSV content into the large text area.
Click the "Load Data" button.
The dashboard will instantly update with your new metrics.
Understanding the Metrics
Total Tests Currently Automated: The sum of all automated tests across all teams and test types.
Tests Planned for Automation (Overall): The total number of tests targeted for automation across the entire QA effort.
Overall Automation Progress: A visual bar indicating the percentage of Total Tests Currently Automated against Tests Planned for Automation (Overall).
Team Cards: Each card represents a specific QA team.
Total Tests in Category: The total number of tests associated with that team.
Planned to Automate: The number of tests the team plans to automate.
Tests Automated: The number of tests the team has currently automated.
Click to see Breakdown by Test Type: Click this link to expand/collapse a detailed list of automation progress for specific test types (Unit, Functional, API, etc.) within that team.
Warnings:
Overall Automation Warning: Appears if Total Tests Currently Automated is greater than Tests Planned for Automation (Overall), indicating a potential data entry error or an oversight in updating planned targets.
Roll-up Warning (per team): Appears if the sum of the automated counts for a team's individual test types (e.g., CSM_Unit_Automated + CSM_Functional_Automated + ...) does not match the _Automated value provided for that team in the CSV (e.g., CSM_Automated). This flags an inconsistency in the provided data.
Printing the Dashboard
Click the "Print Dashboard" button in the header. The CSV input area and header navigation links will be automatically hidden for a cleaner printout.
🛠️ Developer Information
This dashboard is a single HTML file, making it extremely easy to deploy and manage.
Data Loading Configuration
You can control how data is loaded when the index.html page first opens:
LOAD_FROM_HARDCODED_ON_STARTUP constant:
Locate this JavaScript constant at the top of the <script> block in index.html:
const LOAD_FROM_HARDCODED_ON_STARTUP = true; // or false


Set to true: The dashboard will automatically load data from the HARDCODED_CSV_DATA string when the page loads. This is useful for consistent demonstration or if you have a fixed set of metrics you want to display by default.
Set to false: The dashboard will load random data initially. Users will then need to manually input data via the "Update Data via CSV" section.
HARDCODED_CSV_DATA constant:
If LOAD_FROM_HARDCODED_ON_STARTUP is true, the dashboard will use the data defined in this multiline string:
const HARDCODED_CSV_DATA = `Metric,Value
PlannedToAutomate,1000
CSM_Total,200
// ... your default CSV data here ...
`;

You can directly edit the content within these backticks (`) to change the default data that loads on startup.
Note: Direct file system access (e.g., loading from C:\temp\rawdata.csv) is not possible due to browser security policies. The HARDCODED_CSV_DATA string is the intended way to embed default data.
Regression Test Scenarios
The "Developer Readme" section directly within the dashboard's HTML includes three pre-defined CSV scenarios that you can copy and load to test the dashboard's behavior:
Scenario 1: All Green (High Automation Across the Board)
Expected outcome: High automation percentages, mostly green progress bars and team cards, no warnings.
Scenario 2: Mixed Coverage (Green, Yellow, Red)
Expected outcome: Varying automation levels, displaying different color codes for progress and team cards, no warnings.
Scenario 3: Data Inconsistencies (Triggering Warnings)
Expected outcome: Triggers both the overall "Automated > Planned" warning and team-specific "Roll-up Mismatch" warnings. This scenario is crucial for verifying the warning logic.
Use the "Copy CSV Data" link and "Load CSV Data" button provided for each scenario directly on the dashboard to quickly test these cases.
Technologies Used
HTML5: Structure of the dashboard.
Tailwind CSS: For rapid and responsive styling. Loaded via CDN.
JavaScript (Vanilla JS): For all interactive elements, data parsing, calculations, and dynamic content updates.

💡 Future Enhancements
Data Persistence: Implement local storage or a simple backend (e.g., Firebase Firestore) to save and load data, removing the need to paste CSV on every refresh.
Chart Integration: Use a charting library (e.g., Chart.js, D3.js) to visualize trends over time or breakdown data more effectively.
More Granular Metrics: Add metrics for defect counts, execution times, or pass/fail rates.
Filtering and Sorting: Allow users to filter teams or sort data based on different criteria.
User Interface Improvements: Enhance user experience with more interactive elements, animations, or a more sophisticated layout.

🤝 Contributing
Contributions are welcome! If you have suggestions for improvements or find any issues, please open an issue or submit a pull request.
📄 License
This project is open-source and available under the MIT License.
