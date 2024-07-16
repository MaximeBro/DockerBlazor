# DockerBlazor

Petit projet réalisé dans le cadre de ma candidature au Mastère Professionnel MAALSI pour l'école du CESI de Rouen.

## Architecture du projet

- Vous trouverez dans le dossier `Docker` les fichiers nécessaires au lancement des containers via ```docker-compose up --build -d```.
  Attention les certificats ne sont pas fournis* et donc à générer par vous-même si vous souhaitez lancer l'application.


- Vous trouverez dans le dossier `DockerBlazor` le projet Blazor SSR avec [.Net 8](https://dotnet.microsoft.com/en-us/download/dotnet/8.0) et [MudBlazor 7.2](https://mudblazor.com/) (librairie front).
  Cette application web ne comporte rien d'autre qu'une simple page d'accueil.


### Remarques
>Le Dockerfile contient par défaut les certificats de DEBUG, vous n'avez pas besoin d'en générer à moins que vous ne souhaitiez un réel environnement de production.