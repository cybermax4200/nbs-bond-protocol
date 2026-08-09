# Credit Methodology

## Carbon Credit Calculation

credits_per_period = (carbon_sequestered_kg / 1000) * credit_conversion_factor

Where `credit_conversion_factor` is set at bond issuance per methodology:
- VERRA-VCS: 1.0 (standard)
- GOLD-STANDARD: 1.0
- ACR: 0.95 (conservative)
- CAR: 1.05 (includes buffer pool)

## Biodiversity Credit Calculation

Biodiversity credits are calculated using project-specific metrics:
- Habitat hectares restored
- Species Abundance Index (SAI) improvement
- Biodiversity Unit (UK BNG methodology)

On-chain, metrics are carried by a report as `BiodiversityMetrics` and converted
with integer-fixed-point rates (100% = `1_000_000`):

credits = ( habitat_ha * 1_000_000 + species_abundance * 100_000 + biodiversity_units * 1_000_000 ) / 1_000_000

## Credit Type Allocation (CouponEngine)

The bond's `credit_type` (Carbon | Biodiversity | Basket) determines how a report
is converted into distributable credits:

- **Carbon**: `credits = carbon_sequestered_kg / 1_000`
- **Biodiversity**: `credits = biodiversity_credit_calculation(metrics)`; requires metrics present
- **Basket**: both are computed, and holders accrue carbon and biodiversity credits
  **separately** (queryable via `accrued_credits_by_type`) plus a combined total

## Oracle Data Sources
- Accredited Auditors: annual baseline verification
- Satellite Imagery: monthly NDVI/biomass proxy
- IoT Sensors: continuous soil carbon/moisture
- Community Monitors: quarterly species surveys
