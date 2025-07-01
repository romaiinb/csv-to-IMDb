# csv-to-IMDb

Import any CSV representing your list of films and ratings straight into your IMDb account with a single command.

No browser automation • No fragile selectors • About half a second per title

---

## What it does

This script processes a simple CSV—`Title`, `Year`, `your rating`—and

1. Looks up missing IMDb IDs (`ttXXXXXXX`) via the free OMDb API.
2. Saves a checkpoint file named `imdb_ratings_ready.csv` for review or editing.
3. Submits each rating (1–10) to your IMDb profile through IMDb’s private GraphQL endpoint using your session cookie.



---

## Prerequisites

|       | Version |
|-------|---------|
| Python| 3.7 or newer |
| Packages | `pandas`, `requests`, `tqdm` |

```bash
pip install pandas requests tqdm
```

---

## Get a free OMDb API key

1. Open <https://www.omdbapi.com/apikey.aspx>
2. Select the Free plan (1,000 requests per day).
3. Confirm the email you receive.
4. Copy the API key that you received by mail (example: `abcd1234`).

---

## Retrieve your IMDb session cookie

1. Log in to IMDb in a desktop browser (Sign in with IMDb)
2. Open Developer Tools (F12) and switch to the Network tab.
3. Click on Doc button (Chrome Browser) or HTML button (FireFox) and select Fetch/XHR sub-categories.
4. Reload the page, click any request, and find 'cookie:', select and Copy the whole cookie string (everything after 'cookie: ').
5. Paste this string into a file named `cookie.txt` (single line).

Keep `cookie.txt` private and delete it after running the import.

---

## Base CSV format

`base.csv` needs only three columns; additional columns are ignored.

```csv
Title,Year,your rating
Sicario,2015,8
Ex Machina,2015,9
Top Gun: Maverick,2022,7
```

* **Title** – film title as written on SensCritique (accents allowed).
* **Year** – four-digit release year.
* **your rating** – integer 1–10.

If you exported a larger file, simply remove or rename extra columns.

---

## Quick start

```bash
# 1. Clone the repository
git clone https://github.com/your-username/csv-to-IMDb.git
cd csv-to-IMDb

# 2. Add your files
#    a) base.csv   (Title, Year, your rating)
#    b) cookie.txt (session cookie copied earlier)

# 3. Run
python csv-to-IMDb.py                # default filenames
# or
python csv-to-IMDb.py path/to/base.csv path/to/cookie.txt
```

When prompted, enter your OMDb key. The script will then:

* Fetch missing IDs and update `const`.
* Write `imdb_ratings_ready.csv`.
* Push ratings to IMDb via GraphQL.

---

## Limits and best practices

* OMDb free tier: 1,000 requests per day.
* IMDb GraphQL: informal limit around 1,000 ratings per day. The script pauses 0.3–0.6 seconds between calls; adjust if needed.
* Privacy: the cookie never leaves your machine or Colab session. Delete `cookie.txt` afterwards.

---

## FAQ

| Question | Answer |
|----------|--------|
| Will this break my IMDb account? | No. Ratings are submitted exactly as if you clicked the star in the web interface. |
| Two-factor authentication enabled? | Disable 2FA temporarily or create an IMDb-only password in account settings. |
| Some titles are not found | Edit `imdb_ratings_ready.csv`, fill in the `const` manually, and rerun the import section. |
| Does it work with Sign in with Apple? | No, only work with Sign in with IMDb. |

---



