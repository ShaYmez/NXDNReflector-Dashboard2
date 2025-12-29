# Changelog

All notable changes to NXDNReflector-Dashboard2 will be documented in this file.

## [2.0.1] - 2025-01-28

### Added
- Initial release of NXDNReflector-Dashboard2
- Modern glass-morphism UI design with Tailwind CSS
- Real-time dashboard updates via JavaScript (5-second polling)
- Live transmission (TX) detection and display
- Connected repeater monitoring
- Last heard list with timestamp, callsign, target, and repeater
- System information display (uptime, CPU load, temperature, disk usage)
- Setup wizard for easy initial configuration
- GDPR-compliant callsign anonymization option
- QRZ.com integration for callsign lookups
- Logo support (local files or external URLs)
- Responsive design for desktop, tablet, and mobile
- Support for PHP 7.4 through 8.3

### Features
- **Dashboard Layout**: Based on YSFReflector-Dashboard2 design
- **NXDN Log Parsing**: Custom parser for NXDNReflector log format
- **TX Detection**: Smart transmission detection with 180-second timeout
- **Live Updates**: No page reloads required, fully dynamic updates
- **System Monitoring**: CPU, temperature, disk, and uptime tracking
- **Customizable Branding**: Dashboard name, tagline, and logo configuration

### Technical Details
- Adapted from YSFReflector-Dashboard2 codebase
- Modified log parsing for NXDN format differences:
  - "Transmission from CALLSIGN at REPEATER to TG XXXX" format
  - "Currently linked repeaters" format
  - Different transmission end markers
- Updated configuration for NXDNReflector paths and settings
- Changed "Gateways" terminology to "Repeaters" for NXDN context
- Talk Group (TG) display instead of reflector ID

### Configuration
- Default log path: `/var/log/NXDNReflector/`
- Default log prefix: `NXDNReflector`
- Default config path: `/etc/NXDNReflector.ini`
- Default executable path: `/usr/local/bin/NXDNReflector`

### Known Issues
- None at release

### Credits
- Based on YSFReflector-Dashboard2 by M0VUB (ShaYmez)
- Adapted for NXDNReflector compatibility
- Built with Tailwind CSS 3.4

---

## Version History

### Legend
- **Added**: New features
- **Changed**: Changes in existing functionality
- **Deprecated**: Soon-to-be removed features
- **Removed**: Removed features
- **Fixed**: Bug fixes
- **Security**: Vulnerability fixes
