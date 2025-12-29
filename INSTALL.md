# NXDNReflector-Dashboard2 - Installation Guide

## Prerequisites

Before installing NXDNReflector-Dashboard2, ensure you have:

- A working NXDNReflector installation
- Web server (Apache, Nginx, or lighttpd)
- PHP 7.4 or higher (tested up to PHP 8.3)
- Node.js 16.x or higher
- Git

## Quick Installation

### 1. Install Web Server and PHP

#### Ubuntu/Debian:
```bash
sudo apt update
sudo apt install apache2 php php-cli php-mbstring php-xml git nodejs npm
sudo systemctl enable apache2
sudo systemctl start apache2
```

#### CentOS/RHEL:
```bash
sudo yum install httpd php php-cli php-mbstring php-xml git nodejs npm
sudo systemctl enable httpd
sudo systemctl start httpd
```

### 2. Clone the Repository

```bash
cd /var/www/html
sudo git clone https://github.com/ShaYmez/NXDNReflector-Dashboard2.git
cd NXDNReflector-Dashboard2
```

### 3. Install Dependencies and Build

```bash
sudo npm install
sudo npm run build:css
```

### 4. Set Permissions

```bash
sudo chown -R www-data:www-data /var/www/html/NXDNReflector-Dashboard2
sudo chmod -R 755 /var/www/html/NXDNReflector-Dashboard2
```

**Note**: Replace `www-data` with your web server user if different (e.g., `apache`, `nginx`, `http`).

### 5. Configure Web Server

#### Apache Configuration

Create `/etc/apache2/sites-available/nxdn-dashboard.conf`:

```apache
<VirtualHost *:80>
    ServerName nxdn.yourdomain.com
    DocumentRoot /var/www/html/NXDNReflector-Dashboard2
    
    <Directory /var/www/html/NXDNReflector-Dashboard2>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    
    ErrorLog ${APACHE_LOG_DIR}/nxdn-dashboard-error.log
    CustomLog ${APACHE_LOG_DIR}/nxdn-dashboard-access.log combined
</VirtualHost>
```

Enable the site:
```bash
sudo a2ensite nxdn-dashboard
sudo systemctl reload apache2
```

#### Nginx Configuration

Create `/etc/nginx/sites-available/nxdn-dashboard`:

```nginx
server {
    listen 80;
    server_name nxdn.yourdomain.com;
    root /var/www/html/NXDNReflector-Dashboard2;
    
    index index.php index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
    
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }
    
    location ~ /\.ht {
        deny all;
    }
}
```

Enable the site:
```bash
sudo ln -s /etc/nginx/sites-available/nxdn-dashboard /etc/nginx/sites-enabled/
sudo systemctl reload nginx
```

### 6. Initial Configuration

1. Open your web browser and navigate to `http://nxdn.yourdomain.com/setup.php`
2. Complete the setup wizard with your NXDNReflector configuration
3. Click "Save Configuration"
4. **Important**: Delete the setup file for security:

```bash
sudo rm /var/www/html/NXDNReflector-Dashboard2/setup.php
```

## Troubleshooting

### Permission Issues

If you encounter permission errors:

```bash
sudo chown -R www-data:www-data /var/www/html/NXDNReflector-Dashboard2
sudo chmod -R 755 /var/www/html/NXDNReflector-Dashboard2
sudo chmod -R 777 /var/www/html/NXDNReflector-Dashboard2/config
```

### Log File Access Issues

Ensure the web server can read NXDNReflector log files:

```bash
sudo chmod 755 /var/log/NXDNReflector
sudo chmod 644 /var/log/NXDNReflector/*.log
```

### CSS Not Loading

If styles are missing, rebuild the CSS:

```bash
cd /var/www/html/NXDNReflector-Dashboard2
sudo npm run build:css
```

### Dashboard Shows "Config Not Found"

1. Ensure `config/config.php` exists
2. Check file permissions
3. Rerun the setup wizard at `setup.php`

## SSL/HTTPS Configuration (Recommended)

### Using Let's Encrypt

```bash
sudo apt install certbot python3-certbot-apache
sudo certbot --apache -d nxdn.yourdomain.com
```

For Nginx:
```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d nxdn.yourdomain.com
```

## Updating

To update the dashboard to the latest version:

```bash
cd /var/www/html/NXDNReflector-Dashboard2
sudo git pull origin main
sudo npm install
sudo npm run build:css
```

## Advanced Configuration

### Custom Logo

Place your logo in `img/logo.png` or configure in `config/config.php`:

```php
define("LOGO", "https://example.com/your-logo.png");
```

### Timezone Configuration

Edit `config/config.php`:

```php
define("TIMEZONE", "America/New_York");
```

### GDPR Compliance

Enable callsign anonymization in `config/config.php`:

```php
define("GDPR", true);
```

## Support

For issues and questions:
- GitHub Issues: https://github.com/ShaYmez/NXDNReflector-Dashboard2/issues
- Documentation: https://github.com/ShaYmez/NXDNReflector-Dashboard2
