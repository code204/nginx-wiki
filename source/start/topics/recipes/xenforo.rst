
.. meta::
   :description: A sample NGINX configuration for XenForo.

XenForo
=======

XenForo: https://xenforo.com

Configuring XenForo is pretty simple, just note that "$uri&$args" is needed for the profile tooltip to work properly. 

Recipe
------

.. code-block:: nginx

    server {

        server_name     localhost;

        root    html/xenforo;
        index   index.php index.html;

        location / {
            try_files $uri $uri/ /index.php?$uri&$args;
        }

        location ~ \.php$ {
            fastcgi_pass    127.0.0.1:9000;
            fastcgi_param   SCRIPT_FILENAME $document_root$fastcgi_script_name;
            include         fastcgi_params;
        }

    }
