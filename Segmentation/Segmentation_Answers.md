# Question 1

```sql
SELECT *
FROM data
WHERE NOT(Joined in last 6 months)
and opened in the last 6 months
and donor = yes
UNION ALL
SELECT *
FROM data
WHERE joined in last 6 months
AND donor = yes
```

# Question 2
All segments concern only ALS Full List customers and exclude customers who didn't open an email 90 days prior to 11/01/2018. We assume that Donor and Ad status are binary.
In this case, we can note each of the events as:
* ALS - Full List: *FL*
* Active Status: *AC*
* ALS - Ad Names: *AD*
* Donor = yes: *DN*

Following these notations:
* Segment 1: ```FL AND AC AND AD AND DN```
* Segment 2: ```FL AND AC AND AD AND NOT(DN)```
* Segment 3: ```FL AND AC AND NOT(AD) AND DN```
* Segment 4: ```FL AND AC AND NOT(DN)```

Hence, we can see that these segments are not exclusive and Segment 2 and 4 have some overlapping. We can solve that by defining Segment 4 as ```FL AND AC AND NOT(AD) AND NOT(DN)```


# Question 3
In each of the following days, we have:
* *Violated - Day1* Version I will be sent to Group A and Group B. Since there are members of group C in group B, some general public members would receive the same version of email as the VIPs and board members. Hence, a constraint is violated
* *Unviolated - Day2* Version I will be sent to Group A and Group C, excluding members of those groups that are in group B to respect constraint general public constraint. Version II will be sent to Group B members that are not in Group A and Group C to avoid having a constituent receiving more than one version of an email. Hence, all constraints are respected
* *Violated - Day3* Version I will be sent to group A and B and version II to group C. Since some constituents are in three groups, they would receive more than one version of an e-mail. Another constrain is violated
