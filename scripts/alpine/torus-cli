#!/bin/sh

set -e

echo "Installing torus-cli"

get_version ()
{
    git clone -n https://github.com/manifoldco/torus-cli.git
    
    cd torus-cli
    TAG="$(git describe --tags --abbrev=0 | tr -d 'v')"

    cd ..
    rm -rf torus-cli

    echo "$TAG"
}

download_binary ()
{
    VERSION="$1"

    cd /tmp
    curl -Lso torus-cli.zip "https://get.torus.sh/$VERSION/torus_${VERSION}_linux_amd64.zip"

    unzip torus-cli.zip > /dev/null 2>&1
    rm torus-cli.zip

    echo "/tmp/torus"
}

apk add --no-cache -t .deps git unzip

TAG="$(get_version)"
BINARY="$(download_binary "$TAG")"

mv "$BINARY" /usr/bin

torus -v

apk del .deps
