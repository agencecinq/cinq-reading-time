# CINQ Reading Time

WordPress plugin that stores an estimated reading time (minutes) on posts and exposes a raw integer API. No settings screen.

## Requirements

- WordPress 6.0+
- PHP 8.1+

## Install as a must-use plugin (recommended)

Copy the single file into `mu-plugins` (WordPress loads PHP files in that folder automatically; no activation step):

```bash
cp cinq-reading-time.php wp-content/mu-plugins/
```

Or clone the repo and symlink:

```bash
git clone git@github.com:agencecinq/cinq-reading-time.git
ln -s "$(pwd)/cinq-reading-time/cinq-reading-time.php" wp-content/mu-plugins/cinq-reading-time.php
```

## Install as a regular plugin

1. Copy the folder to `wp-content/plugins/cinq-reading-time`
2. Activate **CINQ Reading Time** in the WordPress admin

## API

```php
// Minutes for the current post in the loop, or a given ID.
$minutes = cinq_reading_time();
$minutes = cinq_reading_time( 42 ); // int, 0 when empty
```

Stored under the private meta key `_cinq_reading_time`. Recalculated on every post save.

### Optional filter

```php
add_filter( 'cinq_reading_time_wpm', fn () => 180 );
```

Default: 200 words per minute.

## Theme usage

```php
$minutes = function_exists( 'cinq_reading_time' ) ? cinq_reading_time( $post_id ) : 0;
```

Timber / Twig: keep formatting in the theme (`%d min read`). This plugin only returns the number.

## Scope

- Post type: `post` only
- No options, no admin UI, no shortcode
