#!/bin/sh

set -e

echo "Installing rancher-cli"

get_version ()
{
    git clone -n https://github.com/rancher/cli.git

    cd cli
    TAG="$(git describe --tags --abbrev=0)"

    cd ..
    rm -rf cli

    echo "$TAG"
}

download_binary ()
{
    VERSION="$1"

    cd /tmp

    curl -Lso rancher.tar.gz "https://github.com/rancher/cli/releases/download/$VERSION/rancher-linux-amd64-$VERSION.tar.gz"
    tar xf rancher.tar.gz
    rm rancher.tar.gz

    echo "/tmp/rancher-$VERSION/rancher"
}

apk add --no-cache -t .deps git

TAG="$(get_version)"
BINARY="$(download_binary "$TAG")"

mv "$BINARY" /usr/bin
rm -rf "$(dirname "$BINARY")"

rancher -v

apk del .deps
