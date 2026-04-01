FROM nginx:alpine

# Copier le fichier de configuration personnalisé
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copier la page HTML statique dans le dossier public par défaut de Nginx
COPY index.html /usr/share/nginx/html/

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
