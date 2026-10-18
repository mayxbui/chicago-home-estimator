# Chicago Home Estimator

A pricing starting point for real estate agents and homebuyers exploring Chicago homes. Enter a property's characteristics, receive an estimated sale price, and review historical transactions and market context.

This BUSA 310 student prototype supports a pricing conversation. It is not an appraisal or a guaranteed listing or sale price.

## What you can do

- **Get an Estimate:** Enter location, property class, size, age, bedrooms, and bathrooms.
- **Review supporting sales:** See past transactions matched by ZIP and optional neighborhood, then ranked by building-area similarity.
- **Explore Sales:** Review monthly transaction counts, median sale prices, and a comparison of equivalent calendar periods.
- **About:** Understand the data sources, accuracy measures, and limitations.
- **Save a summary:** Download the property inputs and result as a JSON file.

## How to use it

1. Choose **Get an Estimate** on the home page.
2. Select the property's ZIP. Leave the optional Assessor neighborhood as **Not provided** if you do not know its verified code.
3. Select the recorded Assessor property class. Use the property's Assessor record rather than guessing from its ZIP or appearance.
4. Enter building area, land area, year built, bedrooms, and full and half bathrooms. Building area uses exterior measurements and may differ from interior living area in a listing.
5. Choose **See My Estimate**. Today's Chicago date is applied by the server.
6. Review the price, limitations, property details, and historical sales. Choose **Edit Property Details** to correct inputs or explore another scenario.
7. Save a summary if useful, or use **Explore Sales** for broader market context.

The supported properties are selected single-family residential classes and individually owned townhomes or row houses. The tool does not cover every property type or location.

## Understanding the result

The tool uses the group's ZIP-based log-price linear regression. Property size, age, rooms, property class, ZIP, and date-based features contribute to the estimate. The optional neighborhood code only filters historical examples; it does not affect the price.

Recorded sales cover September 1, 2019 through August 11, 2026. Estimates after that period extend the fitted time trend; accuracy for the later period has not been established. Market summaries describe the supplied transaction sample, not every Chicago home or current listings.

Average absolute error describes performance across evaluated sales, not an individual property's price range. No calibrated property-specific prediction interval is provided. Historical examples may differ in condition, renovations, layout, and sale circumstances; review their suitability before using them in a client discussion.

## Preview on your computer

From the `chicago-home-estimator` folder, run:

```text
python -m pip install -r requirements.txt
python dev_server.py
```

Open http://localhost:8000 in your browser. Keep the terminal open while testing and press Ctrl+C to stop. Opening the HTML file directly will not run the Python prediction service.

Try an estimate, edit an input, save a summary, and change the ZIP on the market page. For automated checks:

```text
python -m unittest test_website_model.py test_api.py
```

<!-- ## Project structure

- `public/index.html`: website pages and property form.
- `public/styles.css`: responsive appearance.
- `public/app.js`: navigation, form interactions, and API requests.
- `api/estimate.py`: Python backend for predictions, supporting sales, and market summaries.
- `website_model.py`: the group's existing prediction calculation, unchanged by this migration.
- `app_assets`: supplied data, exported coefficients, and settings used on the server.
- `dev_server.py`: local preview server.

The website uses HTML, CSS, JavaScript, and a Python backend. The requirements file contains the dependencies for this application.

Keep `app_assets/final_model_coefficients.csv` and `app_assets/final_model_settings.json` from the same export together. Other pickle and joblib files are not used for active estimates. Section 11 of `../04_final_model_testing.ipynb` documents the export and checks, with supporting results in `../model_artifacts/zip_log_price/`. The final holdout has been evaluated and should not be reused to select or tune revised models.

Students should review the interface and documentation, make the wording their own, and record coding assistance in the notebook's AI Use Log according to the assignment policy. -->
