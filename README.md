# laravel-deployment-action
Github action for deploying Laravel

```
# This is a basic workflow to help you get started with Actions

name: Production Deployment

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the develop branch
  push:
    branches: [ main ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # Trigger workflow on the branch in question
    if: ${{ github.ref == 'refs/heads/main' }}
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v2

      - name: Laravel Deployment Action
        # You may pin to the exact commit or the version.
        # uses: Pentangle/laravel-deployment-action@a6342bb89f4907d7b1bfd907cd61236ea4088b88
        uses: Pentangle/laravel-deployment-action@v2.0.0
        with:
          # SSH key for deploying, Should be added as a **secret**
          DEPLOY_KEY: 
          # IP address of the server being deployed to, Should be added as a **secret**
          SERVER_IP: 
          # Custom port for ssh and rsync
          SERVER_PORT: # optional, default is 22
          # required, used for SSH and deployment path if APP_PATH not specified
          SSH_USER: 
          # required, used for deployment path if APP_PATH not specified
          APP_NAME: 
          # leave blank for /srv/users/<SSH_USER>/apps/<APP_NAME>
          APP_PATH: # optional
          # 
          COMPOSER_COMMAND: # optional, default is composer install --no-progress --optimize-autoloader
          # version of node to install
          NODE_VERSION: # optional, default is 16.14
          # requires package-lock.json to be present
          NPM_INSTALL_COMMAND: # optional, default is npm ci --quiet
          # build process command
          BUILD_COMMAND: # optional, default is npm run dev
          # commands to run on server with prefix
          ARTISAN_COMMANDS: # optional, default is php artisan inspire
