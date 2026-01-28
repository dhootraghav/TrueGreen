# Core Workflow – TrueGreen (MVP)

This document describes the core user workflow for the TrueGreen MVP. It explains, in plain terms, how a business records operational data, attaches evidence, and receives trustworthy outputs. This workflow is intentionally simple and human-in-the-loop, prioritising accuracy, traceability, and clarity over automation.

---

## 1. Organisation and site setup

A business begins by creating an organisation in TrueGreen. The organisation represents the legal or operational entity whose sustainability data is being tracked.

Within the organisation, the business adds one or more sites. A site represents a physical or operational location where activities occur, such as an office, factory, warehouse, retail store, or other operational unit.

Each site includes a name and a country. The country is used to determine which emission factors apply to activities recorded at that site. No additional operational details are required at this stage to keep setup lightweight for small and medium-sized businesses.

---

## 2. Recording operational activities

TrueGreen focuses on recording real operational activities supported by business documents. For the MVP, four activity types are supported: electricity consumption, fuel combustion, business travel, and packaging placed on the market.

Each activity follows the same core pattern:

* the user selects a site,
* defines a reporting period,
* enters a quantity,
* uploads supporting evidence,
* and saves the activity as an operational record.

The entered quantity is treated as the source data. Uploaded documents serve as supporting evidence and enable later verification.

---

## 3. Electricity consumption workflow

To record electricity consumption, the user selects a site and specifies the reporting period. The user uploads the relevant electricity bill or utility document for that period.

The user then manually enters the total electricity consumed during the period, using the value shown on the bill. For the MVP, electricity is recorded in kilowatt-hours (kWh).

The uploaded document serves as evidence linking the entered value to a real business record. TrueGreen does not automatically extract data from the document in the MVP, included in later scope.

Once the activity is saved, TrueGreen calculates the associated greenhouse gas emissions using the applicable grid electricity emission factor for the site’s country and reporting year. The system records the calculated CO2e value, the assigned emissions scope (Scope 2), and the emission factor details used in the calculation.

---

## 4. Fuel combustion workflow

To record fuel consumption, the user selects a site and specifies the reporting period. The user selects the fuel type, such as diesel or petrol.

The user uploads supporting evidence, such as fuel receipts, invoices, or internal fuel logs, and manually enters the quantity of fuel consumed during the period. For the MVP, fuel is recorded in litres.

The entered quantity is treated as the source data, with the uploaded document providing traceable evidence.

Once saved, TrueGreen calculates emissions using the relevant fuel combustion emission factor. The system records the calculated CO2e value, assigns Scope 1 emissions, and stores the emission factor details and version used.

---

## 5. Business travel workflow

To record business travel, the user selects a site and specifies the reporting period. The user selects the travel mode, such as car, rail, or flight.

The user uploads supporting documents, such as travel invoices, booking confirmations, mileage logs, or expense records, and enters the total distance travelled. For the MVP, travel distance is recorded in kilometres (km).

TrueGreen treats the entered distance as the source data and links it to the uploaded evidence.

Emissions are calculated using the appropriate travel emission factor based on the selected mode. The resulting CO2e value is recorded as Scope 3 emissions, along with the emission factor details and factor set version.

---

## 6. Packaging placed on the market workflow

To record packaging data, the user selects a site and specifies the reporting period. The user selects the packaging material type, such as plastic, paper, metal, or glass.

The user uploads supporting documents, such as bills of materials, packaging specifications, supplier invoices, or production records, and manually enters the quantity of packaging placed on the market during the period. For the MVP, packaging quantities are recorded in kilograms (kg).

Packaging activities record quantities only. No emissions are calculated for packaging in the MVP. The purpose of this activity is to establish accurate, evidence-backed records of packaging placed on the market, which are essential for future EPR-related reporting and analysis.

---

## 7. Emissions calculation and traceability

For activity types where emissions are calculated, TrueGreen performs emissions calculations using predefined emission factor sets. Each site is associated with a country, and emission factors are selected based on site country, reporting year, activity type, and unit.

Each emissions calculation is stored as an immutable calculation record. This record includes the input quantity, normalized unit, calculated CO2e value, assigned emissions scope, emission factor identifier, factor source, year, and factor set version.

This approach ensures that emissions results remain reproducible and auditable even if emission factors are updated in the future.

---

## 8. Viewing results and outputs

Users can view each activity alongside its supporting evidence and any calculated emissions. This provides a clear, traceable link from document to data to result.

TrueGreen can generate simple summaries and exports, such as CSV files, that aggregate operational data and emissions over a selected period. These outputs are designed to support internal tracking and serve as inputs to external ESG or EPR processes without embedding compliance logic directly into the core system.

---

## 9. What the MVP does not do

The MVP does not provide ESG ratings, scores, or narrative assessments. It does not submit EPR filings, calculate regulatory fees, or claim compliance with any specific regulatory framework.

The MVP is intentionally focused on capturing operational truth with evidence and producing transparent, trustworthy outputs that can be used downstream for reporting or compliance purposes.

---

