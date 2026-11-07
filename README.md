# XX Delivery SLA & Capacity Investigation

## Business brief
A fictional XX delivery operator in Riyadh has reported a decline in on-time delivery performance while order volumes have increased. The Head of Operations wants an evidence-based investigation into where delivery time is being wasted and whether existing driver capacity can be allocated more effectively before approving additional hiring of drivers.

I have been asked (as an analyst) to answer:

1. Has on-time delivery performance deteriorated?
2. At which hubs, zones, days, and hours is the problem concentrated?
3. Which delivery-process stage contributes most to late deliveries?
4. Is the pattern associated with demand relative to scheduled driver capacity?
5. Which operational changes are justified by the evidence, and what should be tested before finishing?


## Scope
- Domain: XX delivery operations.
- Geography: fictional Riyadh operating network.
- Period: 1 January–31 December 2025.
- Grain of primary fact: one order record as supplied in the operational export.
- Main analytical unit for capacity: hub × date × hour.
- Primary outcome: on-time delivery against the applicable zone SLA, subject to a documented eligibility rule.

## Data
All supplied records are **synthetic and generated for this portfolio exercise**. They do not describe a real company's data.

Raw files are in [`data/raw/`](data/raw/):
- `orders_raw.csv` — order-level operational export, including event timestamps and status.
- `drivers_raw.csv` — driver master data.
- `driver_shifts_raw.csv` — scheduled driver shifts by date and hub.
- `hubs_raw.csv` — hub reference data.
- `zones_raw.csv` — delivery-zone reference data.
- `sla_targets_raw.csv` — SLA target by zone type.
