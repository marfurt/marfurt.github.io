---
layout: docs
title: Compression serveur GZip
description: Learn about gzip compression on server-side.
group: web
lang: fr
---

## Client

La requête doit contenir le header `Accept-Encoding: gzip, deflate`.


## Serveur

La réponse doit contenir le header `Content-Encoding: gzip`

Apache offre deux possibilités de compression:
- `mod_deflate` est standard et simple à mettre en oeuvre
- `mod_gzip` permet de pré-compresser le contenu


### mod_deflate

Voir la [documentation Apache](http://apache.org).

Une possibilité est de spécifier les extensions des fichiers devant être compressés:

	<IfModule mod_deflate.c>
    	<filesMatch "\.(js|css|html|php)$">
        	SetOutputFilter DEFLATE
	    </filesMatch>
	    
		# S'assure que les proxies renvoient le bon contenu
		Header append Vary User-Agent env=!dont-vary
	</IfModule>
	
Une autre possibilité est d'utiliser le MIME type pour spécifier les fichiers à compresser:

	<IfModule mod_deflate.c>
		SetOutputFilter DEFLATE
		DeflateCompressionLevel 9 # De 1 (faible) à 9 (fort)
	</IfModule>

	<Location />
		AddOutputFilterByType DEFLATE text/plain text/xml text/html text/css
		AddOutputFilterByType DEFLATE image/svg+xml
		AddOutputFilterByType DEFLATE application/xhtml+xml
		AddOutputFilterByType DEFLATE application/xml
		AddOutputFilterByType DEFLATE application/rss+xml
		AddOutputFilterByType DEFLATE application/atom_xml
		AddOutputFilterByType DEFLATE application/x-javascript

		# S'assure que les proxies renvoient le bon contenu
		Header append Vary User-Agent env=!dont-vary
	</Location>

### Compression via PHP

	<?php
	
	if(substr_count($_SERVER[‘HTTP_ACCEPT_ENCODING’], ‘gzip’)) {
		ob_start(“ob_gzhandler”);
	}
	else {
		ob_start();
	}
	
	?>


### Tester le fonctionnement

http://www.gidnetwork.com/tools/gzip-test.php


## Liens utiles

http://www.alsacreations.com/article/lire/914-compression-pages-html-css-gzip-deflate.html
