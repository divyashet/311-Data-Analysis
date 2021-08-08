

311 Service Request Data Analysis

Background

The 311 system is used by New York city residents to report complaints related to non-

emergency problems for e.g., Noise -Residential, Hot water, Illegal Parking etc. The NYC data

for 311 service requests data was made available to the public on 10/18/2011 and ever since

has been updated daily.

The data set used for the data analysis is available at [https://github.com/USA4UNHCR/data-eng-](https://github.com/USA4UNHCR/data-eng-test)

[test](https://github.com/USA4UNHCR/data-eng-test)[ ](https://github.com/USA4UNHCR/data-eng-test)a git repository which is an archive of 311 complaints for NYC from 2010 to present. The

data contains 21914707 rows and 41 columns. The size of the data is around 10 GB.

Part 1: Data Analysis

From the 311 Service Request data analysis we could see that ‘Noise – Residential’ complaint

had the highest number of complaints i.e. around 1795446.

The chart below represents the ‘Top 5 Zip Codes ‘ when it comes to number of complaints

received. The highest complaint received is for the zip code 11226.





Q1: The number of complaints per department

\1. 10011 zip code

10011 zip code belongs to borough ‘Manhattan’. Agency NYPD received the highest number

of complaints in Manhattan i.e., 26,951.

\2. 11217 zip code

11217 zip code belongs to borough ‘Brooklyn’. Here again the NYPD has received the

highest number of complaints in Brooklyn i.e., 35,768 which is higher than Manhattan.

Q2: Which other zip code it is most and least similar to.

The pie chart below shows that Brooklyn has been adversely affected by 29.5% followed

by Queens with 22.5%, another borough that has been immensely affected. While

Manhattan and Bronx have a similar percentage 19.5 %, 18.5% respectively. The least

impacted area among the boroughs is the Staten Island which is around 4.8%.





Part 2: Data Engineering

Assumption

The challenging part with this large data set was to read the csv file and it was time consuming

using the pandas library.

One of the approaches would be to create a random data set and using it for the analysis. The

random data set would behave as a subset of the entire population. For my analysis, I have

used the dask library. The entire csv file was read in 0.038 seconds which helped in computing

and analysis of the data.

Engaging the stakeholders

It is important to engage the stakeholders during the early stages of analysis. This helps in

defining the problem, scoping the efforts, and architecting the system. It is also important to

work closely with the stakeholders to get a periodic review of the system which will ensure

that it is meeting their expectations and their feedback can be addressed sooner rather than

later.

My personal preference is using Agile methodology with which the development team can

work in close associations with all the stakeholders. This includes discussing the

requirements, understanding the data, identifying the end-users and their expectation, and

the timelines for the solution delivery.





System Architecture

The system is designed in a modular format that way the changes in one component would

have minimal impact on other components in the system. The architecture comprises of the

following components:

**Cloud Storage**: This component provides the raw data which the system processes to get the

expected result. Although represented as a single component for simplicity, it could be

multiple sources from which the system can get its raw data.

**Automation Tool**: This component would be the brain behind this system. The

language choice would be Python using Jupyter Notebooks because of its powerful data

analytics features, huge collection of helpful libraries like pandas, numpy, dask, etc., and great

developer community. This component is responsible for:

• Aggregating data from multiple data sources (if applicable)

• Filtering data to ensure only clean and relevant data attributes are processed

• Mapping data to transform them into meaningful information that can be used in the

analysis

• Storing the processed data in the data storage component for persistence

• Handling any errors and exceptions while processing

**Data Storage**: This component is responsible for storing a snapshot of the data processed by

the Automation Tool component. This data can be used in historical data analytics. It is





generally cost-effective to store a high volume of data than to process a high volume of data.

Depending on the schema and volume requirements of the system, a big data source such as

Hadoop, No SQL DB such as MongoDB, or a SQL DB such as SQL Server could be used in the

data storage component

**Data Visualization:** This component is responsible for the user interface of the system. This

will be the component that the users will interact with to extract the information they are

looking for in the system. Hence, this component will be user-friendly, intuitive, and feature-

rich to provide easy-to-consume information. The choice for this component is Tableau,

Looker for Big data which has powerful integration features with various data storage

components. Its capabilities also include the creation of dashboards to showcase connected

pieces of information.

User Interface

As indicated in the data visualization component of the system architecture user interface

plays a key role in displaying the required information to the users. The best choice for this

use case would be to use Tableau to integrate with the data storage component and display

the results to the end-user. Tableau has dashboarding capabilities and supports data

visualization using charts. The users can easily filter data based on their preferences and

multiple pieces of key information can be added on the dashboard.

Monitoring, testing, and maintenance





The diagram shows a sequence of events that are encountered in the development, testing

and maintenance stages.

Observability is one of the key aspects of any software solution that deals with important

information. The automation tool will have alerting in place to ensure that any exceptions

caused during the data processing, gets reported. The alert could be as simple as sending out

an email to the required group of individuals.

To ensure the accuracy of the information that is processed by the automation tool it is

important to include automated tests. Unit testing is a best approach to ensure each unit that

contributes to the data processing is tested with a small amount of mock data and check for

accuracy of the results with the expected data attributes. Integration tests can also be added

for and testing of the system, but this may not be required depending on the use case of the

system.

Maintenance is another key component for any system. Since the system architecture is

modularized, it would be easier to maintain each component independent of the other. There

is a possibility of minimal impact on other components for any major changes that are carried

out in one of the modules. Any cool changes, configuration changes etc. should be maintained

in a version control system like git that way historical changes can be referenced when

needed. There should be enough documentation about the key components used in the

system to ensure that knowledge is captured and shared with a broader group for e.g. the

stakeholders.

Any security issues

Any systems that deal with huge volume of data, should account for the security requirements

for it. If the data source has sensitive data attributes like PII, financial records, health records

etc. special attention needs to be given for the security of such data elements. The storage

component should have encryption capabilities to ensure that the data is securely stored. And

if the end-user audience is not intended to view sensitive data attributes, they need to be

masked with appropriate rules depending on the system requirements.

On the dashboard level we can implement row level security. This helps in ensuring that the

certain rows of data are restricted to certain users/ population. Also, on the tableau server

we can maintain Groups to restrict the access of dashboards to certain users.

