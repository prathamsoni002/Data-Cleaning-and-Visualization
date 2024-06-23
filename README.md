# Data-Cleaning-and-Visualization
*This is no code repository. It is a repo for displaying the output of the Project*


**Project Aim:** 

To extract data available in CSV format from the official UK government website that lists all registered companies till 2023-2024 that provide various types of employability visas, and filter out the tech-based companies providing 'Skilled Worker Visas'.

**Data Format:** 

CSV file with more than 130k records that includes the Organization Name, Town/City, County, Type of Visa, Route.

**Problems:** 

1. Organization names were not properly formatted. Issues included commas (,), extra spaces, non-alphanumeric characters (e.g., *, -, /), and entries with both original and newly registered company names in the same record. These issues likely arose from various forms filled during registration, leading to many typos.
2. Similar typos in Town/City columns.
3. Does not Specify the industry of the Orginazations, thus it was impossible to find out wich company can porvide Tech based jobs or not.
4. Simple list of companies, no feature of segration of the companies. 

**Solution and Approaches** 

1. Using Pandas to clean the data, solve all the typos using Regualr Expressions.
2. To find out which company is Tech based and which is not, (for more than 80K records which provides Skilled worker visa) manual searching was not possible.
   Thus, I had to find another option.
   On the UK government website, there's an option to search for registered company details using the company name (https://find-and-update.company-information.service.gov.uk/). The search results show that every registered company has one or more SIC codes (UK Standard Industrial Classification), which classify companies based on their activities.
   
   The full list of SIC codes and their descriptions can be found at: https://classification.codes/classifications/industry/uk-sic/.
   
    But this was not the final solution. Manual searching for 80K records was not possible. But luckly, UK govt supports API for providing the company based data.
    Thus, by creating API request call we can get the corresponding SIC codes.

    Various Options were considered to for this process, including
  _*Apache Airflow*, *Apache Nifi*_ etc, to create a stable data pipline that creates batched of data and process them.

   But, Using basic _*Python request library*_ the process has been done, because of the simplicity and one time nature of the requirement.

   Manual filtering out the SIC codes that matches the tech - releated industry and then every SIC fetched for all the records havebeen cross checked. When the SIC if matches, a the Orginazation is termed to a Tech based company.

#DataCleaning:
Google Colab link: https://colab.research.google.com/drive/1BOs-9jeP69sgAUeq4s4jqDsLAHa6DpWO?usp=sharing


**Visualization**

#DataVisualization:
Google colab link: https://colab.research.google.com/drive/1ovvQpo3Kk1ugsKsSwRq5qaBp6Ux_Jddj?usp=sharing

*Using Kibana and Elasticsearch*
  Pie chart representation of companies present in Various UK Cities
   ![image](https://github.com/prathamsoni002/Data-Cleaning-and-Visualization/assets/114599961/313fc9ef-54a3-46c3-a5ca-c30ec592dcc1)


*Using Python to list out the companies based on the selected Town/City and the TechProbab score(calculated based on the closeness of selected SIC codes to be a Tech Relevant)*

![image](https://github.com/prathamsoni002/Data-Cleaning-and-Visualization/assets/114599961/0e6c37cf-37e5-4aa5-8a68-00b3669de7c1)


*Future Scope*:

Fetch the company address or use the Town/City to generate latitude and longitude for visualization using geo maps in Kibana.
 
