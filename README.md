# ⚕️ MediChat AI – Online Doctor Consultation Application

A beginner-friendly web app built with **Python**, **Streamlit** and **Google Gemini** that gives
**general health information**, explains possible causes in simple language, suggests which
**type of specialist** to see, and tells users when to seek medical help.

> ⚠️ **Medical disclaimer:** This application is **not a replacement for a qualified doctor**.
> It never provides a confirmed diagnosis and never prescribes medicines or dosages.
> In an emergency, contact your local emergency number or go to the nearest hospital immediately.

---

## ✨ Main Features

- **Patient information** – name, age, optional gender and basic health notes (with validation)
- **AI consultation** – describe symptoms and get possible causes, a suggested specialist and an urgency level
- **7 medical categories** – General Physician, Cardiologist, Dermatologist, Neurologist, Dentist, Pediatrician, Orthopedic Specialist
- **Chat interface** – ask follow-up questions; history is kept during the session
- **Symptom form** – structured input (symptoms, duration, severity)
- **Medical safety** – emergency keyword detection, no diagnosis, no prescriptions, disclaimers on every page
- **Privacy** – no database, nothing saved to disk, one-click "Delete my data & chat"
- **Modern, mobile-friendly dashboard** with sidebar navigation

## 🧰 Technologies Used

| Technology | Purpose |
|---|---|
| Python 3.10+ | Main language |
| Streamlit | Web interface |
| Google AI Studio + Gemini API | AI responses (Flash model) |
| `google-genai` SDK | Official Google Gen AI Python SDK |
| GitHub | Source code hosting |
| Streamlit Community Cloud | Free deployment |

## 📁 Project Files

```
your-project/
├── app.py            # the application
├── requirements.txt  # Python libraries
└── README.md         # this guide
```

---

## 🖥️ Installation (Local Computer)

1. **Install Python 3.10 or newer** from <https://www.python.org/downloads/> (tick "Add Python to PATH" on Windows).
2. **Put the three files in one folder** and open a terminal inside it.
3. **Create a virtual environment** (an isolated space for this project's libraries):

   ```bash
   python -m venv venv
   ```

4. **Activate it:**

   - Windows: `venv\Scripts\activate`
   - macOS / Linux: `source venv/bin/activate`

5. **Install the libraries:**

   ```bash
   pip install -r requirements.txt
   ```

## 🔑 Get a Gemini API Key from Google AI Studio

1. Open <https://aistudio.google.com/> and sign in with your Google account.
2. Click **Get API key** (left menu) → **Create API key**.
3. Copy the key. **Treat it like a password – never share it or put it in your code or on GitHub.**

## 🔐 Configure the API Key

The app looks for `GEMINI_API_KEY` first in an **environment variable**, then in **Streamlit secrets**.

### Option A – Streamlit secrets (recommended)

1. In your project folder, create a folder named `.streamlit`.
2. Inside it, create a file named `secrets.toml` containing:

   ```toml
   GEMINI_API_KEY = "paste-your-key-here"
   ```

3. **Protect it:** create a file named `.gitignore` in your project folder containing this line so the
   key is never uploaded to GitHub:

   ```
   .streamlit/secrets.toml
   ```

### Option B – Environment variable

- Windows (PowerShell): `$env:GEMINI_API_KEY="paste-your-key-here"`
- macOS / Linux: `export GEMINI_API_KEY="paste-your-key-here"`

### Optional – choose a different model

Model names change over time. The app tries `gemini-3.5-flash`, then `gemini-2.5-flash`.
To force a model, add this to `secrets.toml` (or set it as an environment variable):

```toml
GEMINI_MODEL = "model-name-from-google-ai-studio"
```

## ▶️ Run the App Locally

```bash
streamlit run app.py
```

Your browser opens at <http://localhost:8501>. Press `Ctrl + C` in the terminal to stop it.

---

## 🧪 How to Test the Application

| Test | What to do | Expected result |
|---|---|---|
| App starts | `streamlit run app.py` | Header and sidebar appear, no red errors |
| Missing key | Remove the key and send a chat message | A clear "API key not found" message; sidebar shows ❌ |
| Validation | Save Patient Information with an empty name | Red error messages |
| Normal consultation | Symptom Form: "mild sore throat for 2 days" | Possible causes, specialist, urgency, tips, no medicine names |
| Emergency | Chat: "I have chest pain and trouble breathing" | 🚨 emergency notice appears first |
| Medicine request | Chat: "Which tablet and dose should I take?" | AI politely refuses to prescribe |
| Chat memory | Ask a follow-up like "Is that serious?" | AI answers using earlier context |
| Privacy | Click **Delete my data & chat** | Chat and patient profile are cleared |
| Mobile | Open the page on a phone or shrink the browser | Layout stacks neatly |

**Common problems**

- *"API key rejected"* → check the key; make sure `secrets.toml` is inside `.streamlit/`.
- *"Model not found"* → set `GEMINI_MODEL` to a model listed in Google AI Studio.
- *"Quota / too many requests"* → wait a minute (free tier has limits).
- *`ModuleNotFoundError`* → activate your virtual environment and run `pip install -r requirements.txt`.

---

## 🐙 Upload the Project to GitHub

1. Create a free account at <https://github.com/>.
2. Click **+ → New repository**. Name it (e.g. `medichat-ai`), choose **Public** (needed for the free Streamlit plan unless you link a private repo), and click **Create repository**.
3. Install Git from <https://git-scm.com/downloads>, then run these commands in your project folder:

   ```bash
   git init
   git add app.py requirements.txt README.md .gitignore
   git commit -m "Initial commit: MediChat AI"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/medichat-ai.git
   git push -u origin main
   ```

   (Sign in when asked. If GitHub requests a password, create a *Personal Access Token* under
   Settings → Developer settings.)

4. **Check:** open your repository on GitHub and make sure `secrets.toml` is **not** there.

> No Git? On your repository page choose **Add file → Upload files** and drag in `app.py`, `requirements.txt` and `README.md`.

## ☁️ Deploy on Streamlit Community Cloud

1. Go to <https://share.streamlit.io/> and sign in with GitHub.
2. Click **Create app** (or **New app**) → choose **Deploy a public app from GitHub**.
3. Select your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings → Secrets** and paste:

   ```toml
   GEMINI_API_KEY = "paste-your-key-here"
   ```

5. Click **Deploy**. After a minute or two you get a public link like `https://your-app.streamlit.app`.

To update the app later, push changes to GitHub (`git add .`, `git commit -m "update"`, `git push`) – it redeploys automatically.

## 🔒 Privacy and Safety Notes

- The app has no database and writes nothing to disk; data lives only in the browser session.
- Messages are sent to Google's Gemini API. Review Google's terms for your API tier, and tell users not to enter ID numbers, phone numbers or addresses.
- Safety rules are built into the AI instructions **and** a local keyword check, but no system is perfect. Always see a qualified doctor for real medical decisions.

## 📜 License

Free to use for learning and personal projects. Not intended for real clinical use.# komail
