# Variables de entorno
Crea un fichero `.env` junto al fichero `docker-compose.yml` con las variables de entorno necesarias. Usa el fichero de ejemplo `.env.sample` para ver qué variables de entorno son necesarias.

# Problemas resueltos y configuración
En la configuración que hay en `nextcloud_data/config/config.php` tuve que añadir:

```php
'overwrite.cli.url' => 'https://nextcloud.rgmf.es',
'overwriteprotocol' => 'https',
'overwritehost' => 'nextcloud.rgmf.es',
```

De esta forma, la aplicación de Nextcloud de Android y DAVx, me funcionó.
