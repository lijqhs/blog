# blog

## Quick steps for update this site

- `git clone ...`
- `git submodule update --init --recursive`
- `hugo new content posts/xxxx.md`
- `zsh update.sh`


## Steps for create a new site

1. [Create and Configure](https://gohugo.io/getting-started/quick-start/)
2. [Host on GitHub Pages](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

## Install Hugo on Ubuntu

[installation guide](https://gohugo.io/installation/linux/)

- install [Go](https://go.dev/doc/install)

    ```shell
    wget https://go.dev/dl/go1.21.5.linux-amd64.tar.gz
    rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.5.linux-amd64.tar.gz
    export PATH=$PATH:/usr/local/go/bin
    ```
- install [Dart Sass](https://gohugo.io/hugo-pipes/transpile-sass-to-css/#dart-sass)

    ```sh
    sudo snap install dart-sass
    ```
- install [hugo](https://github.com/gohugoio/hugo/releases)

    ```sh
    wget https://github.com/gohugoio/hugo/releases/download/v0.121.1/hugo_extended_0.121.1_linux-amd64.deb
    sudo dpkg -i hugo_extended_0.121.1_linux-amd64.deb
    ```