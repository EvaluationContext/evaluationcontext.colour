# HSL.ToHex

Converts HSL color values to hexadecimal format

=== "Syntax"

    ```dax
    EvaluationContext.Colour.HSL.ToHex( h, s, l, alpha )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | h | <span class="type-label int64">INT64</span> | :material-check: | Hue (0-360) |
    | s | <span class="type-label number">DOUBLE</span> | :material-check: | Saturation (0-1) |
    | l | <span class="type-label number">DOUBLE</span> | :material-check: | Lightness (0-1) |
    | alpha | <span class="type-label number">DOUBLE</span> | :material-close: | The alpha value (0-1) |

    <span class="type-label string">STRING</span> Hex color string with optional alpha

=== "Example"

    ```dax
    EvaluationContext.Colour.HSL.ToHex(0, 1, 0.5) // Returns "#FF0000"
    ```

=== "Definition"

    ```dax
    function 'EvaluationContext.Colour.HSL.ToHex' =
    		(
    			h: INT64,
    			s: DOUBLE,
    			l: DOUBLE,
    			alpha: DOUBLE
    		) =>
    		
    			VAR C = ( 1 - ABS(2 * l - 1 ) ) * s
    			VAR X = C * ( 1 - ABS( MOD( H / 60, 2 ) - 1 ) )
    			VAR M = l - C / 2
    		
    			VAR RGB1 = SWITCH(
    				true,
    				h < 60, C & "," & X & ",0",
    				h < 120, X & "," & C & ",0",
    				h < 180, "0," & C & "," & X,
    				h < 240, "0," & X & "," & C,
    				h < 300, X & ",0," & C,
    				C & ",0," & X
    			)
    		
    			VAR RPrime = 		VALUE( LEFT( RGB1, SEARCH(",", RGB1 ) - 1 ) )
    			VAR Remaining = 	RIGHT( RGB1, LEN( RGB1 ) - SEARCH( ",", RGB1 ) )
    			VAR GPrime = 		VALUE( LEFT( Remaining, SEARCH( ",", Remaining ) - 1) )
    			VAR BPrime = 		VALUE( RIGHT( Remaining, LEN( Remaining ) - SEARCH( ",", Remaining ) ) )
    		
    			VAR FinalR = 		ROUND( ( RPrime + M) * 255, 0)
    			VAR FinalG = 		ROUND( ( GPrime + M) * 255, 0)
    			VAR FinalB = 		ROUND( ( BPrime + M) * 255, 0)
    		
    			VAR result =
    				"#" &
    				EvaluationContext.Colour.Int.ToHex(FinalR, 2) &
    				EvaluationContext.Colour.Int.ToHex(FinalG, 2) &
    				EvaluationContext.Colour.Int.ToHex(FinalB, 2) &
    				IF( NOT ISBLANK( alpha ), EvaluationContext.Colour.Int.ToHex( alpha * 255, 2 ) )
    		
    			RETURN result
    ```