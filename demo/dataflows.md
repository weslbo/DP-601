# Dataflows demo

Imagine you work in a company that wants to expand a new market in Europe. You're doing research and you want to know where are the majority of children born. Or, you company sells products targetted to senior people and you want to know where in Europe you have the largest population of senior people. 

Well, there is this database for Europe statistics called eurostat, which has an API that we can connect to from within DataFlows. Let's go into a demo.

## Explore the Eurostat Databases:

- Navigate to https://ec.europa.eu/eurostat/data/database
- Explore the data explorer and expand Detailed datasets
- > Population and social conditions
    - > Population projects
        - > EUROPOP2023
            - > Population on 1st January by age, sex and type of projection (proj_23np)
- You can download the zip file but this would not allow us to refresh the data
- Let's explore the data (https://ec.europa.eu/eurostat/databrowser/product/view/PROJ_23NP)
- Let's explore how we can use web based REST APIs to retrieve the data. Here's the documentation: https://wikis.ec.europa.eu/display/EUROSTATHELP/API+Statistics+-+data+query
- Click on Download Data on this page only > TSV (1 time-series = 1 row), No compression
- The link will look like this: https://ec.europa.eu/eurostat/api/dissemination/sdmx/2.1/data/PROJ_23NP$DEFAULTVIEW/?format=TSV. Download the file

## Create a Dataflow gen2 in Microsoft Fabric

- Get data > View more > Text/CSV
- Upload file: estat_proj_23np$defaultview_filtered.tsv
- Next
- Delimiter: Tab
- Do **not** detect data types
- Split Column1 using the comma
- Use first row as header
- Rename geo\TIME_PERIOD to geo
- Filter (exclude) EA20 and EU27_2020 (these represent the Euro area with 20 countries and European Union - 27 countries)

- Enable column profile + enable details pane
- Remove T from sex (total)
- Remove columns: freq, age, unit
- Replace value F with Female and Male in the sex column
- Enter new data (manually by copying pasting below)

BSL: Baseline projects

LFRT: Sensitivity test - lower fertility

LMRT: Sensitivity test - lower mortality

HMIGR: Sensitivity test - higher migration

LMIGR: Sensitivity test - lower migration

NMIGR: Sensitivity test - no migration


- Split column by COLON
- Rename fields to Code and Type of projection (hint: do this directly in the M-formula)
- Rename query to Projections
- Rename estat_xxx query to Population
- Merge query with inner join
- Expand field: Type of projection
- Re-order the new field and put it at the beginnig of the table
- Remove the "projection" field as it is no longer necessary.

- Select all the year fields (2022->2100)
- Unpivot columns
- Rename "Attribute" to "Year"
- Rename "Value" to "Population"
- Pivot column "Type of projection". Use "Population" as the Value column

- Get new data (enter manually), by copy pasting from https://www.iban.com/country-codes
- Remove last 2 columns
- Merge with inner query
- Expand Column and rename to Country

- Add destination to lakehouse. Table name population
- Rename dataflow and publish

- Validate the results in the lakehouse