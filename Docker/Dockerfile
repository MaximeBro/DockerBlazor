# 1ère étape : installer, configurer et lancer nginx
# On utilise l'image nginx pour héberger notre proxy nginx, l'image alpine est réduite par rapport à une image traditionnelle
FROM nginx:alpine

# On utilise l'utilisateur root plutôt que d'en créer un spécifique à notre image (soucis de simplicité)
USER root

# On définit le répertoire dans lequel on exécute nos commandes (à l'intérieur du container)
WORKDIR /etc/nginx/conf.d

# On supprime la config par défaut de nginx pour la remplacer avec la nôtre
RUN rm /etc/nginx/conf.d/default.conf
COPY /home/docker/nginx /etc/nginx/conf.d

# On déplace les certificats
COPY /home/docker/certs /etc/nginx/ssl

# On ouvre les ports HTTP & HTTPS nécessaires au fonctionnement du site pour notre container
EXPOSE 80/tcp
EXPOSE 443/tcp

# On lance nginx en mode background
CMD ["nginx", "-g", "daemon off;"]


# Étape intermédiaire pour si vous n'avez pas de certificat valide signé par une autorité reconnue
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
RUN dotnet dev-certs https


# 2ème étape : lancer notre app blazor SSR
# On utilise seulement le runtime .Net, pas besoin du sdk car ici on n'en fera rien
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime

# On exécute maintenant nos commandes dans le répertoire ci-dessous
WORKDIR /home/asp-app

# On récupère les fichiers de notre application
COPY build /home/asp-app

# Cette ligne permet de copier le certificat DEBUG reçu via l'étape intermédiaire, à éviter si vous avez un certificat valide signé
COPY --from=build /root/.dotnet/corefx/cryptography/x509stores/my/* /root/.dotnet/corefx/cryptography/x509stores/my/

# On donne les droits d'execution à notre dll (qui souvent ne les a pas après un publish -c release)
RUN chmod +x DockerBlazor.dll

# On définit notre executable qui sera lancé au démarrage du container
ENTRYPOINT ["dotnet", "DockerBlazor.dll"]



# On se donne crédit quand même
LABEL maintainer="MaximeBro"