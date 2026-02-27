# 🚜 Coral Island Crop Analysis (Power BI Report)

### 📊 Project Description
This is my first independent data analytics project. As a fan of the farming simulator video game *Coral Island*, I realized I was making decisions based on "gut feeling" rather than data. I wanted to apply my Power BI skills to a real-world (or game-world) problem: **How do I make the most money with limited resources?**

In the game economy, players face a classic resource allocation problem. You have limited gold, limited land, and limited time (stamina). You constantly have to choose between:
* **Short-Term Cash Flow:** Buying cheap seeds (e.g., Turnips) that grow fast but have low margins.
* **Long-Term Capital Investment:** Saving up for expensive Saplings (e.g., Almond Trees) that cost 4,000g and take 28 days to mature, but produce fruit forever.

My goal was to move beyond guessing and build a report that tells me exactly what to plant and when.


### 💾 About the Dataset
I couldn't find a clean dataset that matched the latest game update, so I built my own (`Crops_Data.csv`) using data from v1.1 game telemetry and community wikis.

**Key Data Constraints & Logic:**
* **Season Length:** The game operates on a strict **28-day season**. All calculations (Revenue per Season) are capped at this limit.
* **Seasonality:** Most crops only grow in a specific season (e.g., Spring). However, the dataset accounts for **Multi-Season Crops** (like Snowdrops or Hot Peppers) which appear as distinct entries for each season they are viable in.
* **Asset Classes:** I added a custom classification to distinguish between:
    * **Standard Crops:** Single-harvest inventory (e.g., Cauliflower).
    * **Regrowing Crops:** Inventory that produces multiple yields per season (e.g., Blueberries).
    * **Trees (Saplings):** Permanent capital assets that have a "Dormant Season" but do not depreciate (die) after harvest.

### 📈 Key Findings & Results
*(Visuals from the Power BI Report will be added here)*
