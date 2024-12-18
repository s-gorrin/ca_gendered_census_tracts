## Census Data project

(US Census Data source)[https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-data.2021.html#list-tab-1656998034]

Downloaded 2021 and 2019 Unified School District datasets

#### First, 2021

X14\_SCHOOL\_ENROLLMENT column names span B14xxxx, which start at row 11811 of the metadata  
X14\_SCHOOL\_ENROLLMENT GEOID joins to ACS\_2021\_5YR\_SDU GEOID\_Data  
1. Tables are joined ont to first with Keep all input records *unchecked*  
	* results in 10863 joined records
1. Joined table features exported to `census2021_school_enrollment`
1. Aliased fields B14001[e/m][1/2] to Age >3 total [e/m] and Age >3 in School [e/m]
	* NOTE: "in school" appears to range from pre-K or kindergarten up through grad school
1. Added a percentage field to hold the percentage of the total that is enrolled in school
	* hid all other data fields and some ID fields for visual clarity
1. % in School calculated simply with `(total / in school) * 100`
	* some nulls where there were no population converted to 0s manually
	* highest percentage was 69.33, but significant margin of error
1. Upon realizing that some records had margins of error greater than the estimate,
a definition query was written to remove those records
	* this resulted in 10836 records, so it removed 27 rows
	* after filter, new highest percentage of enrollment is 66.65%
1. Layer is symbolized with graduated colors by percentage of population in school, per school district.
**Result: a map of what percentage of residents age 3+ are in school, per school district.**


#### Do it again, but with 2019

There are 10893 rows of X14\_SCHOOL\_ENROLLMENT

School enrollment table columns again start at 11811 of the metadata  
All steps from above are done again.
	* Join results in 10845 rows
	* Joined features exported to `census2019_school_enrollment`
	* Definition query to remove high margins of error results in 10818 rows, removing again 27 rows
	* % in School is calculated with no nulls
	* *It is at this point I discover there are no meaningful differences between 2021 and 2019*

After combining the tables and taking the difference of the two percentage columns,
I have proved that they are all the same. Womp womp.



### Looking at Gendered Census Tracts

1. Download and import `ACS_2021_5YR_TRACT_06_CALIFORNIA` along with metadata and `X01_AGE_AND_SEX`
1. Join total population, male population, female population to tracts and export features to a new layer
1. Make a new field for "Percentage Male" and calculate.
	* discover that some tracts have 0 population, making them look all female when symbolized
1. Write a definion query to retain only rows with population > 0
1. Write search queries to identify tracts with +/-66% male, and make them into new feature layers
	* 75 for men, 18 for women
1. Create a new "Primary Industry" field for each layer and attempt to identify what might be
	causeing the tract to have such a stark gender divide.
	* for mostly women, three of them are universities, several appear to be retirement communities
		and there are several unknowns
	* for men, more than half are prisons or jails. CA State Hospital is included in this category.
		There are also some VA hospitals, one oil field, and a whole lot of military bases, and others.
1. Make a pie chart for the men's layer to show the distribution


##### Make bay area detail map
1. Using both layers, identify each area of the bay area that had a strong gender disparity
1. Create a point layer with Layer to Points in order to keep the polygons but also symbolize
	each with an icon to show what's there.
1. Format labels to find a label direction that's readable without overlapping
1. Add the one bay area unknown from the men's point later to the women's point layer so that
	the duplicate "?" icon can be removed from the legend.
	* this was the biggest pain of the whole project.
1. Create a layout for the map and add legend, details, title, and so on. Forgot to add name.
