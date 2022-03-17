# laravel-deployment-action
Github action for deploying Laravel

```
name: Development Deployment

on:
  push:
    branches: [ branch-name ]

jobs:
  deploy-branch-name:
    if: ${{ github.ref == 'refs/heads/branch-name' }}
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2
      - name: Laravel Deployment Action
        uses: Pentangle/laravel-deployment-action@v1.0.0
        with:
          DEPLOY_KEY: ${{ secrets.DEPLOYKEY }}
          SERVER_IP: 0.0.0.0
          SERVER_PORT: 22
          SSH_USER: ssh-user
          APP_NAME: app-name
          APP_PATH: "" # leave blank for /srv/users/<SSH_USER>/apps/<APP_NAME>
          COMPOSER_COMMAND: "" # leave blank for composer install --no-progress --optimize-autoloader
          BUILD_COMMAND: "npm run dev"
          ARTISAN_COMMANDS: |
            php artisan storage:link --force
            php artisan migrate --force
            php artisan optimize:clear
            php artisan queue:restart
            php artisan schedule:sync
```
