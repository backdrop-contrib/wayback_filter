# Wayback Filter

As articles age, their links break. This module
offers the reader a working link to the Internet
Archive Wayback Machine in addition to the
old and probably broken links.

This Drupal release was featured on
[The Drop Times](https://www.thedroptimes.com/55408/preserving-web-how-drupals-wayback-filter-uses-internet-archive-mend-broken-links),
highlighting its role in preserving the web by using the Internet Archive to mend broken links and combat link rot.

## Installation

- Install this module using the [official Backdrop CMS instructions](https://backdropcms.org/guide/modules).

## Issues

Bugs and feature requests should be reported in the [Issue Queue](https://github.com/backdrop-contrib/wayback_filter/issues).

## Configuration

The module allows you to configure how and when Wayback links should appear:

- **Wayback link mode**: Choose whether to append a link after the original or replace the original link entirely.
- **Wayback link icon/text**: A Backdrop core icon name (e.g., `archive`, `clock-counter-clockwise`), emoji, Unicode character, or plain text to display for the archive link.
- **Place Wayback links on nodes older than...**: Select how many years old a node must be before links are added. Setting this to 0 means all articles get links.
- **Additional link fields to process**: Specify the machine names of extra link fields that should get Wayback links (one per line). The `body` field is handled separately through the text format filter.

### Backdrop Icon Library

Backdrop CMS includes a built-in icon library that can be used for the Wayback link icon. To use a core icon, simply enter its machine name in the **Icon or text** field.

Recommended core icons:
- `archive` (Default)
- `clock-counter-clockwise`
- `rewind`
- `hourglass`
- `link-break`

For a full list of available icons, you can check the `core/misc/icons` directory or refer to the [Backdrop Icon API documentation](https://docs.backdropcms.org/documentation/icon-api).

## Usage

1. Configure the module at Administer > Configuration > Content authoring > Wayback.
2. If you are processing a text field like `body`, you must also enable the "Add Wayback links" filter for your desired text formats:
   - Go to Administer > Configuration > Content authoring > Text formats.
   - Click "Configure" for the text format you want to use.
   - Check the "Add Wayback links" box under "Enabled filters".
   - Save the configuration.
3. For specific link fields, just add the field's machine name to the "Fields to process" setting in the Wayback configuration.
4. The icon field accepts Backdrop core icon names, emoji, Unicode characters, or plain text. HTML markup is not supported.

Note: The Wayback links are added to external links (`http://` or `https://`) automatically. They are shown regardless of whether the original link is broken or not, providing a "fallback" in case the site dies in the future.

The links only appear on full node view pages (not teasers or listings).

## Porting Notes (Drupal 7 to Backdrop CMS)

This module was ported from Drupal 7 to Backdrop CMS with the following changes:

- **Configuration Management**: Settings are now stored in Backdrop's JSON-based configuration system (`wayback_filter.settings.json`).
- **Architecture**: The link processing was moved from the filter process callback to `hook_preprocess_node()`, matching the Drupal 11 version of the module. This avoids a Backdrop/Drupal 7 issue where text filters run during entity load (before page context exists), which prevented the filter from detecting the current node. The filter is still registered in the text format UI so it can be enabled/disabled per format.
- **D11 Parity**: Settings and functionality (icon support, link field support, append/replace modes) have been aligned with the Drupal 11 version of the module.
- **Icon API Integration**: Added support for Backdrop's core icon library, allowing machine names of core icons to be used as Wayback links.
- **Standards**: Updated hooks and documentation to meet Backdrop CMS standards.

## Current Maintainers

- [Justin Keiser](https://github.com/keiserjb)

## Credits

- Maintained in Drupal by [Steven Snedker](https://www.drupal.org/u/steven-snedker), and
  [Vertikal.dk](https://www.drupal.org/u/vertikaldk).
- Ported to Backdrop CMS in February 2026 by [Justin Keiser](https://github.com/keiserjb).

## License

This project is GPL v2 software. See the LICENSE.txt file in the Backdrop CMS
core directory for details.
