## Census Data project
#### This represents approximately the steps taken to get from data to results.
##### Please see the PDF and SVG files to see what these steps created.

[US Census Data source](https://www.census.gov/geographies/mapping-files/time-series/geo/tiger-data.2021.html#list-tab-1656998034)

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
1. Make a pie chart for the men's layer to show the distribution.


#### Make bay area detail map
1. Using both layers, identify each area of the bay area that had a strong gender disparity
1. Create a point layer with Layer to Points in order to keep the polygons but also symbolize
	each with an icon to show what's there.
1. Format labels to find a label direction that's readable without overlapping
1. Add the one bay area unknown from the men's point later to the women's point layer so that
	the duplicate "?" icon can be removed from the legend.
	* this was the biggest pain of the whole project.
1. Create a layout for the map and add legend, details, title, and so on.
