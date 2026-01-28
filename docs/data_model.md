# Data Model – TrueGreen (MVP)

This document defines the minimum set of entities TrueGreen needs to support the MVP workflow:
record operational activities, attach evidence, calculate emissions using versioned emission factors,
and generate traceable outputs.

The model is intentionally small. Anything not required for the MVP workflow is excluded.

---

## 1) Organisation

**What it is:** The business entity whose operational sustainability data is being tracked.  
**Why it exists:** Top-level container for sites and all recorded data.  
**Core fields (conceptual):** Name, created metadata.

---

## 2) Site

**What it is:** A physical or operational unit where responsibility for activities sits (office, factory, store, warehouse).  
**Why it exists:** Groups activities and defines geography for factor selection.  
**Core fields (conceptual):** Organisation reference, site name, country (later can extend to region/state).

---

## 3) Activity

**What it is:** A single operational record for a site over a defined period.  
**Why it exists:** Core unit of tracking and the input to calculations and reporting.  
**MVP activity types:**
- Electricity consumption (kWh)
- Fuel combustion (litres; subtype: diesel/petrol)
- Business travel (km; subtype: car/rail/flight)
- Packaging placed on market (kg; subtype: plastic/paper/metal/glass)

**Core fields (conceptual):** Site reference, activity type, subtype, period start/end, quantity, unit, optional notes.

---

## 4) Evidence

**What it is:** A document supporting an activity entry (bill, receipt, invoice, BoM, spec, log).  
**Why it exists:** Traceability and basic verification.  
**Core fields (conceptual):** Activity reference, storage pointer, filename/type, uploaded metadata, optional notes.

---

## 5) Emission Factor Set

**What it is:** A versioned dataset of emission factors from a named source, tied to a geography and year.  
**Why it exists:** Factors change over time and differ by location; sets preserve reproducibility.  
**Core fields (conceptual):** Source, geography, year, version, status.

---

## 6) Emission Factor

**What it is:** A single conversion value inside a factor set (e.g., diesel litre → kg CO2e).  
**Why it exists:** Deterministic calculation requires precise mapping by activity type, subtype, and unit.  
**Core fields (conceptual):** Factor set reference, activity type, subtype, unit, value (kg CO2e per unit), scope.

---

## 7) Calculation Record

**What it is:** An immutable record of a performed emissions calculation for an activity.  
**Why it exists:** Keeps outputs reproducible and auditable even if factors change later.  
**Core fields (conceptual):** Activity reference, factor set and factor references, normalized quantity/unit, result (kg CO2e), scope, computed timestamp, input snapshot.

**MVP rule:** Electricity, fuel, and travel activities produce calculation records. Packaging does not (quantity-only in MVP).

---

## Relationships (plain English)

- An organisation has many sites.
- A site belongs to one organisation.
- A site has many activities.
- An activity belongs to one site.
- An activity can have multiple evidence files.
- Evidence belongs to one activity.
- A factor set has many factors.
- A factor belongs to one factor set.
- An activity can have zero or one calculation record in MVP.
- A calculation record belongs to one activity and references one factor (and its factor set).
