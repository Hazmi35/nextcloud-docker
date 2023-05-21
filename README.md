# nextcloud-docker
Nextcloud Official Container Image but with some additional packages

Available on [Docker Hub](https://hub.docker.com/r/hazmi35/nextcloud) and [GitHub Container Registry](https://github.com/Hazmi35/nextcloud-docker/pkgs/container/nextcloud)!

## Current changes:
- static ffmpeg binary installed, can be used for previews
- bz2 and smbclient php module installed

## ffmpeg previews
To enable ffmpeg previews, add this to your config.php file.
```php
'enable_previews' => true,
  'enabledPreviewProviders' =>
  array (
    0 => 'OC\\Preview\\TXT',
    1 => 'OC\\Preview\\MarkDown',
    2 => 'OC\\Preview\\OpenDocument',
    3 => 'OC\\Preview\\PDF',
    4 => 'OC\\Preview\\MSOffice2003',
    5 => 'OC\\Preview\\MSOfficeDoc',
    6 => 'OC\\Preview\\Image',
    7 => 'OC\\Preview\\Photoshop',
    8 => 'OC\\Preview\\TIFF',
    9 => 'OC\\Preview\\SVG',
   10 => 'OC\\Preview\\Font',
   11 => 'OC\\Preview\\MP3',
   12 => 'OC\\Preview\\Movie',
   13 => 'OC\\Preview\\MKV',
   14 => 'OC\\Preview\\MP4',
   15 => 'OC\\Preview\\AVI',
 )
 ```
