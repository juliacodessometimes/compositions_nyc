---
title: "DxD"
author: "Julia Bloom"
date: "January 22, 2021"
output: html_document
---





## 311 Complaint Data

Reading in dataset

```r
complaint_raw <- read.csv("311_Service_Requests_from_2010_to_Present_Dec18toDec20.csv", encoding="UTF-8", na.strings = "", row.names = NULL)
# Should be 5,212,242 obs
```


```r
head(complaint_raw)
```

```
##   X.U.FEFF.Unique.Key           Created.Date            Closed.Date Agency
## 1            41309122 01/01/2019 12:00:00 AM 01/10/2019 12:00:00 AM  DOHMH
## 2            41310910 01/01/2019 12:00:00 AM 01/01/2019 12:00:00 AM  DOHMH
## 3            41314898 01/01/2019 12:00:00 AM 01/01/2019 12:00:00 AM  DOHMH
## 4            41315045 01/01/2019 12:00:00 AM 01/03/2019 12:00:00 AM  DOHMH
## 5            41315071 01/01/2019 12:00:00 AM 01/02/2019 12:00:00 AM  DOHMH
## 6            41315216 01/01/2019 12:00:00 AM 01/16/2019 12:00:00 AM  DOHMH
##                               Agency.Name              Complaint.Type
## 1 Department of Health and Mental Hygiene                      Rodent
## 2 Department of Health and Mental Hygiene                      Rodent
## 3 Department of Health and Mental Hygiene                      Rodent
## 4 Department of Health and Mental Hygiene                      Rodent
## 5 Department of Health and Mental Hygiene                      Rodent
## 6 Department of Health and Mental Hygiene Unsanitary Pigeon Condition
##                     Descriptor                Location.Type Incident.Zip
## 1               Mouse Sighting      3+ Family Apt. Building        11373
## 2                 Rat Sighting      3+ Family Apt. Building        10459
## 3 Condition Attracting Rodents        Other (Explain Below)        11208
## 4 Condition Attracting Rodents          Commercial Building        11412
## 5               Mouse Sighting      3+ Family Apt. Building        10468
## 6                 Pigeon Waste 3+ Family Apartment Building        11694
##        Incident.Address       Street.Name  Cross.Street.1
## 1       90-34 52 AVENUE         52 AVENUE            <NA>
## 2   899 EAST 169 STREET   EAST 169 STREET            <NA>
## 3       790 ELDERT LANE       ELDERT LANE   DUMONT AVENUE
## 4                  <NA>              <NA>            <NA>
## 5   2825 CLAFLIN AVENUE    CLAFLIN AVENUE            <NA>
## 6 152 BEACH  118 STREET BEACH  118 STREET OCEAN PROMENADE
##             Cross.Street.2 Intersection.Street.1 Intersection.Street.2
## 1                     <NA>                  <NA>                  <NA>
## 2                     <NA>                  <NA>                  <NA>
## 3         LINDEN BOULEVARD                  <NA>                  <NA>
## 4                     <NA>        LIBERTY AVENUE        DUNKIRK STREET
## 5                     <NA>                  <NA>                  <NA>
## 6 ROCKAWAY BEACH BOULEVARD                  <NA>                  <NA>
##   Address.Type          City Landmark Facility.Type Status
## 1      LATLONG      ELMHURST     <NA>           N/A Closed
## 2      LATLONG         BRONX     <NA>           N/A Closed
## 3      ADDRESS      BROOKLYN     <NA>           N/A Closed
## 4 INTERSECTION  Saint Albans     <NA>           N/A Closed
## 5      LATLONG         BRONX     <NA>           N/A Closed
## 6      ADDRESS Rockaway Park     <NA>           N/A Closed
##                 Due.Date
## 1 01/31/2019 01:28:20 AM
## 2 01/31/2019 12:57:25 AM
## 3 01/31/2019 03:56:12 PM
## 4 01/31/2019 03:03:23 PM
## 5 01/31/2019 12:23:06 PM
## 6 01/31/2019 03:11:49 PM
##                                                                                                                                                                                                                     Resolution.Description
## 1 The Department of Health and Mental Hygiene will review your complaint to determine appropriate action.  Complaints of this type usually result in an inspection.  Please call 311 in 30 days from the date of your complaint for status
## 2 The Department of Health and Mental Hygiene will review your complaint to determine appropriate action.  Complaints of this type usually result in an inspection.  Please call 311 in 30 days from the date of your complaint for status
## 3 The Department of Health and Mental Hygiene will review your complaint to determine appropriate action.  Complaints of this type usually result in an inspection.  Please call 311 in 30 days from the date of your complaint for status
## 4 The Department of Health and Mental Hygiene will review your complaint to determine appropriate action.  Complaints of this type usually result in an inspection.  Please call 311 in 30 days from the date of your complaint for status
## 5 The Department of Health and Mental Hygiene will review your complaint to determine appropriate action.  Complaints of this type usually result in an inspection.  Please call 311 in 30 days from the date of your complaint for status
## 6 The Department of Health and Mental Hygiene will review your complaint to determine appropriate action.  Complaints of this type usually result in an inspection.  Please call 311 in 30 days from the date of your complaint for status
##   Resolution.Action.Updated.Date    Community.Board        BBL  Borough
## 1         01/10/2019 12:00:00 AM Unspecified QUEENS         NA   QUEENS
## 2         01/01/2019 12:59:56 AM  Unspecified BRONX         NA    BRONX
## 3         01/01/2019 04:11:05 PM        05 BROOKLYN 3042719001 BROOKLYN
## 4         01/03/2019 12:00:00 AM          12 QUEENS         NA   QUEENS
## 5         01/02/2019 12:00:00 AM  Unspecified BRONX         NA    BRONX
## 6         01/16/2019 12:00:00 AM          14 QUEENS 4162270058   QUEENS
##   X.Coordinate..State.Plane. Y.Coordinate..State.Plane.
## 1                    1019585                     208494
## 2                    1013183                     241128
## 3                    1022225                     183607
## 4                    1046613                     196294
## 5                    1011869                     257276
## 6                    1029147                     150009
##   Open.Data.Channel.Type Park.Facility.Name Park.Borough Vehicle.Type
## 1                 MOBILE        Unspecified       QUEENS         <NA>
## 2                 MOBILE        Unspecified        BRONX         <NA>
## 3                  PHONE        Unspecified     BROOKLYN         <NA>
## 4                  PHONE        Unspecified       QUEENS         <NA>
## 5                 MOBILE        Unspecified        BRONX         <NA>
## 6                  PHONE        Unspecified       QUEENS         <NA>
##   Taxi.Company.Borough Taxi.Pick.Up.Location Bridge.Highway.Name
## 1                 <NA>                  <NA>                <NA>
## 2                 <NA>                  <NA>                <NA>
## 3                 <NA>                  <NA>                <NA>
## 4                 <NA>                  <NA>                <NA>
## 5                 <NA>                  <NA>                <NA>
## 6                 <NA>                  <NA>                <NA>
##   Bridge.Highway.Direction Road.Ramp Bridge.Highway.Segment Latitude
## 1                     <NA>      <NA>                   <NA> 40.73887
## 2                     <NA>      <NA>                   <NA> 40.82847
## 3                     <NA>      <NA>                   <NA> 40.67055
## 4                     <NA>      <NA>                   <NA> 40.70524
## 5                     <NA>      <NA>                   <NA> 40.87279
## 6                     <NA>      <NA>                   <NA> 40.57830
##   Longitude                                 Location
## 1 -73.87249   (40.7388739110531, -73.87249162291612)
## 2 -73.89545  (40.82846874659817, -73.89545303526818)
## 3 -73.86311   (40.67055409879978, -73.8631053928292)
## 4 -73.77507  (40.70523868495376, -73.77507291150168)
## 5 -73.90013 (40.872794400702894, -73.90013453825375)
## 6 -73.83838   (40.5783023947916, -73.83837606412298)
```


Filtering only noise-related complaints

```r
complaint_raw$Created.Date <- as.character(complaint_raw$Created.Date)

# Dataset represents all complaints that could possibly be related to noise, tha talso have location information and date information
complaint_1 <- complaint_raw %>%
  filter(Complaint.Type=="Noise" | Complaint.Type=="Noise - Street/Sidewalk"| Complaint.Type=="Noise - Residential"| Complaint.Type=="Noise - Commercial"| Complaint.Type=="Noise - Park"| Complaint.Type=="Noise - Vehicle" | Complaint.Type=="Collection Truck Noise"| Complaint.Type=="Noise - House of Worship"| Complaint.Type=="Noise - Helicopter"| Complaint.Type=="Unsanitary Pigeon Condition"| Complaint.Type=="Rodent") %>%
  select(Created.Date, Complaint.Type, Descriptor, Location.Type, Borough, Latitude, Longitude) %>%
  drop_na(Latitude) %>%
  drop_na(Created.Date) %>%
  separate(col = Created.Date, into = c("complaint_date", "complaint_time", "complaint_AMPM"), sep = "[ ]")

complaint_1$complaint_date <- as.Date(complaint_1$complaint_date, "%m/%d/%Y")
# Should be 1,374,393 obs and 9 vars
```

Filtering out complaints before 2019 and after 2021 and converting dates

```r
# Dataset represents complaints filed after Jan 1 2019 and before Jan 1 2021
complaint_clean <- complaint_1 %>% 
  filter(complaint_date >= as.Date("2019-01-01")) %>%
  filter(complaint_date < as.Date("2021-01-01"))
# Should be 1,326,009 obs
```


```r
head(complaint_clean)
```

```
##   complaint_date complaint_time complaint_AMPM              Complaint.Type
## 1     2019-01-01       12:00:00             AM                      Rodent
## 2     2019-01-01       12:00:00             AM                      Rodent
## 3     2019-01-01       12:00:00             AM                      Rodent
## 4     2019-01-01       12:00:00             AM                      Rodent
## 5     2019-01-01       12:00:00             AM                      Rodent
## 6     2019-01-01       12:00:00             AM Unsanitary Pigeon Condition
##                     Descriptor                Location.Type  Borough
## 1               Mouse Sighting      3+ Family Apt. Building   QUEENS
## 2                 Rat Sighting      3+ Family Apt. Building    BRONX
## 3 Condition Attracting Rodents        Other (Explain Below) BROOKLYN
## 4 Condition Attracting Rodents          Commercial Building   QUEENS
## 5               Mouse Sighting      3+ Family Apt. Building    BRONX
## 6                 Pigeon Waste 3+ Family Apartment Building   QUEENS
##   Latitude Longitude
## 1 40.73887 -73.87249
## 2 40.82847 -73.89545
## 3 40.67055 -73.86311
## 4 40.70524 -73.77507
## 5 40.87279 -73.90013
## 6 40.57830 -73.83838
```



## Dept of Building Permits

Reading in the dataset

```r
# All "NULL" columns are ones I am sure we will not use
dob_raw <- read.csv("DOB_Permit_Issuance.csv", encoding="UTF-8", na.strings = "", row.names = NULL, colClasses=c(NA, "NULL", NA, NA, "NULL", "NULL", NA, "NULL", "NULL", "NULL", "NULL", NA, NA, NA, "NULL", "NULL", NA, NA, NA, NA, NA, NA, "NULL", "NULL", NA, NA, NA, NA, "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", NA, NA, "NULL", "NULL", "NULL"))
# Should be 3,720,041 obs
```


```r
head(dob_raw)
```

```
##         BOROUGH House..     Street.Name Job.Type Zip.Code Bldg.Type
## 1     MANHATTAN    1230      6TH AVENUE       A2    10020         2
## 2 STATEN ISLAND     715   OCEAN TERRACE       A2    10301         2
## 3      BROOKLYN    9952           3 AVE       DM    11209         1
## 4      BROOKLYN     179     LOTT STREET       DM    11226         1
## 5      BROOKLYN    2917       AVENUE  N       DM    11210         2
## 6      BROOKLYN     245 FRANKLIN AVENUE       A3    11205         2
##   Residential Work.Type Permit.Status Filing.Status Permit.Type
## 1        <NA>        OT        ISSUED       RENEWAL          EW
## 2        <NA>        OT        ISSUED       RENEWAL          EW
## 3        <NA>      <NA>        ISSUED       INITIAL          DM
## 4        <NA>      <NA>        ISSUED       INITIAL          DM
## 5        <NA>      <NA>        ISSUED       INITIAL          DM
## 6         YES        EQ        ISSUED       INITIAL          EQ
##   Permit.Sequence.. Permit.Subtype Filing.Date Issuance.Date
## 1                 2             OT  12/11/2020    12/11/2020
## 2                 3             OT  12/11/2020    12/11/2020
## 3                 1           <NA>  06/17/2020    06/17/2020
## 4                 1           <NA>  06/17/2020    06/17/2020
## 5                 1           <NA>  06/17/2020    06/17/2020
## 6                 1             OT  06/17/2020    06/17/2020
##   Expiration.Date Job.Start.Date LATITUDE LONGITUDE
## 1      11/02/2021     12/23/2019 40.75898 -73.98109
## 2      12/31/2020     08/02/2019 40.60851 -74.10207
## 3      05/10/2021     06/17/2020 40.61334 -74.03558
## 4      02/21/2021     06/17/2020 40.64554 -73.95403
## 5      03/04/2021     06/17/2020 40.61714 -73.94580
## 6      06/17/2021     06/17/2020 40.69122 -73.95736
```

Filtering out permits that are in process

```r
# Each row in dataset is a permit that is not in process
dob_1 <- dob_raw %>%
  filter(Permit.Status != "IN PROCESS") %>%
  mutate(state = "NY") %>%
  unite(Address, House.., Street.Name, BOROUGH, state, Zip.Code, sep = ",", remove = FALSE)

dob_1$Filing.Date <- as.Date(as.character(dob_1$Filing.Date), "%m/%d/%Y")
dob_1$Issuance.Date <- as.Date(as.character(dob_1$Issuance.Date), "%m/%d/%Y")
dob_1$Expiration.Date <- as.Date(as.character(dob_1$Expiration.Date), "%m/%d/%Y")
dob_1$Job.Start.Date <- as.Date(as.character(dob_1$Job.Start.Date), "%m/%d/%Y")
# Should be 3,687,902 obs
```

Filtering out permits expired before 2019

```r
# Dataset represents permits that expired or afer Jan 1 2019 in order to cut down on the number of rows. This date was chosen because even if we decide on an "average" amout of construction, we will likely not want to include any construction projects that concluded before this date
dob_2 <- dob_1 %>% 
  filter(Expiration.Date >= as.Date("2019-01-01")) %>%
  subset(select = -c(House.., Street.Name, Zip.Code, state))
# Should be 111,454 obs
```

Getting addresses for rows with missing lat lon

```r
# This dataset has only unique addresses for rows with missing lat lon coordinates
dob_address_missing <- dob_2 %>%
  filter(is.na(LATITUDE)) %>%
  subset(select = c(Address, BOROUGH)) %>%
  distinct(Address, .keep_all = TRUE) %>%
  mutate_geocode(Address)
# Should be 125 obs

# Writing to csv for safekeeping
write.csv(dob_address_missing,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Raw/dob_address_missing.csv", row.names = FALSE)
```

Merging missing lat lon coordinates and getting final dataset

```r
dob_address_missing <- read.csv("dob_address_missing.csv", encoding="UTF-8", na.strings = "", row.names = NULL)

dob_address_missing$Address <- as.character(dob_address_missing$Address)

# Final dataset represents all permits not still in process that expired after Jan 1,  2019
dob_clean <- dob_2 %>%
  left_join(dob_address_missing, by = "Address") %>%
  mutate(latitude = ifelse(!is.na(LATITUDE), LATITUDE, lat)) %>%
  mutate(longitude = ifelse(!is.na(LONGITUDE), LONGITUDE, lon)) %>%
  subset(select = -c(LATITUDE, LONGITUDE, BOROUGH.y, lon, lat))
# Should be 111,454 obs, 17 vars
```


```r
head(dob_clean)
```

```
##                                    Address     BOROUGH.x Job.Type
## 1       1230,6TH AVENUE,MANHATTAN,NY,10020     MANHATTAN       A2
## 2 715,OCEAN TERRACE,STATEN ISLAND,NY,10301 STATEN ISLAND       A2
## 3             9952,3 AVE,BROOKLYN,NY,11209      BROOKLYN       DM
## 4        179,LOTT STREET,BROOKLYN,NY,11226      BROOKLYN       DM
## 5         2917,AVENUE  N,BROOKLYN,NY,11210      BROOKLYN       DM
## 6    245,FRANKLIN AVENUE,BROOKLYN,NY,11205      BROOKLYN       A3
##   Bldg.Type Residential Work.Type Permit.Status Filing.Status Permit.Type
## 1         2        <NA>        OT        ISSUED       RENEWAL          EW
## 2         2        <NA>        OT        ISSUED       RENEWAL          EW
## 3         1        <NA>      <NA>        ISSUED       INITIAL          DM
## 4         1        <NA>      <NA>        ISSUED       INITIAL          DM
## 5         2        <NA>      <NA>        ISSUED       INITIAL          DM
## 6         2         YES        EQ        ISSUED       INITIAL          EQ
##   Permit.Sequence.. Permit.Subtype Filing.Date Issuance.Date
## 1                 2             OT  2020-12-11    2020-12-11
## 2                 3             OT  2020-12-11    2020-12-11
## 3                 1           <NA>  2020-06-17    2020-06-17
## 4                 1           <NA>  2020-06-17    2020-06-17
## 5                 1           <NA>  2020-06-17    2020-06-17
## 6                 1             OT  2020-06-17    2020-06-17
##   Expiration.Date Job.Start.Date latitude longitude
## 1      2021-11-02     2019-12-23 40.75898 -73.98109
## 2      2020-12-31     2019-08-02 40.60851 -74.10207
## 3      2021-05-10     2020-06-17 40.61334 -74.03558
## 4      2021-02-21     2020-06-17 40.64554 -73.95403
## 5      2021-03-04     2020-06-17 40.61714 -73.94580
## 6      2021-06-17     2020-06-17 40.69122 -73.95736
```



## Street construction

Reading in the dataset

```r
# All "NULL" columns are ones I am sure we will not use
street_raw <- read.csv("Street_Construction_Permits.csv", encoding="UTF-8", na.strings = "", row.names = NULL, colClasses=c("NULL", "NULL", "NULL", "NULL", "NULL", NA, "NULL", NA, "NULL", NA, "NULL", "NULL", NA, "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", NA, NA, NA, NA, NA, NA, NA, NA, "NULL", "NULL", "NULL", "NULL", "NULL", "NULL", "NULL"))
# Should be 10,304,935 obs and 12 vars
```


```r
head(street_raw)
```

```
##           PermitStatusShortDesc        PermitSeriesShortDesc
## 1 DELINQUENT CUTFORM/COMPACTION        STREET OPENING PERMIT
## 2                       EXPIRED SIDEWALK CONSTRUCTION PERMIT
## 3                       EXPIRED        STREET OPENING PERMIT
## 4                       EXPIRED        STREET OPENING PERMIT
## 5 DELINQUENT CUTFORM/COMPACTION        STREET OPENING PERMIT
## 6                       EXPIRED        STREET OPENING PERMIT
##                        PermitTypeDesc PermitTotalSqFeet
## 1 NYC PARKS - RECONSTRUCTION CONTRACT                NA
## 2                     REPAIR SIDEWALK                NA
## 3                          REPAIR GAS                16
## 4 NYC PARKS - RECONSTRUCTION CONTRACT                NA
## 5                        REPAIR WATER                NA
## 6            MAJOR INSTALLATION - GAS                12
##          PermitIssueDate          IssuedWorkStartDate
## 1 11/01/2007 12:00:00 AM 11/01/2007 12:00:00 AM +0000
## 2 09/14/2012 12:00:00 AM 09/17/2012 12:00:00 AM +0000
## 3 08/12/2010 12:00:00 AM 08/17/2010 12:00:00 AM +0000
## 4 08/07/2006 12:00:00 AM 08/07/2006 12:00:00 AM +0000
## 5 03/18/1999 12:00:00 AM 03/17/1999 12:00:00 AM +0000
## 6 11/01/1995 12:00:00 AM 11/01/1995 12:00:00 AM +0000
##              IssuedWorkEndDate BoroughName PermitHouseNumber
## 1 12/31/2007 12:00:00 AM +0000      QUEENS              <NA>
## 2 10/17/2012 12:00:00 AM +0000       BRONX              <NA>
## 3 09/16/2010 12:00:00 AM +0000       BRONX              2926
## 4 09/30/2006 12:00:00 AM +0000       BRONX              <NA>
## 5 03/31/1999 12:00:00 AM +0000       BRONX             92-98
## 6 11/30/1995 12:00:00 AM +0000       BRONX              <NA>
##           OnStreetName  FromStreetName    ToStreetName
## 1 CLOVERDALE BOULEVARD         57 ROAD       59 AVENUE
## 2       HOLLAND AVENUE ALLERTON AVENUE    ARNOW AVENUE
## 3        MICKLE AVENUE     ADEE AVENUE    ARNOW AVENUE
## 4      BRONX BOULEVARD  MAGENTA STREET ROSEWOOD STREET
## 5     EAST  165 STREET   GERARD AVENUE   WALTON AVENUE
## 6         LOGAN AVENUE  BARKLEY AVENUE     OTIS AVENUE
```

Transforming date columns so they can be filtered and dropping missing locations

```r
# Dataset is the same but drops missing locations that cannot be geocoded
street_1 <- street_raw %>%
  separate(col = PermitIssueDate, into = c("issue_date", "issue_time", "issue_AM_PM"), sep = "[ ]") %>%
  separate(col = IssuedWorkStartDate, into = c("workstart_date", "workstart_time", "workstart_AM_PM", "workstart_del"), sep = "[ ]") %>%
  separate(col = IssuedWorkEndDate, into = c("workend_date", "workend_time", "workend_AM_PM", "workend_del"), sep = "[ ]") %>%
  drop_na(OnStreetName) %>%
  mutate(State = "NY") %>%
  unite(Address_from, OnStreetName, FromStreetName, BoroughName, State, sep = ", ", remove = "False") %>%
  unite(Address_to, OnStreetName, ToStreetName, BoroughName, State, sep = ", ", remove = "False") %>%
  subset(select = -c(workstart_del, workend_del, FromStreetName, ToStreetName, OnStreetName, State))

street_1$issue_date <- as.Date(as.character(street_1$issue_date), "%m/%d/%Y")
street_1$workstart_date <- as.Date(as.character(street_1$workstart_date), "%m/%d/%Y")
street_1$workend_date <- as.Date(as.character(street_1$workend_date), "%m/%d/%Y")
# Should be 9,998,603 obs
```

Filtering out permits ending 2019 and filtering out denied/cancelled/voided permits

```r
# Dataset represents accepted permits with end dates before Jan 1, 2019. This date was chosen because even if we decide to taken an "average" of construction by year, we will not need to take in account projects that stopped before this date
street_2 <- street_1 %>%
  filter(workend_date >= as.Date("2019-01-01")) %>%
  filter(PermitStatusShortDesc == "CONFIRMATION REC'D" | PermitStatusShortDesc == "EMERGENCY" | PermitStatusShortDesc == "ISSUED & PRINTED" | PermitStatusShortDesc == "AMENDED AFTER ISSUE" | PermitStatusShortDesc == "EXTENDED & PRINTED") %>%
  drop_na(workstart_date)
# Should be 77,177 obs
```

Getting a database of addresses for geocoding and dropping duplicated locations

```r
# Dataset represents all unique addresses from the "from" and "to" categories
street_addressonly <- street_2 %>%
  subset(select = c(Address_from, Address_to, BoroughName)) %>%
  mutate(id = row_number()) %>%
  melt(id.vars = c("id", "BoroughName"), variable.name = "Address") %>%
  distinct(value, .keep_all = TRUE)
# Should be 34,048 obs

# Exporting for geocoding 
write.csv(street_addressonly,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Raw/street_address.csv", row.names = FALSE)
```

Reading in same dataset with geocoded addresses

```r
street_addressonly <- read.csv("street_total.csv", encoding="UTF-8", na.strings = "", row.names = NULL)
# Should be 34,048 obs

street_addressonly$Address <- as.character(street_addressonly$Address)
```

Merging "from" address coordinates to dataset

```r
# Same dataset as street_2, but with merged coordinates for "from" addresses
street_3 <- street_2 %>%
  left_join(street_addressonly, by = c("Address_from" = "Address")) %>%
  mutate(point_match = row_number())

street_3 <- rename(street_3, latitude_from = latitude)
street_3 <- rename(street_3, longitude_from = longitude)
# Should be 77,177 obs
```

Merging "to" address coordinates to dataset and finalizing clean dataset

```r
# Final dataset has permits by row, with 2 coordinates per row indicated where construction begins (from) and ends (to). These two sets of coordinates will be used to create a segment in the geospatial software
street_clean <- street_3 %>%
  left_join(street_addressonly, by = c("Address_to" = "Address")) %>%
  subset(select = -c(BoroughName.y, id.x, Direction.x, Direction.y, id.y, issue_time, issue_AM_PM, workstart_time, workstart_AM_PM, workend_time, workend_AM_PM, BoroughName.x))

street_clean <- rename(street_clean, latitude_to = latitude)
street_clean <- rename(street_clean, longitude_to = longitude)
# Should be 77,177 obs, and 16 vars
```


```r
head(street_clean)
```

```
##   PermitStatusShortDesc     PermitSeriesShortDesc
## 1   AMENDED AFTER ISSUE     STREET OPENING PERMIT
## 2      ISSUED & PRINTED BUILDING OPERATION PERMIT
## 3      ISSUED & PRINTED BUILDING OPERATION PERMIT
## 4      ISSUED & PRINTED BUILDING OPERATION PERMIT
## 5      ISSUED & PRINTED BUILDING OPERATION PERMIT
## 6      ISSUED & PRINTED BUILDING OPERATION PERMIT
##                                PermitTypeDesc PermitTotalSqFeet issue_date
## 1                    MAJOR INSTALLATION - GAS              1800 2013-12-24
## 2    PLACE EQUIPMENT OTHER THAN CRANE OR SHOV                NA 2020-10-21
## 3    PLACE EQUIPMENT OTHER THAN CRANE OR SHOV                NA 2020-10-21
## 4         OCCUPANCY OF SIDEWALK AS STIPULATED                NA 2020-10-18
## 5    PLACE EQUIPMENT OTHER THAN CRANE OR SHOV                NA 2020-10-18
## 6 PLACE CONSTRUCTION OFFICE TRAILER ON STREET                NA 2020-10-18
##   workstart_date workend_date
## 1     2024-01-14   2024-04-13
## 2     2020-10-25   2020-12-31
## 3     2020-10-25   2020-12-31
## 4     2020-10-18   2020-12-31
## 5     2020-10-18   2020-12-31
## 6     2020-10-18   2020-12-31
##                                    Address_from
## 1 ELTON STREET, SCHROEDERS AVENUE, BROOKLYN, NY
## 2            SHELL ROAD, AVENUE Y, BROOKLYN, NY
## 3        SHELL ROAD, COBECK COURT, BROOKLYN, NY
## 4   CLYMER STREET, BEDFORD AVENUE, BROOKLYN, NY
## 5   CLYMER STREET, BEDFORD AVENUE, BROOKLYN, NY
## 6   BEDFORD AVENUE, CLYMER STREET, BROOKLYN, NY
##                                    Address_to PermitHouseNumber
## 1 ELTON STREET, VANDALIA AVENUE, BROOKLYN, NY              <NA>
## 2      SHELL ROAD, COBECK COURT, BROOKLYN, NY              <NA>
## 3        SHELL ROAD, DANK COURT, BROOKLYN, NY              <NA>
## 4           CLYMER STREET, BEND, BROOKLYN, NY               142
## 5           CLYMER STREET, BEND, BROOKLYN, NY               142
## 6 BEDFORD AVENUE, TAYLOR STREET, BROOKLYN, NY              <NA>
##   latitude_from longitude_from point_match BoroughName latitude_to
## 1      40.65495      -73.87284           1    BROOKLYN    40.65572
## 2      40.58795      -73.97420           2    BROOKLYN    40.58721
## 3      40.58721      -73.97421           3    BROOKLYN    40.58650
## 4      40.70647      -73.96375           4    BROOKLYN    40.70606
## 5      40.70647      -73.96375           5    BROOKLYN    40.70606
## 6      40.70647      -73.96375           6    BROOKLYN    40.70591
##   longitude_to
## 1    -73.87342
## 2    -73.97421
## 3    -73.97427
## 4    -73.96441
## 5    -73.96441
## 6    -73.96310
```



## Sidewalk Cafe Licenses

Reading in the dataset

```r
cafe_raw <- read.csv("Sidewalk_Caf__Licenses_and_Applications.csv", encoding="UTF-8", na.strings = "", row.names = NULL)
# Should be 1,121 obs
```


```r
head(cafe_raw)
```

```
##   LICENSE_NBR LIC_STATUS            BUSINESS_NAME
## 1 2037224-DCA   Inactive        PARK AVE CAKE LLC
## 2 2038098-DCA   Inactive       CAMPANIA FELIX LLC
## 3 2080055-DCA   Inactive  MBG TAVERNS ON 6TH CORP
## 4 1191523-DCA     Active   SHIRT RESTAURANT CORP.
## 5 1437756-DCA   Inactive 33 WEST 54TH STREET, LLC
## 6 1422663-DCA   Inactive               CLGM, INC.
##                 BUSINESS_NAME2 BUILDING      STREET     CITY STATE   ZIP
## 1                    L'EXPRESS      249  PARK AVE S NEW YORK    NY 10003
## 2 SAN MATTEO PIZZERIA E CUCINA     1559     2ND AVE NEW YORK    NY 10028
## 3                         <NA>      757     6TH AVE NEW YORK    NY 10010
## 4                       ISLAND     1305 MADISON AVE NEW YORK    NY 10128
## 5                Il GATTOPARDO       33   W 54TH ST NEW YORK    NY 10019
## 6            YEFSI ESTAIATORIO     1481    YORK AVE NEW YORK    NY 10075
##           SWC_TYPE SWC_SQ_FT SWC_TABLES SWC_CHAIRS    DOHMH LATITUDE
## 1       Unenclosed       310          7         22 50043852 40.73800
## 2         Enclosed       345         10         25 50042812 40.77456
## 3       Unenclosed       270         10         20     <NA> 40.74484
## 4 Small Unenclosed        83          2          8 40385587 40.78490
## 5 Small Unenclosed        46          1          4 40851852 40.76204
## 6       Unenclosed       171          9         20 41637080 40.77105
##   LONGITUDE COMMUNITY_DISTRICT CITY_COUNCIL_DISTRICT
## 1 -73.98766                105                     2
## 2 -73.95417                108                     5
## 3 -73.99183                104                     3
## 4 -73.95567                108                     4
## 5 -73.97689                105                     4
## 6 -73.95088                108                     5
##                    CD_URL          APP_ID     APP_SWC_TYPE APP_SQ_FT
## 1      http://www.cb5.org 27968-2018-RSWC       Unenclosed       310
## 2    http://www.cb8m.com/  8622-2018-RSWC         Enclosed       345
## 3 http://www.nyc.gov/mcb4  2797-2020-RSWC       Unenclosed       270
## 4    http://www.cb8m.com/ 26825-2019-RSWC Small Unenclosed        83
## 5      http://www.cb5.org 12177-2018-RSWC Small Unenclosed        46
## 6    http://www.cb8m.com/ 14358-2018-RSWC       Unenclosed       171
##   APP_TABLES APP_CHAIRS                   APP_STATUS APP_STATUS_DATE
## 1          7         22 Application Review Completed      03/25/2019
## 2         10         25               Pending Review      11/20/2019
## 3         10         20               Pending Review      05/29/2020
## 4          2          8 Application Review Completed      01/14/2020
## 5          1          4 Application Review Completed      03/22/2019
## 6          9         20 Application Review Completed      03/28/2019
##   EXPIRATION_DATE APP_TOO_DATE SUBMIT_DATE           INTAKE  INTAKE_DD
## 1      12/15/2020         <NA>  11/15/2018 Ready For Review 11/15/2018
## 2      05/20/2020   05/20/2020  05/17/2018 Ready For Review 05/17/2018
## 3      06/29/2020   06/29/2020  02/06/2020 Ready For Review 02/06/2020
## 4      09/15/2021         <NA>  09/17/2019 Ready For Review 09/17/2019
## 5      09/15/2020         <NA>  09/04/2018 Ready For Review 09/04/2018
## 6      09/15/2020         <NA>  09/20/2018 Ready For Review 09/27/2018
##                    DPQA SEND_PACKAGE_DD             CP      CP_DD
## 1              Approved      11/15/2018           <NA>       <NA>
## 2 Issued Temp Op Letter      05/18/2018        Proceed 10/08/2019
## 3 Issued Temp Op Letter      02/07/2020 Pending Review 02/07/2020
## 4              Approved      09/18/2019           <NA>       <NA>
## 5              Approved      09/04/2018           <NA>       <NA>
## 6              Approved      09/27/2018           <NA>       <NA>
##                      CB      CB_DD HEARING HEARING_DD HEARING_PUBLIC
## 1 Review Period Expired 01/10/2019  Waived 01/10/2019           <NA>
## 2 Review Period Expired 10/08/2019  Waived 10/08/2019           <NA>
## 3 Review Period Expired 04/07/2020  Waived 04/07/2020           <NA>
## 4    Recommend Approval 10/31/2019  Waived 11/07/2019           <NA>
## 5 Review Period Expired 11/01/2018  Waived 11/01/2018           <NA>
## 6 Review Period Expired 11/21/2018  Waived 11/21/2018           <NA>
##   HEARING_PUBLIC_DD                    CC      CC_DD            MOO
## 1              <NA> Review Period Expired 01/31/2019       Approved
## 2              <NA> Review Period Expired 10/29/2019 Pending Review
## 3              <NA> Review Period Expired 04/28/2020 Pending Review
## 4              <NA> Review Period Expired 11/28/2019       Approved
## 5              <NA> Review Period Expired 11/22/2018       Approved
## 6              <NA> Review Period Expired 12/12/2018       Approved
##       MOO_DD       ISSUANCE ISSUANCE_DD
## 1 03/25/2019         Issued  03/25/2019
## 2       <NA> Pending Review        <NA>
## 3       <NA> Pending Review        <NA>
## 4 01/14/2020         Issued  01/14/2020
## 5 03/22/2019         Issued  03/22/2019
## 6 03/28/2019         Issued  03/28/2019
```

Subsetting and gettings date variables in order

```r
# This dataset will only contain licenses that were approved and issued
cafe_1 <- cafe_raw %>%
  subset(select = c(LIC_STATUS, SWC_TYPE, SWC_SQ_FT, SWC_TABLES, SWC_CHAIRS, LATITUDE, LONGITUDE, APP_STATUS, ISSUANCE, ISSUANCE_DD)) %>%
  filter(ISSUANCE == "Issued") %>%
  filter(APP_STATUS == "Application Review Completed") %>%
  subset(select = -c(APP_STATUS, ISSUANCE))

cafe_1$ISSUANCE_DD <- as.Date(as.character(cafe_1$ISSUANCE_DD), "%m/%d/%Y")
# Should be 805 obs
```

Finalizing cleaned file for geospatial software

```r
# Dropping rows that are missing lat lon
cafe_clean <- cafe_1 %>%
  na.omit(LONGITUDE) %>%
  na.omit(LATITUDE)
# Should be 805 obs
```

Final cleaned file

```r
head(cafe_clean)
```

```
##   LIC_STATUS         SWC_TYPE SWC_SQ_FT SWC_TABLES SWC_CHAIRS LATITUDE
## 1   Inactive       Unenclosed       310          7         22 40.73800
## 2     Active Small Unenclosed        83          2          8 40.78490
## 3   Inactive Small Unenclosed        46          1          4 40.76204
## 4   Inactive       Unenclosed       171          9         20 40.77105
## 5     Active       Unenclosed       104          6         12 40.73908
## 6     Active       Unenclosed       335         16         32 40.72719
##   LONGITUDE ISSUANCE_DD
## 1 -73.98766  2019-03-25
## 2 -73.95567  2020-01-14
## 3 -73.97689  2019-03-22
## 4 -73.95088  2019-03-28
## 5 -74.00545  2020-05-27
## 6 -74.00320  2020-01-07
```



## Open Restaurant Applications

Reading in the dataset

```r
open_raw <- read.csv("Open_Restaurant_Applications.csv", encoding="UTF-8", na.strings = "", row.names = NULL)
# Should be 11,744
```


```r
head(open_raw)
```

```
##   objectid                               globalid
## 1    10639 {9A535733-A800-471F-8D63-2C1E16BD4F07}
## 2    10645 {3F853C0F-ED0D-4063-84F7-062BD3122D12}
## 3    10289 {096E1404-EBAE-48F5-8DDF-8ABD9D1F57D1}
## 4    10274 {3B982638-4EB7-4BFE-8FA4-29F2DE80833B}
## 5    10259 {2CBACAD1-49B6-4D8D-8F25-A3F415A9C586}
## 6    10321 {87B61FDF-720D-4E56-8DD5-0A70B7D2AC10}
##   Seating.Interest..Sidewalk.Roadway.Both.                 Restaurant.Name
## 1                                 sidewalk                          SUBWAY
## 2                                     both              BLUE BOTTLE COFFEE
## 3                                     both Prince Laban&Chinese restaurent
## 4                                 sidewalk          Philly Pretzel Factory
## 5                                  roadway                    About Coffee
## 6                                     both                   BICKLES TO GO
##       Legal.Business.Name              Doing.Business.As..DBA.
## 1    FRESH SUBWAY 168 INC                    Fresh Sub 168 Inc
## 2 BLUE BOTTLE COFFEE, INC                   BLUE BOTTLE COFFEE
## 3            Renessa inc. Prince Kababish & Chinese restaurant
## 4  Snacking Made Easy LLC               Philly Pretzel Factory
## 5        ABOUT COFFEE LLC                         ABOUT COFFEE
## 6        BICKLES 2 GO INC                         BICKLES 2 GO
##   Building.Number                     Street   Borough Postcode
## 1       undefined 18524A HORACE HARDING EXPY    Queens    11365
## 2       undefined            20 BROAD STREET Manhattan    10005
## 3            3756                  74 street    Queens    11372
## 4             131                    5th Ave  Brooklyn    11217
## 5              71            SULLIVAN STREET Manhattan    10012
## 6             726             COURTLANDT AVE     Bronx    10451
##                         Business.Address
## 1 18524A HORACE HARDING EXPY, Queens, NY
## 2         20 BROAD STREET, Manhattan, NY
## 3             3756 74 street, Queens, NY
## 4              131 5th Ave, Brooklyn, NY
## 5      71 SULLIVAN STREET, Manhattan, NY
## 6          726 COURTLANDT AVE, Bronx, NY
##   Food.Service.Establishment.Permit.. Sidewalk.Dimensions..Length.
## 1                            50053455                           30
## 2                            50104404                           20
## 3                            50069734                           18
## 4                            50097413                          130
## 5                            50047872                           NA
## 6                            50104163                           20
##   Sidewalk.Dimensions..Width. Sidewalk.Dimensions..Area.
## 1                           6                        180
## 2                           4                         80
## 3                           8                        144
## 4                          50                       6500
## 5                          NA                         NA
## 6                           5                        100
##   Roadway.Dimensions..Length. Roadway.Dimensions..Width.
## 1                          NA                         NA
## 2                          20                          8
## 3                          18                          8
## 4                          NA                         NA
## 5                          10                          5
## 6                          20                          8
##   Roadway.Dimensions..Area. Approved.for.Sidewalk.Seating
## 1                        NA                           yes
## 2                       160                           yes
## 3                       144                           yes
## 4                        NA                           yes
## 5                        50                            no
## 6                       160                           yes
##   Approved.for.Roadway.Seating Qualify.Alcohol SLA.Serial.Number
## 1                           no              no              <NA>
## 2                          yes              no              <NA>
## 3                          yes              no              <NA>
## 4                           no              no              <NA>
## 5                          yes              no              <NA>
## 6                          yes              no              <NA>
##   SLA.License.Type Landmark.District.or.Building landmarkDistrict_terms
## 1             <NA>                            no                   <NA>
## 2             <NA>                           yes                    yes
## 3             <NA>                            no                   <NA>
## 4             <NA>                            no                   <NA>
## 5             <NA>                            no                   <NA>
## 6             <NA>                            no                   <NA>
##   healthCompliance_terms     Time.of.Submission Latitude Longitude
## 1                    yes 08/25/2020 08:48:00 PM       NA        NA
## 2                    yes 08/26/2020 10:45:00 AM       NA        NA
## 3                    yes 08/15/2020 04:55:00 PM 40.74763 -73.89160
## 4                    yes 08/15/2020 09:58:00 AM 40.67865 -73.97893
## 5                    yes 08/14/2020 05:08:00 PM 40.72463 -74.00389
## 6                    yes 08/17/2020 10:29:00 AM 40.82075 -73.91765
##   Community.Board Council.District Census.Tract     BIN        BBL
## 1              NA               NA           NA      NA         NA
## 2              NA               NA           NA      NA         NA
## 3               3               25          289 4029808 4012840065
## 4               6               39          131 3019193 3009440004
## 5               2                3           47 1007347 1004890008
## 6               1               17           69 2091199 2024020005
##                                      NTA
## 1                                   <NA>
## 2                                   <NA>
## 3                        Jackson Heights
## 4                     Park Slope-Gowanus
## 5 SoHo-TriBeCa-Civic Center-Little Italy
## 6         Melrose South-Mott Haven North
```


Subsetting and getting date variables in order

```r
# This dataset contains applications that were approved
open_1 <- open_raw %>%
  subset(select = c(Seating.Interest..Sidewalk.Roadway.Both., Sidewalk.Dimensions..Area., Roadway.Dimensions..Area., Approved.for.Sidewalk.Seating, Approved.for.Roadway.Seating, Qualify.Alcohol, Latitude, Longitude, Business.Address, Time.of.Submission)) %>%
  mutate(flag = ifelse(Approved.for.Sidewalk.Seating == "no" & Approved.for.Roadway.Seating == "no", 1, 0)) %>%
  filter(flag == 0) %>%
  mutate(latlong = ifelse(is.na(Latitude) | is.na(Longitude), 1, 0)) %>%
  separate(col = Time.of.Submission, into = c("date", "time", "AM_PM"), sep = "[ ]")

open_1$date <- as.Date(as.character(open_1$date), "%m/%d/%Y")
open_1$Business.Address <- as.character(open_1$Business.Address)
# Should be 11,381 obs
```

Subsetting to get addresses for obs missing latlong and geocoding

```r
# This dataset contains only unique addresses for rows that were missing coordinates
open_addressonly <- open_1 %>%
  filter(latlong == 1) %>%
  subset(select = c(Business.Address)) %>%
  distinct(Business.Address, .keep_all = TRUE) %>%
  mutate_geocode(Business.Address)
# Should be 2,461 obs
```

Cleaning up geocoding and writing out file with obs that could not be geocoded for manual cleaning

```r
# This dataset contains addresses that were unable to be geocoded or were obviously incorrectly geocded
open_addressonly_smallmerge <- open_addressonly %>%
  mutate(flag_na = ifelse(is.na(lon) | is.na(lat), 1, 0)) %>%
  mutate(flag_latlong = ifelse(lon < -75, 1, 0)) %>%
  filter(flag_na == 1 | flag_latlong == 1) %>%
  subset(select = c(Business.Address))

write.csv(open_addressonly_smallmerge,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/open_address.csv", row.names = FALSE)
# Should be 16 obs

# Reading in file after doing a manual cleanup of addresses
open_addressonly_smallmerge <- read.csv("open_address.csv", encoding="UTF-8", na.strings = "", row.names = NULL)

open_addressonly_smallmerge$Business.Address <- as.character(open_addressonly_smallmerge$Business.Address)
open_addressonly_smallmerge$Business.Address2 <- as.character(open_addressonly_smallmerge$Business.Address2)

# Geocoding the final missed addresses
open_addressonly_smallmerge %>% mutate_geocode(Business.Address2)
# Should be 16 obs
```

Merging the geocoded addresses and exporting them for safekeeping

```r
# This dataset contains all unique correctly geocoded addresses
open_addressonly_final <- open_addressonly %>%
  left_join(open_addressonly_smallmerge, by = "Business.Address") %>%
  mutate(lat = ifelse(!is.na(Business.Address2), lat.y, lat.x)) %>%
  mutate(lon = ifelse(!is.na(Business.Address2), lon.y, lon.x)) %>%
  subset(select = c(Business.Address, lat, lon))

write.csv(open_addressonly_final,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Raw/open_addressfinal.csv", row.names = FALSE)
# Should be 2,461 obs
```

Reading in finalized geocoded datasets

```r
# Again, dataset is all unique + correctly geocded restaurant addresses
open_addressonly_final <- read.csv("open_addressfinal.csv", encoding="UTF-8", na.strings = "", row.names = NULL)

open_addressonly_final$Business.Address <- as.character(open_addressonly_final$Business.Address)
# Should be 2,461 obs
```

Merging the geocoded addresses with the final dataset

```r
# Dataset merges together all corrected lat lon coordinates with the original dataset
open_2 <- open_1 %>%
  left_join(open_addressonly_final, by = "Business.Address") %>%
  mutate(latitude = ifelse(!is.na(Latitude), Latitude, lat)) %>%
  mutate(longitude = ifelse(!is.na(Longitude), Latitude, lon)) %>%
  mutate(sidewalk_dimensions = ifelse(!is.na(Sidewalk.Dimensions..Area.), Sidewalk.Dimensions..Area., 0)) %>%
  mutate(roadway_dimensions = ifelse(!is.na(Roadway.Dimensions..Area.), Roadway.Dimensions..Area., 0)) %>%
  mutate(total_dimensions = sidewalk_dimensions + roadway_dimensions) %>%
  mutate(flag_both = ifelse(Approved.for.Sidewalk.Seating == "yes" & Approved.for.Roadway.Seating == "yes", 1, 0)) %>%
  mutate(flag_sidewalk = ifelse(Approved.for.Sidewalk.Seating == "yes" & flag_both == 0, 1, 0)) %>%
  mutate(flag_roadway = ifelse(Approved.for.Roadway.Seating == "yes" & flag_both == 0, 1, 0)) %>%
  subset(select = c(Business.Address, latitude, longitude, date, Qualify.Alcohol, flag_both, flag_roadway, flag_sidewalk, total_dimensions))
# Should be 11,381 obs
```

Final cleaning and subsetting for export

```r
open_2[open_2$flag_both == 1, "approved_area"] <- "both"
open_2[open_2$flag_sidewalk == 1, "approved_area"] <- "sidewalk"
open_2[open_2$flag_roadway == 1, "approved_area"] <- "roadway"

# Final dataset contains only columns we want
open_clean <- open_2 %>%
  subset(select = c(Business.Address, latitude, longitude, date, Qualify.Alcohol, approved_area, total_dimensions))
# Should be 11,381 obs and 7 variables
```

Final cleaned file

```r
head(open_clean)
```

```
##                         Business.Address latitude longitude       date
## 1 18524A HORACE HARDING EXPY, Queens, NY 40.73988 -73.78841 2020-08-25
## 2         20 BROAD STREET, Manhattan, NY 40.70688 -74.01126 2020-08-26
## 3             3756 74 street, Queens, NY 40.74763  40.74763 2020-08-15
## 4              131 5th Ave, Brooklyn, NY 40.67865  40.67865 2020-08-15
## 5      71 SULLIVAN STREET, Manhattan, NY 40.72463  40.72463 2020-08-14
## 6          726 COURTLANDT AVE, Bronx, NY 40.82075  40.82075 2020-08-17
##   Qualify.Alcohol approved_area total_dimensions
## 1              no      sidewalk              180
## 2              no          both              240
## 3              no          both              288
## 4              no      sidewalk             6500
## 5              no       roadway               50
## 6              no          both              260
```



## Vehicle Traffic Counts

Reading in the dataset

```r
vehicle_raw <- read.csv("Traffic_Volume_Counts__2014-2019_.csv", encoding="UTF-8", na.strings = "", row.names = NULL)

vehicle_raw$date <- as.Date(as.character(vehicle_raw$Date), "%m/%d/%Y")
# Should be 27,289 obs and 32 variables
```


```r
head(vehicle_raw)
```

```
##   ID Segment.ID           Roadway.Name            From               To
## 1  2      70376               3 Avenue East 154 Street  East 155 Street
## 2  2      70376               3 Avenue East 155 Street  East 154 Street
## 3 56     176365 Bedford Park Boulevard Grand Concourse Valentine Avenue
## 4 56     176365 Bedford Park Boulevard Grand Concourse Valentine Avenue
## 5 62     147673               Broadway West 242 Street       240 Street
## 6 62     158447               Broadway West 242 Street       240 Street
##   Direction       Date X12.00.1.00.AM X1.00.2.00AM X2.00.3.00AM
## 1        NB 09/13/2014            204          177          133
## 2        SB 09/13/2014            140           51          128
## 3        EB 09/13/2014             94           73           65
## 4        WB 09/13/2014             88           82           75
## 5        SB 09/13/2014            255          209          149
## 6        NB 09/13/2014            255          209          149
##   X3.00.4.00AM X4.00.5.00AM X5.00.6.00AM X6.00.7.00AM X7.00.8.00AM
## 1          126          141          134          121          180
## 2          116          144          146          153          219
## 3           61           64           73           65          113
## 4           60           65           67           71          142
## 5          148          128          136          199          354
## 6          148          128          136          199          354
##   X8.00.9.00AM X9.00.10.00AM X10.00.11.00AM X11.00.12.00PM X12.00.1.00PM
## 1          223           272            386            339           513
## 2          226           273            317            325           403
## 3          169           210            182            245           244
## 4          198           212            205            237           257
## 5          473           567            634            781           785
## 6          473           567            634            781           785
##   X1.00.2.00PM X2.00.3.00PM X3.00.4.00PM X4.00.5.00PM X5.00.6.00PM
## 1          506          520          611          573          546
## 2          414          379          376          329          362
## 3          233          280          272          264          236
## 4          245          237          276          223          240
## 5          779          732          809          707          675
## 6          779          732          809          707          675
##   X6.00.7.00PM X7.00.8.00PM X8.00.9.00PM X9.00.10.00PM X10.00.11.00PM
## 1          582          528          432           328            282
## 2          418          335          282           247            237
## 3          213          190          199           183            147
## 4          217          198          186           162            157
## 5          641          556          546           465            425
## 6          641          556          546           465            425
##   X11.00.12.00AM       date
## 1            240 2014-09-13
## 2            191 2014-09-13
## 3            103 2014-09-13
## 4            103 2014-09-13
## 5            324 2014-09-13
## 6            324 2014-09-13
```

Grouping by times slots so we have fewer to variables

```r
# This dataset just groups hourly columns together
vehicle_1 <- vehicle_raw %>%
  mutate(midnight_to_sevenam = X12.00.1.00.AM + X1.00.2.00AM + X2.00.3.00AM + X3.00.4.00AM + X4.00.5.00AM + X5.00.6.00AM + X6.00.7.00AM) %>%
  mutate(sevenam_to_noon = X7.00.8.00AM + X8.00.9.00AM + X9.00.10.00AM + X10.00.11.00AM + X11.00.12.00PM) %>%
  mutate(noon_to_sevenpm = X12.00.1.00PM + X1.00.2.00PM + X2.00.3.00PM + X3.00.4.00PM + X4.00.5.00PM + X5.00.6.00PM + X6.00.7.00PM) %>%
  mutate(sevenpm_to_midnight = X7.00.8.00PM + X8.00.9.00PM + X9.00.10.00PM + X10.00.11.00PM + X11.00.12.00AM) %>%
  mutate(sevenam_to_sevenpm = sevenam_to_noon + noon_to_sevenpm)
# Should be 27,289
```

Grouping by segment ID and date and collapsing down to segment and date

```r
# Each row in this dataset represents one day at one location
vehicle_2 <- vehicle_1 %>%
  group_by(Segment.ID, date) %>%
  mutate(sevenam_to_sevenpm_total = sum(sevenam_to_sevenpm)) %>%
  mutate(sevenpm_to_midnight_total = sum(sevenpm_to_midnight)) %>%
  mutate(noon_to_sevenpm_total = sum(noon_to_sevenpm)) %>%
  mutate(sevenam_to_noon_total = sum(sevenam_to_noon)) %>%
  mutate(midnight_to_sevenam_total = sum(midnight_to_sevenam)) %>%
  ungroup() %>%
  group_by(Segment.ID, date, sevenam_to_sevenpm_total, sevenpm_to_midnight_total, midnight_to_sevenam_total, sevenam_to_noon_total, noon_to_sevenpm_total) %>%
  summarise()
# Should be 18,937 obs 7 vars
```

Getting averages per sample day and collapsing down so each row is a segment

```r
# Now each row is a now just a segment, with vehicle frequencies averaged across observation days. This repreents the actual number of observations we're working with
vehicle_3 <- vehicle_2 %>%
  group_by(Segment.ID) %>%
  mutate(num_sample_day = n()) %>%
  ungroup() %>%
  group_by(Segment.ID) %>%
  mutate(alldays_seventoseven = sum(sevenam_to_sevenpm_total)) %>%
  mutate(alldays_sevenamtonoon = sum(sevenam_to_noon_total)) %>%
  mutate(alldays_noontosevenpm = sum(noon_to_sevenpm_total)) %>%
  mutate(alldays_sevenpmtomid = sum(sevenpm_to_midnight_total)) %>%
  mutate(alldays_midtosevenam = sum(midnight_to_sevenam_total)) %>%
  mutate(ave_seventoseven = alldays_seventoseven/num_sample_day) %>%
  mutate(ave_sevenamtonoon = alldays_sevenamtonoon/num_sample_day) %>%
  mutate(ave_noontosevenpm = alldays_noontosevenpm/num_sample_day) %>%
  mutate(ave_sevenpmtomid = alldays_sevenpmtomid/num_sample_day) %>%
  mutate(ave_midtosevenam = alldays_midtosevenam/num_sample_day) %>%
  ungroup() %>%
  group_by(Segment.ID, num_sample_day, ave_seventoseven, ave_sevenamtonoon, ave_noontosevenpm, ave_sevenpmtomid, ave_midtosevenam) %>%
  summarise()
# Should be 1,586 obs and 7 vars
```

Reading in adjusted segment data so we can join the gespatial tables later

```r
# We have to do this because the LION segments have leading zeros that make each number 7 digits, and we need an exact match with the zeros for the shapefile file

vehicle_numadj <- read.csv("traffic_shapefile.csv", encoding="UTF-8", na.strings = "", row.names = NULL, colClasses=c("character", NA))
# This file contains all the LION segments from the shapefile that we will be matching on

colnames(vehicle_numadj)[1] <- "segmentid"
colnames(vehicle_numadj)[2] <- "Segment.ID"

vehicle_numadj <- vehicle_numadj %>% distinct(segmentid, .keep_all = TRUE)
# Should be 208,955 obs
```

Merging final cleaned datasets to use for geospatial analysis

```r
# Here we are matching the leading zero version of the LION segments from the shapefile to the vehicle data
vehicle_4 <- vehicle_3 %>%
  left_join(vehicle_numadj, by = "Segment.ID")
# Should be 1,586 obs

# All the rows that matched successfully
vehicle_4_large <- vehicle_4 %>%
  filter(!is.na(segmentid)) %>%
  ungroup()
# Should be 1,486 obs

# Reading back in rows that failed to match. These will get manually geocoded as point data since they can't be matched to the segements
vehicle_4_small <- read.csv("vehicle_4_small.csv", encoding="UTF-8", na.strings = "", row.names = NULL, colClasses=c(NA, NA, NA, NA, NA, NA, NA, "character"))
# Should be 100 obs

# Stacking the final dataset together
vehicle_clean <- rbind(vehicle_4_large, vehicle_4_small)
# Should be 1,586 obs again
```

Final clean dataset

```r
head(vehicle_clean)
```

```
## # A tibble: 6 x 8
##   Segment.ID num_sample_day ave_seventoseven ave_sevenamtono~
##        <int>          <int> <chr>            <chr>           
## 1        202              1 7088             2494            
## 2       1416              9 7193.33333333333 2474.22222222222
## 3       1883              9 7173             2486.88888888889
## 4       2147              9 8006             2798            
## 5       2367              9 9904.44444444445 3753            
## 6       2369              9 10112.3333333333 3840.77777777778
## # ... with 4 more variables: ave_noontosevenpm <dbl>,
## #   ave_sevenpmtomid <dbl>, ave_midtosevenam <chr>, segmentid <chr>
```



## Writing clean files to csv for easy import to GIS software later


```r
# 311 Complaint clean file
write.csv(complaint_clean,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/complaint_clean.csv", row.names = FALSE)

# Dept of Building permits clean file
write.csv(dob_clean,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/dob_clean.csv", row.names = FALSE)

# Street construction file clean file
write.csv(street_clean,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/street_clean.csv", row.names = FALSE)

# Sidewalk Cafe clean file
write.csv(cafe_clean,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/cafe_clean.csv", row.names = FALSE)

# Open restaurant applications clean file
write.csv(open_clean,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/open_clean.csv", row.names = FALSE)

# Vehicle traffic count clean file
write.csv(vehicle_clean,"C:/Users/pantalaimon/Documents/Grants/DxD2020/Data/Clean/vehicle_clean.csv", row.names = FALSE)
```


