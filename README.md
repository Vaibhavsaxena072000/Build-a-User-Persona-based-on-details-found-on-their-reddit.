# Reddit User Persona Builder

The **Reddit User Persona Builder** is a Python-based tool that takes a Reddit user's profile URL, scrapes their recent posts and comments, analyzes their behavior, writing style, and sentiment, and generates a structured text file that resembles a user research persona — complete with real citations from their Reddit activity.

---

## Features

* Scrape public Reddit profiles via Reddit API
* Analyze posts and comments for:

  * Frequent words and topics
  * Subreddit behavior
  * Emotional tone
  * Writing style
* Build a structured, human-readable persona
* Cite Reddit posts/comments for every insight
* Save the output in a downloadable `.txt` file

---

## Installation

Install the required Python packages:

```bash
pip install praw textblob
python -m textblob.download_corpora
```

> If using Google Colab, the notebook auto-handles package installs and file downloads.

---

## Reddit API Setup

1. Go to [https://www.reddit.com/prefs/apps](https://www.reddit.com/prefs/apps)
2. Click **Create App** or **Create Another App**
3. App type: `script`
4. Fill in:

   * Name: `PersonaBuilder`
   * Redirect URI: `http://localhost:8080`
5. After saving, copy:

   * `client_id` (top-left under the app name)
   * `client_secret` (under "secret")

Update the script with your credentials:

```python
CLIENT_ID = "your_client_id"
CLIENT_SECRET = "your_client_secret"
USER_AGENT = "colab:RedditPersonaBuilder:v1.0 (by /u/your_reddit_username)"
```

---

## Code Structure and Explanation

The main components of the project include:

### 1. `extract_username(url)`

Extracts the Reddit username from a full profile URL.

* Input: `https://www.reddit.com/user/SomeUser/`
* Output: `SomeUser`

### 2. `fetch_user_data(username, limit=30)`

Fetches the user's recent posts and comments using Reddit API.

* Returns two lists: `posts` and `comments`, each with subreddit, text, and URL.

### 3. `build_user_persona(posts, comments)`

Analyzes all textual content to:

* Identify top subreddits
* Extract frequent words
* Determine average sentiment and writing style
* Compose a persona with categorized traits
* Select sample posts/comments as citations

### 4. `save_persona_to_txt(username, persona, citations)`

Takes the analyzed data and writes it into a structured `.txt` file.

* Sections include: Name, Archetype, Motivations, Frustrations, etc.
* Each trait includes a citation from actual Reddit content

### 5. `main(profile_url)`

Pipeline function that:

* Extracts the username
* Calls all helper functions above
* Triggers file download (in Colab)

## Usage Example

```python
profile_url = "https://www.reddit.com/user/Hungry-Move-6603/"
main(profile_url)
```

The script will:

1. Extract the username from the URL
2. Scrape posts and comments (limit 30 each)
3. Build a detailed persona with:

   * Top subreddits
   * Motivations
   * Frustrations
   * Behavior and Habits
   * Goals and Needs
   * Personality
4. Output a `.txt` file like `Hungry-Move-6603_persona.txt`
5. Download it automatically in Colab

---

## Output Example

```
USER PERSONA FOR u/Hungry-Move-6603

-----------------------------------------
Name: u/Hungry-Move-6603
Occupation: Inferred from Reddit activity
Location: Inferred from subreddits
Status: Inferred from comment content
Archetype: Derived from themes (e.g. Explorer, Analyst)
-----------------------------------------

MOTIVATIONS:
- Based on common themes in posts and comments
Cited: "Productive weekend activities in LKO? [removed]..." → https://www.reddit.com/r/lucknow/comments/1lx50qm/productive_weekend_activities_in_lko/

FRUSTRATIONS:
- Common complaints or emotional language
Cited: "Productive weekend activities in LKO? [removed]..." → https://www.reddit.com/r/lucknow/comments/1lx50qm/productive_weekend_activities_in_lko/

BEHAVIOR AND HABITS:
- Posts in lucknow, nagpur, IndiaUnfilter, indiasocial, amiugly
- Writing style: Concise

GOALS AND NEEDS:
- Derived from language like 'I want', 'I hope', etc.
Cited: "Productive weekend activities in LKO? [removed]..." → https://www.reddit.com/r/lucknow/comments/1lx50qm/productive_weekend_activities_in_lko/

PERSONALITY:
- Based on sentiment, writing tone and subreddit types
- Tone: Neutral
- Style: Concise
Cited: "Productive weekend activities in LKO? [removed]..." → https://www.reddit.com/r/lucknow/comments/1lx50qm/productive_weekend_activities_in_lko/
```

---

## Tech Stack

* `praw` — Reddit API wrapper
* `textblob` — sentiment and NLP
* `collections.Counter` — frequency analysis
* `google.colab.files` — download support (for Colab)

---

## Possible Extensions

* Export persona as Markdown or PDF
* Use VADER or BERT for deeper sentiment
* Streamlit app for interactive usage
* Visual dashboards (word clouds, topic maps)

---

## Contributing

Pull requests and suggestions are welcome!

* Add new traits to the persona
* Improve NLP logic (e.g., personality typing)
* Add database or CSV export

---

## License

MIT License — use it freely with attribution.

---

## Author

**Vaibhav Saxena**

