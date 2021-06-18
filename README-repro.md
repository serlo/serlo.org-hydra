To reproduce the refresh token issue:

1. `git clone --recursive https://github.com/serlo/serlo.org-hydra.git`
1. `cd serlo.org-hydra`
1. `(cd serlo.org && yarn && yarn start)` to start serlo.org locally (provides the login endpoint)
1. `(cd frontend && yarn && yarn dev)` to start the frontend (OAuth2 client)
1. `yarn start` to start hydra
1. `yarn oauth:frontend:client` to create the client in hydra.
1. Open `http://localhost:3000` and click on "Anmelden"
1. After successful login, click on "Refresh Token" below the header. You'll see "refreshing token" in the browser console and the error in hydra logs.
