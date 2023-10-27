# WeGo Public Transit
[WeGo Public Transit](https://www.wegotransit.com/) is a public transit system serving the Greater Nashville and Davidson County area. WeGo provides local and regional bus routes, the WeGo Star train service connecting Lebanon to downtown Nashville, along with several other transit services.

In this project, you'll be analyzing the bus spacing to look for patterns and try to identify correlations to controllable or external factors. Specifically, you'll be using a dataset containing information on the headway, or amount of time between vehicle arrivals at a stop. This dataset contains a column HDWY_DEV, which shows the headway deviation. This variable will be negative when bunching has occurred (shorter headway than scheduled) and will be positive for gapping (longer headway than scheduled). Note that you can calculate headway deviation percentage as HDWY_DEV/SCHEDULED_HDWY.

Goals of this project:
1. How much impact does being late or too spaced out at the first stop have downstream?
2. What is the impact of the layover at the start of the trip (the difference between the first top arrival and departure time)? Does more layover lead to more stable headways (lower values for % headway deviation)?
3. How closely does lateness (ADHERENCE) correlate to headway?
4. What is the relationship between distance or time travelled since the start of a given trip and the headway deviation? Does headway become less stable the further along the route the bus has travelled?
5. How much of a factor does the driver have on headway and on-time performance? The driver is indicated by the OPERATOR variable.
6. How does direction of travel, route, or location affect the headway and on-time performance?
7. How does time of day or day of week affect headway and on-time performance? Can you detect an impact of school schedule on headway deviation (for certain routes and at certain times of day)?
8. Does weather have any effect on headway or on-time performance? To help answer this question, the file bna_weather.csv contains historical weather data recorded at Nashville International Airport. 

# **WeGO Data Dictionary**

## **Definition:**
- **Trip:** 
  A run of the vehicle from one end of the route to another in one direction. Two trips constitute one round trip. The `TRIP_ID` field provides a unique identifier for each trip.

## **Fields:**

- **CALENDAR_ID:** 
  - Identifier for the date.

- **SERVICE_ABBR:** 
  - Indicates the schedule type operating that day.
    * `1` = Weekday
    * `2` = Saturday
    * `3` = Sunday
  - *Note:* Normally corresponds to the day of the week, but sometimes Saturday or Sunday service will run on a weekday (e.g., during a holiday).

- **ADHERENCE_ID:** 
  - Unique identifier for each record.

- **DATE:** 
  - Trip date.

- **ROUTE_ABBR:** 
  - Route identifier.
    * Routes can be found [here](https://www.wegotransit.com/ride/maps-schedules/bus/). 
    * *Example:* Route 55 is Murfreesboro Pike.

- **BLOCK_ABBR:** 
  - Indicates the section (block) of the route that the given stop is on.

- **OPERATOR:** 
  - Indicates the operator (driver).

- **TRIP_ID:** 
  - Identifies the trip.

- **OVERLOAD_ID:** 
  - Signifies a record from a trip added by the dispatcher, not part of the original schedule for the day.
    * `0` = Part of the original schedule.
    * Other = Added trip.

- **ROUTE_DIRECTION_NAME:** 
  - Indicates the direction of the trip, either to downtown or from downtown.

- **TIME_POINT_ABBR:** 
  - *(Description not provided)*.

- **ROUTE_STOP_SEQUENCE:** 
  - *(Description not provided)*.

- **TRIP_EDGE:** 
  - Defines the stop type.
    * `1` = First stop on the trip.
    * `0` = Intermediate stop.
    * `2` = Last stop on the trip.

- **LATITUDE/LONGITUDE:** 
  - Location in lat/long format.

- **SCHEDULED_TIME:** 
  - Scheduled time for the stop.

- **ACTUAL_ARRIVAL_TIME:** 
  - Actual arrival time at the stop.

- **ACTUAL_DEPARTURE_TIME:** 
  - Actual departure time from the stop.

- **ADHERENCE:** 
  - Difference between actual departure time and scheduled time. 
  - Negative indicates departure time after scheduled time, and positive indicates departure time before scheduled time.

- **SCHEDULED_HDWY:** 
  - Scheduled headway in minutes for the given timepoint crossing record. 
  - Headway is the difference between the `SCHEDULED_TIME` and the previous scheduled time for that stop.

- **ACTUAL_HDWY:** 
  - Actual headway. 
  - *Note:* Does not exclude overloads, as we want to know about them for actual headway performance.

- **HDWY_DEV:** 
  - Calculates headway deviation in minutes as the difference between actual and scheduled headway. 
  - Negative values indicate a shorter headway than scheduled (i.e. bunching) and positive values indicate a longer headway than scheduled (i.e. gapping).

- **ADJUSTED_EARLY_COUNT:** 
  - *(Description not provided)*.

- **ADJUSTED_LATE_COUNT:** 
  - *(Description not provided)*.

- **ADJUSTED_ONTIME_COUNT:** 
  - *(Description not provided)*.

- **STOP_CANCELLED:** 
  - Flags whether a crossing was canceled or waived.

- **PREV_SCHED_STOP_CANCELLED:** 
  - Flags whether the previous timepoint crossing was canceled or waived. Useful for excluding records where the headway values are extremely high because the bus is just coming off a detour.

- **IS_RELIEF:** 
  - Flags whether a particular crossing is a relief - i.e. the first timepoint crossing of a new driver on the bus/block.

- **BLOCK_STOP_ORDER:** 
  - *(Description not provided)*.

- **DWELL_IN_MINS:** 
  - Actual Departure Time - Actual Arrival Time (in minutes).
