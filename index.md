## Natural Disasters 
CFG Project by @V_Mayya

Given the recent wildfires in Australia, heat wave in Europe and other natural disasters over the years, my project will be exploring the impact and methods that nations have used to deal with the aftermath of such disasters. It will specifically focus on types of key natural disasters during the years of 2000-2022 (along with their magnitudes), events, number of fatalities, the recovery period, economic impact, support after the disaster and others.

The idea to create a project based around natural disasters was developed after reading the book 'Extreme Economies'. One of the incidents described in the book was about how Aceh (a province of Indonesia) managed to resume its daily operations almost immediately after disaster struck. The economic resilience and methods the region used to dampen the impact of the natural disaster inspired me to create this project. 

### Implications

The creation of this project is intended to: 
- understand the impact of climate change and natural disasters on individuals and wildlife
- learn about which methods were best to recover from the aftermath of a disaster 
- learn more about the economic resilience and unity of a nation during moments of crisis

### Setting up tables and columns

**COUNTRIES**: country_unique_ID, country_code, countries where disaster struck along with their respective regions

**NATURAL DISASTER TYPES**: natural_disaster_unique_ID, natural disaster classification (earthquake, tsunami, wildfires, cyclones, etc.) 

**EVENTS**: dates of natural disasters, country_unique_ID,  natural_disaster_unique_ID, magnitude of each event
 
Note: Magnitudes have been determined on an integer scale by -
- Earthquake: Earthquake Magnitude Scale 
- Hurricane: Saffir-Simpson Hurricane Wind Scale (from categories 1 to 5)
- Tsunami: Richter Scale/Tsunami or Seismic Magnitude Scale 
- Volcanic Activity: Volcanic Exposivity Index (**VEI**) 
- Drought: Palmer Drought Severity Index 
- Wildfire: Measured according to class A, B and so on - converted to integers for purpose of data analysis; so class 1, 2 and so on 
- Flood: **DFO** Flood magnitude scale or Flood magnitude = log (Duration × Severity × Area Affected)
- Extreme Temperature/Heat Wave: Heat Wave Magnitude Index or others (1: Mild, 5: Severe) 

Data points with value NULL represent either N/A if magnitude is not measured in terms of an integer scale or insufficient data available. 

**FATALITIES**: number of fatalities, species impacted (number of animals affected), dates of disaster, country_unique_ID 

**OTHER IMPACTS**: number of displaced individuals/injuries, dates of disaster, country_unique_ID 

**RECOVERY**: dates of disaster, country_unique_ID, number of days for complete recovery, method country used to deal with aftermath of disaster

**ECONOMIC IMPACT**: 
1. Table 1: economic damage in terms of total monetary impact/revenue lost by businesses (in billions of dollars), country_unique_ID, dates of natural disasters

2. Table 2: disaster losses as a % of global GDP, country_unique_ID, dates of natural disasters 

**SUPPORT**: organisations that have offered support during the aftermath, total amount of support offered, country_unique_ID

```
CREATE DATABASE natural disasters;

USE natural disasters;
```
Some of the tables will have primary and foreign constraints. The first table is for countries with country_unique_ID to uniquely identify all lists of countries. Creating and inserting data into the tables:

```
-- Table 1
CREATE TABLE countries (
  country_unique_ID INT,
  country_code VARCHAR(10) UNIQUE,
  country VARCHAR(35),  
  CONSTRAINT PK_country_unique_ID PRIMARY KEY (country_unique_ID)); 
  
INSERT INTO countries (country_unique_ID, country_code, country) Values (1, 'AF', Afghanistan'),(2,'AL' 'Albania'),(3, 'DZ', 'Algeria'),(4, 'AS', 'American Samoa'),(5, 'AD', 'Andorra'),(6, 'AO', 'Angola'),(7, 'AI', 'Anguilla'),(8, 'AQ', 'Antarctica'),(9, 'AG', 'Antigua And Barbuda'),(10, 'AR', 'Argentina'),(11, 'AM','Armenia'),(12, 'AW','Aruba'),(13, 'AU', 'Australia'), (14, 'AT’, 'Austria'),(15, 'AZ’, 'Azerbaijan'),(16, 'BS’, 'Bahamas'),(17, 'BH’, 'Bahrain'),(18, 'BD’, 'Bangladesh'),(19, 'BB’, 'Barbados'),(20, 'BY’, 'Belarus'),(21, 'BE’, 'Belgium'),(22, 'BZ’, 'Belize'),(23, 'BJ’, 'Benin'),(24, 'BM’, 'Bermuda'),(25, 'BT’, 'Bhutan'),(26, 'BO’, 'Bolivia'),(27, 'BA’, 'Bosnia And Herzegovina'),(28, 'BW’, 'Botswana'),(29, 'BV’, 'Bouvet Island'),(30, 'BR’, 'Brazil'),(31, 'IO’, 'British Indian Ocean Territory'),(32, 'BN’, 'Brunei Darussalam'),(33, 'BG’, 'Bulgaria'),(34, 'BF’, 'Burkina Faso'),(35, 'BI’, 'Burundi)',(36, 'KH’, 'Cambodia'),(37, 'CM’, 'Cameroon'),(38, 'CA’, 'Canada'),(39, 'CV’, 'Cape Verde'),(40, 'KY’, 'Cayman Islands'),(41, 'CF’, 'Central African Republic'),(42, 'TD’, 'Chad'),(43, 'CL’, 'Chile'),(44, 'CN’, 'China'),(45, 'CX’, 'Christmas Island'),(46, 'CC’, 'Cocos (keeling) Islands'),(47, 'CO’, 'Colombia'),(48, 'KM’, 'Comoros'),(49, 'CG’, 'Congo'),(50, 'CD’, 'Congo),(51, 'CK’, 'Cook Islands'),(52, 'CR’, 'Costa Rica'),(53, 'CI’, 'Cote D'ivoire'),(54, 'HR’, 'Croatia'),(55, 'CU’, 'Cuba'),(56, 'CY’, 'Cyprus'),(57, 'CZ’, 'Czech Republic'),(58, 'DK’, 'Denmark'),(59, 'DJ’, 'Djibouti'),(60, 'DM’, 'Dominica'),(61, 'DO’, 'Dominican Republic'),(62, 'TP’, 'East Timor'),(63, 'EC’, 'EcuadorDo '),(64, 'EG’, 'Egypt'),(65, 'SV’, 'El Salvador'),(66, 'GQ’, 'Equatorial Guinea'),(67, 'ER’, 'Eritrea'),(68, 'EE’, 'Estonia'),(69, 'ET’, 'Ethiopia'),(70, 'FK’, 'Falkland Islands (malvinas)'),(71, 'FO’, 'Faroe Islands'),(72, 'FJ, 'Fiji'),(73, 'FI’, 'Finland'),(74, 'FR’, 'France'),(75, 'GF’, 'French Guiana'),(76, 'PF’, 'French Polynesia'),(77, 'TF’, 'French Southern Territories'),(78, 'GA’, 'Gabon'),(79, 'GM’, 'Gambia'),(80, 'GE’, 'Georgia'),(81, 'DE’, 'Germany'),(82, 'GH’, 'Ghana'),(83, 'GI’, 'Gibraltar'),(84, 'GR’, 'Greece'),(85, 'GL’, 'Greenland'),(86, 'GD’, 'Grenada'),(87, 'GP’, 'Guadeloupe'),(88, 'GU’, 'Guam'),(89, 'GT’, 'Guatemala'),(90, 'GN’, 'Guinea'),(91, 'GW’, 'Guinea-bissau'),(92, 'GY’, 'Guyana'),(93, 'HT’, 'Haiti'),(94, 'HM’, 'Heard Island And Mcdonald Islands'),(95, 'VA’, 'Holy See (vatican City State)'),(96, 'HN’, 'Honduras'),(97, 'HK’, 'Hong Kong'),(98, 'HU’, 'Hungary'),(99, 'IS’, 'Iceland'),(100, 'IN’, 'India'),(101, 'ID’, 'Indonesia'),(102, 'IR’, 'Iran),(103, 'IQ’, 'Iraq'),(104, 'IE’, 'Ireland)',(105, 'IL’, 'Israel'),(106, 'IT’, 'Italy'),(107, 'JM’, 'Jamaica'),(108, 'JP’, 'Japan'),(109, 'JO’, 'Jordan'),(110, 'KZ’, 'Kazakstan'),(111, 'KE’, 'Kenya'),(112, 'KI’, 'Kiribati'),(113, 'KP’, 'Korea, Democratic People's Republic Of'),(114, 'KR’, 'Korea’, Republic OfOkay '),(115, 'KV’, 'Kosovo'), (116, 'KW’, 'Kuwait'),(117, 'KG’, 'Kyrgyzstan'),(118, 'LA’, 'Lao People's Democratic Republic'),(119, 'LV’, 'Latvia'),(120, 'LB’, 'Lebanon'),(121, 'LS’, 'Lesotho'),(122, 'LR’, 'Liberia'),(123, 'LY’, 'Libyan Arab Jamahiriya'),(124, 'LI’, 'Liechtenstein'),(125, 'LT’, 'Lithuania'),(126, 'LU’, 'Luxembourg'),(127, 'MO’, 'Macau'),(128, 'MK’, 'Macedonia, The Former Yugoslav Republic Of'),(129, 'MG’, 'Madagascar'),(130, 'MW’, 'Malawi'),(131, 'MY’, 'Malaysia'),(132, 'MV’, 'Maldives'),(133, 'ML’, 'Mali'),(134, 'MT’, 'Malta'),(135, 'MH’, 'Marshall Islands'),(136, 'MQ’, 'Martinique'),(137, 'MR’, 'Mauritania'),(138, 'MU’, 'Mauritius'),(139, 'YT’, 'Mayotte'),(140, 'MX’, 'Mexico'),(141, 'FM’, 'Micronesia, Federated States Of'),(142, 'MD’, 'Moldova, Republic Of'),(143, 'MC’, 'Monaco'),(144, 'MN’, 'Mongolia'),(145, 'MS’, 'Montserrat'),(146, 'ME’, 'Montenegro'),(147, ‘MA’, 'Morocco'),(148, 'MZ’, 'Mozambique'),(149, 'MM’, 'Myanmar'),(150, 'NA’, 'Namibia'),(151, 'NR’, 'Nauru'),(152, 'NP’, 'Nepal'),(153, 'NL’, 'Netherlands),(154, 'AN’, 'Netherlands Antilles'),(155, 'NC’, 'New Caledonia'),(156, 'NZ’, 'New Zealand'),(157, 'NI’, 'Nicaragua'),(158, 'NE’, 'Niger'),(159, 'NG’, 'Nigeria'),(160, 'NU’, 'Niue'),(161, 'NF’, 'Norfolk Island'),(162, 'MP, Northern Mariana Islands'),(163, 'NO’, 'Norway'),(164, 'OM’, 'Oman'),(165, 'PK’, 'Pakistan'),(166, 'PW’, 'Palau'),(167, 'PS’, 'Palestinian Territory, Occupied'),(168, 'PA’, 'Panama'),(169, 'PG’, 'Papua New Guinea'),(170, 'PY’, 'Paraguay'),(171, 'PE’, 'Peru'),(172, 'PH’, 'Philippines'),(173, 'PN’, 'Pitcairn'),(174, 'PL’, 'Poland'),(175, 'PT’, 'Portugal'),(176, 'PR, 'Puerto Rico'),(177, 'QA’, 'Qatar'),(178, 'RE’, 'Reunion'),(179, 'RO’, 'Romania'),(180, 'RU’, 'Russian Federation'),(181, 'RW’, 'Rwanda'),(182, 'SH’, 'Saint Helena'),(183, 'KN’, 'Saint Kitts And Nevis'),(184, 'LC’, 'Saint Lucia'),(185, 'PM’, 'Saint Pierre And Miquelon'),(186, 'VC’, 'Saint Vincent And The Grenadines'),(187, 'WS’, 'Samoa'),(188, 'SM’, 'San Marino'),(189, 'ST’, 'Sao Tome And Principe'),(190, 'SA’, 'Saudi Arabia'),(191, 'SN’, 'Senegal'),(192, 'RS’, 'Serbia'),(193, 'SC’, 'Seychelles'),(194, 'SL’, 'Sierra Leone'),(195, 'SG’, 'Singapore'),(196, 'SK’, 'Slovakia'),(197, 'SI’, 'Slovenia'),(198, 'SB’, 'Solomon Islands'),(199, 'SO’, 'Somalia'),(200, 'ZA’, 'South Africa'),(201, 'GS’, 'South Georgia And The South Sandwich Islands'),(202, 'ES’, 'Spain'),(203, 'LK’, 'Sri Lanka'),(204, 'SD’, 'Sudan'),(205, 'SR’, 'Suriname'),(206, 'SJ’, 'Svalbard And Jan Mayen'),(207, 'SZ’, 'Swaziland'),(208, 'SE’, 'Sweden'),(209, 'CH’,'Switzerland'),(210, 'SY’, 'Syrian Arab Republic'),(211, 'TW’, 'Taiwan, Province Of China'),(212, 'TJ’, 'Tajikistan'),(213, 'TZ’, 'Tanzania,United Republic Of'),(214, 'TH’, 'Thailand'),(215, 'TG’, 'Togo)',(216, 'TK’, 'Tokelau'),(217, 'TO’, 'Tonga'),(218, 'TT’, 'Trinidad And Tobago'),(219, 'TN’, 'Tunisia'),(220, 'TR’, 'Turkey'),(221, 'TM', 'Turkmenistan'),(222, 'TC’, 'Turks And Caicos Islands'),(223, 'TV’, 'Tuvalu'),(224, 'UG’, 'Uganda'),(225, 'UA’, 'Ukraine'),(226, 'AE’, 'United Arab Emirates'),(227, 'GB’, 'United Kingdom'),(228, 'US’, 'United States'),(229, 'UM’, 'United States Minor Outlying Islands'),(230, 'UY’, 'Uruguay'),(231, 'UZ’, 'Uzbekistan'),(232, 'VU’, 'Vanuatu'),(233, 'VE’, 'Venezuela'),(234, 'VN’, 'Vietnam'),(235, 'VG’, 'Virgin Islands, British'),(236, 'VI’, 'Virgin Islands, U.S.'),(237, 'WF’, 'Wallis And Futuna'),(238, 'EH’, 'Western Sahara'),(239, 'YE’, 'Yemen'),(240, 'ZM’, 'Zambia'),(241, 'ZW’, 'Zimbabwe); 
  
```
The next table lists the types of natural disasters along with a unique ID as well. 

```
-- Table 2
CREATE TABLE types (
  natural_disaster_ID INT,
  type VARCHAR(40), 
  CONSTRAINT PK_natural_disaster_ID PRIMARY KEY (natural_disaster_ID)); 
  
INSERT INTO types (natural_disaster_ID, type) Values (1, 'Drought'), (2, 'Earthquake'), (3, 'Extreme Temperature'), (4, 'Flood'), (5, 'Landslide'), (6, 'Mass Movement'), (7, 'Storm/Cyclone/Hurricane'), (8, 'Volcanic activity'), (9, 'Wildfire'), (10, 'Tsunami'); 

```

Table 3 (events): 

```
CREATE TABLE events (
  date DATE,
  natural_disaster_ID INT,
  country_code VARCHAR(10),
  magnitude DEC(10,2), 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_natural_disaster_ID FOREIGN KEY (natural_disaster_ID) references types(natural_disaster_ID)); 
  
  
INSERT INTO events (date, natural_disaster_ID, country_code, magnitude) Values ('2004-10-23', 2, 'JP', 6.8), ('2005-08-23', 7, 'US', 5), ('2008-05-12', 2, 'CN', 7.9), ('2011-03-11', 2, 'JP', 7.4), ('2011-07-25', 4, 'TH', 7), ('2012-10-22', 7, 'US', 3), ('2017-08-17', 7, 'US', 4), ('2017-09-16', 7, 'US', 5), ('2017-08-30', 7, 'US', 5), ('2021-08-26', 7, 'US', 4), ( 
  
```

Table 4 (fatalities - consists of 4 tables, each containing around 5 years data):

```
-- 2000-2005
CREATE TABLE fatalities_table_1 (
  number_of_fatalities INT,
  species_impacted VARCHAR(55),
  country_code VARCHAR(10),
  natural_disaster_ID INT,
  date DATE, 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_natural_disaster_ID FOREIGN KEY (natural_disaster_ID) references types(natural_disaster_ID), 
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date)); 
  
INSERT INTO fatalities_table_1 (date, natural_disaster_ID, country_code, species_impacted, number_of_fatalities) Values ('2004-10-23', 2, 'JP', 5000, 68),  
  
-- 2005-2010
CREATE TABLE fatalities_table_2 (
  number_of_fatalities INT,
  species_impacted VARCHAR(55),
  country_code VARCHAR(10),
  natural_disaster_ID INT,
  date DATE, 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_natural_disaster_ID FOREIGN KEY (natural_disaster_ID) references types(natural_disaster_ID), 
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date)); 
  
INSERT INTO fatalities_table_2 (date, natural_disaster_ID, country_code, species_impacted, number_of_fatalities) Values 
  
-- 2010-2015
CREATE TABLE fatalities_table_3 (
  number_of_fatalities INT,
  species_impacted VARCHAR(55),
  country_code VARCHAR(10),
  natural_disaster_ID INT,
  date DATE, 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_natural_disaster_ID FOREIGN KEY (natural_disaster_ID) references types(natural_disaster_ID), 
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date)); 

INSERT INTO fatalities_table_3 (date, natural_disaster_ID, country_code, species_impacted, number_of_fatalities) Values 

--2015-2022
CREATE TABLE fatalities_table_4 (
  number_of_fatalities INT,
  species_impacted VARCHAR(55),
  country_code VARCHAR(10),
  natural_disaster_ID INT,
  date DATE, 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_natural_disaster_ID FOREIGN KEY (natural_disaster_ID) references types(natural_disaster_ID), 
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date)); 
  
INSERT INTO fatalities_table_4 (date, natural_disaster_ID, country_code, species_impacted, number_of_fatalities) Values 
 
```

Table 5 (other impacts): 

```
CREATE TABLE other_impacts (
  date DATE,
  country_code VARCHAR(10),
  displaced_or_injured INT, 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date)); 
  
INSERT INTO other_impacts (date, country_code, displaced_or_injured) Values ('2004-10-23','JP', 4805), (
```

Table 6 (recovery):

```
CREATE TABLE recovery (
  date DATE,
  country_code VARCHAR(10),
  days_to_recover INT,
  method_to_deal_with_disaster VARCHAR(100) 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date));  
  
INSERT INTO recovery (date, country_code, days_to_recover, method_to_deal_with_disaster) Values ('2004-10-23','JP', ), (
```

Tables 7 and 8 (economic impact):

```
CREATE TABLE economic_impact_1 (
  total_monetary_impact INT,
  date DATE,
  country_code VARCHAR(10) 
  CONSTRAINT FK_country_code FOREIGN KEY (country_code) references countries(country_code),
  CONSTRAINT FK_date FOREIGN KEY (date) references events(date));  
  
 INSERT INTO economic_impact_1 (total_monetary_impact, date, country_code) Values (40, '2004-10-23', 'JP'), (173, '2005-08-23', 'US'), (107,'2008-05-12', 
 'CN'), (253, '2011-03-11', 'JP'), (48, '2011-07-25', 'TH'), (59, '2012-10-22', 'US'), (105, '2017-08-17', 'US'), (75, '2017-09-16', 'US'), (63, '2017-08-30', 'US'), (65, '2021-08-26', 'US')
 
 -- Note: Data from the international disasters database EM-DAT
  
 CREATE TABLE economic_impact_2 
  %_of_global_GDP DEC(10,2),
  region VARCHAR(100)); 
  
 INSERT INTO economic_impact_2 (region, %_of_global_GDP) Values ('World', 4.0), ('Europe', 0.7), ('Latin America and Caribbean', 3.0), ('North America', 4.1), ('East Asia and Pacific', 4.7), ('Sub-Saharan Africa', 6.1), ('Middle East and North Africa', 5.7), ('Central Asia', 6.6), ('South Asia', 15);

-- Note: the above data is a rough estimate taken from the S&P Global Ratings graph 
```

Table 9 (support):

```
CREATE TABLE support (
  organisations VARCHAR(150),
  amount VARCHAR(100),
  country_unique_ID INT, 
  CONSTRAINT FK_country_ID FOREIGN KEY (country_unique_ID) references countries(country_unique_ID)); 
  
```

Creating a trigger to capitalise organisations:

```
DELIMITER //
CREATE TRIGGER organisations_trig
BEFORE INSERT on support
FOR EACH ROW
BEGIN
SET NEW.organisations = CONCAT(UPPER(SUBSTRING(NEW.organisations,1,1)),LOWER(SUBSTRING(NEW.organisations,2))); 
END//
```

### Queries for Data Analysis

- Economic impact to a particular country (Japan chosen as an example) over the years of 2000-2022 demonstrated through the query shown as follows 

```
SELECT SUM(total_monetary_impact), country_code FROM economic_impact_1 WHERE country_code = .. GROUP BY country_code ORDER BY total_monetary_impact DESC; 
```

Based on the locations of countries that have faced the greatest economic impact in terms of monetary damage over the years of 2000-2022, economic resilience of the country can be analysed by comparing economic indicators of the country (in terms of GDP and other indices) to other countries along with the data that results from the query. 

If a country has been able to sustain its economy well despite large monetary damages due to natural disasters, other countries can try utilising methods the country has used to cope with the aftermath of the disaster. 

In the case of Japan, total economic damage of major natural disasters during the period was around .... Japan's economy as of 2022 is ...
Learning more about Japan's economic resilience can help other countries build plans and policies to deal with such issues. 

```
SELECT %_of_global_GDP, region FROM economic_impact_2 ORDER BY %_of_global_GDP desc; 
```
| region | %_of_global_GDP | 
| South Asia | 15 | 
| Central Asia | 6.6 |
| Sub-Saharan Africa | 6.1 |
| Middle East and North Africa | 5.7 | 
| East Asia and Pacific | 4.7 |
| World | 4.0 |
| Latin America and Caribbean | 3.0 |
| Europe | 0.7 |

The data demonstrates how the impact of climate change that has resulted in natural disasters has had varying effects based on different regions. According to S&P Global Ratings, South Asia is around 10 times more exposed to the economic impact of climate change compared to Europe. 'Climate change could see 4% of global annual economic output lost by 2050 and hit many poorer parts of the world disproportionately hard, a new study of 135 countries has estimated.' By ordering the data, it can observed that South Asia has the highest disaster losses as a % of GDP with Central Asia just below. 

All of these facts highlight the importance of dealing with climate change and economic support that must be offered to Asian economies. It is difficult to find a solution that can be used for all regions. However, certain measures such as bringing about awareness of disaster risk management, analysing certain impacts (job losses, tax revenue loss and others), developing strategic plans considering various stakeholders and others can help mitigate the impact. 

There has been a lot of research done in this area:
https://www.journals.uchicago.edu/doi/full/10.1093/reep/rez004 

https://www.suncorpgroup.com.au/uploads/190905-Economic-benefits-of-Suncorp-Insurance-REPORT-PDF-version.pdf

https://www.routledge.com/Disasters-and-Economic-Recovery/Downey/p/book/9780367258580

- Country with the maximum and minimum number of fatalities during 2000-2022 demonstrated through 2 subqueries shown as follows

```
-- Maximum number of fatalities
-- 1. Create View to use for later 
CREATE VIEW max_fatalities_by_country AS 
(SELECT MAX(number_of_fatalities) AS 'max_number_of_fatalities_by_country', country_code FROM ((SELECT * FROM fatalities_table_1) UNION ALL (SELECT * FROM fatalities_table_2) UNION ALL (SELECT * FROM fatalities_table_3) UNION ALL (SELECT * FROM fatalities_table_4)) AS all_fatalities_table GROUP BY country_code ORDER BY MAX(number_of_fatalities) desc); 

-- 2. Select country with maximum number of fatalities during 2000-2022
SELECT * FROM max_fatalities_by_country LIMIT 1; 

--Minimum number of fatalities
-- 1. Create View to use for later 
CREATE VIEW min_fatalities_by_country AS 
(SELECT MIN(number_of_fatalities) AS 'min_number_of_fatalities_by_country', country_code FROM ((SELECT * FROM fatalities_table_1) UNION ALL (SELECT * FROM fatalities_table_2) UNION ALL (SELECT * FROM fatalities_table_3) UNION ALL (SELECT * FROM fatalities_table_4)) AS all_fatalities_table GROUP BY country_code ORDER BY MIN(number_of_fatalities) asc); 

-- 2. Select country with maximum number of fatalities during 2000-2022
SELECT * FROM min_fatalities_by_country LIMIT 1;

```

- Number of species of wildlife impacted in countries that have had moderate to severe earthquakes

```
SELECT SUM(species_impacted) AS 'No. of animals impacted', country_code FROM ((SELECT * FROM fatalities_table_1) UNION ALL (SELECT * FROM fatalities_table_2) UNION ALL (SELECT * FROM fatalities_table_3) UNION ALL (SELECT * FROM fatalities_table_4)) AS all_fatalities WHERE country_code IN (SELECT country_code FROM events WHERE magnitude >= 6) GROUP BY country_code HAVING SUM(species_impacted) > 100; 
``` 

According to the earthquake magnitude scale, magnitudes greater than 6 can cause severe destruction. The subquery will allow the user to find the countries and their respective number of animals impacted for all moderate to severe earthquakes where number of species impacted were greater than 100. 

This can then be compared with total number of earthquakes of magnitude greater than 6 for each country (Japan in this example) using the following query.

``` 
SELECT COUNT(country_code) AS 'Number of earthquakes of magnitude >= 6' FROM events WHERE magnitude >= 6 AND country_code = .. ; 

``` 

A percentage can be established that will demonstrate the % that more than 3 different species of wildlife were impacted during moderate to severe earthquakes. This will demonstrate the true impact of one type of natural disaster on wildlife. In Japan, this amounts to around: 

Note that the figures are based on only major natural disasters that have taken place and might not account for all types of wildlife species impacted. 

- Number of massively destructive earthquakes (magnitude >= 6.0) by country

``` 
SELECT COUNT(country_code), country_code AS 'Number of earthquakes of magnitude >= 6' FROM events WHERE magnitude >=6 GROUP BY country_code ORDER BY COUNT(country_code) desc;

``` 
Output: 


From the output, it can be observed that ... country had the highest number of destructive earthquakes during the period of 2000-2022. ....

``` 
-- And to generally find out number of massively destructive earthquakes (magnitude > 6) during 2000-2022 in % to total number of earthquakes 

SELECT COUNT(country_code) AS 'Number of earthquakes of magnitude >= 6' FROM events WHERE magnitude >=6;

SELECT COUNT(country_code) AS 'Total number of earthquakes' FROM events;

-- % of earthquakes that had a significant impact (magnitude >=6) is: .. % during the period of 2000-2022. 

``` 

- Number of hurricanes/storms/cyclones by country

As an example, we can compare the number of hurricanes during the period of 2000-2022 to find which country has had the highest number of hurricanes. 

``` 
SELECT COUNT(country_code), country_code AS 'Number of Hurricanes' FROM events WHERE natural_disaster_ID = 7 GROUP BY country_code ORDER BY COUNT(country_code) desc;

``` 
... like U.S.A had the highest number of hurricanes during the period of 2000-2022. 

- Establishing other trends

Other trends can be identified by changing the GROUP BY condition accordingly or by using JOIN statements. For example, a trend can be established with magnitudes of a certain disaster such as earthquakes, number of fatalities and dates of disasters. By first getting data using the SELECT statement, a graph with time as the independent variable and other variables such as number of fatalities and magnitudes as the dependent variables can be used to derive relationships.

In this instance, a causal relationship between magnitudes of earthquake and number of fatalities over time can be established (based on a priori hypothesis and intuition). However, in most instances, since correlation is not causation, more information is needed to establish trends. 

```
-- Relationship between magnitudes of earthquakes and number of fatalities over time (2000-2022)
CREATE VIEW magnitude_and_fatalities_view AS
SELECT c.date, c.natural_disaster_ID, c.magnitude, d.number_of_fatalities FROM events c INNER JOIN fatalities_table_1 d ON c.date = d.date INNER JOIN fatalities_table_2 e ON c.date = e.date INNER JOIN fatalities_table_3 f ON c.date = f.date INNER JOIN fatalities_table_4 g ON c.date = g.date; 

-- Full view and condition to find relationship between magnitudes of earthquakes and number of fatalities over time
SELECT * FROM magnitude_and_fatalities_view; 
SELECT * FROM magnitude_and_fatalities_view WHERE natural_disaster_ID = 2; 

-- Total number of fatalities by natural disaster type and country (or remove country_code completely) 
SELECT c.natural_disaster_ID, c.country_code, SUM(number_of_fatalities) AS 'Total number of fatalities' FROM fatalities_table_1 c INNER JOIN fatalities_table_2 d ON natural_disaster_ID.c = natural_disaster_ID.d INNER JOIN fatalities_table_3 e ON natural_disaster_ID.d = natural_disaster_ID.e INNER JOIN fatalities_table_4 f ON natural_disaster_ID.e = natural_disaster_ID.f; 

```
- Generating a stored function to produce magnitude scales for all disasters from 2000-2022 

```
DELIMITER //
CREATE FUNCTION magnitude_scale(
	natural_disaster_ID INT
) 
RETURNS VARCHAR(150)
DETERMINISTIC
BEGIN
    DECLARE mag_scale VARCHAR(150);
	  IF natural_disaster_ID = 1 THEN SET mag_scale = 'Palmer Drought Severity Index';
    ELSEIF natural_disaster_ID = 2 THEN SET mag_scale = 'Earthquake Magnitude Scale';
    ELSEIF natural_disaster_ID = 3 THEN SET mag_scale = 'Heat Wave Magnitude Index or Others';
    ELSEIF natural_disaster_ID = 4 THEN SET mag_scale = 'Flood magnitude scale or log (Duration × Severity × Area Affected)';
    ELSEIF natural_disaster_ID = 5 THEN SET mag_scale = 'Others';
    ELSEIF natural_disaster_ID = 6 THEN SET mag_scale = 'Others';
    ELSEIF natural_disaster_ID = 7 THEN SET mag_scale = 'Saffir-Simpson Hurricane Wind Scale';
    ELSEIF natural_disaster_ID = 8 THEN SET mag_scale = 'Volcanic Exposivity Index';
    ELSEIF natural_disaster_ID = 9 THEN SET mag_scale = 'Integer Classes (for purpose of data analysis)';
    ELSEIF natural_disaster_ID = 10 THEN SET mag_scale = 'Richter Scale/Tsunami or Seismic Magnitude Scale';
    END IF; 
    Return mag_scale;
END//

SELECT date, natural_disaster_ID, magnitude, magnitude_scale(natural_disaster_ID) AS 'Magnitude Scale' FROM events; 
    
```
The resulting output from the events table is:

| date | natural_disaster_ID | magnitude | Magnitude Scale | 

|  |  | 
|  |  |
|  |  |
| | | 
| |  |
|  | |
| |  |
| |  |

### Further Questions/Extensions and Limitations 

Extensions:
- Would be interesting to conduct data analysis related to climate change (such as GHG or carbon emissions, sea level rises) months prior to the disaster to find any causal effects of climate change on increasing the risk of disaster in a country
- Include all countries by region to link to economic impact table 2
- Include names of disasters to better assist analysis of data and generate more subqueries using LIKE and others

Limitations: 
- Limitation could be natural disasters accounts for only small number of fatalities/gdp loss compared to other things but still equally impactful 
- Other types of disasters not included? 
- Impact of natural disasters can be measured not only through number of fatalities, displaced individuals and economic impact but also through other ways such as number of business re-openings after disaster, population growth,  

### References 
- https://www.emdat.be/
- https://ourworldindata.org/natural-disasters
- https://cdd.publicsafety.gc.ca/srchpg-eng.aspx?dynamic=false
- https://www.weforum.org/agenda/2022/04/climate-change-global-gdp-risk/#:~:text=Over%20the%20past%2010%20years,to%20insurance%20firm%20Swiss%20Re
- https://www.forbes.com/sites/rogerpielke/2019/10/31/surprising-good-news-on-the-economic-costs-of-disasters/?sh=867d75b1952e 
- https://www.mtu.edu/geo/community/seismology/learn/earthquake-measure/magnitude/
- https://github.com/lukes/ISO-3166-Countries-with-Regional-Codes/blame/master/all/all.csv
- https://www.med.or.jp/english/pdf/2005_07/334_340.pdf
-https://www.sciencedirect.com/science/article/pii/S2212094721000335#:~:text=For%20example%2C%20Hurricane%20Katrina%2C%20which,nearby%20in%20Mississippi%20as%20a
- https://www.britannica.com/event/Sichuan-earthquake-of-2008
- https://education.nationalgeographic.org/resource/tohoku-earthquake-and-tsunami
- https://rmets.onlinelibrary.wiley.com/doi/10.1002/wea.2133
- https://www.nationalgeographic.com/environment/article/hurricane-sandy
- https://www.weather.gov/hgx/hurricaneharvey
- https://edition.cnn.com/specials/hurricane-irma
- https://www.mtu.edu/geo/community/seismology/learn/earthquake-measure/magnitude/
- https://www.sms-tsunami-warning.com/pages/richter-scale
- https://www.usgs.gov/media/images/volcanic-explosivity-index-vei-a-numeric-scale-measures-t
- https://climatedataguide.ucar.edu/climate-data/palmer-drought-severity-index-pdsi
- https://www.nwcg.gov/term/glossary/size-class-of-fire
- https://floodobservatory.colorado.edu/SatelliteGaugingSites/DFOFloodIndexExplanation.pdf
- https://www.worldvision.org/disaster-relief-news-stories/2021-hurricane-ida-facts

### Connect with me
If anything in this project is of interest to you, you're planning to use some of the information or have any questions, please do connect and send a message on Linkedin :) Thanks!

