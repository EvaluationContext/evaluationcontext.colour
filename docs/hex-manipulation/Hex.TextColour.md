# Hex.TextColour

Determines appropriate text color (black/white) for contrast against background

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.TextColour( backgroundHex )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | backgroundHex | <span class="type-label string">STRING</span> | :material-check: | The background hex color to evaluate (e.g., "#01B8AA") |

    <span class="type-label string">STRING</span> #000000 for dark text or #FFFFFF for light text

=== "Examples"

    ```dax
    EvaluationContext.Colour.Hex.TextColour( backgroundHex )
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.TextColour' =
    		(
    			backgroundHex: STRING
    		) =>
    		
    			VAR L = EvaluationContext.Colour.Hex.Luminance( backgroundHex )
    			VAR result = IF( L > 0.5, "#000000", "#FFFFFF")
    		
    			RETURN result
    ```