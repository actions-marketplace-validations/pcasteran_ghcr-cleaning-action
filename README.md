# GitHub Container registry cleaning action

GitHub action allowing to clean a GitHub Container registry by deleting the unnecessary images and
image [indices](https://docs.docker.com/registry/spec/manifest-v2-2/). Unnecessary can mean:

- untagged images not referenced by any image index
- untagged image indices and their referenced images
- tagged images related to a closed Pull Request
- tagged image indices related to a closed Pull Request and their referenced images

There are actually many possible combinations, for a list of all the managed cases see
the [unit tests](cleaning_test.go).

## Authentication

As per
the [documentation](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-with-a-personal-access-token-classic),
the authentication to the GHCR registry must be done using a personal access token. Only classic tokens can be used,
fined-grained ones are currently (2023-01) not supported.

The [recommendation](https://docs.github.com/en/rest/packages?apiVersion=2022-11-28#delete-package-version-for-a-user)
is to create a new PAT with only the `read:packages` and `delete:packages` scopes. To do so, you can
use [this](https://github.com/settings/tokens/new?scopes=read:packages,delete:packages) link.