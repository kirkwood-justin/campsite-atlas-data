# Campsite Atlas Open Data

Every campground in the U.S. federal recreation system (Forest Service, Army
Corps, National Park Service, BLM, Bureau of Reclamation, Fish & Wildlife),
cleaned from the Recreation.gov RIDB full export and refreshed nightly.
This repository snapshot: data retrieved September 06, 2026.

## campgrounds.csv (one row per campground, 5,780 rows)
| Column | Meaning |
|---|---|
| `facility_id` | RIDB facility id; page at campsiteatlas.com/campgrounds/{id}/ and booking at recreation.gov/camping/campgrounds/{id} |
| `name`, `state`, `agency`, `rec_area` | Identity; agency is the RIDB abbreviation (FS, NPS, USACE, BLM, BOR, FWS) |
| `lat`, `lon` | Facility coordinates; blank when RIDB reports 0,0 (unknown) |
| `reservable` | True when bookable on Recreation.gov; False = first-come, first-served |
| `total_sites` | Campsite count from site-level records |
| `electric`, `water`, `sewer` | True when at least one site reports the hookup |
| `pets`, `campfires` | True when at least one site allows it |
| `max_rv_length_ft` | Largest max-vehicle-length reported by any site; blank if none |
| `confirmed_free` | True only when the official fee record explicitly says no fee |
| `book_url`, `nps_url` | Recreation.gov booking page; official NPS campground page when one exists |

Amenity flags roll up from campsite records, so they mean "available somewhere
in this campground," not "every site." Absence of `confirmed_free` is not proof
a campground charges.

## Refresh cadence
The site's nightly job republishes this file at https://campsiteatlas.com/data/;
this repository syncs from it daily (`.github/workflows/sync.yml`). The commit
log is the changelog. `SNAPSHOT.txt` carries the retrieval date.

## License
Public-domain federal data; this compilation is dedicated to the public domain
under [CC0 1.0](LICENSE). Attribution appreciated: [Campsite Atlas](https://campsiteatlas.com).
Questions or corrections: [open an issue](https://github.com/kirkwood-justin/campsite-atlas-data/issues).
