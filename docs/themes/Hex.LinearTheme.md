# Hex.LinearTheme

Creates a linear gradient variant of a hex color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.LinearTheme( hexColor, variant, steps, linearRange )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The base hex color (e.g., "#01B8AA") |
    | variant | <span class="type-label int64">INT64</span> | :material-check: | The variant index (1-N, wraps around if exceeds steps) |
    | steps | <span class="type-label int64">INT64</span> | :material-check: | The number of steps in the gradient (minimum = 2) |
    | linearRange | <span class="type-label number">DOUBLE</span> | :material-check: | The range of luminance adjustment |

    <span class="type-label string">STRING</span> Gradient variant color in hex format

=== "Examples"

    ```dax
    EvaluationContext.Colour.Hex.LinearTheme("#118DFF", 2, 7, 0.5) // Returns "#0061BBFF"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.LinearTheme' =
    		(
    			hexColor: STRING,
    			variant: INT64,
    			steps: INT64,
    			linearRange: DOUBLE
    		) =>
    		
    			VAR StepSize = linearRange / ( steps - 1 )
    			VAR AdjustedVariant = MOD( variant - 1, steps ) + 1
    			VAR Hex =
    				EvaluationContext.Colour.Hex.AdjustLuminance(
    					hexColor,
    					( (AdjustedVariant - 1) * StepSize ) - ( linearRange / 2 )
    				)
    		
    			RETURN Hex
    ```