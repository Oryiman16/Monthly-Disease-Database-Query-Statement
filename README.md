

CREATE DATABASE IF NOT EXISTS MonthlyDiseaseRecords;

USE MonthlyDiseaseRecords;


CREATE TABLE DiseaseTable(
`Code` INT,
Disease VARCHAR (150),
`Source of infection` VARCHAR (150),
`Outbreak status` VARCHAR (150)
);

LOAD DATA INFILE 'DiseaseTable.csv' INTO TABLE DiseaseTable
FIELDS TERMINATED BY ','
IGNORE 1 LINES;


CREATE TABLE AnimalsAffected(
parent INT,
Species VARCHAR (150),
`Age Group`VARCHAR (100),
Sex VARCHAR (15),
`Number susceptible` INT,
`Number of cases` INT,
`Number of death` INT
);

LOAD DATA INFILE 'AnimalsAffected.csv' INTO TABLE AnimalsAffected
FIELDS TERMINATED BY ','
IGNORE 1 LINES;

CREATE TABLE BasesForDiagnosis(
parent INT,
`Basis of diagnosis` VARCHAR (150)
);

LOAD DATA INFILE 'BasesForDiagnosis.csv' INTO TABLE BasesForDiagnosis
FIELDS TERMINATED BY ','
IGNORE 1 LINES;


CREATE TABLE DiseaseControlMeasure(
parent INT,
`Disease control measure` VARCHAR (150)
);

LOAD DATA INFILE 'DiseaseControlMeasure.csv' INTO TABLE DiseaseControlMeasure
FIELDS TERMINATED BY ','
IGNORE 1 LINES;


CREATE TABLE Location(
parent INT,
Outlet VARCHAR (150)
);

LOAD DATA INFILE 'Location.csv' INTO TABLE Location
FIELDS TERMINATED BY ','
IGNORE 1 LINES;


--Some of the join querries used to query the tables
show databases

use monthlydiseaserecords

show tables
select * from diseasetable

select species, count(species)
from animalsaffected
group by species

 
select species, `number susceptible`, (`number of death`/ `number of cases`)*100 DeathPercentage
from animalsaffected
order by 1,2


select disease, species, `number susceptible`, (`number of death`/ `number of cases`)*100 DeathPercentage
from animalsaffected
inner join diseasetable
on animalsaffected.parent = diseasetable.`code`
 
select outlet, disease, species, `number susceptible`
from animalsaffected
inner join diseasetable
on animalsaffected.parent = diseasetable.`code`
inner join location
on location.parent= diseasetable.`code`

--4 Table Join

select outlet, disease, species, `basis of diagnosis`
from animalsaffected
inner join diseasetable
on animalsaffected.parent = diseasetable.`code`
inner join location
on location.parent= diseasetable.`code`
inner join basesfordiagnosis
on basesfordiagnosis.parent = location.parent

--5 Table Join

select outlet, disease, species, `basis of diagnosis`, `disease control measure`
from animalsaffected
inner join diseasetable
on animalsaffected.parent = diseasetable.`code`
inner join location
on location.parent= diseasetable.`code`
inner join basesfordiagnosis
on basesfordiagnosis.parent = location.parent
inner join diseasecontrolmeasure
on basesfordiagnosis.parent = diseasecontrolmeasure.parent

-- Outlet with Highest Death 

Select outlet, MAX(`number of death`) as TotalDeathCount
From animalsaffected
inner join location
on location.parent = animalsaffected.parent
Group by outlet
order by TotalDeathCount desc

