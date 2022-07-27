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

Creating the database to use:

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
  date DATE,
  CONSTRAINT
  FK_countryanddate_ID
  FOREIGN KEY
  (country_unique_ID, date)); 
```
