FROM debian:buster

#on reinstaller update, on upgrade pr trouver les maj manquantes et on reinstalle nginx a chqe fois et on met le y pour eviter detre bloquer ds le prompt qui demande si oui ou non on veut continuer starfoullah 

RUN apt-get update -y
RUN apt-get upgrade -y
RUN apt-get install nginx -y
RUN apt-get install openssl -y

RUN mkdir -p /etc/nginx/ssl

#x509 norme de contrat 
#-nodes pr retirer les mdp pck interdit ds le sujet
# out et keyout pour donner la ou on stock le certif et la cle
#subj equivalent de -y 

#subj tu donnes des infos que ssl deande genre country, state, locality, etc"
RUN openssl req -x509 -nodes -out /etc/nginx/ssl/inception.crt -keyout /etc/nginx/ssl/inception.key -subj "/C=FR/ST=Paris/L=Paris/0=42Paris/OU=lkhamlac.42.fr/CN=lkhamlac.fr"

RUN mkdir -p var/run/nginx

COPY conf/nginx.conf /etc/nginx/nginx.conf

RUN chmod 755 /var/www/html
RUN chown -R www-data:www-data /var/www/html
EXPOSE 443

#on lance nginx au premier plan pou que le container se stop pas
CMD ["nginx", "-g","daemon off;"]
