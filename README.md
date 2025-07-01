# csv-to-IMDb
Easily import your movie list and personal ratings from a CSV file directly into your IMDb account.



Automatically import your movies ratings to IMDb using the OMDb API and IMDb’s internal GraphQL endpoint.

Description

csv-to-IMDb.ipynb is a one-stop script that will:
	1.	Fill in the const column in your base.csv by fetching IMDb IDs (ttXXXXXXX) via the OMDb API.
	2.	Save an intermediate file named imdb_ratings_ready.csv for backup or manual review.
	3.	Submit each rating (1–10) to your IMDb account using the GraphQL API and your session cookie.

Prerequisites
	•	Python 3.7 or newer
	•	Python packages:
	•	pandas
	•	requests
	•	tqdm

**Install dependencies with:**

pip install pandas requests tqdm


**Getting an OMDb API Key**
	1.	Navigate to: https://www.omdbapi.com/apikey.aspx
	2.	Choose the Free plan (up to 1,000 requests per day).
	3.	Complete the signup form and confirm your email.
	4.	Copy the API key (e.g., abcd1234) for use in the script.

**Retrieving IMDb Session Cookies**

To authenticate without Selenium, export your IMDb session cookie:
	1.	Log in to IMDb in your web browser.
	2.	Open Developer Tools (F12) and go to the Network tab.
	3.	Filter by Fetch/XHR and reload the page.
	4.	Click any request, then under Headers → Request Headers, copy the Cookie header value.
	5.	Paste this cookie string into a file named cookie.txt (single line).

**Usage**
	1.	Place the following two files in the same directory as the script:
	•	base.csv (SensCritique export with columns: Title, Year, your rating)
	•	cookie.txt (IMDb session cookie)
	2.	Run the script csv-to-IMDb.ipynb


	3.	When lunched, enter your OMDb API key.
	4.	The script will:
	•	Fetch missing IMDb IDs via OMDb.
	•	Create imdb_ratings_ready.csv.
	•	Submit your ratings to IMDb via GraphQL.

**Optional Arguments**

You can supply custom file paths:

python import_imdb_ratings.py path/to/base.csv path/to/cookie.txt

**Security & Limits**
	•	Cookie privacy: Keep cookie.txt secure and delete it after use.
	•	OMDb quota: 1,000 requests per day (free plan).
	•	IMDb rate limit: Approximately 1,000 ratings per day.

**Contributing**

Contributions are welcome! Please open an issue or submit a pull request.

