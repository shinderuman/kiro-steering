# Coding Standards

## General Guidelines
- Write clean, readable, and maintainable code
- Use meaningful variable and function names (avoid names like 'hoge', 'foo', 'bar')
- Add appropriate comments for complex logic
- Follow language-specific conventions and best practices

## Go-specific Guidelines
- Follow Go naming conventions (camelCase for private, PascalCase for public)
- Use descriptive error messages with context
- Prefer explicit error handling over silent failures
- Use consistent logging format across the project
- Group related functionality into well-named functions

## PHP-specific Guidelines
- Use single quotes for string literals by default
- NEVER use variable interpolation inside double quotes
- Use string concatenation with `.` operator or `sprintf()` function
- Use `PHP_EOL` for line breaks instead of `\n`
- For echo statements with line breaks, use comma separator: `echo $foo, PHP_EOL` (not `echo $foo . PHP_EOL`)

### PHP String Examples
```php
// Good
$message = 'Hello world';
$fullMessage = $greeting . ' ' . $name;
$formatted = sprintf('User %s has %d points', $name, $points);
echo $message, PHP_EOL;

// Bad
$message = "Hello world";
$fullMessage = "$greeting $name";
$formatted = "User $name has $points points";
echo $message . PHP_EOL;
```

## Function Organization Guidelines
**CRITICAL RULE: Functions MUST be organized in call order**

- **MANDATORY: When adding ANY new function, place it immediately after the function that calls it**
- **DO NOT place new functions at the end of the file or in random locations**
- **Follow the exact execution flow: if function A calls function B, then function B must be defined immediately after function A**
- Start with main function first, followed by functions it calls directly
- For each function, place its helper functions immediately after it
- This creates a natural top-down reading flow that matches execution order
- Private helper functions should be placed directly under their calling function

### Example Function Order
```go
func main() { ... }

func process() { ... }        // Called by main

func initConfig() { ... }     // Called by process
func fetchData() { ... }      // Called by process
func processData() { ... }    // Called by process

func validateItem() { ... }   // Called by processData
func formatOutput() { ... }   // Called by processData
```

### Enforcement Rules
- Always check the call order before placing a new function
- If you place a function in the wrong location, it MUST be moved to the correct position
- The correct position is always immediately after the calling function, following the natural execution flow
- This is MANDATORY for code readability and maintainability

## Code Review Standards
- Ensure all functions have clear, descriptive names
- Verify error handling is comprehensive and informative
- Check for consistent formatting and style
- Remove any placeholder names or temporary code before committing
- Verify functions are placed in correct call order