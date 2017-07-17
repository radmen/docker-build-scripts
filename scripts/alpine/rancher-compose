#!/bin/sh

set -e

echo "Installing rancher-compose"

get_version ()
{
    git clone -n https://github.com/rancher/rancher-compose.git

    cd rancher-compose
    TAG="$(git describe --tags --abbrev=0)"

    cd ..
    rm -rf rancher-compose

    echo "$TAG"
}

download_binary ()
{
    VERSION="$1"

    cd /tmp

    curl -Lso rancher.tar.gz "https://github.com/rancher/rancher-compose/releases/download/$VERSION/rancher-compose-linux-amd64-$VERSION.tar.gz"
    tar xf rancher.tar.gz
    rm rancher.tar.gz

    echo "/tmp/rancher-compose-$VERSION/rancher-compose"
}

apk add --no-cache -t .deps git curl

TAG="$(get_version)"
BINARY="$(download_binary "$TAG")"

mv "$BINARY" /usr/bin
rm -rf "$(dirname "$BINARY")"

rancher-compose -v

apk del .deps
