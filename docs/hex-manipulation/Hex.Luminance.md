# Hex.Luminance

Extracts the luminance component from a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.Luminance( hexColor )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to evaluate (e.g., "#01B8AA") |

    <span class="type-label number">DOUBLE</span> Luminance value (0-1)

=== "Example"

    ```dax
    EvaluationContext.Colour.Hex.Luminance( "#5E81AC") // Returns 0.52
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.Luminance' =
    		(
    			hexColor: STRING
    		) =>
    		
    			VAR CleanHex = IF( LEFT( hexColor, 1) = "#", MID( hexColor, 2, 6), MID( hexColor, 1, 6 ) )
    			VAR R = EvaluationContext.Colour.Hex.ToInt( MID( CleanHex, 1, 2 ) )
    			VAR G = EvaluationContext.Colour.Hex.ToInt( MID( CleanHex, 3, 2 ) )
    			VAR B = EvaluationContext.Colour.Hex.ToInt( MID( CleanHex, 5, 2 ) )
    		
    			VAR Mx = MAX( MAX( R, G ), B)
    			VAR Mn = MIN( MIN( R, G ), B)
    			VAR Delta = Mx - Mn
    		
    			VAR L = ( Mx + Mn ) / 2
    			VAR result = ROUND( L, 4 ) / 255
    		
    			RETURN result
    ```