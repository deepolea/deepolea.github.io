# DeepOlea Web Platform

DeepOlea is a technology company based in Gaziantep, Turkey, specializing in transforming artificial intelligence and machine learning into real-world IT solutions. 

This repository contains the source code for the DeepOlea corporate and academic portfolio website. It features a custom-built, lightweight internationalization (i18n) system, responsive design, and a clean architectural separation between commercial projects and academic research.

## 📂 Project Structure

The project follows a clean, modular folder structure to maintain the "Don't Repeat Yourself" (DRY) principle:

    deepolea/
    │
    ├── index.html              # Main landing page
    ├── js/
    │   └── main.js             # Centralized JavaScript (i18n, scroll animations, copy functions)
    ├── lang/
    │   ├── tr.json             # Turkish translation dictionary
    │   └── en.json             # English translation dictionary
    ├── lab/
    │   ├── index.html          # DeepOlea Lab (Academic Works & Papers)
    │   └── fisformer.html      # Academic Project detail page (e.g., FISformer)
    ├── projects/
    │   ├── index.html          # Corporate & Commercial Projects
    │   └── accreditation.html  # DeepOlea Accreditation Platform Project
    └── images/                 # Global assets, logos, and project figures

## Key Features

* **Dynamic i18n (Bilingual Support):** Fully supports Turkish (TR) and English (EN). Translations are fetched asynchronously from JSON files, enabling instant language switching without page reloads. Language preferences are stored in the browser's `localStorage`.
* **FOUC Prevention:** Includes a custom CSS/JS fade-in mechanism to prevent the "Flash of Unstyled Content" (FOUC) during language loads, ensuring a smooth user experience.
* **DeepOlea Lab:** A dedicated sub-directory (`/lab`) showcasing academic research, published papers, and experimental deep learning models, complete with BibTeX citation copy functionality.
* **Corporate Projects:** A separate sub-directory (`/projects`) strictly focused on commercial, AI-supported IT solutions with gallery-style UI showcases.
* **Vanilla Stack:** Built with pure HTML, CSS, and Vanilla JavaScript. No heavy frameworks, ensuring lightning-fast load times and easy maintenance.

## How to Add a New Page or Project

1. **Create the HTML File:** Place the new HTML file in either the `/projects/` or `/lab/` folder depending on its context.
2. **Add the Script Tag:** Ensure the centralized `main.js` is linked at the bottom of the body. Since it's in a sub-folder, use the relative path:
    `<script src="../js/main.js"></script>`
3. **Use Data Attributes for Text:** Do not hardcode text. Use the `data-i18n` attribute for all text elements.
    `<h1 data-i18n="new_project_title">Default Title</h1>`
4. **Update JSON Dictionaries:** Add the corresponding key-value pairs to the bottom of both `lang/tr.json` and `lang/en.json`.
5. **Add Images:** Place all related `.jpg` or `.png` files into the root `/images/` folder (or specific sub-folders) and link them using relative paths.

## Local Testing

Due to the Fetch API used for the JSON translation files, this project must be run on a local web server (opening the HTML file directly via the `file://` protocol will cause CORS errors for the language files). 

**Option 1: Using Python (CLI)**
If you have Python installed, open your terminal in the root project folder (`~/Projects/deepolea.github.io`) and run:
```bash
python3 -m http.server
```
Then, open your browser and go to `http://127.0.0.1:8000`.

**Option 2: Using Visual Studio Code**
1. Install the **Live Server** extension.
2. Right-click `index.html` and select **"Open with Live Server"**.
3. The site will open at `http://127.0.0.1:5500`.

## Deployment

The project is deployed directly to the production server using `rsync`. Since deployment configurations contain sensitive server details (like IP addresses and directory paths), the actual deployment script is not included in this public repository.

If you want to set up your own automated deployment, you can create a local `deploy.sh` file with a command similar to the one below:

```bash
# Example deployment command (replace placeholders with your actual details)
rsync -avz --delete \
  --exclude '.git' \
  --exclude 'deploy.sh' \
  --exclude '.gitignore' \
  --exclude 'README.md' \
  --exclude 'server_password.txt' \
  --chown=www-data:www-data \
  --chmod=D755,F644 \
  ./ USER@YOUR_SERVER_IP:/path/to/remote/directory/ 
```
To deploy all local changes to the live server:
```bash
./deploy.sh
```

*Note: When you run this command, you will be prompted to enter the server's password manually. The script includes a `--delete` flag to keep the server perfectly mirrored with the local directory. To keep your repository clean and prevent leaking server details (like IP addresses and paths), ensure your local `deploy.sh` script is explicitly excluded from version control via `.gitignore`.*

---
*© 2026 DeepOlea · [deepolea.com]*