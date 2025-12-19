# Contextual background
In Brazil, every infrastructure project with medium/high environmental impact must have an environmental license. In order to do that, one of the steps is to estimate the trade-off needed depending on the impact caused. The math for doing that is relatively straightforward, however, each municipality has its owns rules of trade-off, and there is not a unified platform where the consultants can check the value per type of intervention, and per location. Usually this is a very manual process, where consultants need to visit governmental websites and go through multiple PDFs. Thus, the main motivation of this project is to create an unique platform where the consultants can go and get the trade-off values per type and location of intervention.

# Environmental trade-off calculator

This project is a small full-stack web app to help estimate environmental trade-off for isolated trees, patch and PPA areas, required under local(Sao Paulo municipalities) regulations.

The frontend is a simple HTML/CSS/JavaScript single page with tabs for each workflow, calling the Flask endpoints via fetch and rendering tables with the detailed results and totals.

The backend is a Flask API (with Swagger/OpenAPI docs) that reads compensation rules from CSV files and a SQLite database. It supports three main operations:

Isolated trees – given quantity, group (native/exotic), municipality and whether the species is endangered, the API returns the tree-level trade-off and the total trade-off per item and per lot.

Forest patches / area (m²) – given municipality and patch area, it looks up the trade-off factor (per m²) and computes the total patch trade-off.

Permanent Preservation Area(PPA) – similar to patches, but using a separate rules municipality table for PPA trade-off.

Species conservation status – query a species (family + scientific name) and return its IUCN-style status (EW, CR, EN, VU, etc.). This is useful in case of the consultant not knowing if a specie is endangered or not (this information is required for calculate isolated trees trade-off).

For both cases the compensation will be automatically calculated based on individual municipalities environmental rules.

---
## How to run

You need to create a virtual env(python3.11) 
```
python3.11 -m venv .venv
```

Then install the libraries listed on `requirements.txt`

```
(env)$ pip install -r requirements.txt
```
In order to run the API, inside your virtual env:

```

(env)$ python -m flask --app app run --host 0.0.0.0 --port 5002

```
In sequence, you can use postman or another tool to make requests for the API, examples of possible requests can be found at:
http://127.0.0.1:5002/apidocs/#/

Otherwise, you can open the index.html file contained into the mvp_fullstack_front repository in your browser.

