# NPM unable to resolve dependency tree undefined

## Prerequisites

    docker pull verdaccio/verdaccio
    docker run -it --rm --name verdaccio -p 4873:4873 verdaccio/verdaccio
    npm adduser --registry http://localhost:4873
    (cd app; npm install)

## Triggering bug

Create tarballs for all dependencies

    for pkg in base plugin third-party; do; (cd $pkg; npm pack); done

Install tarballs in application

    cd app
    npm install ../{base,plugin}/sandbox-*-1.0.0.tgz ../third-party/third-party-1.0.0.tgz
