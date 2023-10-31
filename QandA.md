### Observation on Arrival and Departure Times

There are a large number of observations where the actual arrival time is the exact same second as the actual departure time. 

**Question:** Are these stops where the bus didn't end up stopping?

**Answer:** Most mid-trip timepoints will only have a single recorded time, but they may still have stopped. If the bus was there for less than a few minutes, then only one time is recorded.

---

### Relationship Between Headway and Adjusted Late or Early Count

**Question:** Is there a relationship between headway and adjusted late or early count? Some headway devs are null, but the late count is 1.

**Answer:** Adjusted late counts are derived from schedule adherence and do not relate directly to headway. Buses with adherence values of beyond negative 6 are generally considered late.

---

### Reasons for Null Value in the Headway Column

**Question:** Besides a bus being the first one on a route, are there any other reasons for a null value in the headway column?

**Answer:** This value will be null for all records where `Trip_Edge = 2` (last stop on trip). This is because we only track headway for departures, and the last stop is an arrival only.

---

### Acceptable Range for Headway Deviation

**Question:** Is there an acceptable range for headway deviation?

**Answer:** Our generally accepted range is 50% to 150% of the scheduled headway. For example, if scheduled headway is 10 minutes, a headway deviation in either direction of 5 minutes or less would be acceptable, even if it isn’t ideal.

---

### Meaning of Adjusted Columns

**Question:** What is the meaning of the adjusted columns (`ADJUSTED_EARLY_COUNT`, `ADJUSTED_LATE_COUNT`, `ADJUSTED_ONTIME_COUNT`), and how are they being adjusted?

**Answer:** "Adjusted" means that some additional logic has been used beyond just the adherence value, where beyond negative 6 is late and beyond +1 is early, with everything in between being on-time. This logic includes scenarios where our staff applied waivers to allow early departures, such as an express bus that has already picked up everyone at a park-and-ride lot and is only dropping people off at the remaining stops. This logic also allows for early timepoint records for all records where `Trip_Edge = 2` (end of trip), since it is not a problem if a bus ends its trip early as long as it didn’t pass other timepoints early along the way.

**Question:** Trip Edges Inconsistencies?

**Answer:** "I suspect the trip ids with additional trip edges may be added service. Check the overload_id field to see if it is not 0. If it is not zero, that is an added trip. It looks like this is the case in the example below.
For the trips with too few edges, there are two possibilities I can think of. It’s possible this is due to cancelled service that did not operate for some reason (breakdown, accident, etc.). This can also happen when an overload_id is present if the overload trip was only a partial trip (for example, a bus covering from the midpoint of a route to the end of the route when the originally scheduled bus broke down mid-trip."

**Question:** How to present results?

**Answer:** "Regarding results to present, I would be interested in particular locations, times of day, and operators with that appear to have either recurring issues or a lot of variation. It would also be interesting to know the degree to which there is (or is not) a relationship between adherence values (which are measured relative to schedule) and headway deviation values (which are measured relative to where the surrounding buses on the same route are in relation to a given bus).
Identifying when and where extended, extreme bunching and gapping incidents occur would also be valuable. For example, if two buses were running right on top of each other for multiple trips, we would want to ask the question of the supervisor as to why this was allowed to continue happening for a long period of time."