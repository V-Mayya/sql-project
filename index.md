## Natural Disasters 
CFG Project

Given the recent wildfires in Australia, heat wave in Europe and other natural disasters over the years, my project will be exploring the impact and methods that nations have used to deal with the aftermath of such disasters. It will specifically focus on types of key natural disasters during the years of 2000-2022 (along with their magnitudes), events, number of fatalities, the recovery period, economic impact, support after the disaster and others.

The idea to create a project based around natural disasters was developed after reading the book 'Extreme Economies'. One of the incidents described in the book was about how Aceh (a province of Indonesia) managed to resume its daily operations almost immediately after disaster struck. The economic resilience and methods the region used to dampen the impact of the natural disaster inspired me to create this project. 

### Implications

The creation of this project is intended to: 
- understand the impact of climate change and natural disasters on individuals and wildlife
- learn about which methods were best to recover from the aftermath of a disaster 
- learn more about the economic resilience and unity of a nation during moments of crisis

### Setting up tables and columns

**COUNTRIES**: country_unique_ID, countries where disaster struck

**NATURAL DISASTER TYPES**: natural_disaster_unique_ID, natural disaster classification (earthquake, tsunami, wildfires, cyclones, etc.) 

**EVENTS**: dates of natural disasters, country_unique_ID,  natural_disaster_unique_ID, magnitude of each event

**FATALITIES**: number of fatalities, species impacted, dates of disaster, country_unique_ID 

**OTHER IMPACTS**: number of displaced individuals/injuries, dates of disaster, country_unique_ID 

**RECOVERY**: dates of disaster, country_unique_ID, number of days for complete recovery, method country used to deal with aftermath of disaster

**ECONOMIC IMPACT**: 
1. Table 1: economic damage in terms of total monetary impact/revenue lost by businesses, country_unique_ID, dates of natural disasters

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
  country VARCHAR(35), 
  CONSTRAINT
  PK_country_unique_ID
  PRIMARY KEY
  (country_unique_ID)); 
  
INSERT INTO countries (country_unique_ID, country) Values (1, 'Afghanistan'),(2,'Albania'),"DZ|Algeria","AS|American Samoa","AD|Andorra","AO|Angola","AI|Anguilla","AQ|Antarctica","AG|Antigua And Barbuda","AR|Argentina","AM|Armenia","AW|Aruba","AU|Australia","AT|Austria","AZ|Azerbaijan","BS|Bahamas","BH|Bahrain","BD|Bangladesh","BB|Barbados","BY|Belarus","BE|Belgium","BZ|Belize","BJ|Benin","BM|Bermuda","BT|Bhutan","BO|Bolivia","BA|Bosnia And Herzegovina","BW|Botswana","BV|Bouvet Island","BR|Brazil","IO|British Indian Ocean Territory","BN|Brunei Darussalam","BG|Bulgaria","BF|Burkina Faso","BI|Burundi","KH|Cambodia","CM|Cameroon","CA|Canada","CV|Cape Verde","KY|Cayman Islands","CF|Central African Republic","TD|Chad","CL|Chile","CN|China","CX|Christmas Island","CC|Cocos (keeling) Islands","CO|Colombia","KM|Comoros","CG|Congo","CD|Congo, The Democratic Republic Of The","CK|Cook Islands","CR|Costa Rica","CI|Cote D'ivoire","HR|Croatia","CU|Cuba","CY|Cyprus","CZ|Czech Republic","DK|Denmark","DJ|Djibouti","DM|Dominica","DO|Dominican Republic","TP|East Timor","EC|Ecuador","EG|Egypt","SV|El Salvador","GQ|Equatorial Guinea","ER|Eritrea","EE|Estonia","ET|Ethiopia","FK|Falkland Islands (malvinas)","FO|Faroe Islands","FJ|Fiji","FI|Finland","FR|France","GF|French Guiana","PF|French Polynesia","TF|French Southern Territories","GA|Gabon","GM|Gambia","GE|Georgia","DE|Germany","GH|Ghana","GI|Gibraltar","GR|Greece","GL|Greenland","GD|Grenada","GP|Guadeloupe","GU|Guam","GT|Guatemala","GN|Guinea","GW|Guinea-bissau","GY|Guyana","HT|Haiti","HM|Heard Island And Mcdonald Islands","VA|Holy See (vatican City State)","HN|Honduras","HK|Hong Kong","HU|Hungary","IS|Iceland","IN|India","ID|Indonesia","IR|Iran, Islamic Republic Of","IQ|Iraq","IE|Ireland","IL|Israel","IT|Italy","JM|Jamaica","JP|Japan","JO|Jordan","KZ|Kazakstan","KE|Kenya","KI|Kiribati","KP|Korea, Democratic People's Republic Of","KR|Korea, Republic Of","KV|Kosovo","KW|Kuwait","KG|Kyrgyzstan","LA|Lao People's Democratic Republic","LV|Latvia","LB|Lebanon","LS|Lesotho","LR|Liberia","LY|Libyan Arab Jamahiriya","LI|Liechtenstein","LT|Lithuania","LU|Luxembourg","MO|Macau","MK|Macedonia, The Former Yugoslav Republic Of","MG|Madagascar","MW|Malawi","MY|Malaysia","MV|Maldives","ML|Mali","MT|Malta","MH|Marshall Islands","MQ|Martinique","MR|Mauritania","MU|Mauritius","YT|Mayotte","MX|Mexico","FM|Micronesia, Federated States Of","MD|Moldova, Republic Of","MC|Monaco","MN|Mongolia","MS|Montserrat","ME|Montenegro","MA|Morocco","MZ|Mozambique","MM|Myanmar","NA|Namibia","NR|Nauru","NP|Nepal","NL|Netherlands","AN|Netherlands Antilles","NC|New Caledonia","NZ|New Zealand","NI|Nicaragua","NE|Niger","NG|Nigeria","NU|Niue","NF|Norfolk Island","MP|Northern Mariana Islands","NO|Norway","OM|Oman","PK|Pakistan","PW|Palau","PS|Palestinian Territory, Occupied","PA|Panama","PG|Papua New Guinea","PY|Paraguay","PE|Peru","PH|Philippines","PN|Pitcairn","PL|Poland","PT|Portugal","PR|Puerto Rico","QA|Qatar","RE|Reunion","RO|Romania","RU|Russian Federation","RW|Rwanda","SH|Saint Helena","KN|Saint Kitts And Nevis","LC|Saint Lucia","PM|Saint Pierre And Miquelon","VC|Saint Vincent And The Grenadines","WS|Samoa","SM|San Marino","ST|Sao Tome And Principe","SA|Saudi Arabia","SN|Senegal","RS|Serbia","SC|Seychelles","SL|Sierra Leone","SG|Singapore","SK|Slovakia","SI|Slovenia","SB|Solomon Islands","SO|Somalia","ZA|South Africa","GS|South Georgia And The South Sandwich Islands","ES|Spain","LK|Sri Lanka","SD|Sudan","SR|Suriname","SJ|Svalbard And Jan Mayen","SZ|Swaziland","SE|Sweden","CH|Switzerland","SY|Syrian Arab Republic","TW|Taiwan, Province Of China","TJ|Tajikistan","TZ|Tanzania, United Republic Of","TH|Thailand","TG|Togo","TK|Tokelau","TO|Tonga","TT|Trinidad And Tobago","TN|Tunisia","TR|Turkey","TM|Turkmenistan","TC|Turks And Caicos Islands","TV|Tuvalu","UG|Uganda","UA|Ukraine","AE|United Arab Emirates","GB|United Kingdom","US|United States","UM|United States Minor Outlying Islands","UY|Uruguay","UZ|Uzbekistan","VU|Vanuatu","VE|Venezuela","VN|Viet Nam","VG|Virgin Islands, British","VI|Virgin Islands, U.s.","WF|Wallis And Futuna","EH|Western Sahara","YE|Yemen","ZM|Zambia","ZW|Zimbabwe

  
```
The next table lists the types of natural disasters along with a unique ID as well. 

```
-- Table 2
CREATE TABLE types (
  natural_disaster_ID INT,
  type VARCHAR(40), 
  CONSTRAINT
  PK_natural_disaster_ID
  PRIMARY KEY
  (natural_disaster_ID)); 
  
INSERT INTO types (natural_disaster_ID, type) Values (1, 'Drought'), (2, 'Earthquake'), (3, 'Extreme Temperature'), (4, 'Flood'), (5, 'Landslide'), (6, 'Mass Movement'), (7, 'Storm/Cyclones'), (8, 'Volcanic activity'), (9, 'Wildfire'), (10, 'Tsunami'); 

```

Table 3 (events): 

```
CREATE TABLE events (
  date DATE,
  natural_disaster_ID INT,
  country_unique_ID INT,
  magnitude DEC(10,2)
  CONSTRAINT
  FK_naturaldisasterandcountry_ID
  FOREIGN KEY
  (natural_disaster_ID, country_unique_ID)); 
```

Table 4 (fatalities):

```
CREATE TABLE events (
  number_of_fatalities INT,
  species_impacted VARCHAR(55),
  country_unique_ID INT,
  date DATE
  CONSTRAINT
  FK_countryanddate_ID
  FOREIGN KEY
  (country_unique_ID, date)); 
```

Table 5 (other impacts): 

```
CREATE TABLE other_impacts (
  date DATE,
  country_unique_ID INT,
  displaced_or_injured INT
  CONSTRAINT
  FK_countryanddate_ID
  FOREIGN KEY
  (country_unique_ID, date)); 
```

Table 6 (recovery):

```
CREATE TABLE recovery (
  date DATE,
  country_unique_ID INT,
  days_to_recover INT,
  method_to_deal_with_disaster VARCHAR(100) 
  CONSTRAINT
  FK_countryanddate_ID
  FOREIGN KEY
  (country_unique_ID, date)); 
```

Tables 7 and 8 (economic impact):

```
CREATE TABLE economic_impact_1 (
  total_monetary_impact INT,
  date DATE,
  country_unique_ID INT
  CONSTRAINT
  FK_countryanddate_ID
  FOREIGN KEY
  (country_unique_ID, date)); 
  
 CREATE TABLE economic_impact_2 (
  %_of_global_GDP INT,
  country_unique_ID INT,
  date DATE
  CONSTRAINT
  FK_countryanddate_ID
  FOREIGN KEY
  (country_unique_ID, date)); 

```

Table 9 (support):

```
CREATE TABLE economic_impact_2 (
  organisations VARCHAR(150),
  amount VARCHAR(100),
  country_unique_ID INT 
  CONSTRAINT
  FK_country_ID
  FOREIGN KEY
  (country_unique_ID)); 
```
### Queries for Data Analysis

1. Total economic impact to a particular country (Japan chosen as an example) over the years of 2000-2022 demonstrated through the query shown as follows 

```
SELECT SUM(total_monetary_impact), country_unique_ID FROM economic_impact_1 WHERE country_unique_ID = .. GROUP BY country_unique_ID ORDER BY total_monetary_impact DESC; 
```

Implications and analysis: Based on the locations of countries that have faced the greatest economic impact in terms of monetary damage over the years of 2000-2022, economic resilience of the country can be analysed by comparing economic indicators of the country (in terms of GDP and other indices) to other countries along with the data that results from the query. 

If a country has been able to sustain its economy well despite large monetary damages due to natural disasters, other countries can try utilising methods the country has used to cope with the aftermath of the disaster. 

In the case of Japan, total economic damage of major natural disasters during the period was around .... Japan's economy as of 2022 is ...
Learning more about Japan's economic resilience can help other countries build plans and policies to deal with such issues. 

2. Country with the maximum and minimum number of fatalities during 2000-2022 demonstrated through 2 subqueries shown as follows

```
-- Maximum number of fatalities
SELECT country AS 'country with max. fatalities' FROM countries WHERE country_unique_ID IN (SELECT MAX(number_of_fatalities) FROM events); 

--Minimum number of fatalities
SELECT country AS 'country with min. fatalities' FROM countries WHERE country_unique_ID IN (SELECT MIN(number_of_fatalities) FROM events);  

```

Implications and analysis: 



4. Number of species of wildlife impacted in countries that have had moderate to severe earthquakes 

```
SELECT country, COUNT(species_impacted) AS 'No. of species impacted' FROM events WHERE country_unique_ID IN (SELECT country_unique_ID WHERE magnitude >= 6) GROUP BY country HAVING COUNT(species_impacted) > 3; 
-- (or no need after group by)
``` 

Implications and analysis: According to the earthquake magnitude scale, magnitudes greater than 6 can cause severe destruction. The subquery will allow the user to find the countries and their respective number of species impacted (in terms of types such as birds, fish - 2) for all situations where number of species impacted were greater than 3. 

This can then be compared with total number of earthquakes of magnitude greater than 6 for each country (Japan in this example) using the following query.

``` 
SELECT COUNT(country_unique_ID) WHERE magnitude >= 6 AND country_unique_ID = .. ; 

``` 

A percentage can be established that will demonstrate the % that more than 3 different species of wildlife were impacted during moderate to severe earthquakes. This will demonstrate the true impact of one type of natural disaster on wildlife. In Japan, this amounts to around: 

Note that the figures are based on only major natural disasters that have taken place and might not account for all types of wildlife species impacted. 

### Further Questions/Extensions and Limitations 

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

### Connect with me
If anything in this project is of interest to you, you're planning to use some of the information or have any questions, please do connect and send a message on Linkedin :) Thanks!
