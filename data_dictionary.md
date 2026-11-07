# Data Dictionary

## orders_raw.csv
| Column | Meaning | Initial questions |
|---|---|---|
| OrderID | Operational order identifier | Is it unique in the extract? What do repeated IDs represent? |
| CustomerID | Synthetic customer key | Is it needed for the operational question? |
| HubID | Hub associated with the order | Does it match the zone's assigned hub? |
| ZoneID | Delivery zone | Does every value exist in zones? |
| OrderCreatedAt | Time the order was created | Can it be parsed consistently? |
| ReadyAt | Time the order was ready for dispatch | Can it be missing? |
| AssignedAt | Time a driver was assigned | Can it precede ReadyAt? |
| PickedUpAt | Pickup event timestamp | Can it be missing? |
| DeliveredAt | Delivery completion timestamp | Should it exist for every status? |
| PromisedDeliveryAt | Promised completion timestamp | Is this the correct SLA reference? |
| DriverID | Driver assigned to the order | Does the driver exist in the driver master? |
| DistanceKM | Recorded delivery distance | Is it actual route distance or an estimate? |
| OrderStatus | Delivered, Cancelled, or Failed | Which statuses belong in each KPI denominator? |
| DeliveryFeeSAR | Delivery fee in SAR | Not a core SLA field; retain only if justified |
| FailureReason | Reason recorded for cancellation/failure | Are categories mutually exclusive and complete? |

## drivers_raw.csv
| Column | Meaning |
|---|---|
| DriverID | Synthetic driver identifier |
| CurrentHubID | Driver's current/home hub in the master extract |
| VehicleType | Motorcycle, car, or van |
| JoinDate | Driver start date |
| EmploymentType | Full-time, part-time, or contract |

**Caution:** `CurrentHubID` is not necessarily the hub where a driver worked on a historical date. Use the shift roster to investigate historical allocation.

## driver_shifts_raw.csv
| Column | Meaning | Initial questions |
|---|---|---|
| ShiftID | Shift record identifier | Is it unique? |
| DriverID | Scheduled driver | Does driver exist? |
| ShiftDate | Calendar date of shift | Can it be parsed? |
| ShiftStart | Scheduled local start time | How will hour-level availability be represented? |
| ShiftEnd | Scheduled local end time | Do any shifts overlap? |
| HubID | Hub where shift was scheduled | Can a driver appear at multiple hubs on one date? |

A scheduled shift is not proof that the driver was present, logged into the dispatch system, idle, or available for a new order. Treat this as **scheduled capacity**, not observed real-time capacity.

## hubs_raw.csv
HubID, HubName, Region, OperatingStart, OperatingEnd.

## zones_raw.csv
ZoneID, ZoneName, HubID, ZoneType, ReferenceDistanceKM.

## sla_targets_raw.csv
ZoneType, SLATargetMinutes, EffectiveFrom. Confirm whether SLA should be measured from order creation or another event before finalizing the KPI.
