# RGB.ToHex

Converts RGB color values to hexadecimal format

=== "Syntax"

    ```dax
    EvaluationContext.Colour.RGB.ToHex( red, green, blue, alpha )
    ```

    | Parameter | Type | Required | Description |
    |:---:|:---:|:---:|---|
    | red | <span class="type-label int64">INT64</span> | :material-check: | The red value (0-255) |
    | green | <span class="type-label int64">INT64</span> | :material-check: | The green value (0-255) |
    | blue | <span class="type-label int64">INT64</span> | :material-check: | The blue value (0-255) |
    | alpha | <span class="type-label number">DOUBLE</span> | :material-close: | The alpha value (0-1) |

    <span class="type-label string">STRING</span> Hex color string with optional alpha

=== "Example"

    ```dax
    EvaluationContext.Colour.RGB.ToHex(255, 0, 0) // Returns "#FF0000"
    EvaluationContext.Colour.RGB.ToHex(255, 0, 0, 0.5) // Returns "#FF000080"
    ```

=== "Definition"

    ```dax
    EvaluationContext.Colour.RGB.ToHex =
        (
            red: INT64,
            green: INT64,
            blue: INT64,
            alpha: DOUBLE
        ) =>

            "#" &
            EvaluationContext.Colour.Int.ToHex( red, 2 ) &
            EvaluationContext.Colour.Int.ToHex( green, 2 ) &
            EvaluationContext.Colour.Int.ToHex( blue, 2 ) &
            IF( NOT ISBLANK( alpha ), EvaluationContext.Colour.Int.ToHex( alpha * 255, 2 ) )
    ```