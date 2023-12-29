# Fundraising-for-Charity-Organization
## NGO Charity Organization Data Analysis

**Interact with Dashboard:**

https://public.tableau.com/app/profile/oladele.oladimeji.samuel/viz/Donationbystate/Dashboard1
https://public.tableau.com/app/profile/oladele.oladimeji.samuel/viz/Donation-Donordata/Dashboard2

### INTRODUCTION
I was given a hypothetical situation as a Data Analyst working for the charity, Education for ALL. I have been asked by the Head of Fundraising to present the data on donor insights and donation rates.

Within the Fundraising team, my objectives are to:

1. Increase the number of donors in our database.
2. Increase the donation frequency of our donors.
3. Increase the value of donations in our database.
In two weeks, my team will be having a fundraising strategy meeting for the following year. I needed to present insights from the donation data to my team and inform my fundraising strategy to increase donations for the following year.

The following data sets were used to answer the business problem;
1. FOR_Donation_Data
2. FOR_Donor_Data.

I applied some SQL commands to analyse data such as; JOIN, ORDER BY, WHERE, BETWEEN, AND, OR, SUM(), COUNT(), AVG(), GROUP BY, HAVING.
Also, I used Root Cause Analysis to better understand the business problem and ask right questions.
As a result, I have found out crucial insights of provided data sets, prepared visualisations, and report for my team.

### ROOT CAUSE ANALYSIS PROCESS

The business problem is that the charity organisation needed to grow their funding for the following year.
Therefore, in a bid to raise more funds we need to pay attention on the following;

1. Increase the number of people donating to the organisation
2. Ways to encourage donors to donate more frequently
3. Get donors to increase the value of their donations.

To understand the problem, I needed to analyse existing data bases of Donors and Donations. Also, I should present crucial numbers and visualisations of our data sets.
I decided to ask some questions to dig the problem deeper:

- How many donors we have in existing database?
- What is the amount of their donations?
- What is the frequency of the donations?
- Who are the top 10 donors?
- Is amount of donations depends on gender, job field, university degree, car?

Also, I realised that I should figure out what is happening, why some people donate regularly and some of them do not. I had to specify main symptoms and trends of the dataset.

Moreover, I applied Root Cause Analysis to ask:

1. Why do we not enough donors as we need?
2. Why can we not see the donors’ average income in our data base?
3. Why in our database we cannot see when people joined our organisation and how long they stay with us?
4. Why we do not add their date of birth to our dataset to research what is the age group of our donors?
5. Why do we not have information about the marital status of donors in our dataset?
6. Why do we not have information of how donors heard about Education for ALL?

### INSIGHTS FROM THE ANALYSIS

- I have been provided with 2 relational databases such as: FO_Donation_Data and EFO_Donor_Data to answer the business problem.
- SQLite Database Management System was used to find out main insights.
- Donation Dataset includes such data: Id, First name, Last Name, Email, Gender, Job field, Donation, State, Shirt Size.
- Donor Dataset includes such data: Id, Donation frequency, University, Car, Second language, Favourite colour, Movie genre.
- Both data sets were imported into SQLite.
- SELECT statement was used to fetch data from a database.
- Tableau was used for Report visualization

Some other aggregate functions were used such as;

- COUNT() To find the total number of donors
- SUM() To find the total sum of donations
- MAX() To find the largest amount of donations
- MIN() To return the smallest value of donations
- Other clauses were used such as the WHERE, JOIN, HAVING, ORDER BY, GROUP BY.
  
**Total number of donors and Total donations**

```SELECT COUNT(*) total_donor, SUM(donation) total_donation FROM Donation_Data```

**Max and Min donations**

```SELECT donation_frequency, MAX(donation) maximum_donation, MIN(donation) minimum_donation, COUNT(donation) total_donor FROM Donation_Data a JOIN Donor_Data2 ON a.id = b.id GROUP BY donation_frequency ORDER BY MAX(donation) desc```

**Total fund raised from each state.** Majority of donors are from California and just one donor from South Dakota, Maine and Wyoming

```SELECT state, count (*) total_donor, SUM(donation) total_donation FROM Donation_Data a join Donor_Data2 b ON a.id = b.id GROUP BY state ORDER BY COUNT (*) desc```

**Using the top 3 states as case study, donors who donanate weekly donate least**

```SELECT state, donation_frequency, COUNT(*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE state in ('California','Texas','Florida') GROUP BY state, donation_frequency ORDER BY state, SUM(donation) desc```

**What frequency genetares over 7000 and from which state?**

```SELECT state, donation_frequency, COUNT(*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id GROUP BY state, donation_frequency HAVING SUM(donation) > 7000 ORDER BY state, SUM(donation) desc```

**Which industry has more donotion? More donor from the business development industry**

```SELECT job_field, COUNT (*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b on a.id = b.id GROUP BY job_field ORDER BY COUNT (*) desc```

**Frequency of donation. We have more donation from donors who donated once**

```SELECT donation_frequency, COUNT (*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id GROUP BY donation_frequency ORDER BY SUM(donation) desc```

**Those that gave once, what kind of job do they do. which top 3industry has more donor?**

```SELECT job_field, COUNT(*) total_donor, SUM(donation) total_donation FROM Donation_Data a join Donor_Data2 b on a.id = b.id WHERE donation_frequency = 'Once' GROUP BY job_field ORDER BY COUNT(*) desc LIMIT 3```

**Those that gave yearly, What kind of job do they do and which top3 industry has more donor?**

```SELECT job_field, COUNT(*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE donation_frequency = 'Yearly' GROUP BY job_field ORDER BY count(*) desc LIMIT 3```

**Total donations from educated and non educated donors**

```SELECT COUNT (*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE university is null```

```SELECT COUNT (*) total_donor, SUM(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE university is not null```

**Educated donors donate more. Top 10 donors with university education**

```SELECT first_name, last_name, university, donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE university is not null ORDER BY donation desc LIMIT 10```

**Top 10 donors without unversity education**

```SELECT first_name, last_name, university, donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE university is null ORDER BY donation desc LIMIT 10```

**How many donor with university education in California donated more than 450?**

```SELECT university, donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE university is not null AND donation > 450 AND state = 'California'```

**How many donor without university education in California donated more than 450?**

```SELECT university, donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE university is null AND state='California' AND donation > 450```

**Donors with cars donate more. top 10 donors without a car**

```SELECT first_name, last_name, car, donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE car is not null ORDER BY donation desc LIMIT 10```

**Top 10 donors without a car**

```SELECT first_name, last_name, car, donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE car is null ORDER BY donation desc LIMIT 10```

**Majority of the donors could afford a car**

```SELECT COUNT (*) total_donor, sum(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE car is not null```

```SELECT COUNT (*) total_donor, sum(donation) total_donation FROM Donation_Data a JOIN Donor_Data2 b ON a.id = b.id WHERE car is null```

### TABLEAU VISUALIZATION

We receive majority of donations with frequency Yearly and Once.

![image](https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/830cb2b3-6915-43e5-b272-61c73ff20bb8)

More funds come from donors who live in California, Texas and Florida.

![image](https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/df975fcd-8046-405f-9af1-70525df45156)

Map showing donors who live in California, Texas and Florida and other states with high donations.

![image](https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/81972ee3-98a3-411c-b488-40f77a3eae37)

Majority of donations come from donors who have university education

![image](https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/268b171f-8a0d-4111-88fc-54425e0f0d5c)

Majority of donations come from donors who are car owners

![image](https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/6e254431-c776-46ba-87c2-5f32f355fa67)

#### FINDINGS AND RECOMMENDATIONS

As a result of data set analysis, I have found out:
- The total number of donors we have in the database is 1000
- The sum of donations we collected is $249085
- The largest amount of donations $500
- The smallest amount of donation is $5
  

**Top 10 donors with a university education**

<img width="761" alt="image" src="https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/bf36bba3-062d-473e-92ce-98078f3cf56c">

**We have more donation from donors who donated once**

<img width="768" alt="image" src="https://github.com/mrdimejisam/Fundraising-for-Charity-Organization/assets/111657348/440e958f-d2a8-4d17-b26f-c4df51dc6b0e">


### CONCLUSION

I have analysed 2 data sets FO_Donation_Data and EFO_Donor_Data to help Education for ALL to understand business problem of involving new donors more deeply and find a way to raise more donations with regular frequency.

Therefore, our donors include different types of people with varying identities. They live in different states, work in absolutely unsimilar job fields, some of them have university education and some of them no.

However, there are some crucial points that we need to count and try to use for increasing charity activeness of our donors and their donations.
I have found out that frequency of Yearly and Once donations is much higher than Monthy. Weekly frequency is very low. So, we need to work on improvement of donation frequency, especially Weekly donations. Also, we have some people in our base who do not donate at all, so maybe we should contact them and try to realise why they are not active donors. I also found out that the occupation of our donors have no influence on the amount of donation. Job field is not crucial thing.

Also, we need to attract more donors from other states, since now majority of them are from Florida, California and Texas.
Majority of donations come from donors who are car owners. 939 donors own a car while 61 donors do not have a car. Another very significant point is that top 10 donors, who donate between $493 and $500 have university education. Thus, we can notice that people, who are educated themselves are happy to support others to get education. Some people with no university education also provide big amounts, but few of them.

In conclusion, we must concentrate to improve our databases, add more useful information about our donors. There is lack of valuable data. Genre, Movies are not useful to solve our business problems. We must find useful channels for promoting our charity organisation.
Since we have good support among educated people, we could organize seminars in universities or set up awareness schemes to sensitize students about us
