# 🚜 Coral Island Crop Analysis (Power BI Report)

## 📖 Project Description
This is my first independent data analytics project. As a fan of the farming simulator video game *Coral Island*, I realized I was making decisions based on "gut feeling" rather than data. I wanted to apply my Power BI skills to a real-world (or game-world) problem: **How do I make the most money with limited resources?**

In the game economy, players face a classic resource allocation problem with limited gold, limited land, and limited time (stamina). You constantly have to choose between:
* **Short-Term Cash Flow:** Buying cheap seeds (e.g., Turnips) that grow fast but have low profit margins.
* **Long-Term Capital Investment:** Saving up for expensive assets (e.g., Almond Trees) that cost 4,000g and take 28 days to mature, but produce fruit indefinitely.

My goal was to move beyond guessing and build a commercial pricing model that projects cumulative profit and identifies the most capital-efficient investments over a 36-month period.

## 💾 About the Dataset & Constraints
I couldn't find a clean dataset that matched the latest game update, so I built my own custom `Crops_Data.csv` using data from v1.1 game telemetry and community wikis. 

**Key Data Constraints & Game Logic:**
* **Season Length:** The game operates on a strict 28-day season. All calculations (Revenue per Season) are capped at this limit.
* **Asset Classes & Depreciation:** The dataset contains 89 distinct assets divided into distinct classes with entirely different depreciation lifecycles:
  1. **Standard Crops:** Single-harvest inventory (e.g., Cauliflower) that requires constant repurchasing.
  2. **Regrowing Crops:** Inventory that produces multiple yields per season (e.g., Blueberries) and requires annual repurchasing.
  3. **Trees & Seedlings:** Permanent capital assets that have a dormant season but do not die after harvest, representing a one-time sunk cost.

## ⚙️ The Technical Challenge: Context Transition & Double-Counting
What started as a simple revenue calculation quickly became a complex DAX modeling challenge. Because of seasonal granularity, **Multi-Season Crops** (like Snowdrops or Lychee) appear as distinct rows for every season they are viable. 

A standard row-level profit calculation resulted in double-counting the initial Capital Expenditure (seed cost) for these assets, artificially tanking their long-term profit margins when aggregated in visual dashboards. 

## 🛠️ The Solution: Amortization & Dynamic DAX Variables
To achieve perfect logic alignment and calculate true cumulative profit, I engineered a series of DAX measures utilizing `VAR` (Variables) and hardcoded arrays (`IN`) to dynamically adjust the math based on the asset class.

* **Asset Amortization:** Implemented DAX logic to identify multi-season crops and automatically amortize (split) their initial seed cost across their active seasons, preventing the engine from double-charging the initial investment.
* **Cumulative 3-Year Profit:** Built sequential DAX measures that separated the initial baseline year from stabilized recurring annual profit, allowing for accurate long-term forecasting.
* **Dynamic 3-Year ROI %:** Developed a nested conditional DAX formula to calculate the true 3-year expenditure based on the specific asset's lifecycle before dividing by the cumulative profit.

<details>
<summary><b>💻 Click to view the Dynamic ROI % DAX Code</b></summary>

```dax
3-Year ROI % = 
VAR MultiSeasonList = {"Cotton", "Hot Pepper", "Lily", "Snowdrop", "Radish", "Avocado", "Banana", "Cocoa Bean", "Dragonfruit", "Jackfruit", "Lemon", "Lychee", "Pear", "Papaya", "Plum", "Rambutan", "Snake Fruit"}

VAR IsMultiSeason = 'Crops_CI'[Crop Name] IN MultiSeasonList

VAR TotalSeedCost_3Yrs =
    IF('Crops_CI'[Asset Class] = "Tree",
        'Crops_CI'[Seed Cost],
        
        IF('Crops_CI'[Asset Class] = "Standard Crop",
            'Crops_CI'[Seed Cost] * 'Crops_CI'[Max Harv per Season] * 3,
            
            IF(IsMultiSeason,
                ('Crops_CI'[Seed Cost] / 2) * 3,
                'Crops_CI'[Seed Cost] * 3
            )
        )
    )

RETURN
DIVIDE([Total Profit Yr 3], TotalSeedCost_3Yrs, 0)
```


## 📈 Key Findings & Results
(Visuals from the Power BI Report will be added here)
