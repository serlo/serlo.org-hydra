<img src="https://assets.serlo.org/meta/logo.png" alt="Serlo logo" title="Serlo" align="right" height="60" />

# Serlo.org Hydra

This repository provides a local environment for our Hydra integration.

## Assumptions

- You'll need a running serlo.org local environment (i.e. on the typical http://de.serlo.localhost:4567).

## Development

### Install dependencies

Run `yarn` to install the dependencies of all packages.

### Start

Run `yarn start` to start everything needed to run serlo.org locally.
Now open [http://de.serlo.localhost:4567](http://de.serlo.localhost:4567). Happy coding!

    "oauth:migrate": "docker-compose run hydra migrate sql --yes --read-from-env",
    "oauth": "npm-run-all -s -c oauth:clear oauth:client oauth:user",
    "oauth:clear": "docker-compose run hydra clients delete test_client --endpoint http://hydra:4445",
    "oauth:client": "docker-compose run hydra clients create --skip-tls-verify --endpoint http://hydra:4445 --id test_client --secret CHANGEMENOWOMG --grant-types authorization_code --response-types code --scope openid,email --callbacks http://127.0.0.1:4446/callback --token-endpoint-auth-method client_secret_post",
    "oauth:frontend": "npm-run-all -s -c oauth:frontend:clear oauth:frontend:client",
    "oauth:frontend:clear": "docker-compose run hydra clients delete frontend.serlo.org --endpoint http://hydra:4445",
    "oauth:frontend:client": "docker-compose run hydra clients create --skip-tls-verify --endpoint http://hydra:4445 --id frontend.serlo.org --secret frontend.serlo.org --grant-types authorization_code,refresh_token --response-types code --scope openid,offline_access --callbacks http://localhost:3000/api/auth/callback --post-logout-callbacks http://localhost:3000/api/auth/logout-callback --token-endpoint-auth-method client_secret_post",
    "oauth:user": "docker-compose run -p 4446:4446 hydra token user --skip-tls-verify --client-id test_client --client-secret CHANGEMENOWOMG --port 4446 --auth-url http://localhost:4444/oauth2/auth --token-url http://hydra:4444/oauth2/token --scope openid,email",
