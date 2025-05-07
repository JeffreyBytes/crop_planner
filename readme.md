# Stardew Valley Crop Planner

A tool for planning crop schedules in the Stardew Valley game.

#### **[Live version on github.io](http://jeffreybytes.github.io/crop_planner)**

---

### New in v2

* Multiple year planning
* Import/export plans
* Import existing plans from the old v1 planner
  * (only works if old plans are on the same browser)
* Greenhouse plans separated from outdoor Farm plans
* Improved planner design
* Slightly improved responsive design for mobile devices
* Crop info and Settings moved to pop-out sidebar
* Improved Crop Info panel
* More settings
* More seasonal statistics
* A few keyboard shortcuts:
  * Left/Right arrows = navigate seasons
  * `ESC` = open/close sidebar (opens to crop info)
  * `~` (tilde) = toggle between outdoor farm/greenhouse

---

### Crop Info
Crop info is stored in config.json.
This data is retrieved from game files in `[install dir]/Content/Data/`,
specifically Crops.xnb and ObjectInformation.xnb.
I use [XNBNode by Draivin](https://github.com/Draivin/XNBNode) to decompress these files
and parse them with a Python script to save into the config.json file.

---

### Development Utilities
If you are interested in contributing to the Crop Planner,
I have included some Python utility scripts that I use in my development workflow.
These are located in `./utils/`, and require Python 3 to run.
Each script has its own dependencies:

* `update-config.py` - Updates crop data in config.json using data from decompiled game files
  * **Dependencies**:
     * Stardew Valley
     * [XNBNode](https://github.com/Draivin/XNBNode)
     * `xcompress32.dll` (proprietary dll required by XNBNode, place in XNBNode folder)
* `watch-less.py` - Watches `style.less` for changes and recompiles CSS using Less CSS
   * **Dependencies**:
     * less (Less CSS)
     * less-plugin-clean-css (for minifying the resulting CSS)
     * [Install with npm](https://lesscss.org/usage/#command-line-usage)

---

### Item Prices
All items have a **base price** which the game uses to calculate the sell price (when you ship items) and buy price (when you buy items from stores) of that item. Buy price is simply <code>Base Price * 2</code>.

The calculation for sell price of an item (without added Profession bonuses) is below. The Quality of an item is used numerically as a multiplier: 0 for regular; 1 for silver; 2 for gold.
```
(int) Sell Price = Base Price * (1 + (Quality * 0.25))
```

*Note: some items have sell/buy prices that deviate from the above formulas. These prices are likely hard-coded into the game.*

---

### Profit-per-day
Crop profits-per-day are calculated using the _**minimum sell price**_ of a crop.
Profit per day: `((Total Yields * Sells For) - (Seed Price * Total Plantings)) / (Final Harvest Date - 1)`

**Example 1—Parsnip**

Parsnips take 4 days to grow after the day they are planted.
In Spring, they can be planted six times and yield a total of 6 Parsnips,
assuming replanting occurs on the same day of harvesting.
The last harvest occurs on Day 25.
Seeds cost 20g, and Parsnips sell for a minimum of 35g.
```
((6 * 35g) - (20g * 6)) / (25 - 1)
90g / 24
= 3.75g/day
```

**Example 2—Corn**

Corn takes 14 days to grow after the day it is planted.
In Spring and Fall, it is planted once and can yield a total of 11 Corn.
The last harvest occurs on Day 55.
Seeds cost 150g, and Corn sells for a minimum of 50g.
```
((11 * 50g) - (150g * 1)) / (55 - 1)
400g / 54
= 7.4g/day
```

---

_All copyrighted content (images, textures, etc.) belongs to their respective owners (ConcernedApe / Stardew Valley) and is not included under the MIT license of this project._
