# pbasu-CORS-articles

Access-Control-Allow-Origin Multiple Origin Domains on Apache using scripting
https://stackoverflow.com/questions/1653308/access-control-allow-origin-multiple-origin-domains

Sounds like the recommended way to do it is to have your server read the Origin header from the client, compare that to the list of domains you would like to allow, and if it matches, echo the value of the Origin header back to the client as the Access-Control-Allow-Origin header in the response.

With .htaccess you can do it like this:

# ----------------------------------------------------------------------
# Allow loading of external fonts
# ----------------------------------------------------------------------
<FilesMatch "\.(ttf|otf|eot|woff|woff2)$">
    <IfModule mod_headers.c>
        SetEnvIf Origin "http(s)?://(www\.)?(google.com|staging.google.com|development.google.com|otherdomain.example|dev02.otherdomain.example)$" AccessControlAllowOrigin=$0
        Header add Access-Control-Allow-Origin %{AccessControlAllowOrigin}e env=AccessControlAllowOrigin
        Header merge Vary Origin
    </IfModule>
</FilesMatch>


https://enable-cors.org/server_iis7.html
https://dzone.com/articles/do-you-really-know-cors
