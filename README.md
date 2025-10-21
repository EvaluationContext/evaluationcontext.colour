# EvaluationContext.Colour

A DAX UDF library for manipulation of hex colours for Power BI

[![Download From DaxLib](https://img.shields.io/badge/Download%20from%20DaxLib-009688?style=for-the-badge&logo=cloudsmith&logoColor=white)](https://daxlib.org/package/EvaluationContext.Colour/)
[![Download Example PBIP](https://img.shields.io/badge/Download%20Example%20PBIP-607D8B?style=for-the-badge&logo=microsoftpowerbi&logoColor=white)](https://github.com/EvaluationContext/evaluationcontext.colour/tree/main/PowerBI)

## Getting Started

1. Download the library from [DaxLib](https://daxlib.org/package/EvaluationContext.Colour/)
2. Install using TMDL view
3. Start using the functions in your measures
   
For detailed examples, check out our [example PBIP file](https://github.com/EvaluationContext/evaluationcontext.colour/tree/main/PowerBI).

---

## Function Categories

### Conversion Functions
- `Hex.ToInt` - Convert hex colour to integer format
- `Int.ToHex` - Convert integer to hex colour format
- `RGB.ToHex` - Transform RGB values to hex colour
- `HSL.ToHex` - Convert HSL color to hex format

### Hex Colour Manipulation Functions
- `Hex.Hue` - Extract hue component from hex colour
- `Hex.Saturation` - Extract saturation component from hex colour
- `Hex.Luminance` - Extract luminance component from hex colour
- `Hex.Alpha` - Extract alpha channel from hex colour
- `Hex.AdjustHue` - Adjust the hue of a hex colour
- `Hex.AdjustSaturation` - Adjust the saturation of a hex colour
- `Hex.AdjustLuminance` - Adjust the luminance of a hex colour
- `Hex.AdjustAlpha` - Adjust the alpha channel of a hex colour
- `Hex.AdjustColour` - Adjust multiple colour properties simultaneously
- `Hex.TextColour` - Determine optimal text colour (black or white) for contrast

### Theme Functions
- `Hex.Theme` - Use pre-built color palettes
- `Hex.LinearTheme` - Build linear color themes
- `Hex.Interpolate` - Create smooth color transitions between colours

---

Full documentation is available at our [GitHub Pages site](https://evaluationcontext.github.io/evaluationcontext.colour/).

[![Built with Material for MkDocs](https://img.shields.io/badge/Material_for_MkDocs-526CFE?style=for-the-badge&logo=MaterialForMkDocs&logoColor=white)](https://squidfunk.github.io/mkdocs-material/)