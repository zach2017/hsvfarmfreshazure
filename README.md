# Huntsville Fresh Food Directory

A one-page website that lists farmers markets and pick-your-own farms around Huntsville, Alabama. It shows when each place is open, what it grows, where it is on a map, and why the fruits and vegetables are good for you.

The whole site is a single file: `huntsville-fresh-food-directory.html`.

## Quick start

1. Download `huntsville-fresh-food-directory.html`.
2. Double-click it. It opens in your web browser.
3. Stay connected to the internet the first time, so the styles, map library, and fonts can load.

That's it. There is nothing to install and no server to run.

## What's on the page

| Section | What it does |
| --- | --- |
| Top bar | Links to each section and a yellow button that switches between light and dark mode |
| In season now | Shows the produce that is usually ready to harvest this month |
| Find a market or farm | A searchable list of all 14 places, with filters for type of place and day of the week |
| Map | A pin for every place; tap a pin for a popup with hours, produce, and directions |
| What's good for you | A card for each fruit and vegetable; tap one for health benefits, a picking tip, and where to get it |

## How to use it

- **Search:** type a food, town, or name, such as `peaches`, `Madison`, or `eggs`.
- **Filter:** choose "Farmers Market" or "Pick Your Own", and pick a day in the "Open on" menu.
- **Show on map:** press this on any card to jump to that pin and open its popup.
- **Get directions:** opens Google Maps with the place's full address.
- **Produce chips:** the yellow chips (for example "Apples") open the health-benefits popup.
- **Zoom:** use "Whole region" or "Huntsville close-up" above the map, or the + and − buttons.

## Features

- **Light and dark mode.** The page follows your device setting until you press the button; after that it remembers your choice in that browser.
- **Mobile friendly.** The layout stacks into one column on phones, and buttons are large enough to tap with a thumb.
- **Color-blind friendly.** Meaning never depends on color alone:
  - Markets are green circles; pick-your-own farms are yellow diamonds with a dark outline.
  - In-season months are dark bars with a yellow underline.
  - Open and closed badges use ✓ and ✕.
- **Keyboard friendly.** Every control can be reached with the Tab key and shows a clear focus ring.

## Where the information comes from

| Information | Source |
| --- | --- |
| Names, addresses, hours, produce, category | The file `huntsville_farms_and_markets.csv`, copied into the page unchanged |
| Days of the week and "Open in / Closed in" badges | Worked out by the page from the hours text in the CSV |
| Map pin positions | Estimated from each street and town; not exact |
| Health benefits, picking tips, harvest months | General nutrition and growing knowledge for North Alabama |

Things to keep in mind:

- **Pins are approximate.** The CSV has addresses but no coordinates. Rural farms may be off by more than a few blocks. Use "Get directions" for the exact location.
- **The map is a simple drawing.** It shows the Tennessee River, main highways, and town names, not individual streets.
- **Five foods are extras.** Sweet potatoes, collard greens, okra, watermelon, and sweet corn are not in the CSV. They are included as common market staples and are not tied to a specific farm.
- **One possible typo.** E & J Farms is listed as opening at "8:38 AM" in the CSV. It is shown as written.
- **Hours change.** Many places are seasonal or weather-dependent. Call ahead before a long drive.
- **Not medical advice.** The nutrition notes are general information.

## How to update it

Open the HTML file in any text editor (Notepad, TextEdit, VS Code) and scroll to the `<script>` section near the bottom.

### Add or change a place

1. Find the line that starts with ``const CSV = ` ``.
2. Add or edit a row. Keep the same five columns, in this order:

   ```
   Name,Location,Times,Type of Produce,Category
   ```

3. Put quotes around any value that contains a comma:

   ```
   New Farm Stand,"123 Main St, Huntsville, AL",Saturdays 8:00 AM - 12:00 PM (May-Sep),"Tomatoes, peaches",Farmers Market
   ```

4. Add a map pin for it in the `GEO` list just below, using the exact same name:

   ```js
   "New Farm Stand": [34.7300, -86.5860],
   ```

   The two numbers are latitude and longitude. To find them, right-click the spot in Google Maps and copy the numbers shown.

Tips so the page reads your hours correctly:

- Write days in full with an "s": `Saturdays`, `Mondays - Fridays`, or `Daily`.
- Write months as three-letter ranges in parentheses: `(Apr-Sep)`.
- Use `Pick Your Own` in the Category column for U-pick farms. Anything else is treated as a market.

### Add or change a fruit or vegetable

Find the `PRODUCE` list and copy an existing entry. Each one has:

| Field | Meaning |
| --- | --- |
| `id` | A short unique name with no spaces |
| `name` | What visitors see |
| `color` | The dot color, as a hex code |
| `months` | Harvest months as numbers, where 0 is January and 11 is December |
| `season` | The same months in words |
| `match` | The word to look for in the CSV's produce column, such as `/peach/` |
| `headline`, `benefits`, `tip` | The text shown on the card and in the popup |

### Change the colors

Near the top of the file, inside `<style>`, the colors are listed once for light mode under `:root` and again for dark mode. The main ones:

| Name | Used for |
| --- | --- |
| `--field` | Dark green header |
| `--leaf` | Green buttons and in-season bars |
| `--sun` | Yellow accents |
| `--paper` | Page background |
| `--ink` | Main text |

Change a value in both the light and dark lists to keep the two modes matched.

## What it's built with

- **HTML and JavaScript** in one file, with no build step.
- **Tailwind CSS** (version 4, browser build) for styling.
- **Leaflet** (version 1.9.4) for the map, pins, and popups.
- **Google Fonts:** Alfa Slab One for headings and Figtree for body text.

These three load from the internet when the page opens. If you are offline, the text still appears but the styling and map will not.

## Putting it online

Because it is one file, you can host it almost anywhere:

- Upload it to any web host and rename it `index.html` if you want it to be the home page.
- Drop it into a free static host such as GitHub Pages or Netlify.
- Email it or share it on a USB drive; it opens directly in a browser.

## Troubleshooting

| Problem | Likely cause and fix |
| --- | --- |
| The page looks plain and unstyled | No internet connection, or a content blocker stopped Tailwind from loading. Reconnect and refresh. |
| The map area is blank | Leaflet did not load. Check the connection and refresh. |
| A new place has no pin | Its name in `GEO` does not exactly match its name in the CSV. |
| A new place never shows for the right day | The day names in its hours are abbreviated. Write them in full. |
| Dark mode will not go back to automatic | Clear the site's saved data in your browser, or just use the button. |
