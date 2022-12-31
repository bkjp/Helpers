## 1. Django part

    1. Setting well **env** and **env.sample** files
    2. **Settings well staticfiles and mediafiles dir**
       For staticfiles and mediafiles create a volumes on the host that match staticfiles and mediafiles in the django container
       ```
        volumes:
          - /home/bkjp/fast-jobs-projects/volumes/staticfiles
       ```


5. **Create symbolic link**

    sudo ln -s /etc/nginx/sites-available/web-1.conf /etc/nginx/sites-enabled/web-1.conf
    sudo ln -s /etc/nginx/sites-available/web-2.conf /etc/nginx/sites-enabled/web-2.conf

6. Next, check Nginx for any syntax error with the following command:

    sudo nginx -t

7. Finally, restart the Nginx service to apply the configuration changes:

    sudo systemctl restart nginx

## 2. Nginx configurations

Follow these steps to configure well your nginx
- Create all your config file for your websites: **domain-1.conf**, **domain-2.conf** ... and put it in the directory
 **/etc/nginx/sites-available/**

- Make a symbolic link to all that conf files to the diresctory **/etc/nginx/sites-enabled/**.
    > $ sudo ln -s  /etc/nginx/sites-availables/filename.conf /etc/nginx/sites-enabled/filename.conf
- Create your settings files for different options you will need to include in nginx at the **/etc/nginx/conf.d/** directory.conf file.
    1. ssl_settings.conf
    2. logging_settings.conf
    3. gzip_settings.conf
    4. common_headers.conf
    5. ...

    and use include instructions to include them where you want.
    > include /etc/nginx/conf.d/*.conf

 - Since you will not need to use the default config file nginx use to serve the default html page you need to deactivate it. In the /etc/nginx/sites-availble/ there is a file named **default** which is the file containeing the default bloc server nginx use to serve default HTML. To deactivate it you just need to go in **/etc/nginx/nginx.conf** adn change
    > include /etc/nginx/sites-enabled/*

    to
    > include /etc/nginx/sites-enabled/*.conf

    Like this since **default** file inside **/etc/nginx/sites-available/** does not have **.conf** extension, that instruction will only  include all file with **.conf**