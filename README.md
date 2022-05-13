Tigase's Docker Maven build package

# Supported tags and respective `Dockerfile`s

-   [`3-temurin-17`, `latest` (*temurin-17/Dockerfile*)](temurin-17/Dockerfile)
-   [`3-temurin-11` (*temurin-11/Dockerfile*)](temurin-11/Dockerfile)

# What is Tigase Maven image?

It's an image used for building and deploying Tigase artifacts. It contains dedicated settings file with credentials exposed as variables facilating building in CI.

# Usage

* `tigase.internalrepo.username` and `tigase.internalrepo.password` for archiva hosted repository
* `tigase.githubrepo.username` and `tigase.githubrepo.password` for (private) maven repository hosted on github

Usage is completely simple and boil down to adding above variables as parameters to `mvn` command prefixed with `-D` and setting relevant credentials

```bash
docker run -v "$(pwd)":/opt/maven -w /opt/maven --rm tigase/tigase-maven-docker:3-temurin-17 mvn -Dtigase.internalrepo.username=<username> -Dtigase.internalrepo.password=<password> clean install deploy
```

# Building & Publishing

We should build multi-arch images, please prepare build environment as outlined in https://docs.docker.com/desktop/multi-arch/ (because of the limitations of multi-arch one MUST push using `build` to properly push multi-arch tag)

```bash
for VERSION in 11 17 ;  do
  docker buildx build --platform linux/amd64,linux/arm64 -t tigase/tigase-maven-docker:3-temurin-${VERSION} -f temurin-${VERSION}/Dockerfile --no-cache ./ --push ; \
done
docker buildx build --platform linux/amd64,linux/arm64 -t tigase/tigase-maven-docker:latest -f temurin-${VERSION}/Dockerfile --no-cache ./ --push ; \
```

# License

<img alt="Tigase Tigase Logo" src="https://github.com/tigase/website-assets/blob/master/tigase/images/tigase-logo.png?raw=true" width="25"/> Official <a href="https://tigase.net/">Tigase</a> repository is available at: https://github.com/tigase/tigase-server/.

Copyright (c) 2004 Tigase, Inc.
