name: Deploy to Azure Web App

on:
  push:
    branches:
      - main # Replace with your branch name if different

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout Code
      uses: actions/checkout@v3

    - name: Set up Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18.x' # Replace with your node version

    - name: Install Dependencies
      run: npm install

    - name: Build Project
      run: npm run build # Replace if you have a different build command

    - name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: your-app-name # Replace with your Azure Web App name
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: . # This deploys the entire project root folder
