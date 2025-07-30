# Coding Standards

## General Guidelines:
- Write clean, readable, and maintainable code
- Use meaningful variable and function names (avoid names like 'hoge', 'foo', 'bar')
- Add appropriate comments for complex logic
- Follow language-specific conventions and best practices

## Go-specific Guidelines:
- Follow Go naming conventions (camelCase for private, PascalCase for public)
- Use descriptive error messages with context
- Prefer explicit error handling over silent failures
- Use consistent logging format across the project
- Group related functionality into well-named functions

## Code Review Standards:
- Ensure all functions have clear, descriptive names
- Verify error handling is comprehensive and informative
- Check for consistent formatting and style
- Remove any placeholder names or temporary code before committing

## PHP-specific Guidelines:
- Use single quotes for string literals by default
- NEVER use variable interpolation inside double quotes
- Use string concatenation with `.` operator or `sprintf()` function
- Use `PHP_EOL` for line breaks instead of `\n`
- For echo statements with line breaks, use comma separator: `echo $foo, PHP_EOL` (not `echo $foo . PHP_EOL`)

### PHP String Examples:
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
