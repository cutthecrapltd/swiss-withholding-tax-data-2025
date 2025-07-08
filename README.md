# swiss-withholding-tax-data-2025
Swiss Withholding Tax Data 2025 Compressed
# Swiss Withholding Tax Data 2025

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
