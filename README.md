# dotnet-release-action

Action to release .NET services

```yml
name: Release

on:
  release:
    types:
      - released
  workflow_dispatch:

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Build
        uses: sitkoru/dotnet-release-action@v1
        with:
          docker_registry: ${{ secrets.DOCKER_REGISTRY_URL }}
          docker_image: ${{ secrets.DOCKER_IMAGE_NAME }}
          docker_registry_username: ${{ secrets.DOCKER_REGISTRY_LOGIN }}
          docker_registry_password: ${{ secrets.DOCKER_REGISTRY_TOKEN }}
          project_path: src/PROJECT/PROJECT.csproj
          docker_file: ${{ secrets.HOST_WORKING_DIR }}
          # uncomment if private nuget feed required
          # nuget_host: ${{ secrets.NUGET_HOST }}
          # nuget_token: ${{ secrets.BOT_TOKEN }}
```
