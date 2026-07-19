# Data Preprocessing Notes

This repo includes `meta_v2building.ipynb`, originally used by [teammate] to build a `meta_v2` table from the full **MM-Food-100K** dataset, including downloading and validating ~100K associated images locally.

**For this submission, only the CSV metadata (`MM-Food-100K.csv`) is used.** The image files were not downloaded, since doing so locally wasn't necessary for this stage of analysis and would require significant disk space and download time.

## What was and wasn't run

- **Cells 0–2** (build metadata from a local `.jsonl` file, then run a sanity check) are **not executed**. These were part of an earlier pipeline step tied to a local file that isn't part of this submission, and are kept in the notebook for reference only.
- **Cell 3** (image path/hash spot-check) and the `file_exists` flag produced in cell 4 are **not meaningful** without the local image folder — `file_exists` will always evaluate to `False` in this environment.
- The core logic actually used is `build_meta_v2_from_csv()` in cell 4, which parses the `ingredients`, `portion_size`, and `nutritional_profile` columns from the raw CSV into structured fields.

## Next steps

If image-level analysis is needed later, the image download step can be added back in using the `image_url` column already present in the CSV.
