# Edge_STREETFINDER

Point d'entrée commun du serveur StreetFinder : un seul conteneur Caddy (`edge`) écoute sur
80/443, porte les certificats Let's Encrypt et transmet chaque domaine au Caddy interne de son
application, sur le réseau Docker externe `edge`.

| Domaine | Destination |
|---|---|
| delay-lama.fr | `streetfinder-reverse-proxy:80` ([Elyss/streetfinder](https://github.com/Elyss/streetfinder)) |
| www.delay-lama.fr, elyss.fr | redirection vers delay-lama.fr |
| pascal-quijoux.fr | `quijoux-reverse-proxy:80` ([Elyss/pascal-quijoux](https://github.com/Elyss/pascal-quijoux)) |
| www.pascal-quijoux.fr | redirection vers pascal-quijoux.fr |

Sur le serveur, ce dépôt se clone à côté des dépôts des applications.
Mise en place, ajout d'un domaine, dépannage : **[GUIDE EDGE.txt](GUIDE%20EDGE.txt)**.

```bash
docker network create edge        # une seule fois
docker compose up -d
docker compose exec edge caddy reload --config /etc/caddy/Caddyfile   # après modification
```
