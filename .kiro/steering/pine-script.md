# Pine Script v6 — TradingView Development

## Language & Version
- Always use Pine Script v6 (`//@version=6`)
- Target platform: TradingView
- Script types: indicators, strategies, and libraries

## Code Structure
- Always start with `//@version=6` as the first line
- Use `indicator()` or `strategy()` declaration immediately after version
- Group related logic into sections with clear `// --- Section Name ---` comments
- Declare inputs at the top, after the indicator/strategy declaration
- Declare variables and constants before main logic
- Place plot statements at the end of the script
- Place alert conditions after plots

## Naming Conventions
- Use camelCase for variables and functions (e.g., `fastLength`, `calcMovingAvg`)
- Use UPPER_SNAKE_CASE for constants (e.g., `MAX_LOOKBACK`, `DEFAULT_LENGTH`)
- Use descriptive names that reflect the trading concept (e.g., `bullishEngulfing`, `trendDirection`)
- Prefix boolean variables with `is` or `has` (e.g., `isBullish`, `hasSignal`)
- Prefix series used as conditions with `cond` or `signal` (e.g., `condLong`, `signalExit`)

## Input Parameters
- Always use `input.*()` functions for configurable values
- Provide sensible default values
- Group inputs using `group` parameter
- Add `tooltip` for non-obvious parameters
- Use appropriate input types: `input.int()`, `input.float()`, `input.bool()`, `input.string()`, `input.color()`, `input.timeframe()`

## Best Practices
- Use `ta.*` namespace for built-in technical analysis functions (e.g., `ta.sma()`, `ta.rsi()`, `ta.crossover()`)
- Use `math.*` for mathematical operations
- Use `str.*` for string operations
- Use `array.*` for array operations
- Avoid repainting: do not reference `close` on unconfirmed bars for signals without `barstate.isconfirmed`
- Use `var` keyword for variables that should persist across bars
- Use `varip` for variables that persist across bars and intrabar updates
- Handle `na` values explicitly with `na()` checks or `nz()` for defaults
- Use `request.security()` correctly — understand its repainting implications
- Use `switch` or ternary `? :` for conditional assignments
- Prefer `math.max()` / `math.min()` over nested ternaries for clamping

## Strategy-Specific Rules
- Always define `strategy()` with explicit `default_qty_type`, `default_qty_value`, `commission_type`, `commission_value`, and `slippage`
- Use `strategy.entry()`, `strategy.close()`, `strategy.exit()` correctly
- Set stop-loss and take-profit with `strategy.exit()` using `stop` and `limit` or `profit` and `loss` parameters
- Include `initial_capital` in strategy declaration
- Consider `process_orders_on_close` and `calc_on_every_tick` settings explicitly

## Plotting & Visuals
- Use meaningful `title` parameters in all `plot()` and `plotshape()` calls
- Use `color.new()` for transparency
- Use conditional colors for dynamic visuals (e.g., green for bullish, red for bearish)
- Use `plotshape()` for signal markers on chart
- Use `bgcolor()` for background highlighting
- Use `hline()` for fixed reference levels

## Error Prevention
- Always check for sufficient bar history before calculations using `bar_index >= requiredBars`
- Use `nz()` to provide fallback values for potentially `na` series
- Avoid division by zero — check denominators
- Be mindful of Pine Script's execution model (once per bar, left to right)
- Limit `request.security()` calls to avoid timeout issues
- Be aware of TradingView's max bars back limitations

## Comments & Documentation
- Add a header comment block explaining the script's purpose, author, and version
- Document the trading logic and signal conditions
- Explain non-obvious calculations
- Note any known limitations or assumptions

## Alerts
- Use `alertcondition()` for custom alert setups
- Provide descriptive `title` and `message` parameters
- Use dynamic placeholders in alert messages: `{{ticker}}`, `{{close}}`, `{{time}}`
