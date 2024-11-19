DSAS version 6.0 Release Notes 

*Date: November 20 2024*

*Version on release 6.0.168*

**INTRODUCTION** 
----------------

The Digital Shoreline Analysis System (DSAS) version 6 is a stand-alone desktop application that calculates shoreline or boundary change over time. The DSAS software requires users to import a reference baseline and a set of shoreline positions (in GeoJSON format) to generate measurement transects. DSAS will then generate intersects and rate transects that contain rate-of-change statistics. In addition, DSAS provides uncertainties associated with rates of change and basic metadata.   

_PLEASE NOTE: The USGS End of Life (EOL) date for ArcMap was February 1, 2024, as there will no longer be software updates and patches released from Esri.  ArcMap’s EOL is the primary reason we have developed DSAS v.6.0 as standalone software that will work with any GIS._ This first update retains essential functionality (all statistical calculations, summary report, and FDGC-compliant metadata) to ensure a minimum viable product was available to the DSAS user base as ArcMap is superseded by ArcGIS Pro.  DSAS Development continues into its second phase (version 6.1) and anticipated updates include reinstating DSAS capacity for shoreline forecasting, and the application of the proxy-datum bias.   

**SUGGESTED CITATION:** Himmelstoss, E.A., Henderson, R.E., Farris, A.S., Kratzmann, M.G., Bartlett, M.K., Ergul, A., McAndrews, J., Cibaj, R., Zichichi, J.L., and Thieler, E.R., 2024, Digital Shoreline Analysis System version 6.0: U.S. Geological Survey software release, [https://doi.org/10.5066/P13WIZ8M.](https://doi.org/10.5066/P13WIZ8M. )  

For a visual overview of the DSAS v6.0 workflow see the [DSAS v6.0 workflow infographic](https://www.usgs.gov/media/images/dsas-v60-infographic) (This can also be found in the DSAS v6.0 interface under: Settings > Introduction). 

_NOTE before getting started: DSAS v6.0 requires input files to be in GeoJSON format. The outputs for DSAS v6.0 are also in GeoJSON format (which include geospatial and tabular data). Some GIS programs, such as QGIS, can view and edit GeoJSON files directly and some, like ArcPRO, require a conversion before they can be viewed._ 

The [DSAS v.5.1 User Guide](https://pubs.usgs.gov/of/2021/1091/ofr20211091.pdf) is available and applicable to many aspects of DSAS v.6.0. The user guide has relevant information providing instruction on the DSAS workflow including how to define a reference baseline for measurements, attribute requirements for baselines and shorelines, and supporting information on rate calculations and statistics. 

**QUICK START** 
----------------

<details>
<summary><b><big> 1. Download and install </b> </big></summary>
Download and install DSAS v6.0. See <a href="https://code.usgs.gov/cch/dsas/-/blob/master/README.md?ref_type=heads">Readme.md </a> 
</details>  

<details>
<summary> <b> <big>2. Prepare SHORELINE DATA </b> </big></summary>
<b> In a GIS prepare the SHORELINE DATA:</b> The shoreline file is a polyline feature with merged shorelines of various dates. The attribute table should include fields automatically generated (ObjectID, Shape) and required attributes added manually by the user. See the <a href="https://pubs.usgs.gov/of/2021/1091/ofr20211091.pdf">DSAS User Guide </a> (pages 10-13) for additional guidance and a full description of Shoreline requirements.  

1.  Add attribute for <b>SHORELINE DATE:</b> The date field is required but not name specific, meaning it can be named DATE\_, DSAS\_date or any other user-defined name. This field should have a data type of “text” or “string”, character length 10.  Dates are required to be formatted as mm/dd/yyyy. A character length of 20 is required for shoreline data spanning different hours within the same day, where dates are formatted as mm/dd/yyyy hh:mm:ss (using either 24-hour time or AM/PM). Note: The computer’s date format must be set to English (USA) mm/dd/yyyy.
 2.  Add attribute for <b> Shoreline positional UNCERTAINTY:</b> The uncertainty field is required but not name specific, meaning it can be named UNCERTAINTY, DSAS\_uncy, or any other user-defined name. This field should have any numeric field as a data type (double, float, integer).
</details>     

<details>
<summary> <b> <big>3. Create the BASELINE </b> </big></summary>
<b> In a GIS Create the BASELINE:</b> The baseline is a polyline feature, parallel to shoreline data located either onshore or offshore. The attribute table should include fields automatically generated (ObjectID, Shape) and required attributes added manually by the user. See the <a href="https://pubs.usgs.gov/of/2021/1091/ofr20211091.pdf">DSAS User Guide  </a>  (pages 13-17) for additional guidance and a full description of Baseline requirements. 
    
1.  Add attributes for the <b>Baseline ID:</b> The baseline identifier (ID) field is required field that is not name specific. This field should have a data type as long integer. DSAS uses the ID value to determine the ordering sequence of transects when the baseline feature class contains multiple segmentsIt is best to have baseline segment IDs in order alongshore. DSAS will not cast transects along baseline segments where the ID value is zero. 
</details>     

<details>
<summary> <b> <big>4. CONVERT to GeoJSON </b> </big></summary>
<b> In a GIS CONVERT DATA to GeoJSON:</b> Shoreline and baseline (and transect if using existing DSAS v5 transects*) data must be converted to a GeoJSON format using a conversion tool such as those available in ArcPro or QGIS. The best practice is to create a new folder in which to put your newly created GeoJSON files since DSAS will save all of its output files int he same directory as the input files.    

_\*DSAS v6.0 can use existing transect data prepared in DSAS v5.0 or v5.1. Transects created in prior versions of DSAS or user-generated transects are not recommended._  
</details> 

<details>
<summary> <b> <big>5. Add DATA to DSAS v6.0 </b> </big></summary>
<b> ADD DATA: </b> Click the “Add Layer” plus sign button.  Select the option to “manage data library” to assign the location of the data. Select the baseline and shoreline data (and transect if applicable). Layers will only be visible if they are in GeoJSON format. 
 </details> 

<details>
<summary> <b> <big>6. SET LAYER PARAMETERS </b> </big></summary>
<b> SET LAYER PARAMETERS:</b> Make selections for layer parameters in the table of contents:  
    
1.  Baseline: choose the Baseline ID Field and select whether your baseline is onshore or offshore.  There are options to show the baseline flow direction (ensuring the order of IDs follow sequentially and in the same direction) and change the marker distance value.   
2.  Shorelines: select the fields from the dropdown menus for the Shoreline Date Field and Shoreline Uncertainty Field. 
3.  For more information see the <a href="https://pubs.usgs.gov/of/2021/1091/ofr20211091.pdf">DSAS User Guide </a> (page 22-25).  
</details>  

<details>
<summary> <b> <big>7. Enter METADATA </b> </big></summary>
<b>Enter METADATA information</b>:  Go to Settings (gear icon) > Metadata to enter basic information that will be used for metadata file creation. 
 </details> 

<details>
<summary> <b> <big>8. CAST TRANSECTS </b> </big></summary>
<b>CAST TRANSECTS:</b> from the DSAS floating toolbar select the Cast Transects button. For descriptions of each element, click the blue help “?” buttons. 
    
1.  Enter a name for your new transects. 
2.  Select the baseline and shoreline layers that will be used to cast transects.     
3.  Enter the transect spacing, transect length, and the smoothing distance.  
4.  If desired, click the “clip to the shoreline extent” which will clip the transects at the furthest shoreline intersection point from the baseline (DSAS User Guide, page 36). 
5.  Click OK to cast transects: the file containing the transects will have a filename with this naming convention: NAME\_transects\_YYYMMDD\_HHMMSS 
6.  Carefully inspect the output transects. Ensure the spacing and orientation of the transects (perpendicular to shorelines) is correct before proceeding to calculate rates.  
7.  If edits are needed, the GeoJSON files may be opened directly in GIS programs such as QGIS, or converted to a shapefile in programs such as ArcGIS Pro. Once edits are made, the user must ensure the file is converted back to a GeoJSON before adding back to DSAS for rate calculation.  
 </details> 

<details>
<summary> <b> <big>9. CALCULATE RATES </b> </big></summary>
<b>CALCULATE  RATES:</b> from the DSAS floating toolbar, select the Calculate Rates button. For descriptions of each element, click the blue help “?” buttons. See the <a href="https://pubs.usgs.gov/of/2021/1091/ofr20211091.pdf">DSAS User Guide </a>  for additional guidance (pages 44-45) and a full description of statistics (section 7, pages 49-56). 

1.  Select baseline, shoreline and transect layers to use for analysis.  
2.  Enter additional optional parameters: Intersection Threshold, Confidence Interval, Output Display, Create DSAS summary report (_recommended_).  
3.  Click “Calculate” to generate the following files: 
4.  Rate transect (NAME\_rates\_YYYMMDD\_HHMMSS). 
    1. The rate file includes standard DSAS statistics: 
        1. NSM: Net shoreline movement (meters) 
        2. SCE: Shoreline change envelope (meters)  
        3. EPR: End point rate (meters per year)  
        4. EPRunc: Uncertainty of the end point rate (meters) 
        5. LRR: Linear regression rate (meters per year)  
        6. LSE: Standard error of linear regression  
        7. LCI: Confidence interval of linear regression—LCI%  
        8.  LR2: R-squared of linear regression 
        9. WLR: Weighted linear regression rate (meters per year) 
        10. WSE: Standard error of weighted linear regression  
        11.  WCI: Confidence interval of weighted linear regression—WCI%  
        12. WR2: R-squared of weighted linear regression 
    2. Additional attributes included  
        1. TCD: The “total cumulative distance” is the measure (in meters) alongshore from the start of the baseline segment with an ID=1 and measured sequentially alongshore to the end of the final baseline segment. 
        2. TransOrder: Assigned by DSAS on the basis of transect order along the baseline. 
5.  Intersect positions (NAME\_intersects\_YYYMMDD\_HHMMSS) this is a point file which contains the points where the shorelines and transects intersect. 
    1. The intersect file includes:  
        1. ShorelineID: The date (mm/dd/yyyy) of the shoreline intersected. 
        2. Distance: The distance (in meters) along the transect from the baseline to the intersect point. 
        3. TransOrder: Assigned by DSAS on the basis of transect order along the baseline. 
6.  Optional but recommended: if checked, DSAS will output a Summary Report text file with the results of rate calculations. The summary will include descriptive information on the selected rate calculations, including input transect filename, unique shoreline dates used, and descriptive (minimum, maximum) values for erosion and accretion. 
 </details> 

<details>
<summary> <b> <big>10. CONVERT DATA </b> </big></summary>    
<b> CONVERT DATA: </b> the DSAS-generated GeoJSON files (transect, rate and, intersect files) are automatically saved to the file location containing the baseline and shoreline data used for analysis. Convert geoJSON back to shapefile (if desired) in the GIS of your choice.  
</details>    

**TIPS for DSAS v6.0** 
----------------
<details>
<summary>TIPS </summary>  
<b>INPUTS:</b> DSAS requires data (shoreline, baseline, transects) to be in **GeoJSON format**. To convert existing feature class data, use a program such as ArcGIS Pro, or QGIS. Most online geojson/shapefile converters will only work with data in geographic coordinates. To generate rates in DSAS v6, your data must be in a meter-based projection, so we suggest using GIS software to convert files.   

<b> OUTPUTS:</b> DSAS outputs GeoJSON files, which include geospatial and tabular data. Data can be converted to shapefile or other formats with the same GIS used to perform the conversion to GeoJSON. 

<b>EDITING:</b> There is no editing functionality in this first phase (v6.0) of DSAS v6. Please use the GIS application of your choice to make edits to data. Some GIS programs, such as QGIS, can view and edit GeoJSON files directly and some, like ArcPRO, require a conversion before they can be edited. Once edits are complete, convert back to a GeoJSON file for use in DSAS v6. 

<b>CHANGE THE MAP ORIENTATION:</b>  click and hold Alt+shift+D and drag the cursor on the map to rotate the DSAS window. Click on the N arrow to re-align to north. 

<b>CLEAR DSAS SETTINGS:</b> delete the “DSASv6” folder in C:\\Users\\USERNAME\\Documents. 

<b>IDENTIFY:</b> click on any element in the map and an information table will appear. 

<b>ATTRIBUTE TALBE:</b> each dataset has an associated data table that can be accessed through the layer controls window. 

<b>CHANGE MAP ELEMENTS:</b> to change the location of map elements such as the north arrow, or scale, go to Settings > Map Elements.  To customize, click all the X buttons to clear default placements, then select desired element from the dropdown menus for each corner of the map. 

<b>NOTIFICATION TIMING:</b> to speed up or slow down the timing of the DSAS warning/information messages, go to Settings > Map Elements and adjust the time shown for Notification timeouts. 
</details> 

**KNOWN ISSUES** 
----------------
<details>
<summary>KNOWN ISSUES </summary>  

<b>BASEMAP ISSUES:</b> The rendering of the map in DSAS version 6.0 depends on reliable internet connection to the underlying map service. If problems arise, the map layer can be turned off by clicking the eye icon for the map layer (World Light Gray Base) and this will not impact the DSAS tool functionality.  

<b>INSTALLATION:</b> If running Windows, you need to download then run the .exe file. Because it is an executable, your security settings and browser may warn you not to download it, you may need to try a different browser or click “more” and “run anyway”. The file DSAS\_6.0\_mac.dmg is packaged for Macintosh and operates on OS Sonoma and beyond. 

<b>ERROR CALCULATING RATES:</b> If rates fail/time out, the problem could be that the dataset is too large/transect spacing is too fine. Attempt with fewer transects or fewer shorelines or a smaller area.  

<b>DATA CONVERTED TO WRONG TYPE:</b> In some cases, ArcPro converts a geojson to a shapefile, but the  field format is wrong (integer instead of Double). In this case, convert to shp in another program such as QGIS (add file, export to .shp). 

<b>PROJECT MANAGEMENT:</b> Clicking on the DSAS desktop icon will open the most recent DSAS project (usually the “default” project). However, we are aware the project management function within Settings contains some bugs.  

<b>BASELINE FLOW ISSUES:</b> To ensure DSAS can properly measure change alongshore, all baselines must be flowing in the same direction. DSAS will issue a warning if it detects a baseline flow issue. In some cases, the warning appears without any obvious issues for the baseline flow. If this warning occurs, it is always best to verify your data (ensuring the “show baseline flow direction” setting is checked under the baseline layer), then dismiss the warning once the data has been verified. If baselines are found to be flowing in the wrong direction, use GIS software editing tools to flip necessary segments then re-import the baseline layer and indicate flow direction. 

<b>FILE SIZE LIMITS:</b> currently DSAS can process datasets up to 100MB.
</details> 