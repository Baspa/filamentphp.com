---
name: Text Input Column with Affix
slug: baspa-text-input-column-affix
author_slug: baspa
categories: [table-builder, table-column, form-field]
description: A TextInputColumn component with prefix and suffix support for labels, icons, and actions
discord_url: https://discord.com/channels/883083792112300104/1367710460182532146
docs_urls:
    v4: https://raw.githubusercontent.com/Baspa/filament-text-input-column-affix/main/README.md
github_repository: Baspa/filament-text-input-column-affix
has_dark_theme: true
has_translations: false
versions: [4]
publish_date: 2024-12-12
---

# Text Input Column with Affix

A powerful extension of Filament's `TextInputColumn` that adds prefix and suffix support for labels, icons, and actions. This component allows you to create more interactive and visually appealing table columns with additional context and functionality.

## Features

- **Prefix and Suffix Labels**: Add text labels before and after the input field
- **Icon Support**: Include icons with customizable colors in prefix and suffix positions
- **Action Buttons**: Add clickable action buttons for enhanced interactivity
- **Inline Layout**: Control whether affixes are displayed inline or as separate elements
- **Full TextInputColumn Compatibility**: Extends all existing TextInputColumn functionality

## Installation

```bash
composer require baspa/filament-text-input-column-affix
```

## Basic Usage

```php
use App\Filament\Tables\Columns\TextInputColumnWithAffix;

TextInputColumnWithAffix::make('price')
    ->prefix('$')
    ->suffix('.00')
    ->numeric()
```

## Prefix and Suffix Labels

Add text labels to provide context for your input fields:

```php
TextInputColumnWithAffix::make('weight')
    ->prefix('Weight: ')
    ->suffix(' kg')
    ->numeric()

TextInputColumnWithAffix::make('email')
    ->prefix('@')
    ->suffix('@company.com')
```

## Icons

Include icons with customizable colors:

```php
TextInputColumnWithAffix::make('phone')
    ->prefixIcon('heroicon-o-phone')
    ->prefixIconColor('success')
    ->suffixIcon('heroicon-o-check-circle')
    ->suffixIconColor('success')

TextInputColumnWithAffix::make('amount')
    ->prefixIcon('heroicon-o-currency-dollar')
    ->prefixIconColor(['primary' => 500])
    ->suffixIcon('heroicon-o-banknotes')
    ->suffixIconColor(['success' => 600])
```

## Actions

Add interactive action buttons:

```php
use Filament\Actions\Action;

TextInputColumnWithAffix::make('quantity')
    ->prefixAction(
        Action::make('decrease')
            ->icon('heroicon-o-minus')
            ->action(fn ($record) => $record->decrement('quantity'))
    )
    ->suffixAction(
        Action::make('increase')
            ->icon('heroicon-o-plus')
            ->action(fn ($record) => $record->increment('quantity'))
    )
```

## Inline Layout

Control whether affixes are displayed inline with the input:

```php
TextInputColumnWithAffix::make('price')
    ->prefix('$')
    ->inlinePrefix() // Display prefix inline
    ->suffix('USD')
    ->inlineSuffix(false) // Display suffix as separate element
```

## Advanced Examples

### Currency Input with Actions

```php
TextInputColumnWithAffix::make('price')
    ->prefix('$')
    ->prefixIcon('heroicon-o-currency-dollar')
    ->prefixIconColor('success')
    ->suffixAction(
        Action::make('calculate_tax')
            ->icon('heroicon-o-calculator')
            ->action(fn ($record, $data) => $record->update(['price' => $data * 1.21]))
    )
    ->numeric()
    ->step(0.01)
```

### Search Input with Clear Action

```php
TextInputColumnWithAffix::make('search')
    ->prefixIcon('heroicon-o-magnifying-glass')
    ->suffixAction(
        Action::make('clear')
            ->icon('heroicon-o-x-mark')
            ->action(fn ($record) => $record->update(['search' => '']))
    )
    ->placeholder('Search...')
```

### Status Input with Visual Indicators

```php
TextInputColumnWithAffix::make('status')
    ->prefixIcon(fn ($state) => match($state) {
        'active' => 'heroicon-o-check-circle',
        'inactive' => 'heroicon-o-x-circle',
        default => 'heroicon-o-question-mark-circle'
    })
    ->prefixIconColor(fn ($state) => match($state) {
        'active' => 'success',
        'inactive' => 'danger',
        default => 'gray'
    })
    ->suffixLabel(fn ($state) => match($state) {
        'active' => '✓',
        'inactive' => '✗',
        default => '?'
    })
```

## Available Methods

### Prefix Methods
- `prefix(string|Htmlable|Closure|null $label, bool|Closure $isInline = false)`
- `prefixAction(Action|Closure $action, bool|Closure $isInline = false)`
- `prefixActions(array $actions, bool|Closure $isInline = false)`
- `prefixIcon(string|BackedEnum|Closure|null $icon, bool|Closure $isInline = false)`
- `prefixIconColor(string|array|Closure|null $color = null)`
- `inlinePrefix(bool|Closure $isInline = true)`

### Suffix Methods
- `suffix(string|Htmlable|Closure|null $label, bool|Closure $isInline = false)`
- `suffixAction(Action|Closure $action, bool|Closure $isInline = false)`
- `suffixActions(array $actions, bool|Closure $isInline = false)`
- `suffixIcon(string|BackedEnum|Closure|null $icon, bool|Closure $isInline = false)`
- `suffixIconColor(string|array|Closure|null $color = null)`
- `inlineSuffix(bool|Closure $isInline = true)`

### Legacy Methods
- `postfix(string|Htmlable|Closure|null $label, bool|Closure $isInline = false)` - Alias for `suffix()`

## Styling

The component uses Filament's built-in styling system and supports all standard TextInputColumn styling options. Affixes are styled consistently with Filament's design system and support dark mode.

## Requirements

- Filament v4
- PHP 8.1+

## License

MIT
