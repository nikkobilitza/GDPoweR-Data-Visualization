

### GDPoweR Data Visualization Code

Note: 
Authors: Nikko Bilitza and Nicolas Prinz of the European Centre for Social Welfare Policy and Research
Contact: Nikko Bilitza (bilitza@euro.centre.org)
Date: 23.07.2024
This work is licensed under a Creative Commons Attribution Non-Commercial 4.0 International (CC BY-NC 4.0) license. This means that non-commercial reuse is allowed provided appropriate credit is given and any changes are indicated.

### Disclaimer:
This publication is part of the GDPoweR – Recovering workers’ data to negotiate and monitor collective agreements in the platform economy, which has received funding by the European Commission, DG Employment, Social Affairs and Inclusion, within the Social Prerogatives and Specific Competencies Lines (SocPL). The information and views set out in this document are those of the authors and do not necessarily reflect the views and official opinion of the European Union. Neither the European Union institutions and bodies nor any person acting on their behalf may be held responsible for the use which may be made of the information contained therein.

### Instructions
The code in this folder was developed to visualize personal data platform workers requested from the platforms they work with through Subject Access Requests. It produces an html-dashboard with statistics and charts on incomes, shifts and working hours and deliveries as well as maps based on GPS locations. This folder also contains a sample dataset of randomly generated mock data and an example dashboard created from this dataset. To create a dashboard with visualizations of your own data, you can fill out the blank Excel file "Blank_Spreadsheet.xlsx" in the folder with your data and save the completed file in the "Your Data" folder. After modifying the markdown code to use your new file instead of the test data, you can push a button to generate the dashboard.

Step-by-step instructions are provided below.
1. Complete the spreadsheet "Blank_Spreadsheet.xlsx" in the folder Your Data
 - Follow the instructions detailed below. Pay special attention to the recommended procedures for dealing with missing data, as improperly handling missing data can cause issues during data processing.
 - Leave columns blank if data is missing

2. rename it to "YourFileName.xlsx"

3. Open the R Project file and then the R Markdown file

4. Click the "Knit" button to update the dashboard, which will then appear in the viewer, it may take a while to load depending on how much data you have. You can either expand the viewer or navigate back to the folder and open "Code_GDPoweR.html" which now contains the dashboard based on your data. Keep in mind that each time you knit the file, it will overwrite the existing file. Therefore, if you want to create more dashboard html files, make sure to rename and save it.

Feel free to adjust the code to your needs. To run individual chunks of code, click on the green play-symbol on the top right corner for each chunk.


### Completing the Blank Spreadsheet with Your Data

This guide provides detailed instructions on how to input data into each column of the provided blank spreadsheet for the corresponding data frames which are seperated out into tabs in the spreadsheet. 
When pasting your data, ensure the columns remain in the correct order to maintain accuracy and consistency across rows. 
Additionally, do not modify the order of the tabs in the spreadsheet.

#### Key Considerations

##### Handling Missing Data
Properly managing missing data is essential to prevent errors during processing and to generate accurate visualizations from the available information. Follow these guidelines:

1. **Entire Dataframe Missing**:  
   If a complete dataframe is unavailable, leave the corresponding tab in the Excel file entirely blank. Do not insert placeholders, delete columns, or remove the tab itself.

2. **Missing Columns within a Dataframe**:  
   If some columns are missing within a dataframe, keep the empty columns intact, including their headers. Do not delete them.

##### Time Zones
The script assumes that the input data is in UTC, which it converts to CEST. If your data is not in UTC or your target timezone is not CEST, you must adjust the script to correctly read and convert the data to your target time zone.

##### Base Pay Types
The spreadsheet and script are configured to process three distinct types of base pay. Ensure your input aligns with the expected format for accurate results.

For questions or assistance, please contact Nikko Bilitza at bilitza@euro.centre.org.

DATAFRAME 1: payments 
Unit of observation: individual orders
Required columns:
$time_stamp: Timestamp of the payment. Format this as a date-time value (e.g., "2023-01-01 01:00:00").
$pay_a, $pay_b, ...: Columns for various forms of base pay per order. Each column should contain numeric values representing different types of base payment. If there is only one column for base pay paste it into pay_a and leave the rest blank.
$total_tips: Total tips received. This should be a numeric value indicating the sum of tips for an order.

DATAFRAME 2: schedules
Unit of observation: individual shifts
Required columns:
$starting_time: Start time of the schedule. Format this as a date-time value (e.g., "2023-01-01 01:00:00").
$ending_time: End time of the schedule. Format this as a date-time value (e.g., "2023-01-01 01:00:00").

DATAFRAME 3: deliveries
Unit of observation: individual orders
Required columns:
$time_accepted: Time when the order was accepted. Format this as a date-time value (e.g.,"2023-01-01 01:00:00").
$time_pick_up: Time when the order or customer was picked up. Format this as a date-time value (e.g., "2023-01-01 01:00:00").
$time_drop_off: Time when the order was completed. Format this as a date-time value (e.g., "2023-01-01 01:00:00").

Location data:
This can be represented in one of two ways:
Separate columns for longitude and latitude: For each location type (accepted, pick-up, and drop-off), provide separate columns for longitude and latitude. Each column should contain numeric values.
Location data in "POINT(longitude latitude)" format: Instead of separate columns for longitude and latitude, provide location data in the format "POINT(longitude latitude)". If you choose this format, delete the columns for longitude and latitude and add the data under the following columns:
$accepted_at_location
$picked_up_at_location
$dropped_off_at_location
After formatting the location data as "POINT(longitude latitude)", follow the provided R script to extract the coordinates for analysis. This will ensure that the location data is properly handled and ready for analysis.

DATAFRAME 4: geolocation
Unit of observation: gelocation pings
This dataframe is for detailed geolocation data provided around movements.
Required columns:
$timestamps_ping: Timestamp of the ping. Format this as a date-time value (e.g., "2023-01-01 01:00:00").
Location data:
This can be represented in one of two ways:
Separate columns for longitude and latitude: For each location type (accepted, pick-up, and drop-off), provide separate columns for longitude and latitude. Each column should contain numeric values.
Location data in "POINT(longitude latitude)" format: Instead of separate columns for longitude and latitude, provide location data in the format "POINT(longitude latitude)". If you choose this format, delete the columns for longitude and latitude and add the data under the following columns:
$location
After formatting the location data as "POINT(longitude latitude)", follow the provided R script to extract the coordinates for analysis. This will ensure that the location data is properly handled and ready for analysis.

DATAFRAME 5: breaks 
Unit of observation: individual breaks
Required columns:
$start_at: Start time of the break. Format this as a date-time value (e.g., "2023-01-01 01:00:00").
$end_at: End time of the break. Format this as a date-time value (e.g., "2023-01-01 01:00:00").
