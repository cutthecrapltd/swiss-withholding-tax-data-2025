# swiss-withholding-tax-data-2025
Swiss Withholding Tax Data 2025 Compressed
markdown# Swiss Withholding Tax Data 2025

Compressed withholding tax data for all 26 Swiss cantons.

## Data Structure

- `00_INDEX.json` - Index file with metadata for all cantons
- `[CANTON]_withholding.json` - Individual canton files (e.g., `ZH_withholding.json`)

## Compression Stats

- Original records: 2,804,810
- Compressed records: 66,017
- Compression ratio: 97.6%
- Accuracy: <1% error rate

## Usage in Applications

```javascript
const BASE_URL = 'https://raw.githubusercontent.com/[YOUR-USERNAME]/swiss-withholding-tax-data-2025/main';

// Load index
const index = await fetch(`${BASE_URL}/00_INDEX.json`).then(r => r.json());

// Load specific canton
const loadCantonData = async (cantonCode) => {
  const response = await fetch(`${BASE_URL}/${cantonCode}_withholding.json`);
  return await response.json();
};
Data Format
Each canton file contains:

Tariff codes (A0N, B1Y, etc.)
Income breakpoints
Tax rates
Minimum tax amounts

License
[Your chosen license]

## Step 4: Using the Data in Your Calculator

Once uploaded, you can access your data via:

```javascript
// In your React calculator component
const GITHUB_DATA_URL = 'https://raw.githubusercontent.com/[YOUR-USERNAME]/swiss-withholding-tax-data-2025/main';

// Load data with caching
const loadWithholdingData = async () => {
  // Check if already cached
  if (window.withholdingData) return window.withholdingData;
  
  // Load index first
  const indexResponse = await fetch(`${GITHUB_DATA_URL}/00_INDEX.json`);
  const index = await indexResponse.json();
  
  // Load only needed cantons on demand
  window.withholdingData = { index, cantons: {} };
  
  return window.withholdingData;
};

// Load specific canton when selected
const loadCanton = async (cantonCode) => {
  if (window.withholdingData.cantons[cantonCode]) {
    return window.withholdingData.cantons[cantonCode];
  }
  
  const response = await fetch(`${GITHUB_DATA_URL}/${cantonCode}_withholding.json`);
  const data = await response.json();
  
  // Cache it
  window.withholdingData.cantons[cantonCode] = data;
  return data;
};
