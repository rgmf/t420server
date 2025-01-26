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

# Actualización de Nextcloud
Dado que estoy usando Docker, lo que tengo que hacer es actualizar la imagen de Nextcloud de Docker y ejecutar el actualizador desde el contenedor. Estos son los pasos a dar, desde el servidor, dentro de la carpeta nextcloud:

1. Actualizar imagen de Nextcloud: `docker compose pull`
2. Reconstruir el contenedor con la nueva imagen: `docker compose up --force-recreate --build -d`
3. Eliminar las imágenes que estén en desuso: `docker image prune -f`

Ahora, tengo que lanzar el actualizador de Nextcloud desde el contenedor (uso el usuario `33` porque es el usuario del contenedor de Nextcloud, no sé si se podría usar otro u omitir):

`docker compose exec -u 33 -it nextcloud php occ upgrade`

También puedes ver el estado actual (versión incluida) de Nextcloud:

`docker compose exec -u 33 -it nextcloud php occ status`
