# Hex.AdjustHue

Adjusts the hue of a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.AdjustHue( hexColor, hueChange )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to adjust (e.g., "<span style="color: #01B8AA">■</span> #01B8AA") |
    | hueChange | <span class="type-label number">DOUBLE</span> | :material-check: | The hue adjustment in degrees (-360 to 360) |

    <span class="type-label string">STRING</span> Modified hex color

=== "Example"

    ```dax
    EvaluationContext.Colour.Hex.AdjustHue("#5E81AC", 260) // Returns "#67AC5E99"
    ```

=== "Definition"

    ```dax
    EvaluationContext.Colour.Hex.AdjustHue =
        (
            hexColor: STRING,
            hueChange: DOUBLE
        ) =>
        
            VAR H = EvaluationContext.Colour.Hex.Hue( hexColor )
            VAR S = EvaluationContext.Colour.Hex.Saturation( hexColor )
            VAR L = EvaluationContext.Colour.Hex.Luminance( hexColor )
            VAR A = EvaluationContext.Colour.Hex.Alpha( hexColor )
        
            VAR NewH = MOD( H + hueChange + 360, 360 )  // Wrap around 0-360
        
            RETURN
                EvaluationContext.Colour.HSL.ToHex( NewH, S, L, A )
    ```