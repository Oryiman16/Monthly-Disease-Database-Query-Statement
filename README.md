

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
