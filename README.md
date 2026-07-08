# 🧙‍♂️ RW3-Windata.fan

**RW3-Windata.fan** is an automated data science pipeline and meta-analytics tool for **Rift Wizard 3**. 

This project uses Optical Character Recognition (OCR) to scrape endgame victory screens shared by the community, cross-references the extracted text against the game's actual Python source code, and generates beautiful data visualizations and Discord-ready summaries of the current endgame meta.

---

## ✨ Features

* **High-Accuracy OCR Scraping:** Uses `EasyOCR` to batch-process folders of Rift Wizard 3 victory screenshots, converting pixel-art UI into structured text data.
* **Source-Code Validation:** Separates Spells from Equipment natively by cross-referencing scraped text directly against Rift Wizard 3's internal source code arrays (`Components.py`, `Equipment.py`, `Spells.py`).
* **Visual Meta Dashboard:** Uses `pandas` and `matplotlib` to generate a 4-panel dashboard showing:
  * Top Winning Spells (Pickrate %)
  * Top Winning Equipment/Components (Pickrate %)
  * Global Game Turn Pacing (Speedrun vs. Stall)
  * Top Priority Purchases & Upgrades
* **The "0%" Report:** Automatically compares the winning data against the game's master spell/item lists to name-and-shame the exact items and spells that have a **0% win representation**.
* **Discord Markdown Generator:** Instantly builds a formatted, emoji-rich summary of the dataset that can be copy-pasted directly into Discord.

---

## 🛠️ How It Works (The Pipeline)

1. **The Scraper:** Reads a designated Google Drive folder full of community victory screenshots.
2. **The Parser:** Uses flexible Regular Expressions (RegEx) to absorb text clipping or boundary anomalies caused by partial image crops, extracting turns, HP, SP, and loadouts.
3. **The Analyzer:** Compiles the clean dataset into a `pandas` DataFrame to crunch median pacing, upgrade priorities, and element frequencies.
4. **The Output:** Renders the visual charts and prints the Discord-ready markdown summary to the console.

---

## 🚀 Usage (Google Colab)

This pipeline is optimized to run in **Google Colab** to take advantage of free GPU-accelerated OCR and easy Google Drive mounting.

### Setup Instructions
1. Upload your cropped Rift Wizard 3 victory screenshots to a folder in your Google Drive (e.g., `MyDrive/RW3/Scraped Images`).
2. Open the main `.py` or `.ipynb` file in Google Colab.
3. Update the `FOLDER_PATH` variable in the script to point to your image folder.
4. Run the cell! The script will:
   * Mount your Google Drive.
   * Process all images and save a dated master text file (e.g., `RW3_wins_data_07.08.26.txt`).
   * Generate the Dashboard, Trash Tier Report, and Discord Summary.

*(Note: If you have already scraped your images and generated the text file, you can use the "Analytics Only" script to instantly re-render the charts without having to process the images again.)*

---

## 🧹 Data Purity & Integrity

To ensure the highest accuracy, the pipeline includes a **Post-OCR Redundancy Audit**. This audit checks for:
* **Ghost Files:** Ensures 100% of the images in the directory were successfully logged.
* **Crop Clipping:** Flags logs where the game's UI text (like Turn numbers) was awkwardly clipped by the edge of the screenshot.
* **Data Purity:** Flags any images that successfully ran through OCR but lack Rift Wizard UI anchors (like `hp`, `spells`, or `equipment`), ensuring meme images or chat screenshots are excluded from the dataset.

---

## 📝 Acknowledgments

* **Rift Wizard 3** by Dylan White - For creating an incredible game with brilliant build diversity.
* Built with `EasyOCR`, `pandas`, and `matplotlib`.
