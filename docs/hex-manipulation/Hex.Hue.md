# Hex.Hue

Extracts the hue component from a HEX color

=== "Syntax"

    ```dax
    EvaluationContext.Colour.Hex.Hue( hexColor )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | hexColor | <span class="type-label string">STRING</span> | :material-check: | The hex color to evaluate (e.g., "<span style="color: #01B8AA">■</span> #01B8AA") |

    <span class="type-label int64">INT64</span> Hue value (0-360)

=== "Example"

    ```dax
    EvaluationContext.Colour.Hex.Hue("#FF0000") // Returns 0
    ```

=== "Definition"

    ```dax
    EvaluationContext.Colour.Hex.Hue =
        (
            hexColor: STRING
        ) =>
        
            VAR CleanHex = IF( LEFT( hexColor, 1) = "#", MID(hexColor, 2, 6), MID( hexColor, 1, 6 ) )
            VAR R = EvaluationContext.Colour.Hex.ToInt( MID( CleanHex, 1, 2 ) )
            VAR G = EvaluationContext.Colour.Hex.ToInt( MID( CleanHex, 3, 2 ) )
            VAR B = EvaluationContext.Colour.Hex.ToInt( MID( CleanHex, 5, 2 ) )
        
            VAR Mx = MAX( MAX( R, G ), B)
            VAR Mn = MIN( MIN( R, G ), B)
            VAR Delta = Mx - Mn
        
            VAR H =
                SWITCH(
                    true,
                    Delta = 0, 0,
                    Mx = R, MOD( ( G - B ) / Delta, 6),
                    Mx = G, ( ( B - R ) / Delta ) + 2,
                    Mx = B, ( ( R - G ) / Delta ) + 4
                ) * 60
        
            VAR result = ROUND(H, 0)
        
            RETURN result
    ```