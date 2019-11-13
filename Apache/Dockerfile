FROM alpine:3.10
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

# Commentaires
RUN apk add apache2 php7-apache2
# Modifier le, fichier /etc/apache2/httpd.conf
RUN sed -i "s|/var/www/localhost/htdocs|/var/www/html|g" /etc/apache2/httpd.conf
# Ecoute sur le port 80
EXPOSE 80
# Données extérieures au conteneur
VOLUME /var/www/html
# Répertoire par défaut
WORKDIR /var/www/html
# USER apache

#CMD /usr/sbin/httpd -D FOREGROUND
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]

