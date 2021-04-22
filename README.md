# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Knowledge of the threshold values
3. A tool which can extract CSV data and autogenerate PDF report (Report reflecting minimum, maximum, breaches and trends of data)
4. Knowledge on the interface or way to notify the weekly report

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | PDF converter can be used to generate weekly report.
Counting the breaches       | Yes           | This is the part of the analysis and also required for unit test.
Detecting trends            | Yes           | This is the part of the analysis and also required for unit test.
Notification utility        | Yes           | This is the part of the analysis and it can be tested by mock function.
### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "No Input" test to  the PDF when CSV present in server is empty.
4. Write test to verify the count of breaches to the PDF 
5. Write test to verify the PDF Report is generated properly using data from CSV files for the trends.
6. Write test if the report contains data as per proper date and time to detect the trend.
7. Test if notification is sent or not, if notification is not sent some error messgae shall be reported.
8. Negative test if server access is not available.
9. Negative test if reciepent address is invalid.
10. Negative test if data present in CSV is in different than expected format.

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | 	pdf file    | report notification (email) | Mock notification function
Report inaccessible server | server access error | report server connection error | fake - Server is not accessible
Find minimum and maximum   | 	csv file |  Minimum and Maximum value in pdf, calculated using csv data | None - it's a pure function
Detect trend               | 	csv file |  Update the trends of data with Time and date values (Timestamp) | None - it's a pure function
Write to PDF               | analyzed output data from csv | Generated PDF report | Fake the csv to PDF converter
