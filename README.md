# Helio Frontend

# Quickstart

Using Helio-Frontend is very easy with docker. You only need to pull the latest version from Docker Hub with next command
```cmd
docker pull emiliocrespoperan/helio-frontend:latest
```

This docker image has the following docker environment variables:
* **HELIO_REST_HOST**. You can tell to Helio-Frontend where is Helio-Rest host. By default the host is http://localhost:4567.
* **HELIO_MODE**. Helio-Frontend has two modes:
  * *APP*. (Default) This mode manages Helio components and mappings.
  * *PLAYGROUND*. This mode fits for people who want to learn about Helio Ecosystem, which contains tutorials that it will be updated frequently.



Use docker compose with the following recipe if you want the  version for this project:

```yml
version: '2'
services:
  helio-rest:
    image: acimmino/helio-rest:latest
    volumes: 
      - type: volume
        source: helio-db
        target: /helio/app
        volume: {}
    ports:
      - "4567:4567"

  frontend:
    image: emiliocrespoperan/helio-frontend:latest
    depends_on:
      - helio-rest
    ports:
      - "4201:80"

volumes:
  helio-db:
    name: helio-db
```

Otherwise, if you want a minimal application to learn about [Helio-Ecosystem](https://github.com/helio-ecosystem), use this docker compose instead:

```yml
version: '2'
services:
  helio-rest:
    image: acimmino/helio-rest:latest
    volumes: 
      - type: volume
        source: helio-db
        target: /helio/app
        volume: {}
    ports:
      - "4567:4567"

  playground:
    image: emiliocrespoperan/helio-frontend:latest
    depends_on:
      - helio-rest
    ports:
      - "4202:80"
    environment:
      - HELIO_REST_HOST=http://localhost:4567
      - HELIO_MODE=PLAYGROUND
      
volumes:
  helio-db:
    name: helio-db
```

### Acknowledgements
This project has been partially funded by:

 | Project       | Grant |
 |   :---:      |      :---      |
 | <img src="https://github.com/helio-ecosystem/helio-ecosystem/assets/4105186/c9081c01-69ed-4ba3-aa1a-fddbaaee19c1" height="80"/>   | The European project [AURORAL](https://www.auroral.eu/) from the European Union's Horizont 2020 research and innovation programme under grant agreement Nº101016854. |
 | <img src="https://github.com/helio-ecosystem/helio-ecosystem/assets/4105186/f1cde449-266f-45f4-a5da-e9c6006f5f3f" height="80"/>  | The European project [COGITO](https://cogito-project.eu/) from the European Union's Horizont 2020 research and innovation programme under grant agreement Nº958310. |

 | Institution       | Grant |
 |   :---:      |      :---      |
 | <img src="https://github.com/helio-ecosystem/helio-frontend/assets/4105186/7456e9d1-a74f-4baa-b83c-6d9f5d9027ec)" height="80"/>  | Collaboration grant from the Education Innovation Program of the Universidad Politécnica de Madrid. |
