# Hex.Interpolate

Interpolates between two hex colors by a given percentage

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.Interpolate( startHexColour, endHexColour, percentage )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | startHexColour | <span class="type-label string">STRING</span> | :material-check: | The starting hex color (e.g., "#FF0000") |
    | endHexColour | <span class="type-label string">STRING</span> | :material-check: | The ending hex color (e.g., "#0000FF") |
    | percentage | <span class="type-label number">DOUBLE</span> | :material-check: | The interpolation percentage (0.0 = start color, 1.0 = end color) |

    <span class="type-label string">STRING</span> Interpolated hex color

=== "Examples"

    ```dax
    EvaluationContext.Colour.Hex.Interpolate("#FF0000", "#0000FF", 0.5) // Returns "#800080"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.Hex.Interpolate' =
    		(
    			startHexColour: STRING,
    			endHexColour: STRING,
    			percentage: DOUBLE
    		) =>
    
    			// Clamp percentage between 0 and 1
    			VAR _ClampedPercentage = MIN( MAX( percentage, 0 ), 1 )
    
    			// Clean Hex codes
    			VAR _StartHex = SUBSTITUTE( startHexColour, "#", "" )
    			VAR _EndHex = 	SUBSTITUTE( endHexColour, "#", "" )
    
    			// Extract and convert RGB components using your existing Hex.ToInt function
    			VAR _StartR = 	EvaluationContext.Colour.Hex.ToInt( MID( _StartHex, 1, 2 ) )
    			VAR _StartG = 	EvaluationContext.Colour.Hex.ToInt( MID( _StartHex, 3, 2 ) )
    			VAR _StartB = 	EvaluationContext.Colour.Hex.ToInt( MID( _StartHex, 5, 2 ) )
    
    			VAR _EndR = 	EvaluationContext.Colour.Hex.ToInt( MID( _EndHex, 1, 2 ) )
    			VAR _EndG = 	EvaluationContext.Colour.Hex.ToInt( MID( _EndHex, 3, 2 ) )
    			VAR _EndB = 	EvaluationContext.Colour.Hex.ToInt( MID( _EndHex, 5, 2 ) )
    
    			// Interpolate RGB values
    			VAR _InterpolatedR = ROUND( _StartR + ( _EndR - _StartR ) * _ClampedPercentage, 0 )
    			VAR _InterpolatedG = ROUND( _StartG + ( _EndG - _StartG ) * _ClampedPercentage, 0 )
    			VAR _InterpolatedB = ROUND( _StartB + ( _EndB - _StartB ) * _ClampedPercentage, 0 )
    
    			// Convert back to hex using your existing RGB.ToHex function
    			VAR result = 
    				EvaluationContext.Colour.RGB.ToHex(
    					_InterpolatedR,
    					_InterpolatedG, 
    					_InterpolatedB,
    					BLANK()  // No alpha
    				)
    
    			RETURN result
    ```