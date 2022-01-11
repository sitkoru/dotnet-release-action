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
      - name: Prepare
        id: prep
        shell: bash
        run: |
          VERSION=${GITHUB_REF#refs/tags/}
          echo ::set-output name=version::${VERSION}
      - name: Build
        uses: sitkoru/dotnet-release-action@v1
        with:
          version: ${{ steps.prep.outputs.version }}
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
