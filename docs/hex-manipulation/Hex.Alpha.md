# Hex.Alpha

Extracts the alpha component from a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.Alpha( hexColor )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to evaluate (e.g., "#01B8AA") |

    <span class="type-label number">DOUBLE</span> Alpha value (0-1)

=== "Examples"

    ```dax
    EvaluationContext.Colour.Hex.Alpha("#5E81AC") // Returns 0.6
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.Alpha' =
    		(
    			hexColor: STRING
    		) =>
    		
    			VAR CleanHex = IF( LEFT( hexColor, 1) = "#", MID( hexColor, 2, 8), MID( hexColor, 1, 8 ) )
    			VAR AlphaHex = IF( LEN( CleanHex ) = 8, MID( CleanHex, 7, 2 ), "FF" )
    			VAR Alpha = EvaluationContext.Colour.Hex.ToInt( AlphaHex )
    			VAR result = ROUND( Alpha / 255, 4 )
    		
    			RETURN result
    ```