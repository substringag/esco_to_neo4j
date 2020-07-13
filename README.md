ESCO on neo4j
===

This docker-compose and the neo4j Scripts help you to get the ESCO - European Skills / Competences, qualifications and Occupations database up and running in a short time.


Getting started
====
1. Run the container
`docker-compose up`

2. Open your browser and open the admin interface http://localhost:7474/

3. Enter no user or password and press enter

4. Go to https://ec.europa.eu/esco/portal/download/ and filter for the newest version, language english, type csv and download everything. Also all the Pillars as CSV.

5. Extract the CSV to the import folder.

6. Enter and run the following the commands in import_esco_en.cql

7. Play around with the example queries here: 

  // Get all occupations with the word "software developer" in it.
  match (o:Occupation)
  where o.preferredLabel contains "software developer"
  return o;

  // Get all occupations with the word "data scientist" in it.
  match (o:Occupation)
  where o.preferredLabel contains "data scientist"
  return o

  // Get all occupations with the word "data scientist" and "software developer".
  match (o1:Occupation), (o2:Occupation)
  where o1.preferredLabel contains "software developer"
  and o2.preferredLabel contains "data scientist"
  return o1, o2;

  // Get all essential skills for occupations with "software developer" in the label
  MATCH (s:Skill)-[:ESSENTIAL_FOR]->(o:Occupation)
  WHERE o.preferredLabel contains "software developer"
  return s, o

Sources
====
* ESCO - European Skills / Competences, qualifications and Occupations database: https://ec.europa.eu/esco/portal
* We used this file and updated it so it works with the newest version of neo4j and fixed some things: https://gist.github.com/rvanbruggen/08535b058736e538997d5b2dd7adcf89