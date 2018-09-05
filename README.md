# running-node-project-with-nginx

Here's step by command if you want to running your node project into nginx server.

1. Install `npm` and `node`
2. Install `pm2`
3. Running your project into specific port like `8080`, `8888`, etc
4. Create configuration file into, you can use nano, vim, or emacs to create the file. For example we use file name `mysubdomain`
```
$ nano /etc/nginx/sites-available/mysubdomain
```
5. Make configuration into your nginx like below, replace the `***` part with your IP address
6. Specify port you've been used for your application, in this following example the port used is `8080`

```
server {
    listen 80;

    server_name subdomain.domain.com;

    location / {
        proxy_pass http://***.***.***.***:8080;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
}
```

7. Link your configuration to sites enabled
```
$ ln -s /etc/nginx/sites-available/mysubdomain /etc/nginx/sites-enabled/
```
8. Update your nginx server with this following command 
```
$ service nginx restart
```
