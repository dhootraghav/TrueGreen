# Schema Decisions – TrueGreen (MVP)

This document locks the few decisions that are easy to assume incorrectly.
These decisions determine how the database schema and API should be built.

---

## 1) Activity granularity

**Decision:** One Activity represents one site, one activity type, and one reporting period entry.  
**MVP default:** Monthly or bill-period entries (user chooses the period start/end based on the document).  
**Reason:** Works across utilities and geographies without forcing calendar-month assumptions.

---

## 2) Evidence requirements

**Decision:** Evidence is strongly encouraged but not technically mandatory for every activity in MVP.  
**MVP default rule:** 
- Electricity: evidence recommended (bill/invoice).
- Fuel: evidence recommended (receipt/log).
- Travel: evidence recommended (expense record/booking).
- Packaging: evidence recommended (BoM/spec/invoice).

**Reason:** SMEs often start with partial records; blocking entries entirely can reduce adoption.
A later “verification status” can enforce stricter completeness.

---

## 3) Evidence-to-activity relationship

**Decision:** One evidence file can support multiple activities.  
**MVP default:** Yes, allowed.

**Reason:** A single invoice or monthly statement can include multiple line items, or one document may justify multiple entries.  
**Implementation note:** This implies evidence links via a join relationship (or multiple evidence rows referencing the same file key).

---

## 4) Emissions recalculation policy

**Decision:** Calculations are immutable once created. Factor updates do not retroactively change past results.  
**MVP default:** Store Calculation Records that snapshot inputs and reference the exact factor and factor set version used.

**Reason:** Reproducibility and auditability. Past reports must remain consistent over time.

---

## 5) Emission factor scope and granularity

**Decision:** Factors are selected at country level in the MVP.  
**MVP default:** Country-level only (no state / grid region complexity in MVP).

**Reason:** Keeps factor selection deterministic and avoids hard-to-source regional datasets early.

---

## 6) Emissions outputs (MVP)

**Decision:** Store total CO2e only (kg CO2e), plus scope.  
**MVP default:** No gas-level breakdown (CO2/CH4/N2O) in MVP.

**Reason:** Keeps calculations and reporting simple while still being credible and useful.

---

## 7) Units (MVP constraints)

**Decision:** Limit accepted units to reduce conversion complexity.  
**MVP default:**
- Electricity: kWh only
- Fuel: litres only
- Travel: km only
- Packaging: kg only

**Reason:** Prevents unit mismatch errors early; conversions can be added later.

---

## 8) Factor matching strictness

**Decision:** Strict matching for calculations.  
**MVP default:** If no matching factor exists for (country, year, activity type, subtype, unit), calculation fails with a clear “missing factor” error.

**Reason:** Avoids silent approximations that harm trust.

---

## 9) Packaging in MVP

**Decision:** Packaging is captured as quantity-only operational truth in MVP.  
**MVP default:** No packaging emissions calculation in MVP; focus on material quantities for future EPR exports.

**Reason:** Packaging emissions introduce lifecycle boundary complexity and multiple factor methodologies.
Capturing quantities first gives EPR readiness without bloating the MVP.
