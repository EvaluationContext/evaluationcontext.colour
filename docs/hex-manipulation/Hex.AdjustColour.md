# Hex.AdjustColour

Adjusts multiple components of a hex color simultaneously

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.AdjustColour( hexColor, hueChange, saturationChange, luminanceChange, alphaChange )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to adjust (e.g., "#01B8AA") |
    | hueChange | <span class="type-label int64">INT64</span> | :material-check: | The hue adjustment in degrees (-360 to 360) |
    | saturationChange | <span class="type-label number">DOUBLE</span> | :material-check: | The saturation adjustment (-1 to 1) |
    | luminanceChange | <span class="type-label number">DOUBLE</span> | :material-check: | The luminance adjustment (-1 to 1) |
    | alphaChange | <span class="type-label number">DOUBLE</span> | :material-check: | The alpha adjustment (-1 to 1) |

    <span class="type-label string">STRING</span> Modified hex color

=== "Example"

    ```dax
    EvaluationContext.Colour.Hex.AdjustColour("#5E81AC", 260, -0.1, 0.4, -0.2) // Returns "#E8EFE766"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.AdjustColour' =
    		(
    			hexColor: STRING,
    			hueChange: INT64,
    			saturationChange: DOUBLE,
    			luminanceChange: DOUBLE,
    			alphaChange: DOUBLE
    		) =>
    		
    			VAR Step1 = IF( HueChange = 0, hexColor, EvaluationContext.Colour.Hex.AdjustHue( hexColor, hueChange ) )
    			VAR Step2 = IF( saturationChange = 0, Step1, EvaluationContext.Colour.Hex.AdjustSaturation( Step1, saturationChange ) )
    			VAR Step3 = IF( luminanceChange = 0, Step2, EvaluationContext.Colour.Hex.AdjustLuminance( Step2, luminanceChange ) )
    			VAR Step4 = IF( alphaChange = 0, Step3, EvaluationContext.Colour.Hex.AdjustAlpha( Step3, alphaChange ) )
    		
    			RETURN Step4
    ```