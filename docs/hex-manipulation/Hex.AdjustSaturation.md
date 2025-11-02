# Hex.AdjustSaturation

Adjusts the saturation of a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.AdjustSaturation( hexColor, saturationChange )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to adjust (e.g., "#01B8AA") |
    | saturationChange | <span class="type-label number">DOUBLE</span> | :material-check: | The saturation adjustment (-1 to 1) |

    <span class="type-label string">STRING</span> Modified hex color

=== "Examples"

    ```dax
    EvaluationContext.Colour.Hex.AdjustSaturation("#5E81AC", -0.1) // Returns "#6A82A099"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.AdjustSaturation' =
    		(
    			hexColor: STRING,
    			saturationChange: DOUBLE
    		) =>
    		
    			VAR H = EvaluationContext.Colour.Hex.Hue( hexColor )
    			VAR S = EvaluationContext.Colour.Hex.Saturation( hexColor )
    			VAR L = EvaluationContext.Colour.Hex.Luminance( hexColor )
    			VAR A = EvaluationContext.Colour.Hex.Alpha( hexColor )
    		
    			VAR NewS = MIN( MAX( S + saturationChange, 0 ), 1 )
    		
    			RETURN
    				EvaluationContext.Colour.HSL.ToHex( H, NewS, L, A )
    ```