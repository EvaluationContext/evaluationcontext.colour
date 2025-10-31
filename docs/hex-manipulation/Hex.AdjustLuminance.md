# Hex.AdjustLuminance

Adjusts the luminance of a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.AdjustLuminance( hexColor, luminanceChange )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to adjust (e.g., "#01B8AA") |
    | luminanceChange | <span class="type-label number">DOUBLE</span> | :material-check: | The luminance adjustment (-1 to 1) |

    <span class="type-label string">STRING</span> Modified hex color

=== "Example"

    ```dax
    EvaluationContext.Colour.Hex.AdjustLuminance("#5E81AC", 0.4) // Returns "#E5EAF199"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.AdjustLuminance' =
    		(
    			hexColor: STRING,
    			luminanceChange: DOUBLE
    		) =>
    		
    			VAR H = EvaluationContext.Colour.Hex.Hue( hexColor )
    			VAR S = EvaluationContext.Colour.Hex.Saturation( hexColor )
    			VAR L = EvaluationContext.Colour.Hex.Luminance( hexColor )
    			VAR A = EvaluationContext.Colour.Hex.Alpha( hexColor )
    		
    			VAR NewL = MIN( MAX( L + luminanceChange, 0 ), 1 )
    		
    			RETURN
    				EvaluationContext.Colour.HSL.ToHex( H, S, NewL, A )
    ```