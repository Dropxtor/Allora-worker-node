
## Exigences ⛓️


- Vous devez acheter un VPS pour exécuter Allora Node
- Vous pouvez acheter chez avec la cryptomonnaie : [PQ Hosting](https://pq.hosting/en/vps)
- Vous devez acheter un VPS qui répond à toutes ces exigences : 
```bash
Operating System : Ubuntu 22.04
CPU : Minimum de 1/2 core
RAM : 2 à 4 GB
Storage : SSD ou NVMe avec au moins 5GB d'espace
```
## Créer un portefeuille et demander un robinet 🚰

- Installer : [Keplr Extension](https://chrome.google.com/webstore/detail/dmkamcknogkgcdfhhbddcghachkejeap)
- Créer un nouveau portefeuille
- Visitez : [Allora Website](https://app.allora.network/points/overview)
- Copiez votre adresse allora à partir d'ici
- Visitez et demandez le robinet : [Allora Faucet](https://faucet.edgenet.allora.network/)
- S'il y a une erreur, essayez 3 à 5 fois 


## Déploiement Partie 1 (à lire attentivement)

- Si vous souhaitez exécuter ce nœud sur un VPS distinct et si vous avez déjà essayé d'exécuter ce nœud sur ce VPS distinct, vous devez supprimer les fichiers du conteneur Docker à l'aide des commandes mentionnées ci-dessous
- N'EXÉCUTEZ PAS CES 2 COMMANDES SUR VPS OÙ VOUS EXÉCUTEZ D'AUTRES NŒUDS, SAUTEZ SIMPLEMENT CETTE PARTIE 1 ET PASSEZ À LA PARTIE 2

```bash
docker stop $(docker ps -aq) && docker rm $(docker ps -aq) && docker rmi -f $(docker images -aq)
```

```bash
docker rm -f $(docker ps -a -q);docker system prune --volumes -a -f
```

## Déploiement Partie 2

- Ouvrir le terminal termius/putty
- Collez ces 2 commandes une par une
```bash
rm -rf allora.sh allora-chain/ basic-coin-prediction-node/
```
```bash
wget https://raw.githubusercontent.com/Dropxtor/Allora-worker-node/main/allora.sh && chmod +x allora.sh && ./allora.sh
```
- Au milieu de l'exécution de la commande, il vous sera demandé keyring phrase, ici vous devez écrire un mot de passe (exemple : 12345678)
- Pendant le collage HEAD_ID, n'utilisez pas Ctrl+C pour copier et Ctrl+V pour coller, sélectionnez simplement l'ensemble KEY_ID et appuyez sur clique droite


## Vérifier l'état du nœud 

Exécutez la commande ci-dessous pour vérifier si votre nœud est en cours d'exécution ou non

```bash
  curl --location 'http://localhost:6000/api/v1/functions/execute' \
--header 'Content-Type: application/json' \
--data '{
    "function_id": "bafybeigpiwl3o73zvvl6dxdqu7zqcub5mhg65jiky2xqb4rdhfmikswzqm",
    "method": "allora-inference-function.wasm",
    "parameters": null,
    "topic": "1",
    "config": {
        "env_vars": [
            {
                "name": "BLS_REQUEST_PATH",
                "value": "/api"
            },
            {
                "name": "ALLORA_ARG_PARAMS",
                "value": "ETH"
            }
        ],
        "number_of_nodes": -1,
        "timeout": 2
    }
}'
```

Vous verrez une réponse comme celle-ci :

```bash
{"code":"200","request_id":"876a58bf-2cad-49ff-a722-86a5da444528","results":[{"result":{"stdout":"{\"infererValue\": \"2908.09263675852\"}\n\n","stderr":"","exit_code":0},"peers":["12D3KooWM99J9Qc9QhsBXiezdJKr9Y6MJN3LDL8XfcBDbCn1qtAp"],"frequency":100}],"cluster":{"peers":["12D3KooWM99J9Qc9QhsBXiezdJKr9Y6MJN3LDL8XfcBDbCn1qtAp"]}}
```
Cela signifie que votre nœud fonctionne bien ✅
