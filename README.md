# LouisevilleJeffersonCountyLandbank-PowerBI-Dashboard
Project that demonstrates all the steps taken to transform raw data into insightful information that empowers data driven decision making. Power BI was the main tool leveraged. Dataset period: Jan/1/2015 to Oct/13/2020.

## Objective
Personal interest in the Real State Industry. Curious about what kind of insights lay behind a US-County Landbank. (What is a County Landbank to begin with?)

## Dataset Description
The __Louisville & Jefferson County Landbank Authority, Inc__ also known as simply __Landbank Authority__ is a non-profit, interlocal entity created in 1988 through Kentucky state statute. It was formed as a partnership between the three major taxing bodies in Jefferson County (Lousville Metro Government, the Commonwealth of Kentucky, and the Jefferson County Public Schools) to address the persistent issue of abandoned, tax-delinquent, and blighted properties in the region.

__Their goal is to tackle urban blight, simplify property titles, and foster neighborhood revitalization__.

__Data Source:__
This project uses open data provided by the Louisville/Jefferson County Information Consortium (LOJIC) through the Louisville Metro Open Data Portal. The data is publicly available and licensed for use subject to the portal’s terms and conditions. LOJIC and its partner agencies provide the data “as is” without warranty regarding accuracy, completeness, or fitness for a particular purpose.

__Attribution__: Mapping Data Source: LOJIC.

## Tools & Technologies
  - __MS Power Point__: Dashboard design and wireframing.
  -  __Power BI__: data cleaning (Power Query M),and visualisation.
    
## Methodology

### 1. Exploratory Data Analysis
  Due to lack of expertise in this industry, I simulated a _Subject Matter Expert (SME)_ throught ChatGPT to which I called: Olivia White, Project Manager at Lousiville Landbank Authority to get answers about the dataset.

  - Pull a sample of 5 rows of the dataset to have an idea of the field data types.
  - Count-summarized all the quantitative columns to assess the impact of missing values (blank or nulls). 
  - Leveraged pandas.info() to find fields with null values and the data types assigned to each column.
    - With this information I assigned the appropriate data types to each column, in particular date fields for further processing. 

  
### 2. Data Cleaning
Business Clarifications:
-  Most of the property sales amounts in the dataset that are listed as 1 USD are correct because the cituy's priority is revitalization, not profit.
-  The field "Post Dir" (Post Directional) appears to relate to address directionals (e.g. rear units), but due to unclear documentation and minimal use, it was excluded from the analysis.
-  Some records have missing Zip Codes. The SME mentioned that some lots are unassigned or hard to map areas. It is important to include them to reflect the Landbank's total impact. Therefore, records were preserved and labeled explicitly as Unknown.
-  Created a "Zone Category" with the idea to make the dashboard more insightful and audience friendly.
  - Residential: single-family and multi-family housing zones.
  - Mixed-Use: zones allow blending residential, office, and small-scale uses.
  - Commercial: retail and commercial zones. From local to large-scale businesses.
  - Industrial: Enterprise and manufacturing zones for industrial use, warehousing, logistincs, etc.
  - Other:  a not mapped category.
-  Parcel Id field: the only field that cannot have duplicate values.
-  Rows excluded/removed:
  - "Post dir" field due to lack of documentation. Same for "Dir" field.
  - "Owner" field: there is only one owner LBA which is the client.  

### 3. Data Modeling
After the dataset has been cleaned and structured, I modelled it following the Kimball approach (Star Schema).

- FactSales: ParcelId, SaleDate, SaleAmount
- DimAddress: St#, Dir, PostDir, StreeName, StType, ZipCode2
- DimZoneCategory: Id [PK], ZoneCategory
- DimNeighborhood: Id [PK], Nhood
- DimCouncilDistrict: Id[PK], CouncilDistrict
- DimApplicant: Id [PK], Applicant (Name of the Applicant)
- DimProgram: SaleProgram, Description, Id [PK]
- DimDate: Date [PK], Build a calendar table

### 4. Dashboard Design & Building (Visualization)
Business Core KPIs:
- Total Sale Amount
- Number fo Properties Sold
- YoY Growth
- Sales by Neighborhood/Program
  - Drillthrough implementation
- Top Applicants / Buyers
- Sales timeline and seasonality
- Data glossary (via tooltips) about: sale program, buyer, and zone 

To see the final version of the dashboard, download this project and open the pbi file using Power BI Desktop.

### 5. Data Storytelling

## Key Findings

## Key Learnings

## Future Improvements
- For the Drillthrough detailed page, add a title that displays the category selected when performing the drillthrough.
  - Use a DAX to extract the selected category out of the report's context. 
