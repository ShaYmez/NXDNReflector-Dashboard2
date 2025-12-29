# Logo Directory

Place your dashboard logo file in this directory.

## Supported Formats

- PNG (.png)
- JPEG (.jpg, .jpeg)
- BMP (.bmp)
- WebP (.webp)
- GIF (.gif)
- SVG (.svg)

## Usage

### Option 1: Auto-Detection (Recommended)

Simply place your logo file with the filename `logo.png`, `logo.jpg`, or any other supported format in this directory. The dashboard will automatically detect and display it.

Example:
```bash
cp /path/to/your/logo.png /var/www/html/NXDNReflector-Dashboard2/img/logo.png
```

The filename must be exactly `logo` (case-insensitive) with one of the supported extensions.

### Option 2: Custom Path

If you prefer a different filename or location, configure it in `config/config.php`:

```php
define("LOGO", "img/my-custom-logo.png");
```

Or use an external URL:

```php
define("LOGO", "https://example.com/your-logo.png");
```

## Notes

- The logo will be automatically scaled to fit within the header
- Recommended size: 200x200 pixels or similar aspect ratio
- Transparent backgrounds (PNG) work best
- The dashboard is responsive and will adjust logo display for mobile devices
