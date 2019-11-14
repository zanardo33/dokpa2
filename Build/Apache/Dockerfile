FROM alpine:3.10
LABEL author="Serge NOEL <serge.noel@easylinux.fr>"

# Commentaires
RUN apk add apache2 php7-apache2 \
# Modifier le, fichier /etc/apache2/httpd.conf
    && sed -i "s|/var/www/localhost/htdocs|/var/www/html|g" /etc/apache2/httpd.conf \
    && ln -s /dev/stdout /var/log/apache2/access.log \
    && ln -s /dev/stderr /var/log/apache2/error.log

# Copier l'arborescence de travail
COPY Files/ /

# Ecoute sur le port 80
EXPOSE 80
# Données extérieures au conteneur
VOLUME /var/www/html/Download
# Répertoire par défaut
WORKDIR /var/www/html
# USER apache

#CMD /usr/sbin/httpd -D FOREGROUND
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]

