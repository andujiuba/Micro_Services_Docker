# BUILDING OUR OWN IMAGE
# Choose the image you want to build from

FROM nginx

LABEL MAINTAINER=andujiuba@spartaglobal.com
# OPTIONAL -- tells who the author is

# Make changes to index.html -- copy from host machine to container

COPY index.html /usr/share/nginx/html/index.html

# Portmap the container -- port 80

EXPOSE 80

# CMB to launch the NGINX web server

CMD ["nginx", "-g", "daemon off;" ]
# makes NGINX global
