# Hex.AdjustAlpha

Adjusts the alpha component of a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.AdjustAlpha( hexColor, alphaChange )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to adjust (e.g., "#01B8AA") |
    | alphaChange | <span class="type-label number">DOUBLE</span> | :material-check: | The alpha adjustment (-1 to 1) |

    <span class="type-label string">STRING</span> Modified hex color

=== "Examples"

    ```dax
    EvaluationContext.Colour.Hex.AdjustAlpha("#5E81AC", -2.0) // Returns "#5E81AC66"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.AdjustAlpha' =
    		(
    			hexColor: STRING,
    			alphaChange: DOUBLE
    		) =>
    		
    			VAR CleanHex = IF( LEFT( hexColor, 1) = "#", MID( hexColor, 2, 6), MID( hexColor, 1, 6 ) )
    			VAR A = EvaluationContext.Colour.Hex.Alpha( hexColor )
    		
    			VAR NewA = EvaluationContext.Colour.Int.ToHex( MIN( MAX( A + alphaChange, 0 ), 1 ) * 255, 2 )
    		
    			VAR result = "#" & CleanHex & NewA
    		
    			RETURN result
    ```