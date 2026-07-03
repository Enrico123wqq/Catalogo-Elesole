# Phase 2 - Parser and Field Discovery

Goal: analyze the raw Universal Capture output and produce a readable field inventory.

Input folder:
output/draft/apify_raw/

Expected input files:
universal_capture_sample.json
universal_capture_full.json

Tasks:
1. Read raw Apify dataset.
2. Detect all top level fields.
3. Detect nested fields.
4. Extract technical table keys.
5. Extract attributes and specifications.
6. Count frequency of each field.
7. Classify fields as general, technical, commercial, media, category, variant, raw, or useless.
8. Suggest normalized Dataset Master field names.
9. Produce reports for human review.

Outputs:
output/validated/field_discovery/field_inventory.csv
output/validated/field_discovery/field_inventory.json
output/validated/field_discovery/report_field_discovery.md
output/validated/field_discovery/category_field_matrix.csv
output/validated/field_discovery/normalization_suggestions.csv

Do not generate Odoo import files in this phase.
