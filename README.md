RAILFLOW
When one train is late, who should wait?
RAILFLOW is a decision-support prototype for planning train movements on a shared rail corridor. Given a delay, failure or track restriction, it compares candidate schedules and recommends where trains should wait, with a plain-language reason. The controller always makes the final call.
Built for Hackathon 2026.
Status: simulation prototype. All inputs are synthetic. There is no live train feed, and RAILFLOW is not connected to signals or field equipment. It is not safety-certified and must not be used for real operations.
The problem
The modeled corridor is Secunderabad ↔️ Wadiaram (70 km), with stations including Bolarum (BMO), Medchal (MED), Manoharabad (MOB) and Wadiaram (WDR).
Section
Length
Track layout
Secunderabad → Bolarum
14.2 km
Double track (separate line per direction)
Bolarum → Wadiaram
55.8 km
Single track (shared, both directions)
On single track, opposing trains can only pass at stations with passing loops. If one train is late, someone has to wait, and where they wait changes every later meeting on the route. Controllers weigh train order, timing and track limits, often within minutes.
How it works
Report. Station staff enter a delay, failure or track restriction (for example, MED–MOB blocked for 25 minutes).
Compare. A constraint solver checks train order, track use and timing against modeled corridor limits, searching candidate train orders and meet points to minimize weighted delay.
Review. The controller sees a recommendation, its estimated impact and the reason. They can accept it or override it.
Solver: CP-SAT (constraint programming). Each solve takes about 3 seconds in our benchmark. Solves are time-limited, so results are feasible, not proven optimal.
Controller view: a simplified Marey chart (time left to right, station position top to bottom). A crossing of two train lines marks a conflict on a shared section.
Features
Disruption reporting: late trains, locomotive failures, signal failures and speed restrictions
Maintenance-window planning: compare candidate start times and estimate their delay cost
Ranked options on a time-distance chart
Plain-language explanations for every recommendation
Human in the loop: RAILFLOW suggests, a person reviews, accepts or overrides
Results (simulation only)
Benchmarked against a first-come-first-served (FCFS) baseline. 30 synthetic trains, 2 random seeds (42 and 101), averages of weighted delay minutes. All solver statuses were FEASIBLE.
Scenario
FCFS
RAILFLOW
Nominal
308.1
301.1
Late priority express
430.6
383.4
Locomotive failure
336.0
334.4
Signal failure + 25 km/h restriction
373.4
371.8
The biggest gain is in the late-express case: 47.3 fewer weighted-delay minutes (about 11%).
These numbers come from a simplified replay on synthetic data. They are not evidence of real-world railway performance.
Demo
Suggested order:
Report a disruption (e.g. MED–MOB blocked for 25 minutes).
Show the recommendation and its reason on the time-distance chart.
Show an override, to demonstrate that the controller stays in charge.
Demo link / recording: [add link here]
Roadmap
Stage
Goals
Now
Working simulation prototype; synthetic benchmark on 30 trains; incident and maintenance planning
Next
Validate on real timetable data; more scenarios and seeds; controller feedback sessions
Later
Pilot with railway stakeholders; safety review before any live use; more corridors
This roadmap is a proposed plan, not a commitment.
Limitations
Synthetic data only; no live feed
Results are feasible solutions within a time limit, not proven optimal
Modeled corridor is simplified (modeled station loops, illustrative Marey chart)
Not safety-certified and not for operational use
