### Build Action

GitHub Action for building and publishing Docker images to [GitHub Packages](https://github.com/orgs/saturdayshdev/packages).

### Usage

To use this action, simply create a workflow in `.github/workflows` and use it:

```yaml
name: Build

on:
  push:
    branches: [main, develop]

env:
  IMAGE_NAME: ${{ github.event.repository.name }}
  IMAGE_TAG: ${{ github.ref == 'refs/heads/main' && 'production' || 'staging' }}
  IMAGE_PATH: docker/${{ github.ref == 'refs/heads/main' && 'production' || 'staging' }}

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - name: Build
        uses: saturdayshdev/build-action@v1.0.0
        with:
          github-token: ${{ secrets.GITHUB_TOKEN }}
          dockerfile: ${{ env.IMAGE_PATH }}/Dockerfile
          image: ${{ env.IMAGE_BASE }}
          tag: ${{ env.IMAGE_TAG }}
```
