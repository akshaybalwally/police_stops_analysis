This readme explains how to make best use of the data from the Stanford Open
Policing Project. We provide an overview of the data and a list of best
practices for working with the data. 

Our analysis code and further documentation are available at
[https://github.com/5harad/openpolicing](https://github.com/5harad/openpolicing).

### Overview of the data file structure

For each dataset, we provide 4 files:

1. A zipped csv file of the cleaned data
2. An RDS of the cleaned data
3. Tarballed (zipped) shapefiles
4. Tarballed (zipped) raw data (available upon request)

### Description of standardized data

Each row in the cleaned data represents a stop. The following details the
maximal set of features we attempted to extract from each location. Coverage
varies by location. Fields with an asterisk were removed for public release due
to privacy concerns. All columns except raw\_row\_number, violation,
disposition, location, officer\_assignment, any city or state subgeography
(i.e. county, beat, division, etc), unit, and vehicle_{color,make,model,type}
are also digit sanitized (each digit replaced with "-") for privacy concerns.

Note that many locations have additional information that could be extracted
(e.g., zip code), but we do not designate a standardized column for information
beyond what is listed below, either because we do not use the information in
our analysis and/or because not enough locations provided this information. We
do pull through some additional columns (discussed on a location-by-location
basis within this readme), which have column names prefixed with "raw\_".

<table>
  <tr>
    <td>Column name</td>
    <td>Column meaning</td>
    <td>Example value</td>
  </tr>
  <tr>
    <td>raw_row_number</td>
    <td>An number used to join clean data back to the raw data</td>
    <td>38299</td>
  </tr>
  <tr>
    <td>date</td>
    <td>The date of the stop, in YYYY-MM-DD format. Some states do not provide
    the exact stop date: for example, they only provide the year or quarter in
    which the stop occurred. For these states, stop_date is set to the date at
    the beginning of the period: for example, January 1 if only year is
    provided.</td>
    <td>"2017-02-02"</td>
  </tr>
  <tr>
    <td>time</td>
    <td>The 24-hour time of the stop, in HH:MM format.</td>
    <td>20:15</td>
  </tr>
  <tr>
    <td>location</td>
    <td>The freeform text of the location. Occasionally, this represents the
    concatenation of several raw fields, i.e. street_number, street_name</td>
    <td>"248 Stockton Rd."</td>
  </tr>
  <tr>
    <td>lat</td>
    <td>The latitude of the stop. If not provided by the department, we
    attempt to geocode any provided address or location using
    Google Maps. Google Maps returns a "best effort" response, which may not
    be completely accurate if the provided location was malformed or
    underspecified. To protect against suprious responses, geocodes more than
    4 standard deviations from the median stop lat/lng are set to NA.
    <td>72.23545</td>
  </tr>
  <tr>
    <td>lng</td>
    <td>The longitude of the stop. If not provided by the department, we
    attempt to geocode any provided address or location using
    Google Maps. Google Maps returns a "best effort" response, which may not
    be completely accurate if the provided location was malformed or
    underspecified. To protect against suprious responses, geocodes more than
    4 standard deviations from the median stop lat/lng are set to NA.
    </td>
    <td>115.2808</td>
  </tr>
  <tr>
    <td>county_name</td>
    <td>County name where provided</td>
    <td>"Allegheny County"</td>
  </tr>
  <tr>
    <td>neighborhood</td>
    <td>This is the neighborhood of the stop and some police departments will
    provide this instead of a location or beat.</td>
    <td>"GRNBELT"</td>
  </tr>
  <tr>
    <td>beat</td>
    <td>Police beat. If not provided, but we have retrieved police department
    shapfiles and the location of the stop, we geocode the stop and find the
    beat using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>district</td>
    <td>Police district. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the district using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>subdistrict</td>
    <td>Police subdistrict. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the subdistrict using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>division</td>
    <td>Police division. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the division using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>subdivision</td>
    <td>Police subdivision. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the subdivision using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>police_grid_number</td>
    <td>Police grid number. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the police grid number using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>precinct</td>
    <td>Police precinct. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the precinct using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>region</td>
    <td>Police region. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the region using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>reporing_area</td>
    <td>Police reporting area. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the reporting area using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>sector</td>
    <td>Police sector. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the sector using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>subsector</td>
    <td>Police subsector. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the subsector using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>substation</td>
    <td>Police substation. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the substation using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>service_area</td>
    <td>Police service area. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the service area using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>zone</td>
    <td>Police zone. If not provided, but we have retrieved police
    department shapfiles and the location of the stop, we geocode the stop and
    find the zone using the shapefiles.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>subject_age</td>
    <td>The age of the stopped subject. When date of birth is given, we
    calculate the age based on the stop date. Values outside the range of
    10-110 are coerced to NA.</td>
    <td>54.23</td>
  </tr>
  <tr>
    <td>subject_dob*</td>
    <td>The date of birth of the stopped subject.</td>
    <td>"1956-02-23"</td>
  </tr>
  <tr>
    <td>subject_yob*</td>
    <td>The year of birth of the subject.</td>
    <td>1983</td>
  </tr>
  <tr>
    <td>subject_race</td>
    <td>The race of the stopped subject. Values are standardized to white,
    black, hispanic, asian/pacific islander, and other/unknown</td>
    <td>"hispanic"</td>
  </tr>
  <tr>
    <td>subject_sex</td>
    <td>The recorded sex of the stopped subject.</td>
    <td>"female"</td>
  </tr>
  <tr>
    <td>officer_id*</td>
    <td>Officer badge number or other form of identification provided by the
    department.</td>
    <td>8</td>
  </tr>
  <tr>
    <td>officer_id_hash</td>
    <td>A unique hash of the officer id used to identify individual officers
    within a location. This is usually just a hash of the provided officer ID
    or badge number. In some places, notably South Carolina Statewide data and
    the Seattle, WA city data, this ID is not unique, so we hash it with other
    officer attributes to make it unique, i.e. officer_last_name, officer_race,
    etc. In about half of locations, however, we get an officer ID but no other
    officer information, so our ability to test for uniqueness and deduplicate
    is limited. In other locations, a small number of IDs are duplicated
    because of what appears to be a data entry issue, i.e. Chicago, IL, where
    0.3% of officer IDs appear to be only the prefix of their ID. </td>
    <td>"a888fdc120"</td>
  </tr>
  <tr>
    <td>officer_age</td>
    <td>The age of the stopped officer. When date of birth is given, we
    calculate the age based on the stop date. Values outside the range of
    10-100 are coerced to NA.</td>
    <td>54.23</td>
  </tr>
  <tr>
    <td>officer_dob*</td>
    <td>The date of birth of the stopped officer.</td>
    <td>"1956-02-23"</td>
  </tr>
  <tr>
    <td>officer_race</td>
    <td>The race of the stopped officer. Values are standardized to white,
    black, hispanic, asian/pacific islander, and other/unknown</td>
    <td>"hispanic"</td>
  </tr>
  <tr>
    <td>officer_sex</td>
    <td>The recorded sex of the stopped officer.</td>
    <td>"female"</td>
  </tr>
  <tr>
    <td>officer_first_name*</td>
    <td>First name of the officer when provided.</td>
    <td>"MIGUEL"</td>
  </tr>
  <tr>
    <td>officer_last_name*</td>
    <td>Last name of the officer when provided.</td>
    <td>"JEFFERSON"</td>
  </tr>
  <tr>
    <td>officer_years_of_service</td>
    <td>Number of years officer has been with the police department.</td>
    <td>22</td>
  </tr>
  <tr>
    <td>officer_assignment</td>
    <td>Department or subdivision to which officer has been assigned.</td>
    <td>"8th District"</td>
  </tr>
  <tr>
    <td>department_id</td>
    <td>ID of department or subdivision to which officer has been assigned.</td>
    <td>90</td>
  </tr>
  <tr>
    <td>department_name</td>
    <td>Name of department or subdivision to which officer has been
    assigned.</td>
    <td>90</td>
  </tr>
  <tr>
    <td>unit</td>
    <td>Unit to which officer has been assigned.</td>
    <td>"Patrol-1st"</td>
  </tr>
  <tr>
    <td>type</td>
    <td>Type of stop: vehicular or pedestrian.</td>
    <td>"vehicular"</td>
  </tr>
  <tr>
    <td>disposition</td>
    <td>Disposition of stop where provided. What is recorded here varies widely
    across police departments.</td>
    <td>"GUILTY"</td>
  </tr>
  <tr>
    <td>violation</td>
    <td>Specific violation of stop where provided. What is recorded here varies
    widely across police departments.</td>
    <td>"SPEEDING 15-20 OVER"</td>
  </tr>
  <tr>
    <td>arrest_made</td>
    <td>Indicates whether an arrest made.</td>
    <td>FALSE</td>
  </tr>
  <tr>
    <td>citation_issued</td>
    <td>Indicates whether a citation was issued.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>warning_issued</td>
    <td>Indicates whether a warning was issued.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>outcome</td>
    <td>The strictest action taken among arrest, citation, warning, and
    summons.</td>
    <td>"citation"</td>
  </tr>
  <tr>
    <td>contraband_found</td>
    <td>Indicates whether contraband was found. When search_conducted is NA,
    this is coerced to NA under the assumption that contraband_found shouldn't
    be discovered when no search occurred and likely represents a data
    error.</td>
    <td>FALSE</td>
  </tr>
  <tr>
    <td>contraband_drugs</td>
    <td>Indicates whether drugs were found. This is only defined when
    contraband_found is true.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>contraband_weapons</td>
    <td>Indicates whether weapons were found. This is only defined when
    contraband_found is true.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>contraband_other</td>
    <td>Indicates whether contraband other than drugs and weapons were found.
    This is only defined when contraband_found is true.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>frisk_performed</td>
    <td>Indicates whether a frisk was performed. This is technically different
    from a search, but departments will sometimes include frisks as a search
    type.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_conducted</td>
    <td>Indicates whether any type of search was conducted, i.e. driver,
    passenger, vehicle. Frisks are excluded where the department has provided
    resolution on both.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_person</td>
    <td>Indicates whether a search of a person has occurred. This is only
    defined when search_conducted is TRUE.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_vehicle</td>
    <td>Indicates whether a search of a vehicle has occurred. This is only
    defined when search_conducted is TRUE.</td>
    <td>TRUE</td>
  </tr>
  <tr>
    <td>search_basis</td>
    <td>This provides the reason for the search where provided and is
    categorized into k9, plain view, consent, probable cause, and other. If a
    serach occurred but the reason wasn't listed, we assume probable cause.
    </td>
    <td>"consent"</td>
  </tr>
  <tr>
    <td>reason_for_arrest</td>
    <td>A freeform text field indicating the reason for arrest where
    provided.</td>
    <td>"outstanding warrant"</td>
  </tr>
  <tr>
    <td>reason_for_frisk</td>
    <td>A freeform text field indicating the reason for frisk where
    provided.</td>
    <td>"suspicious movement"</td>
  </tr>
  <tr>
    <td>reason_for_search</td>
    <td>A freeform text field indicating the reason for search where
    provided.</td>
    <td>"odor of marijuana"</td>
  </tr>
  <tr>
    <td>reason_for_stop</td>
    <td>A freeform text field indicating the reason for the stop where
    provided.</td>
    <td>"EQUIPMENT MALFUNCTION"</td>
  </tr>
  <tr>
    <td>speed</td>
    <td>The recorded speed of the vehicle for the stop.</td>
    <td>76.2</td>
  </tr>
  <tr>
    <td>posted_speed</td>
    <td>The speed limit where the stop was recorded.</td>
    <td>55</td>
  </tr>
  <tr>
    <td>use_of_force_description</td>
    <td>A freeform text field describing the use of force.</td>
    <td>"handcuffed"</td>
  </tr>
  <tr>
    <td>use_of_force_reason</td>
    <td>A freeform text field describing the reason for the use of force.</td>
    <td>"weapons / violence related incident"</td>
  </tr>
  <tr>
    <td>vehicle_color</td>
    <td>A freeform text of the vehicle color where provided; format varies
    widely.</td>
    <td>"BLK"</td>
  </tr>
  <tr>
    <td>vehicle_make</td>
    <td>A freeform text of the vehicle make where provided; format varies
    widely.</td>
    <td>"TOYOTA"</td>
  </tr>
  <tr>
    <td>vehicle_model</td>
    <td>A freeform text of the vehicle model where provided; format varies
    widely.</td>
    <td>"Cherokee"</td>
  </tr>
  <tr>
    <td>vehicle_type</td>
    <td>A freeform text of the vehicle type where provided; format varies
    widely.</td>
    <td>"TRUCK"</td>
  </tr>
  <tr>
    <td>vehicle_registration_state</td>
    <td>A freeform text of the vehicle registration state where provided;
    format varies widely.</td>
    <td>"CA"</td>
  </tr>
  <tr>
    <td>vehicle_year</td>
    <td>Vehicle manufacture year where provided. This value is NA for any year
    before 1800.</td>
    <td>2007</td>
  </tr>
  <tr>
    <td>notes</td>
    <td>A freeform text field containing any officer notes.</td>
    <td>"NO PASSENGERS"</td>
  </tr>
</table>
* Removed for public release for privacy reasons.

### Best practices

We provide some lessons we’ve learned from working with this rich, but
complicated data. 

1. Read over the notes and processing code if you are going to focus on a
   particular location, so you’re aware of the judgment calls we made in
   processing the data. Taking a look at the original raw data is also wise
   (and may uncover additional fields of interest). 
2. Start with the cleaned data from a single small location to get a feel for
   the data. Rhode Island, Vermont, and Connecticut are all load quickly. 
3. Note that loading and analyzing every state simultaneously takes significant
   time and computing resources. One way to get around this is to compute
   aggregate statistics from each state. For example, you can compute search
   rates for each age, gender, and race group in each state, save those rates,
   and then quickly load them to compute national-level statistics broken down
   by age, race, and gender. 
4. Take care when making direct comparisons between locations. For example, if
   one state has a far higher consent search rate than another state, that may
   reflect a difference in search recording policy across states, as opposed to
   an actual difference in consent search rates. 
5. Examine counts over time in each state: for example, total numbers of stops
   and searches by month or year. This will help you find years for which data
   is very sparse (which you may not want to include in analysis). 
6. Do not assume that all disparities are due to discrimination. For example,
   if young men are more likely to receive citations after being stopped for
   speeding, this might simply reflect the fact that they are driving faster.  
7. Do not assume the standardized data are absolutely clean. We discovered and
   corrected numerous errors in the original data, which were often very
   sparsely documented and changed from year to year, requiring us to make
   educated guesses. This messy nature of the original data makes it unlikely
   the cleaned data are perfectly correct. 
8. Do not read too much into very high stop, search, or other rates in
   locations with very small populations or numbers of stops. For example, if a
   county has only 100 stops of Hispanic drivers, estimates of search rates for
   Hispanic drivers will be very noisy and hit rates will be even noisier.
   Similarly, if a county with very few residents has a very large number of
   stops, it may be that the stops are not of county residents, making stop
   rate computations misleading. 

The following contains date ranges, coverage rates, and some notes on each
location.  A coverage rate is 1 - null rate, so it represents the proportion of
data that have values for that feature. The reported coverage rates are also
predicated, which means that some columns coverage is calculated only after
considering another column. For instance, the coverage for contraband_found is
reported after filtering to instances where search_conducted was true. In a
similar fashion, search_basis and reason_for_search are only calculated when
search conducted is true, reason_for_arrest when arrest_made is true, and
contraband_drugs, contraband_weapons, and contraband_alcohol, and
_contraband_other when contraband_found is true.

The notes are not intended to be a comprehensive
description of all the data features in every state, since this would be
prohibitively lengthy. Rather, they are brief observations we made while
processing the data. We hope they will be useful to others. They are worth
reading prior to performing detailed analysis of a location.

Our analysis only scratches the surface of what’s possible with these data.
We’re excited to see what you come up with!

## Little Rock, AR
**Data notes**:
- lat/lng data doesn't appear totally accurate, there are ~18k lat/lngs that
  were coerced to NA because they all equalled "-1.79769313486232E+308"
- Data is deduplicated on date, time, lat, lng, race, sex, and officer name,
  reducing the number of records by ~30.6%
- Data consists only of citations
- raw_defendant_race represents `Defendant Race` in the raw data and is the
  column from which subject_race is derived

## Gilbert, AZ
**Data notes**:
- Data is deduplicated on call_id, reducing the number of records 17.6%; this
  was equivalent to deduping on date, time, location, and officer_id; subject
  name appears to have been entered multiple times per call_id, and often in
  subtly different formats
- Most important data is missing, including outcome (arrest, citation,
  warning), reason for stop, search, contraband, and demographic information
  on the subject (except name, which is redacted for privacy)
- call_type was either TS (traffic stop) or SS (subject stop), which we
  translated to 'vehicular' or 'pedestrian' stops

## Mesa, AZ
**Data notes**:
- INCIDENT_NO appears to refer to the same incident but can involve
  multiple people, i.e. 20150240096, which appears to be an alcohol bust of
  several underage teenagers; in other instances, the rows look nearly
  identical, but given this information and checking several other seeming
  duplicates, it appears as though there is one row per person per incident
- violation is charge_desc in the raw data, and raw_charge represents the
  charge code in the raw data
- subject_race was derived from ethnicity_fixed and race_fixed in the raw data,
  provided in the clean data with raw_*

## Statewide, AZ
**Data notes**:
- Counties were mapped in two ways. First, we determined which counties the
  codes in the County field referred to by using the highways which appeared
  most frequently in each coded county. Second, for stops which had no data in
  the County field, we used the values in the Highway and Milepost fields to
  estimate where the stop took place. For this, we relied on highway marker
  maps (sources:
  [here](https://azdot.gov/docs/business/state-milepost-map.pdf?sfvrsn=0) and
  [here](http://adot.maps.arcgis.com/apps/Viewer/index.html?appid=4f19dfc238c44815b310bc72a9827bc2)
  to map the most frequently traversed highways, which covered the vast
  majority of stops. Using these two methods, we were able to map 95% of stops
  which had any location data (i.e., values in either County or Highway and
  Milepost), and 89% of stops overall.
- It would be possible to map the highway and mile marker data to geo
  coordinates, like we did in Washington.
- There is a two-week period in October 2012 and a two-week period in November
  2013 when no stops are recorded. We also are missing December 2015.
  Dates are sparse in 2009–2010 (and even up until mid-2011). 
- We also received a file with partial data on traffic stops pre-2009; this is
  not included in the dataset. 
- Data for violation reason is largely missing. 
- Raw column `VehicleSearchAuthority` and `DriverSearchAuthority` seem to provide 
  search basis but we lack a mapping for the codes. `ConsentSearchAccepted` 
  gives us information on search type for a small fraction of searches. 
- `raw_TypeOfSearch` includes information on who was 
  searched (e.g., driver vs. passenger), but does not provide information on the 
  type of search (e.g., probable cause vs. consent).  
- Some contraband information is available and so we define a contraband_found
  column in case it is useful to other researchers. But the data is messy and
  there are multiple ways contraband_found might be defined, and so we do not
  include Arizona in our contraband analysis. 
- Additional raw data columns that may be of interest: `ConsentSearchRequested`
  (note that there is also a raw column `ConsentSearchAccepted` -- which populates
  the clean values `search_basis == "consent"`), `IfConsentRequestGranted`,
  (FS, RS, NA), `SubjectDemeanor` (CO, UN, CM, NA), `StopDuration` (A-F, NA),
  `DistractedDriving` (1-2 word free field), `ImmigrationStatusCheck` (boolean, 
  nearly all NA), `VehicleImpounded` (Y, N, I, NA), `ImpoundReason` (LI, NL,
  CN, DE, DM, II, UA, NA), `TypeOfContact` (D, P, E, N, C, NA), `DrugSeizureType`
  (combinations of P, S, T), `DUIBAC`, `DUICharges`, `DUITests` (combinations of
  B, I, U), `PreStopIndicator` (VT = "Vehicle Type, Condition or Modification",
  BL = "Driver Body Language", PB = "Passenger Behavior", DB = "Driving Behavior",
  OT = "Other", NO = "None")
  
## Anaheim, CA
**Data notes**:
- Very little information received, only a reference number, date, year, case
  type (with no translation), and a case type (with no translation)
- reason_for_stop is `Final Case Type D` in the raw data

## Bakersfield, CA
**Data notes**:
- Data is deduplicated on raw columns date_of_birth, subject_address,
  ethnicity, gender_code, occ_date, occ_time, reducing the number of records by
  ~1.2% 
- Data does not include reason for stop, search, contraband fields
- Missing data dictionaries for ticket classes, ticket statuses, and
  statute section
- subject_race is based on ethnicity and race, the raw columns are provided in
  the clean data
- We currently have no data dictionaries for statute_section and statute_name,
  but they are passed through to the clean data
- Data consists only of citations

## Oakland, CA
**Data notes**:
- Data is deduplicated on raw columns contactdate, contacttime, streetname,
  subject_sdrace, subject_sex, and subject_age, reducing the number of records
  by ~5.2%
- Stops from 2013-2015 don't have encountertype like 2016-2017, so we attempt
  to pull it out from ReasonForEncounter; however, this breakdown is imprecise,
  because while one category is "Traffic Violation", another is "Probable
  Cause"; presumably, "Probable Cause" could be a reason for a vehicular stop;
  so, the stop is type vehicular if the encountertype was vehicular or the
  reason for encounter involved a traffic violation; it was classified as
  pedestrian if the encountertype was pedestrian or bicycle, otherwise this
  field is NA, since we can't say whether "Probable Cause" or "Reasonable
  Suspicion" was a vehicular or pedestrian stop
- Contraband is encoded based on ResultOfSearch (pedestrian) and
  subject_resultofsearch (vehicular); None, NA, and anything with "Returned"
  after it are excluded, i.e. "Marijuana - Returned", "Other Weapons -
  Returned," under the assumption that returned items were not contraband
- 2013 is missing the first 3 months of data and 2015 is missing the last 3
  months of data
- Some of the raw columns were named similarly but not exactly the same across
  years, i.e. ResultOfSearch in 2013, 2014, and 2015, but
  subject_resultofsearch in 2016 and 2017; these were renamed to be consistent
  with the latter years in the raw data loading function
- subject_{resultofencounter,typeofsearch,search_conducted,resultofsearch}
  formed the foundation for search and contraband fields and are passed
  through in the clean data
- subject_race is derived from subject_sdrace, which is passed through to the
  clean data

## San Bernardino, CA
**Data notes**:
- Data is deduplicated on raw columns CreateDateTime, Address, and CallType,
  removing ~26.3% of records
- Data does not include most useful information, including demographic,
  outcome, and search/contraband information, so the deduplication above
  potentially over-deduplicates
- type is derived from CallType, which is passed through since we lack a data
  dictionary for some of them

## Long Beach, CA
**Data notes**:
- Data is deduplicated on raw columns Date, Location, Race, Sex, and Officer
  DID, reducing the number of records by ~14.3%
- Data does not include reason for stop, search, or contraband fields 
- violation is a concatenation of 4 violation descriptions, separated by ';'
- type is derived from violation_1_description
- raw columns sex, race, and officer_race are passed through since our
  translations may simplify them
- There is a notable drop in stops from 2008 to 2016, unclear what the origin
  of this may be

## Los Angeles, CA
- Data is deduplicated on raw columns stop_date, stop_time, reporting_district,
  division_description_1, division_description_2, officer_1_serial_number,
  officer_2_serial_number, descent_description, sex_code, and stop_type,
  reducing the number of records by ~17.7%
- Search/contraband, outcome, and location data are missing
- subject_race is derived from descent_description, which is passed through

## San Diego, CA
**Data notes**:
- stop_id in raw data doesn't appear to apply to unique events, as the same
  id has different service_area, subject_race, subject_age, and subject_sex,
  i.e.1099162
- Data is deduplicated on raw columns timestamp, subject_race, subject_sex,
  subject_age, and service_area, reducing the number or records by ~2.0%
- There are no locations, but service_area is provided
- subject_race is derived from subject_race_description which is passed through
- reason_for_search is named SearchBasis in the raw data and search_basis is
  derived from this column
- outcomes are based on ActionTaken, which is passed through as
  raw_action_taken
- search_conducted is named searched in the raw data; when searched is NA, this
  is interpreted as FALSE for search_conducted under the assumption that
  officers sometimes don't record the absence of a search. Furthermore, where
  searched is NA, SearchBasis, SearchBasisOther, and SearchType are all NA, as
  well, suggesting that no search occurred
- If search_conducted was true but contraband_found was NA, it was changed to
  false, under the assumption that NA means false when a search is performed
- 2017 only has data for part of the year

## San Francisco, CA
**Data notes**:
- Search basis in the raw data is only "No Search", consent, or other
  (inventory, incident to arrest, and parole searches) 
- Contraband found is derived from search_vehicle_description, which,
  unfortunately, only has the search basis and "Positive Result" or "Negative
  Result", the former indicating when contraband found is true; it is passed
  through to the clean data
- outcomes are based on result_of_contact_description, which is passed through
- Data is deduplicated on raw columns date, time, race_description, sex, age,
  location, removing ~0.3% of stops

## San Jose, CA
**Data notes**:
- event_number in raw data has indeterminate meaning, several event numbers
  occur at the same time but have up to 16 duplicates; however, some of these
  involve different subjects, so it's unclear whether they are distinct
  incidents or large incidents involving many people
- Data is deduplicated using date, time, location, subject race, and raw_search
  (SEARCH in raw data); this removes about ~4.4% of records, but many of these
  rows are lacking sufficient information for differentiation, i.e. they have
  NA for many of their values
- search_conducted is derived from SEARCH (raw_search in clean data); NAs in
  the original column and converted to FALSE, under the assumption that
  officers sometimes don't record the absence of a search. However, there are
  other values other than the ones provided in the data dictionary (and are not
  NA), these are converted to NA for search_conducted but available in the
  raw_search column for review; some of them appear to be the result malformed
  rows and/or incorrect data entry, i.e. some of them could be race
  classifications
- type is based on `TYCOD DESCRIPTION`, which is passed through as
  raw_call_desc
- race is passed through to provide access to greater granularity
- a translation of `EVENT DISPO` is provided as raw_event_desc; this was used
  for outcomes
- 2013 and 2018 only have partial data

## Santa Ana, CA
**Data notes**:
- Deduping on raw columns Date, Race, Sex, Violation Description, Officer
  (Badge), and Primary Street would reduce this dataset by ~9.7%, but there is
  insufficient information to justify this without the incident time. For
  instance, the highest frequency "incident" deduping on that critera was 16
  male Hispanic drivers failing to stop at a stop sign by the same officer on
  5th Street; while this could be 16 duplicates, it could also be the same
  officer pulling over 16 people throughtout that day
- Data does not include search or contraband information
- Data includes only citations
- 2014 and 2018 only contain partial data

## Statewide, CA
**Data notes**:
- CHP districts roughly map to counties, so we mapped stops to counties using
  the map of CHP districts, which is included in the raw data. Some counties
  appear to have very high stop rates; this is because they have very small
  populations. It seems likely that the stops occurring in those counties are
  not actually the resident population.
- Driver age categories are included in the raw data; these cannot be mapped to
  granular values, so we cannot fill out the driver_age field. 
- Driver race was recorded with high granularity. Raw mapping:
    * A = Other Asian
    * B = Black
    * C = Chinese
    * D = Cambodian
    * F = Filipino
    * G = Guamanian
    * H = Hispanic
    * I = Indian
    * J = Japanese
    * K = Korean
    * L = Laotian
    * O = Other
    * P = Other Pacific Islander
    * S = Samoan
    * U = Hawaiian
    * V = Vietnamese
    * W = White
    * Z = Asian Indian
  `subject_race` is mapped from `raw_race` above.
- Search basis was recorded more finely in raw data. Raw mapping:
    * 1 = Probable Cause (positive)
    * 2 = Probable Cause (negative)
    * 3 = Consent (positive), 202D Required
    * 4 = Consent (negative), 202D Required
    * 5 = Incidental to Arrest
    * 6 = Vehicle Inventory
    * 7 = Parole / Probation / Warrant
    * 8 = Other
    * 9 = Pat Down / Frisk
  `search_basis` is mapped from `raw_search_basis` above.
- Very few consent searches are conducted relative to other states. 
- Contraband found information is only available for a small subset of
  searches: the raw data can tell you if a probable cause search or a consent
  search yielded contraband, but cannot tell you if contraband was located
  during a search conducted incident to arrest. (Note that in many cases we
  cast NA contraband to F, but in this case we do not, because we simply do not
  have contraband recovery data for non-discretionary searches). We still include
  California in our contraband analysis because exclude non-discretionary 
  searches like those incident to arrest. 
- Raw data contains shift time is included, but is not sufficiently granular 
  to yield reliable stop time. 

## Stockton, CA
**Data notes**:
- Data consists of two sets of files, traffic stop surveys and CAD stop files,
  but currently there is no information on how to join them; location is in the
  stop files, but all other demographic information is in the traffic stop
  survey files
- There may be duplicates, but unclear how to identify them, as date, age,
  gender, and race are the only consistently filled in fields, and the maximum
  number of stops for any date, age, gender, race combination is 10, which is a
  reasonable number of stops for that combination over the course of a day in
  the entire city occasionally
- officer_id is coalesced officer_id and officer_id2, the former being 90% null
  and the latter 50% null in the dataset
- Outcomes are based on raw column result, which is passed through
- search_conducted and search_basis are derived from the raw column search,
  which is passed through; where SEARCH was NA, search_conducted as set to
  false, under the assumption that sometimes officers don't record the absence
  of a search
- 2012 has suspiciously little data

## Aurora, CO
**Data notes**:
- Data is deduplicated on raw columns Ticket Date, Ticket Time, Ticket
  Location, First Name, Last Name, sex, and Date of Birth, reducing the number
  of records by ~1.0%
- subject_race was based on Race and Ethnicity in the raw data, which are
  passed through

## Denver, CO
**Data notes**:
- MASTER_INCIDENT_NUMBER has many duplicates, but it's unclear what it
  corresponds to or how to deduplicate it if that is the correct thing to do,
  since the records are nearly identical except for the NEIGHBORHOOD_NAME
- Data does not contain subject demographic or search/contraband information

## Statewide, CO
**Data notes**:
- The state did not provide us with mappings for every police department code
  to police department name.
- Arrest and citation data are unreliable from 2014 onward. Arrest rates drop
  essentially to zero. 
- Counties were mapped using a dictionary provided by the agency. Denver County
  has many fewer stops than expected given the residential population; this is
  because it only contains a small section of highway which is policed by the
  state patrol.
- Rows in raw data represent violations, not stops, so we remove duplicates by
  grouping by the other fields.
- `subject_race` was mapped from `raw_Ethnicity`. 
- Note that data from 2016 came with about 80 fewer columns than the data pre-2016 
  and after 2016, so many values for that year will be NA, including search data 
  (see below for details).
- The data came in three files, the first covered 2010-March 2016; this has full
  data. The second covered Jan-Dec 2016; this was missing many columns, including
  whether a search was conducted. The third data file covered Jan-Dec 2017 and
  had full data. In order to preserve as much search data as possible we use the
  second file with missing data only to fill in the nine months of April-Dec 
  2016. This, in particular, affects the marijuana analysis search rate time 
  series.
- Additional columns in the raw data that may be of interest: `MMJCard`,
  `DUIDType`, `NonUS`, `NonUSDL`, `NonUSDLLocation`, `DLCheck`, 
  `TrafficAccident`, `AccidentSeverity` (0-4), `DUIArrest`, `HVPTCitation`, 
  `SeatBeltCitation`, `FelonyArrest`, `Misdemeanors`, `Felonies` (count),
  `VehicleInspected`, `Recoveries`, `TrafficOral`, `AssistOral`, `AllOtherOral`,
  `GrantCategory`, `GrantLabel`, `Assists`, `AssistsMultiple`, 
  `AssistsCount`, `ContrabandCharge` (petty offense, felony, misdemeanor,
  none, traffic), `Warrant`, `MisdemeanorOrFelony` (M or F)

## Statewide, CT
**Data notes**:
- Counties were mapped by running the cities in the `Intervention Location
  Name` field through Google's geocoder.
- Rows appear to represent violations, not individual stops, because a small
  proportion of rows (1%) report the same officer making multiple stops at the
  same location at the same time. We grouped the data to combine these
  duplicates. We don't want to be overly aggressive in grouping together stops,
  so we only group if the other fields are the same. 
- While there is some search type data, a high fraction of searches are marked
  as "Other".
- While there is some violation data, too much is missing.
- Race (`raw_SubjectRaceCode`, `raw_SubjectEthnicityCode`) mapping:
    * A = Asian/Pacific Islander
    * B = Black
    * H = Hispanic
    * W = White
    * I = Native American
- Search basis (`raw_SearchAuthorizationCode`) mapping:
    * C = consent
    * O = probable cause
    * I = inventory
- The Connecticut state patrol created another website
  ([link](http://ctrp3.ctdata.org/)), where new data will get uploaded going
  forward. We haven't processed this yet.

## Hartford, CT
**Data notes**:
- Data is deduplicated on raw columns InterventionDateTime,
  ReportingOfficerIdentificationID, InterventionLocationDescriptionText,
  SubjectRaceCode, SubjectSexCode, and SubjectAge, reducing the number of rows
  by ~1.1%
- search rate is suspiciously high, ~28%
- hit rate is suspiciously low, ~1%; we exclude Hartford from outcome and
  threshold tests because contraband recovered is so suspiciously low that we
  don't trust it, plus it's so low that it's not even enough data to run the 
  statistical tests reliably.
- subject_race is based on SubjectEthnicityCode and SubjectRaceCode, which are
  based on raw_subject_ethnicity_code and raw_subject_race_code
- search_conducted and search_basis are derived from SearchAuthorizationCode,
  which is passed through as raw_search_authorization_code
- outcomes are based on InterventionDispositionCode, which is passed through as
  raw_intervention_disposition_code
- 2013 and 2016 have only partial data

## Tampa, FL
**Data notes**:
- Data is deduplicated on date, subject_race, subject_dob, officer_last_name,
  officer_first_name, and Driver License Number, reducing the number of rows by
  ~13.2%; it's possible this slightly over-deduplicates, if an officer pulls
  over the same person in the same day
- Data is missing search and contraband information, as well as outcomes other
  than citations
- Hispanic race data is likely underreported, given that ACS 2017 5-year
  estimates suggest Hispanic individuals make up ~25% of the population, but
  only ~4% of stops in Tampa
- The data sources are public (it's unclear what the difference is between the
  stop types):
  - https://publicrec.hillsclerk.com/Traffic/Civil_Traffic_Name_Index_files/
  - https://publicrec.hillsclerk.com/Traffic/Criminal_Traffic_Name_Index_files/
- subject_race is based on Race which is passed through as raw_race

## Saint Petersburg, FL
**Data notes**:
- Only 7 months of data provided
- No demographic, search/contraband, or outcome data

## Statewide, FL
**Data notes**:
- The raw data is very messy. Two different data sets were supplied, both with
  slightly different schemas, just for 2010 to part of 2016. A third dataset
  was supplied for 2016 through 2018. However, they were joined by uniquely
  identifying features. The second data dump goes until 2016, while the first 
  only goes until 2015. The fields missing in the second or third data sets are 
  thus missing for some rows.
- There are many duplicates in the raw data, which we remove in two stages.
  First, we remove identical duplicate rows. Second, we group together rows
  which correspond to the same stop but to different violations or passengers. 
- The original data has a few parsing errors, but they don't seem important as
  they are spurious new lines in the last 'Comments' field.
- The Florida PD clarified to us that both UCC Issued and DVER Issued in the
  `raw_EnforcementAction` column indicated citations, and we consequently coded
  them as such. 
- `subject_race` was mapped from `raw_Ethnicity` and `raw_Race` (the different
  data sets have different practices in terms of recording Hispanic in race vs
  ethnicity fields).
- `raw_SearchType` was used to conclude `search_conducted` and `search_basis`.
- While there is some data on whether items were seized, it is not clear if
  these are generally seized as a result of a search, and we thus do not define
  a contraband_found column for consistency with other states. 
- `raw_EnforcementAction` and `notes` were used to determine `outcome`.
  

## Statewide, GA
**Data notes**:
- The data represent warnings.
- The provided `.txt` was comma-separated, but not quoted. Therefore we had to
  write a script (`convert_GA.py`) to iron out some obviously misaligned
  columns.
- Rows represent individual warnings, and thus need to be aggregated to
  represent a single stop.
- The race field on the warnings form is optional; we have only about 50% race
  coverage, so GA is omitted from all analyses.
- `subject_race` was mapped from `raw_race`.

## Statewide, IA
**Data notes**: 
- The data separates warnings and citations. They are very different with
  respect to which fields they have available. Both contain duplicates. This
  happens when individuals receive more than one warning or citation within the
  same stop. We remove these by grouping by the remaining fields by the stop
  key and date.
- In some cases, there are multiple time stamps per unique (key, date)
  combination. In most of these cases, the timestamps differ by a few minutes,
  but all other fields (except for violation) are the same. In 0.1% of stops,
  the max span between timestamps is more than 60 minutes. In those cases it
  looks like the same officer stopped the same individual more than once in the
  same day.   
- Only citations have `Ethnicity`, which only provides information on whether
  the driver is Hispanic. We therefore exclude Iowa from our main analysis
  because race data is lacking. 
- Only (some) citations have county, the warnings only have trooper district.
  The mapping for the districts is provided in the resources folder. Counties
  were mapped by comparing the identifiers in the `LOCKCOUNTY` field with the
  cities in the `LOCKCITY` field.
- The codes in the county field represent counties ordered alphabetically.
- Additional columns in the raw data that may be of interest: `EQUIPVIOL` 
  (free field -- usually a two-digit code, but some text descriptions of
  the violation), `SCHEDULEDFINE`, `SURCHARGE`, `TOTALCOST`, along with a 
  bunch of columns that are >=99.9% NA, many of which have prefix "DISP" and
  pertain to data that would happen post-arrest.
)

## Idaho Falls, ID
**Data notes**:
- Race and gender are not on the ID driver's license and filled in only rarely,
  subject age is also 100% null
- There is 'reptspec' data, but the values are extrenely vague, i.e. "PAST",
  "SATURATION", "PERSON", "OTHER AGENCY",
- There are 6 more months of data unprocessed with the main files since they
  are of a completely different format, but are available upon request
- The data is missing demographic information as well as search/contraband
  information
- It's unclear whether there are duplicates, since officerid is 0 sometimes and
  there is no demographic information

## Statewide, IL
**Data notes**:
- The data is very messy. The presence and meaning of fields relating to search
  and contraband vary year by year. Caution should be used when inspecting
  search and hit rates over time. We exclude Illinois from our time trend
  marijuana analysis for this reason. 
- We only process statewide data from 2012 to 2017. We received data back to
  2004, but chose not to process it due to format issues and relevance.
- For state patrol stops, there is mostly no information on the county of the
  stop. Instead, stops are mapped to districts (see the district column), which
  have a one-to-many relationship with counties. See the relevant map
  [here](http://www.isp.state.il.us/districts/districtfinder.cfm). There is one
  district (#15) with a lot of stops that does not directly map to counties, as
  it refers to stops made on the Chicago tollways. We use districts in our
  analysis. 
- Counties for local stops could be mapped by running the police departments 
  in the AgencyName field through Google's geocoder.
- The `search_type_raw` field is occasionally "Consent search denied", when a
  search was conducted. This occurs because the search request might be denied
  but a search was conducted anyway. Many searches have missing search type
  data, so we do not rely on `search_basis` when analyzing Illinois searches.
- Race (`raw_DriverRace`) mapping:
    * 1 = White
    * 2 = Black
    * 3 = American Indian or Alaska Native
    * 4 = Hispanic
    * 5 = Asian
    * 6 = Native Hawaiian or Other Pacific Islander
- Outcome (`raw_ResultOfStop`) mapping:
    * 1 = Citation
    * 2 = Written Warning
    * 3 = Verbal Warning (stop card)
- We also pull through raw columns `raw_ReasonForStop` and
  `raw_TypeOfMovingViolation` to populate the `reason_for_stop` and `violation`
  columns in the clean data. We received dictionaries to help do so.
- Note that IL contains state patrol and municipal police departments, but we
  use only the state patrol data in our anlaysis. There are occasional issues
  with some of the municipal P.D. data to watch out for: for example, the 
  search and contraband data is fairly detailed and robust, except for Chicago
  Police, which has lots of NAs for search info (in 2012-2013) and lots of NAs
  for contraband info (in 2014). We do not alter these NA values, 
  but recommend looking more closely into the Chicago city data (see below)
  rather than using the data given to us through the state records request.
- Additional columns in the raw data that may be of interest: IL has really
  detailed search/contraband information. There are about 40 raw columns with
  search/contraband info; they fall into four categories `Vehicle*`, `Driver*`,
  `Passenger*`, and `PoliceDog*`, where `*` delineates things like what type 
  of contraband was found or how much contraband was found, whether consent was 
  requested, whether consent was given, who performed the search, etc. 

## Chicago, IL
**Data notes**:
- Dataset is created by joining arrests and citations on date, hour, officer
  name, and location
- There may be duplicates, but there is often insufficient information to
  deduplicate, i.e. the time resolution is hourly driver_race is null 99% of
  the time, and officer ID appears to be only a prefix of the full ID ~0.3% of
  the time
- Data includes warnings and arrests, but is missing warnings
- violation represents statute_description in the raw data
- subject_race is based on raw columns race and driver_race, which are passed
  through

## Fort Wayne, IN
**Data notes**:
- Roster.csv (police officer info) is available in raw data, but
  doesn't join cleanly to stops data; first names are often truncated and
  nicknames are used, i.e.  Manny vs Manuel; it can be loaded and reviewed
  upon request.
- Data is missing search/contraband information, as well as demographic
  information
- disposition represents Description in the raw data; outcomes are derived from
  this column

## Wichita, KS
**Data notes**:
- Data is deduplicated on raw columns citation_date_time, citation_location,
  defendant_first_name, defendant_last_name, defendant_age, defendant_sex, and
  defendant_race, resulting in ~4.1% fewer records
- Data is missing search/contraband fields
- citation_number in the raw data doesn't appear to be unique. i.e. citation
  "07M000645" is associated with two different dates, locations, and people
- Only citations are included
- violation represents charge_description in the raw data
- disposition represents charge_disposition in the raw data
- subject_race is based on the raw columns defendant_ethnicity and
  defendant_race, which are passed through

## Louisville, KY
**Data notes**:
- While we have raw csvs for all citations, we keep only those records that
  join onto the stops data; the source of this data is here:
  https://data.louisvilleky.gov/dataset/uniform-citation-data
- Data is deduplicated on raw columns officer_gender, officer_race,
  officer_age_range, activity_date, activity_time, activity_location,
  activity_division, division, activity_beat, beat, driver_gender, persons_sex,
  driver_race, persons_race, persons_ethnicity, driver_age_range, person_age,
  persons_home_city, persons_home_state, person_home_zip, reducing the number
  of rows by ~%
- subject_race is based on the raw column driver_race, since it is null 0.03%
  of the time compared to 18.6% for persons_race and 18.60% for
  persons_ethnicity; all are passed through with raw_ prefix
- violation represents raw column charge_desc
- All stops are not null for at least one of the driver_* columns or
  number_of_passengers or was_vehicle_searched columns, implying all stops are
  vehicular
- location used for geocoding is activity_location, which had a lower null rate
  than citation_location, but the latter was passed through as
  raw_citation_location
- subject_age is based on persons_age from the citation data, although it is
  null more often than driver_age_range; the latter, however, only gives a
  range, so couldn't be use for this column; it is passed through though as
  raw_driver_age_range
- search_conducted is based on was_vehcile_searched, which is passed through as
  raw_was_vehcile_searched (sic); there were 3 NAs that were coerced to false
  under the assumption that the officers may simply not have recorded the
  absence of a search
- search_basis was based on reason_for_search; k9 searches matched the pattern
  "K9|K-9|DOG", plain view searches matched anything mentioning plain
  view/smell or anything that could be seen in plain sight and matched the
  following pattern "BAGGIES|DRUGS|GUN|MARIJUANA|ODOR|PILLS|PIPE|PLAIN
  VIEW|SMELL", consent matched "CONSENT|CONSE", probable cause matched
  "PROB|P/C|PC|P.C.", and everything else was classified as "other"; this was
  verified to be accurate for 99.8% of entries; the long tail was not checked,
  but anyone viewing the data can see the original values in the
  reason_for_search column
- data is lacking explicit contraband information, but some of this can be
  inferred from reason_for_search
- frisk_performed is true with reason_for_search matches the pattern "TERRY|PAT",
  it is false otherwise (NA and no match)
- 2018 has data only from January

## Owensboro, KY
**Data notes**:
- There is a list_of_officers.csv as well as the excel spreadsheet
  (preferable given the formatting) that have more officer information
  available upon request
- Data is missing search/contraband information
- Data is all citations, although it appears to include an arrest indicator as
  well, when that also occurred
- Provided longitude is lacking the negative sign, which we add (without which
  all points are in central China)
- subject race is based on RACE in the raw data and passed through as raw_race;
  data does not include Hispanic.
- violation is a concatenation of `Violation Description X` where X is 1 to 9
- type is based on `Violation Description 1`
- 2015 and 2017 only have data for part of the year

## New Orleans, LA
**Data notes**:
- Data is deduplicated on EventDate, BlockAddress, and SubjectID, which reduces
  the number of rows by ~0.07%
- Addresses were partially anonymized by the department replacing the last two
  numbers of the address number with XX; these were replaced with 00 so we
  could at least geocode the block level address
- search_conducted is true when the ActionsTaken includes "Search Occurred: Yes",
  and it's false when that is not present or the ActionsTaken column is NA,
  under the assumption that NA is equivalent to "Stop Results: No action
  taken"
- reason_for_stop is StopDescription in the raw data; type is based on this
  column
- outcomes, search, and contraband fields are all based on the ActionsTaken
  column, which is passed through as raw_actions_taken; NA in this column is
  assumed to be 'no actions taken'
- subject_race is based on SubjectRace raw column, which is passed through as
  raw_subject_race
- data before 2010 is sparse and unreliable so it is removed from the clean
  dataset
- 2018 only has partial data

## Statewide, MA
**Data notes**:
- The search and outcome fields are inconsistent. We take the most progressive
  interpretation: if one of `SearchYN`, `SearchDescr` or the outcome columns
  indicates that there was a search, we label them as such.
- While we define a contraband_found column in case it is useful to other
  researchers, it is sufficiently messy (there are multiple ways you might
  define `contraband_found`, and they are quite inconsistent) that we exclude
  it from our contraband analysis.
- In <1% of the data, `RsltSrchNo` and `RsltSrch<contraband type>` conflict.
  In these cases, we use the value from `RsltSrchNo`.
- Violation data is not very granular.
- Counties were mapped by running the cities in the `CITY_TOWN_NAME` field
  through Google's geocoder.
- There are only a handful of stops in the data before 2007; we drop those
  years as they are clearly unreliable. It appears that the first few months
  (nearly half) of 2007 are also incomplete, but we have not attempted to remove
  the incomplete months.
- `subject_race` was mapped from `raw_Race`
- Additional columns in the raw data that may be of interest: `SpecialEvent`
  (GHSB Speed Detail, Road Block, Blue Blitz; 99% NA), `PlateReader` (boolean),
  `OwnTruckPass` (O, W, T, P)

## Baltimore, MD
**Data notes**:
- Data is missing search/contraband information as well as demographic
  information and outcomes other than citations
- The primary key seems to be a combination of Ticket and Citation Number; when
  Ticket is null, Citation Number isn't and vice versa; both are duplicated
  across rows, so we deduplicate on those two IDs coalesced, resulting in
  ~0.01% fewer records
- Data lacks translations for `Ordinance Code` and `Citation Type`
- Violation data is almsot all null

## Statewide, MD
**Data notes**:
- The data is very messy. It comes from three different time periods: 2007,
  2009-2012, 2013-2014. They all have different column and slightly different
  conventions of how things are recorded. We attempted to standardize the
  fields as much as possible.
- Time resolution of the data varies by year. Prior to 2013, data is reported
  annually. From 2013 onward, data is reported daily. So stop dates prior to
  2013 are not precise to the nearest day and are just reported as Jan 1. 
- Counties could theoretically be mapped by running the police departments in 
  the `Agency` field through Google's geocoder, but this does not work for 
  state patrol stops, for which we have no county information. Maryland's
  data is not good enough for us to include in our analysis, so we chose not
  to do this.
- `subject_race` is mapped from `raw_Race`.
- `outcome` and `arrest_made` are mapped from `raw_Outcome` and `raw_Arrest Made`;
  see processing script for details.
- `search_basis` is a cleaned up version of `reason_for_search` which is a free
  field populated by raw column `Search Reason`. 
- Prior to 2013, there are quite a few NAs for contraband; we do not cast
  these to false because it seems to be too many to assume they're all false --
  it feels more believable that there is actual missing data in these annually
  reported, messy datasets.
- Additional columns from the raw data that may be of interest: `Duration of Search`

## Statewide, MI
**Data notes**:
- The original data had some unquoted fields (`VoidReason` and `Description`)
  which had commas in them. We manually fixed these with a python script, which
  can be found in the `/scripts` folder.
- Driver race data has more than 50% missing data, so we excluded Michigan from
  the analysis in the paper.
- The codes in the `CountyCode` field represent counties ordered
  alphabetically.
- Rows represent violations, not stops, so we remove duplicates by grouping by
  the other fields.
- Michigan data has loads of additional columns, a cluster we find very 
  interesting are `SpeedPosted` (pulled through as `posted_speed`), 
  `SpeedDetected` (pulled through as `speed`), and `SpeedCharged` (pulled
  through as `charged_speed`). Most places with speeding information give just
  speed and posted speed; analyses like the [bunching analysis](http://www.princeton.edu/~fmg/JMP) try to infer the true speed, and 
  whether drivers of different races were discounted at different rates. 
  Michigan's transparency about discounting (from detected speed to charged speed)
  could make this process much easier to analyze. However, we do not do so because
  race information is insufficient. 
- Since all rows have a `TicketNum`, we assume that if any ticket is
  not a warning, then it is a citation.  But then potentially for outcome,
  anything that is not an arrest or warning could have a court summons.
  It's possible raw data columns `Felony`, `Misdemeanor`, `CivilInfraction`
  could help disambiguate.
- Additional raw data columns that may be of interest: Michigan has over 160 
  columns in the raw data, though many of them are >99.9% NA. There are ID columns
  for everything from violation codes, citation codes, infraction codes, incident
  numbers, court code, etc. Other columns: `VehicleImpounded`, `Injury`,
  `Felony`, `Misdemeanor`, `CivilInfraction`.

## Saint Paul, MN
**Data notes**:
- Data is deduplication on `DATE OF STOP`, `RACE OF DRIVER`, `AGE OF DRIVER`,
  `GENDER OF DRIVER`, and `POLICE GRID NUMBER`, resulting in ~0.02% fewer
  records
- Data is lacking contraband and location information
- If a citation was not issued, it's unclear whether a warning was issued or
  something else
- subject_race is based on `RACE OF DRIVER` in the raw data, which is passed
  through as raw_race_of_driver
- search_conducted is based on `VEHICLE SEARCHED?`; "No Data" is assumed to be
  false because it is likely that "No Data" is an autofill value for NA, which
  we coerce to false elsewhere under the assumption that officers sometimes
  don't record the absence of a search; the same is done for frisk_performed

## Statewide, MO
**Data notes**:
- The original data was aggregated. There is detail on a number of fields (age,
  stop purpose, outcome) that is not usable as it is not cross-tabulated with
  the other fields.
- Because this is aggregate data, stop date is only precise to the nearest
  year, and is recorded as Jan 1 for all stops. 
- Note that the `location` column comes from the department's work location,
  which is coarse; and highway patrol stops thus all get mapped to Jefferson 
  City. 

## Statewide, MS
**Data notes**:
- Counties were mapped using the dictionary provided, which is added to the raw
  data folder. Counties are numbered alphabetically.
- There is no data on Hispanic drivers, so we exclude Mississippi from our main
  analysis. 
- `subject_race` was mapped from `raw_race`.
- `violation` was populated with raw column `acd`.
- Additional columns in the raw data that may be of interest: `acdoos` and `aamva`
  have alpha-numeric codes like `acd` (i.e., `violation` in the clean data),
  `acdsev` (0-3; NA for 65%), `acc` (boolean), `court` (mostly MUN or JUS), 
  `elect` (E or NA), `disp` (G, P, D, S, N), `fine`.

## Statewide, MT
**Data notes**: 
- `subject_race` was mapped from `raw_Ethnicity` and `raw_Race`.
- `search_conducted` and `search_basis` were mapped from `raw_SearchType`.
- `violation` is a concatenation of `Violation[1-3]` from the raw data.
- `stop_outcome` is derived from raw columns `EnforcementAction[1-3]`, see
  processing script for details.
- `reason_for_stop` is populated from raw column `ReasonForStop`.
- Additional columns in the raw data that may be of interest: 
  `VehicleIsCommercial`, `VehicleIsMotorcycle`, `ViolationDescription` (which
  gives a bit more detail than the violation columns we pull through into the
  clean data), `ViolationUnlawfulSpeed` (boolean), `AggressiveDriving` (boolean),
  `FaultyOtherDescription` (free field description of equipment violations),
  `WarningOtherViolations[1,2]` (free field description of warning), 
  `WarningsThisRecord` (0-3, indicating how many warnings were given), 
  `CitationsThisRecord` (0-3 indicating how many citations were given),
  `EnforcementAction[1-3]` (gives slightly more detail than `stop_outcome`, 
  e.g., misdemeanor arrest vs felony arrest).

## Raleigh, NC
**Data notes**:
- Data is pulled out of Statewide, NC data, so refer to that for processing
  documentation
- Missing data 2/2004, 2/2005, 5/2005, 10/2005, 11/2005, 3/2006,
  8/2006, 4/2007, 11/2008, 1/2009, 11/2012, 9/2013, 11/2013, 7/2014, 10/2014,
  10/2015

## Statewide, NC
**Data notes**:
- Stop time is often unreliable — we have a large overdensity of 00:00 values,
  which we set to NA. 
- Attempting to deduplicate on StopDate, OfficerId, StopLocation, StopCity,
  PersonID, Age, Gender, Ethnicity, and Race reduced rows by 0%, i.e. there do
  not appear to be duplicates
- The location of the stop is recorded in two different ways. Some stops have a
  county code, which can be mapped using the provided dictionary, which is
  included in the raw data. Other stops are only labeled with the state patrol
  district. Some districts map directly onto counties, in which case we label
  the stop with that county. However, some districts cover multiple counties.
  Stops in these districts can thus not be unambiguously mapped to a single
  county. In both cases, district of the stop is provided in the "district"
  column, providing coarse location data for the vast majority of stops.
- Action is sometimes "No Action" or a similarly minor enforcement action even
  when `DriverArrest` or `PassengerArrest` is TRUE. In these cases, we set
  outcome to be "Arrest" because the outcome field represents the
  most severe outcome of the stop.
- There can be multiple search bases per stop-search-peron, so we collapse them
  into a single value
- There is a 1:N correspondence between StopID and PersonID, so we filtered out
  passengers when joining demographic information to stop data to prevent
  duplicates; this also means that the demographic information pertains to the
  driver
- When joining search data onto the stop data, the data is joined by StopID
  only and not also PersonID, since the person searched could be either the
  driver or passenger; this means that the search data may be of either the
  driver or the passenger, and in 3.6% of cases, it was actually the passenger
  who was searched, but search_conducted is true in either case; fortunately,
  there is a 1:1 correspondence between StopID and and SearchID, as well as
  between SearchID and PersonID (who, again, can be either the driver or
  passenger) and SearchID and ContrabandID 
- subject_race is based on Ethnicity and Race, which are passed through as
  raw_*
- outcomes are based on `raw_action_description`, which is based on the raw column
  Action and translated given the provided codes
- frisk and search data is based on SearchID and search_type_description, which
  is passed through with raw_*; the latter is based on the raw column
  SearchType and translated using the given data dictionary
- stop_purpose_description is based on raw column StopPurpose and is
  translated using the given data dictionary and passed through as
  `reason_for_stop`
- `reason_for_search` represents the raw column Basis
- Additional columns in the raw data that may be of interest:
  `Ounces`, `Pounds`, `Kilos`, `Grams`, `Dosages`, `Weapons` provide 
  greater resolution on contraband; `Gallons`, `Pints`, `Money`,
  `DollarAmt` may also do so; `EncounterForce` (boolean), `EngageForce`
  (boolean); `[Officer,Driver,Passenger]Inury` (all booleans)

## Winston-Salem, NC
**Data notes**:
- Data is pulled out of Statewide, NC data, so refer to that for processing
  documentation
- Missing data 8/2014, 1/2015, 2/2015, and 5/2015

## Greensboro, NC
**Data notes**:
- Data is pulled out of Statewide, NC data, so refer to that for processing
  documentation
- Missing data 8/2015, 11/2015, 11/2016, and 3/2014

## Durham, NC
**Data notes**:
- Data is pulled out of Statewide, NC data, so refer to that for processing
  documentation
- Missing data from 2008-2013:
    - 2008 missing January data
    - 2009 missing February, April, July, September, October, December
    - 2010 missing February, November
    - 2013 missing May

## Fayetteville, NC
**Data notes**:
- Data is pulled out of Statewide, NC data, so refer to that for processing
  documentation

## Charlotte, NC
**Data notes**:
- Data is pulled out of Statewide, NC data, so refer to that for processing
  documentation

## Grand Forks, ND
**Data notes**:
- Data is deduplicated on raw columns agency, date, time, sex, race, age,
  ht_ft, ht_in, house, and street, reducing the number of records by ~14.2%
- Many of the offenses fall into categories other than obvious pedestrian or
  vehicular stops, i.e. BARKING DOG, and are encoded as NA for type, but
  the description is provided in reason_for_stop
- The department says that arrest, search, and contraband are not recorded with
  stop data
- There are unidentified spikes that are relatively large every year in late
  May or early June, i.e. 2010-05-08, 2011-06-02, 2012-05-05, 2013-05-04,
  2014-05-10, 2015-05-09, 2016-05-20; it's unclear what these correspond to and
  the PD has not yet responded to our inquiry
- subject_race is based on raw_race, which is passed through; the data does not 
  appear to include Hispanic.

## Statewide, ND
**Data notes**:
- The data contain records only for citations, not warnings.
- Rows represent individual citations, not stops, so we remove duplicates by
  grouping by the other fields.
- The `violation` field is populated by citation codes and their descriptions.
- `subject_race` is mapped from `raw_Race`.
- Note that deduping by violation_date_time, Age, sex, Race, county_name,
  street_cnty_rd_location, desc_of_area, highway, ref_point reduces rows by
  ~16.6%.

## Statewide, NE
**Data notes**:
- The original data was aggregated. It was grouped by stop reason, outcome and
  whether there was a search separately. Therefore, it is not possible to cross
  tabulate them together. We only use the last grouping.
- State and local stops are mixed together, identifiable by the `raw_dept_lvl`
  field. We map levels 1, 5, 9, 10, 11 to "Nebraska State Agency" in the 
  `deparment_name` field; for the other levels, we fill `department_name` with
  `raw_dept`. Note that levels 1, 2, and 3 are state patrol, local P.D. and 
  sheriff P.D.s, respectively; levels 5-12 are special agencies or sectors of
  some sort; there are no stops for level 4.
- The data is by quarter, not by day. So all stop_dates are the first date of
  the quarter.
- There is a strange jump (Q1) and then dip (Q2–4) in the data for 2012. This
  stems from all state patrol stops for 2012 being recorded as happening
  in the first quarter. Municipal departments seem to have okay dated data for
  2012.

## Statewide, NH
**Data notes**:
- The `driver_race` field was populated by hand-written codes that we manually
  decoded. They are prone to mislabeling and should be used with caution only.
  Also, a very high percentage of stops (>30%) are missing race data entirely.
  We map the most common codes, covering more than 99% of stops with data, but
  we do not interpret the long tail of misspellings because many of them are
  ambiguous, we do not want to make assumptions, and it does not significantly
  improve the data. We exclude this dataset from our analysis because it has
  too much missing race data. 
- We determine stop outcome (citation, warning, etc) using 
  `raw_CITATION_RESPONSE_DSC`, and we determine subject_race from `raw_RACE_CDE`.
- The driver_age field was not populated for the 2014.2 dataset.
- Rows represent violations, not stops, so we remove duplicates by grouping by
  the other fields.

## Statewide, NJ
**Data notes**:
- New Jersey data may be updated: we still
  have a number of questions we are waiting on the state to answer. 
- New Jersey uses sofware produced by [LawSoft
  Inc.](http://www.lawsoft-inc.com). There are two sets of data: CAD (computer
  aided dispatch, recorded at the time of stop) and RMS (record management
  system, recorded later). They have almost completely disjoint fields, and
  only RMS records have information on searches. We believe the data from the
  two systems should really be joined, but according to the NJSP there is not a
  programmatic way to do so. Therefore, we process the CAD data fully, which
  appear to be the dataset which corresponds to traffic stops. We did noticed 
  that you could join the RMS file if you combine a few of the fields in a certain 
  way. This method isn't perfect, and there are lots of nulls; but we include it
  in hopes that some data is better than no data.
- Becuase of the above, we only know search/frisk/contraband information in
  about 13% of stops.
- In the CAD data, there are often multiple rows per incident. Some of these
  are identical duplicates, which we remove. For the remaining records, we
  group by `CAD_INCIDENT`, because the NJSP told us that each `CAD_INCIDENT` ID
  refers to one stop. We verified that more than 99.9% of `CAD_INCIDENT` IDs
  had unique location and time, implying that they did, in fact, correspond to
  distinct events. 
- `driver_race` and `driver_gender` correspond to the race of the driver, not
  the passenger. 
- Statutes are mapped using the [traffic
  code](http://law.justia.com/codes/new-jersey/2013/title-39), where possible.
- The CAD records contain `TOWNSHIP` which could be mapped to a county by 
  running the values through the Google geocoder. 
- Additional raw data columns that might be of interest (note, these are
  only in 13% of data since they come from the spotty, impossible matching
  described above): `Sobriety Test`, `CCH Check`, `NCIC Check`, `Warrant Check`,
  `Warrant`. Note that since we do not have a guarantee that these 13% of rows
  with data are a random or representative sample, we do not recommend drawing
  conclusions from this information.

## Camden, NJ
**Data notes**:
- Data is deduplicated on case_number, Incident Datetime, IncidentLocation,
  OfficerName, SubjectGender, Race, Ethnicity, DateOfBirth, VehicleYear, Color,
  Make, and Model, reducing the number of records by ~5.4%;
- Data does not contain search/contraband fields
- There are 3 CFS_Codes, TRAFFIC STOP, PEDESTRIAN STOP, and freeform text,
  which is classified as vehicular since most reference a driver or traffic
  stop situation
- It appears as though Camden police often classify hispanics as white, since
  the stop rate for whites is extremely high and there are no stops for
  hispanics
- According to the PD, a "summons" is a citation, so that corresponds to
  citation_issued in this data
- outcomes are based on the disposition column
- subject_race is based on Race and Ethnicity, which are passed through as
  raw_race and raw_ethnicity

## Henderson, NV
**Data notes**:
- Data is deduplicated on raw columns location, city, state, zip, off_dt,
  off_ti, dob, ht, sex, wt, eye, hair, make, ofcr_id, reducing the total number
  of records by ~2.1%
- violation is a concatenation of offense_1 and offense_2 in the original data,
  separated by "|"
- Missing reason_for_stop/search/contraband information
- 2012 has no or very little data for July, August, and September, we have an
  outstanding inquiry as to why
- 2018 only has partial data
- Data before 2011 is filtered out since 2010 data is so sparse it appears to
  be recording error
- One of the files, `Traffic Stops 01-01-11 to 05-30-18.xlsx` came corrupted,
  we are attempting to get a clean copy of this
- We assume these are all citations since the primary raw key appears to be
  'cite', although we have an outstanding inquiry to confirm this 
- subject_race is based on raw column race, which is passed through as raw_race

## Statewide, NV
**Data notes**:
- Nevada does not seem to record Ethnicity or have any records of Hispanic
  drivers, so we exclude it from our analysis. 
- Nevada does not record time of stop, making it ineligible for VOD analysis.
- The violation field is a concatenation of two fields in the raw data:
  infraction codes and offense description.
- Additional columns in the raw data that may be of interest: `Citation Number`.

## Statewide, NY
**Data notes**:
- The data include only citations.
- There is no data on searches.
- The data stops at 2017-12-14.
- `subject_race` is mapped from a raw data column which was passed through as
  `raw_RACE`.
- `location` is simply a concatenation of three raw data columns:
  `VIO_STREET`, `HWY_NUM`, `HWY_TYPE`.
- Additional columns in the raw data that may be of interest: `LAW_SECTION`,
  and `DCJS_CODE` (we do, however, provide `violation` in the clean data,
  which is called `LAW_DESCRIPTION` in the raw data, and appears to simply
  be the human readable description of `LAW_SECTION` and `DCJS_CODE`).

## Albany, NY
**Data notes**:
- Data is deduplicated on incident, mapinfo_lo, date, dob, sex, and race,
  reducing the number of records by ~28%
- Search/contraband information is missing, as well as outcomes
- subject_race is based on the raw column race, which is passed through as
  raw_race
- violation represents raw column crime_code_A, which is a description of
  alphanumeric crime_code column

## Columbus, OH
**Data notes**:
- `Incident Number` in the original data seems unreliable as it has several
  hundred entries for 9999 and 99999; furthermore, occasionally, it does
  appear to reference the same incident, but is duplicated for every
  distinct action taken against the subject
- The raw data is deduplicated on `Stop Date`, `Contact End Date`, Ethnicity,
  Gender, ViolationStreet, and ViolationCrossStreet, reducing the number of
  records by ~15.8%
- search_conducted and outcome are based on `Enforcement Taken`, which is
  passed through as raw_enforcement_taken

## Statewide, OH
**Data notes**:
- The stop_purpose field is populated by infraction codes. The corresponding
  laws can be read [here](http://codes.ohio.gov/orc/).
- There is no data for contraband being found, but a related field could
  potentially be reconstructed by looking at searches involving drugs and an
  arrest. We mark contraband_found as TRUE for drug-related arrests (extracted 
  from `raw_ORC_STRING`, but we cannot determine if the remainder are FALSE or
  simply some other type of contraband was recovered).
- Counties were mapped using the provided dictionary, which is included in the
  raw data folder.
- We cannot find disposition codes (in `DISP_STRING`) which clearly indicate
  whether a citation as opposed to a warning was given, although there is a
  disposition for warnings.
- The data contains stops of both type TS and TSA, standing for "traffic stop"
  and "traffic stop additional". The latter have a higher search rate and tend
  to have additional information (i.e., `ASINC_STRING` is not NA). We include
  both types in analysis, as they do not appear to be duplicates (addresses and
  times do not match) and we do not have a clear reason to exclude either. 
- While there is data on search types, they only include consent and K9
  searches, suggesting a potential difference in recording policy (many other
  states have probable cause searches and incident to arrest searches, for
  example).
- `officer_id` refers to a single officer throughout their tenure on the state
  patrol, but it is re-assigned to a new trooper upon an officer's retirement.
- `raw_DISP_STRING` is used to determine subject race, sex, stop outcome, and
  search information. See processing script for mappings.
- Violations were mapped from `raw_ORC_STRING`.
- 2017 data has a slightly different format: information from DISP_STRING and 
  ORC_STRING exist in `raw_DISPOSITIONS` for that year.
- Additional columns from raw data that may be of interest: `ASINC_STRING`

## Cincinnati, OH
**Data notes**:
- Data filters out passengers and where sex is "NON-PERSON" (i.e. business)
- Data is deduplicated on instance_id, interview_date, address_x, sex, race,
  and age_range_cid, which reduces the number of rows by ~56%
- Addresses are "sanitized", i.e. 1823 Field St. -> 18XX Field St.  since 83%
  of given geocodes in the raw data are null, we replace X with 0 and get
  approximate geocoding locations
- Data before 2009 is removed since it is so sparse it is likely not to be
  trusted, and 2018 only has partial data
- reason_for_stop represents incident_type_desc in the raw data
- outcomes are based on raw column actiontakencid, which is passed through as
  raw_action_taken_cid
- type is based on field_subject_cid, which is passed through as
  raw_field_subject_cid
- subject_race is based on race, which is passed through as raw_race
- There are zero stops of Hispanic individuals reported after 2010.

## Oklahoma City, OK
**Data notes**:
- Data is deduplicated on raw columns violDate, violTime, violLocation,
  DfndRace, DfndSex, and DfndDOB, reducing the number of records by ~15.7%
- Partial data from before 2011 is filtered out, although early 2011 still
  seems to have missing/partial data; the last few months of 2017 are also
  missing
- Search/contraband information is missing
- subject_race is based on DfndRace, which is passed through as raw_dfnd_race;
  though the data do not include classification of drivers as Hispanic.

## Tulsa, OK
**Data notes**:
- Data is deduplicated on raw columns violationdate, violation_location,
  officerdiv, race, and sex, reducing the number of records by ~30.0%
- Data is all citations
- Data appears to be all vehicular, although the PD hasn't confirmed that yet
- subject_race is based on raw column race, which is passed through as raw_race

## Statewide, OR
**Data notes**:
- There is basically no data, including no data on Hispanic drivers, so we
  exclude Oregon from our analysis.
- Counts for 2015 and 2016 are much lower than in earlier years. 
- subject_race is mapped from `raw_Race`

## Philadelphia, PA
**Data notes**:
- Data is deduplicated on raw columns datetimeoccur, location, districtoccur,
  lat, lng, gender, age, race, stoptype, individual_frisked,
  individual_searched, individual_arrested, individual_contraband,
  vehicle_frisked, vehicle_searched, vehicle_contraband, reducing the number of
  records by ~1.4%
- Information on citations and warnings is missing, but arrests are included
- search_person and search_vehicle correspond to raw columns
  individual_searched and vehicle_searched; we filled in false for NA values
  under the assumption that unrecorded search data represented the absence of a
  search
- contraband_found is based on raw columns individual_contraband and
  vehicle_contraband, which are passed through as raw_*; if both of these were
  null and search_conducted was true, contraband_found was set to false
- subject_race is based on the raw column race, which is passed through as
  raw_race
- 2018 has only partial data, and it appears to be the same for early 2014

## Pittsburgh, PA
**Data notes**:
- The raw data for pedestrian stops actually has many cities in it, but here we
  filter to only Pittsburgh; vehicular stops do not have an associated city,
  and so are assumed to be only Pittsburgh
- Raw data for vehicle stops has stop end time as well
- There are instances when evidencefound is true but contrabandfound is NA, so
  we have an oustanding inquiry as to what evidencefound refers to; similarly,
  weaponsfound is sometimes true when contrabandfound is false and vice versa,
  so it's unclear whether the contraband is weapons or not, so for now we leave
  out contraband_weapons and have another outstanding inquiry
- if a search was conducted and the stop type was vehicular (pedestrian stops
  don't provide search outcomes) and contrabandfound was NA, we set
  contraband_found to false, otherwise we use the value in the contrabandfound
  field. We do this under the assumption that false and NA for contraband_found
  are equivalent when a search occured, i.e. an officer conducted a search and
  either found nothing or recorded nothing
- search_conducted is true when any one of objectsearched (pedestrian stops),
  contrabandfound, evidencefound, weaponsfound, and nothingfound (vehicular
  stops) is not NA; all these are passed on as raw_*
- Sex and gender do not match 73% of the time in pedestrian data, and race and
  ethnicity mismatch often as well. In both cases, if sex != gender or race !=
  ethnicity, we set the value to NA, otherwise we coalesce(sex, gender) or
  coalesce(race, ethnicity) [this keeps values when one is NA but the other
  isn't]; we pass through all the raw values as raw_*
- There are 4 zone-related columns in the raw data: zone, zone_division,
  policezone, and officerzone; we pass them through as raw_*
- The data is deduplicated on raw columns stop_date, stopstart, stopend,
  address, officer_id, and person_id, reducing the number of rows by ~21.1%
- violation represents raw column crimedescription
- 2008 and early 2009 appear to have partial data and 2018 only has the first 4
  months

## Statewide, RI
**Data notes**:
- The stops are mapped to state patrol zones, which represent police barrack
  juridisdiction areas. However, there is no simple mapping between zones and
  counties. We store state patrol zones in the `district` column and use this
  column in our granular location analyses. 
- contraband information was mapped from `raw_SearchResult[One/Two/Three]`. 
- Column `search_basis` is a standardized version of `reason_for_search`, which, 
  if multiple reasons are provided, uses the hierarchy of: plain view, probable 
  cause, other. And if no search reason is given, we default to probable cause.
  Note that while the raw data contains a `ConsentRequested` column, we have no
  information about whether consent was given.
- Additional columns in the raw data that may be of interest: `SearchFrisk[One/Two/Three]`
  (says whether searches and frisks were of the driver, passenger, or vehicle),
  `Duration` (A/B/C/NA), `AdditionalOccupants`, `Road` (I/S/N/NA), `PlateType`,
  `PriorRecord` (Y/N/T/NA), `ConsentRequested`.
  

## Statewide, SC
**Data notes**:
- The `police_department` field is populated by state patrol agency.
- More data on local stops is available
  [here](http://afc5102.scdps.gov/SCDPS_Exweb/SCDPS/PublicContact/PublicContact-012).
  It is aggregated by race and age group — potentially scrapable if useful.
- While there is data on violation, many of the stops have missing data.
- Violation is a concatenation of `sectionnum` and `offensecode` in the raw data.
- Additional columns in the raw data that may be of interest (Note, many of these
- Original officer\_badge\_number is not unique, so it is hashed with the
  officer's last name and race to create officer\_id\_hash 
  were used to construct search/contraband/arrest/outcome information in the 
  clean data. See processing script for details.): `jailed`, `felonyarrest`,
  `armedwith` (messy free field), `using[drugs/alcohol]`, 
  `contraband[drugs/drugparaphenalia/weapons/other]` (sic), 
  `[passenger/subject/vehicle]searched`.

## Statewide, SD
**Data notes**:
- Race data is missing, so we exclude South Dakota from our analysis. 
- Some county names were misrecorded.
- Additional columns in raw data that may be of interest: `Eye Color`, `Insurance`,
  `Commerical Vehicle` (sic), `Is Accident`, `Haz Mat Vehicle`.

## Statewide, TN
**Data notes**:
- The data contain only citations. 
- The codes in the `CNTY_NBR` field represent counties ordered alphabetically.
- `location` is a concatenation of raw fields `UP_STR_HWY` (highway/street) and 
  `MLE_MRK_NBR` (mile marker). It would be possible to map the highway and mile 
  marker data to geo coordinates, as we did in Washington. However, since we are 
  often missing mile marker or even mile marker and highway, we did not do so 
  (as most would be NA).
- `raw_ORIG_TRFC_VIOL_CDE` maps to `violation`, `raw_CNTY_NBR` maps to 
  `county_name`, `raw_RACE_IND` maps to `subject_race`, `raw_SEX_IND` maps
  to `subject_sex`.
- Additional raw data columns that may be of interest: `SPEED`, `SPEED_LMT`, 
  `TN_RSDNT_IND` (resident boolean), `HZRD_MTRL_IND` (hazardous material boolean), 
  `MTR_CYCL_IND` (motorcycle boolean), `CNSTR_ZNE` (construction zone boolean), 
  `WRKR_PRSNT` (worker present in construction zone boolean), `TRVL_DRCT` (travel 
  direction), `ACCD_IND` (accident boolean), `CMV_IND` (commercial vehicle boolean)

## Nashville, TN
**Data notes**:
- Data is deduplicated on raw columns stop_date_time, stop_location_street,
  officer_employee_number, race, sex, and age_of_suspect, reducing the number
  of records by ~0.3%
- There are 30 (of ~2.6M records) cases where search_conducted is ambiguous
  after the merge and are left as NA, since it's unclear whether they are true
  or false, since being NA after the above merge indicates that there were two
  distinct values for raw column searchoccur
- reason_for_stop and violation are both translations of the original stop_type
  column; this column is sometimes the pretextual reason for the stop and does
  not always represent what the individual was ultimately cited for
- contraband_drugs is raw column drugs_seized, contraband_weapons is
  weapons_seized, and contraband_found is evidenceseized
- citation_issued is derived from traffic_citation_issued and
  misd_state_citation_issued, which are passed through as raw_*;
  misd_state_citation_issued is sometimes NA, so for the purposes of defining
  citation_issued, we consider NA to be false
- warning_issued is derived from verbal_warning_issued and
  written_warning_issued, which are passed through as raw_*;
  written_warning_issued is sometimes NA, so for the purposes of defining
  warning_issued, we consider NA to be false
- search_basis is based on the raw columns search_plain_view, search_consent,
  search_incident_to_arrest, search_warrant, and search_inventory, which are
  all passed on with the raw_* prefix
- subject_race is derived from raw columns suspect_ethnicity and suspect_race,
  which are passed through with the raw_* prefix
- search_person is derived from search_driver and search_passenger, which are
  passed through with the raw_* prefix
- When contraband_found is NA, we fill it with false when a search occurred,
  under the assumption that the officer simply didn't record the absence of
  contraband

## Arlington, TX
**Data notes**:
- Unclear what PRA, xCoordinate, and yCoordinate are in the raw data
- Missing data dictionaries for reason_for_stop, outcome, and search_ outcome,
  the latter two are passed through as raw_*
- subject_race is based on raw column `1st digit (Race)`, which is passed
  through as raw_1st_digit_race
- Only 2016 data was provided

## Austin, TX
**Data notes**:
- Data is deduplicated on raw column street_check_case_number, occurred_date,
  officer, sex, race, ethnicity, yob, veh_type, veh_year, veh_make, veh_model,
  veh_style, and soi, reducing the number of rows by ~0.5%
- Data does not include location or outcomes
- There are no clear pedestrian-only discretionary stops in
  reason_checked_description; SUSPICIOUS PERSON / VEHICLE is one category in
  reason_for_stop, but is included with "vehicular" stops; as such, it may over
  count vehicular stops
- reason_for_stop represents raw column reason_checked_description
- search_person and search_vehicle represent person_searched and
  vehicle_searched in the raw data, which are passed through with raw_*; for
  the canonical columns search_person and search_vehicle, NA values are changed
  to false under the assumption that the absence of a search may not always be
  recorded
- frisk_performed is based on person_search_search_based_on, and is false when
  that column is NA, on the assumption that the officer did not record the
  absence of a frisk
- search_basis is derived from person_search_search_based_on and
  vehicle_search_search_based on, which are passed through with the raw_*
  prefix
- contraband_{found,drugs,weapons} are derived from
  person_search_search_discovered and vehicle_search_search_discovered, which
  are passed through with raw_* prefix; when these values are NA, they are
  assumed to be FALSE for contraband discovery
- reason_for_stop represents the raw column reason_checked_description;
  although, the raw column street_check_description also seems to provide
  information, so is passed through with the raw_ prefix
- subject_race is based on raw columns race and ethnicity; there is also a raw
  race_description column, which is passed through with the raw_ prefix
  (instead of the race column, since it is just a nicer translation of the
  single characters in race); ethnicity is also passed through with the raw_
  prefix

## Garland, TX
**Data notes**:
- Data is deduplicated on raw columns sex, race, vehicle_year, vehicle_color,
  make, vehicle_state, incident_date, incident_time, and officer_badge,
  reducing the number of records by ~33.1%
- incident_address (location in clean) is 100% null, we have an outstanding
  inquiry here
- We assume these are all citations since they appear to be indexed by ticket
  number, but we have an outstanding task to clarify this
- violation represents offense_title in the raw data
- Data is lacking reason_for_stop/search/contraband information
- officer_race is mostly NA or "U", the remainder are white or Asian/Pacific
  Islander, so this data is probably unreliable
- subject_race is based on raw column race, which is passed through with the
  raw_ prefix
- Sometimes the same stop has different speeds recorded; often a pair
  of legitimate values, i.e. going 55 in a 40, but the others will have 0 and
  0 or NA and NA, since possibly multiple tickets are issued for the same
  stop; for each record, we take the max of each to represent the speeds; the
  raw_alleged_speed and raw_posted_speed are passed through; when the values
  were 0 or -Inf, we set them to NA under the assumption that this was a stop
  unrelated to speed
- 2012 and 2018 have only partial data

## Houston, TX
**Data notes**:
- Data is deduplicated on raw columns `Defendant Name`, Gender, Race, Street,
  Block, `Scnd Street`, `Scnd Block`, `Officer Name`, and `Offense Date`,
  reducing the number of records by ~0.02%; there is a possibility this over
  collapses rows in the case where an officer pulls over the same person twice
  in the same day at the same location
- Data is lacking search/contraband information
- Data consists only of citations
- When speed and posted_speed were 0, we set them to NA, under the assumption
  that this was a default value and the stop was unrelated to speed
- subject_race is based on the raw column Race, passed through as raw_race

## Lubbock, TX
**Data notes**:
- Insufficient information here to deduplicate records, if there are duplicates
- Missing reason_for_stop/search/contraband/subject_sex/subject_race data
- There is an outstanding ask for a data dictionary for the disposition codes

## Plano, TX
**Data notes**:
- Data is rather messy from year to year with different columns, and files with
  "all_traffic_stops" in the name are difficult to join into the other incident
  data, since the incident number in those files is populate donly ~15% of the
  time; location data is spread across 4 columns in different files, and each
  is null at least 75% of the time
- violation is a concatenation of violation_description, primary_violation,
  offense, and offense_[1-8], which are all null most of the time, the
  separator is a comma
- Data is deduplicated on date, time, location, officer_id, subject_age,
  subject_race, and subject_sex, reducing the number of records by ~0.0004%,
  but some of this may be over-deduplication because NAs are common in
  location, officer_id, and subject_age
- location is a coalesced version of the raw columns location,
  violation_location, offense_location, and arrest_location, all of which are
  ~75% null independently
- raw_results is a concatenation of officer_result, result, and result_[1-8],
  separated by a comma; outcomes are based on this column, as well as the
  warning, citation, and citation_number columns in the raw data
- search_conducted represents search_conducted, search_performed, and searched
  raw columns coalesced (they are mutually exclusive); similarly, consent in
  search_basis is based on search_consent, search_consent_2, and consent in the
  raw data, coalesced, and arrest_made is a coalesced version of arrest and
  arrested
- When the contraband and contraband_found raw columns are NA, they are assumed
  to be false or no contraband found for the canonical contraband_found column
  in the clean data

## Statewide, TX
**Data notes**:
- There is evidence that minority drivers are labeled as white in the data. For
  example, see
  [this](http://kxan.com/investigative-story/texas-troopers-ticketing-hispanics-motorists-as-white/)
  report from KXAN. We remapped the driver race field as provided using the
  2000 surnames dataset released by the U.S. Census. See the processing script
  or paper for details.
- We asked whether there was a field which provided arrest data, but received
  no clarification. There is data on incident to arrest searches, but this does
  not necessarily identify all arrests. 
- Based on the provided data dictionary as well as clarification from DPS via
  email, we classify THP6 and TLE6 in `HA_TICKET_TYPE` as citations and HP3 as
  warnings.
- The data only records when citations and warnings were issued, but not
  arrests.
- We did not receive any search information in the 2017 data.

## San Antonio, TX
**Data notes**:
- Data is deduplicated on citation_number, reducing the number of rows by
  23.3%; deduping on date, time, location, subject_race, subject_sex, and
  subject age instead reduces the number of records by 25.3%, roughly 2% more
  than only citation number, but, curiously, there are often rows that have
  identical information on those columns but different recorded speeds; so,
  it's unclear whether these are duplicates with misentries or distinct events;
  we air on the side of caution and consider them distinct events; there also
  appears to be multiple offenses related to each citation, and those not
  involving speed are set to 0; accordingly, we take the maximum speed and
  posted speed to represent the speeds for every citation/record
- Data consists only of arrests and citations
- contraband_found is based on the raw column `Contraband Or Evidence`; when
  this is NA, it is set to false under the assumption that an officer may not
  always record the absence of contraband found; the raw column is passed
  through as raw_contraband_or_evidence
- search_basis is based on the raw column `Search Reason`, which is passed
  through as raw_search_reason
- search_conducted is false when `Search Reason` is NA, "No Search", or one of
  the ~200 entries that look like incorrect entries, i.e. A, 9, 6
- subject_race is based on the raw column Race and is passed through as
  raw_race
- arrest_made is based on raw column `Custodial Arrest Made`, which is passed
  through as raw_custodial_arrest made; arrest_made true when `Custodial Arrest
  Made` is true and false when it is false or NA
- 2018 has only the first 4 months of data

## Statewide, VA
**Data notes**:
- The original data was aggregated by week.
- Some rows have an unlikely high number of stops or searches. We have an
  outstanding inquiry on this, but have not heard back. In particular, spikes
  in each week seem to usually be driven by a single officer with an unlikely
  high number of stops or searches (e.g., about 1,000 searches by an officer
  in a single week). Each spike seems to be driven by a different officer. 
  Since this reporting seems highly unlikely, we exclude VA from search analyses. 
- Counties were mapped using the provided dictionary, which is included in the
  raw data folder.
- There are no written warnings in Virginia and verbal warnings are not
  recorded, so all records are citations or searches without further action
  taken. 
- In the raw data, "Traffic arrests" refer to citations without a search.
  "Search arrests" refer to a citation and a search (either before or after the
  citation). "Search stops" refer to searches without a corresponding citation.
- Additional columns in raw data that may be of interest: officer name.

## Burlington, VT
**Data notes**:
- Data is deduplicated on raw columns issued_at, location, race, gender, city,
  dob, lat, lon, reducing the number of records by ~7.0%
- Calls are also provided in the raw data, but aren't loaded here
- subject_race is based on the raw column race which is passed through as
  raw_race, and gender is passed through as raw_gender
- reason_for_stop represents the raw column stop_based_on, and
  reason_for_search represents the raw column search_based_on and forms the
  basis for search_conducted and search_basis
- When reason_for_search, i.e. search_based_on, is NA, we assume search
  conducted is false
- outcomes are based on raw column outcome_of_stop, which is passed through as
  raw_outcome_of_stop

## Statewide, VT
**Data notes**:
- Stop purpose information is not very granular — there are only five
  categories, and we have no way of identifying speeding. See 
  `raw_stop_reason_description`.
- The search type field includes "Consent search — probable cause" and “Consent
  search — reasonable suspicion". It is not entirely clear what these mean; we
  cannot find analogues in other states.
- Counties could be mapped by running the cities in the `raw_stop_city` field 
  through Google's geocoder.
- `location` is a simple concatenation of address, city, state, zip.
- `search_conducted` was mapped from `raw_stop_search_description`.
- `contraband_found` was mapped from `raw_stop_contraband_description`.


## Statewide, WA
**Data notes**:
- Counties were mapped by doing a reverse look-up of the geo lat/long
  coordinate of the highway post that was recorded for the stop, then mapping
  that latitude and longitude to a county using a shapefile. Details are in the
  `WA_map_locations.R` script.
- Arrests and citations are grouped together in the `stop_outcome`, so we
  cannot reliably identify arrests. There is data on incident to arrest
  searches, but this does not necessarily identify all arrests.
- If one were to dedupe on employee_last, employee_first, officer_race, 
  officer_gender, contact_date, contact_hour, highway_type, road_number, milepost, 
  driver_race, driver_age, driver_gender it would yield ~3.4% fewer rows. Without
  deduping, there are a few officers who seem to stop a suspiciously high, but
  not altogether unreasonable, number of people in a an hour. However, we 
  ultimately choose not to dedupe since most of the "duplicate" rows have NA for 
  the driver demographics and other fields. 
- Weigh station stops were removed.
- `raw_enforcements` is simply a concatenation of 12 enforcement columns in the
  raw data.
- Additional columns in the raw data that may be of interest: officer name
- A `raw` enforcement value of 1 corresponds to either a citation or an arrest.
  Under the assumption that most values were citations, we set `citation_issued
  = TRUE` and `arrest_made = NA` when raw enforcement value was 1, although
  this will likely mislabel a small number of arrests.

## Tacoma, WA
**Data notes**:
- reason_for_stop is not recorded, and search/contraband information is not in
  their database, only in written reports; subject_race is also not recorded

## Seattle, WA
**Data notes**:
- citation_issued includes criminal and non-criminal citations
- violation represents raw column mir_description
- type is based on violation (mir_description) and type_description, which is
  passed through as raw_type_description
- outcomes are based on disposition, which represents raw column
  disposition_description
- vehicle_* columns are based on a coalesced combination of veh and vehcile
  (sic) columns in the raw data; this is passed through as
  raw_vehicle_description
- The officer ID associated with the raw column officer\_no\_1 is not unique,
  so it is hashed with the officer's last name to create officer\_id\_hash

## Madison, WI
**Data notes**:
- Data is deduplicated on raw columns Date, Time, onStreet, onStreetName,
  OfficerName, Race, Sex, Make, Model, Year, State, Limit, and OverLimit,
  reducing the numbe rof rows by ~0.7%
- violation represents raw column `Statute Description`
- Search/contraband information is missing
- Data only includes warnings and citations, no arrests
- If there was no `Ticket #`, this was assumed to be a warning
- Shapefiles don't include district 2 and it's accompanying sectors
- subject_race is based on raw column Race, passed through as raw_race
- 2007 has partial data and looks suspect; 2017 is missing October, November,
  and December

## Statewide, WI
**Data notes**:
- The data come from two systems ("7.3" and "10.0") that succeeded each other.
  They have different field names and are differently coded. This is
  particularly relevant for the violation field, which has a different encoding
  between the two systems; in order to map violations, we used the dictionaries
  provided by the state for both systems.
- There are two copies of the data: warnings and citations. Citations seems to
  be a strict subset of warnings, with some citation codes being different.
- The `police_department` field is populated by highway patrol agencies. There
  are only 6 of them.
- There are very few consent searches relative to other states, suggesting a
  potential difference in recording policy. 
- `raw_[individual/vehicle]Contraband` were mapped using a data dictionary 
  provided by the department: 01 = WEAPON(S); 02 = EXCESSIVE CASH;
  03 = ILLICIT DRUG(S)/PARAPHERNALIA; 04 = EVIDENCE OF A CRIME; 05 = INTOXICANT(S);
  06 = STOLEN GOODS; 99 = OTHER; 00 = NONE
- `raw_[individual/vehicle]SearchBasis` were mapped using a data dictionary.
  There is no code for "plain view". 1 = Consent; 2 = Probable Cause; the rest 
  of the search basis categories are are Warrant, Incident to Arrest, Inventory, 
  and Exigent Circumstances
- `violation` was mapped directly from `StatuteDescription` in the raw data.
- `location` is a concatenation of `raw_onHighwayDirection`, `raw_onHighwayName`,
   `raw_fromAtStreetName`, and `county_name`
- There are about 150 columns in the raw data (many columns about road
  type and conditions, many about vehicle details, etc.), however, the vast 
  majority of the columns are 95-100% empty.

## Statewide, WY
**Data notes**:
- Only citations are included in the data.
- The `department_name` field is populated by the state trooper division.
- The violation field is populated by violated statute codes.
- Rows represent citations, not stops, so we remove duplicates by grouping by
  the other fields. 
- `contraband_found` could potentially be derived from violation codes
  (drug/alcohol/weapons), but it would be less reliable and not necessarily
  comparable to how we defined contraband_found for other states, so we do not.
- `department_id` was mapped directly from `emdivision` in the raw data.
- `violation` was mapped directly from `charge` in the raw data.
- `location` is a concatenation of `raw_streetnbr`, `raw_street`, and `city`
  (and note that `city` is actually county, and is mapped to `county_name` 
  with light standardization).
- Additional columns in raw data that may be of interest: `statute`, 
  `is_acciden`.


# Changelog
- December 16th, 2019:
  - More stringent deduping logic
  - Contraband found set to FALSE when NA and search conducted is true
  - Predication correction added to metadata
  - Six more cities
- April 3rd, 2020:
  - Pulled out `raw_HA_RACE_SEX` in Texas Statewide data
  - Seattle, WA and South Carolina Statewide data had non-unique officer IDs,
    so `officer_id_hash` now hashes those original IDs with other personal
    information to create a unique hash; see `officer_id_hash` in table
    description for more information
