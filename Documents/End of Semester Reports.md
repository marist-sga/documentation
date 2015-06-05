# End of Semester Reports

At the end of the semester, Student Activities will ask for all of the event evalutations for clubs and for offier login statistics. Run these queries in phpMyAdmin and export as CSV (_not_ MS Excel) delimited by a comma (`,`) and with headers.


## Event Evaluation Data

```sql
SELECT clubs.name AS ClubName, eventEvaluations. *
FROM eventEvaluations
JOIN  `events` ON eventEvaluations.eventID = events.id
JOIN clubs ON events.clubID = clubs.clubID
ORDER BY clubs.name;
```

## Officer Login Statistics

```sql
SELECT officers.clubID,
clubs.name,
100 * SUM(CASE WHEN officers.lastLogin IS NULL THEN 1 ELSE 0 END ) / COUNT( officers.cwid ) AS pctOfficersNeverLoggedIn,
SUM(CASE WHEN officers.lastLogin IS NULL THEN 1 ELSE 0 END ) AS numNeverLoggedIn, COUNT( officers.cwid ) AS countOfficers
FROM officers
JOIN clubs ON officers.clubID = clubs.clubID
GROUP BY officers.clubID;
```
