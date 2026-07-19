# Data Description & Acquisition

## Project Overview

The system aims to go beyond basic food image classification to act as a practical nutrition assistant. Doing so requires two complementary data sources: a **food dataset** that turns meal photos into structured nutritional signals, and a **customer health dataset** that supplies lifestyle/health context so the same meal can be interpreted differently depending on who's eating it. Combining the two shifts the system from isolated calorie estimation toward context-aware dietary guidance, while avoiding the need to collect private individual medical data.

## Dataset Components

### Food Dataset
Each record links visual, semantic, and nutritional information for a single food item:
- **Image**: real-world photos (restaurant and home-cooked meals, varied lighting/settings)
- **Dish name & ingredients**: structured ingredient-level descriptions for semantic reasoning
- **Cooking method**: e.g. frying, baking, steaming, boiling — important because prep style affects caloric density and fat content, distinguishing nutritionally different versions of visually similar dishes
- **Nutrition estimates**: calories and macronutrient composition, turning the data into a quantitative estimation task rather than pure image classification

### Customer Health Dataset
Provides population-level behavioral and physiological context, used to build representative user archetypes (not individual medical profiles):
- **Activity**: frequency/intensity of movement (work, transport, recreation) → lifestyle segments like sedentary, moderate, highly active
- **Anthropometrics**: clinically measured height, weight, BMI (objective, not self-reported)
- **Baseline health indicators**: additional context relevant to dietary needs

## Relevance to the Project

The food dataset answers *what* is consumed; the customer dataset determines *how* that intake should be interpreted. Mapping food data onto health/activity archetypes lets the system evaluate the same meal differently depending on lifestyle context — enabling personalized, privacy-preserving recommendations instead of generic calorie counts.

## Data Acquisition & Processing

### Food Dataset (from raw MM-Food-100K)
A preprocessing pipeline curated a modeling-ready subset rather than using the raw release directly:
1. **Visual validation** — filtered out low-confidence, ambiguous, synthetic, or non-food images using probabilistic authenticity indicators.
2. **Nutritional consistency check** — cross-checked calorie values against macronutrient composition using standard conversion rules; removed samples with extreme physical inconsistencies while preserving natural variation.
3. **Text normalization** — standardized dish name/ingredient formatting and spelling; parsed portion sizes into structured units for comparable serving scales.
4. **EDA** — examined distributions; flagged long-tailed nutritional variables for later transformation, and retained heavily imbalanced categorical fields as context rather than primary modeling targets.

### Customer Health Dataset (from NHANES 2017–March 2020)
Since NHANES data is split across modular files, acquisition required harmonization:
1. **Schema alignment** — mapped youth and adult physical activity variables into a unified, cross-age-comparable schema.
2. **Merging** — joined body measurement and baseline health variables via respondent ID, keeping only profiling-relevant features and dropping administrative fields; merge strategy prioritized internal consistency over maximizing sample size.
3. **Survey-aware cleaning** — preserved age-restriction-driven missing values as structural (not imputed); screened continuous measurements against documentation guidelines and removed implausible entries.

The result: a curated, quality-controlled food dataset paired with a harmonized behavioral/physiological profile dataset, together forming the foundation for population-segmented, context-aware nutrition guidance.
