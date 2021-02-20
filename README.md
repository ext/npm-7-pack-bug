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

## Result

    npm WARN tarball tarball data for @sandbox/plugin@file:../plugin/sandbox-plugin-1.0.0.tgz (null) seems to be corrupted. Trying again.
    npm WARN tarball tarball data for @sandbox/plugin@file:../plugin/sandbox-plugin-1.0.0.tgz (null) seems to be corrupted. Trying again.
    npm ERR! code ERESOLVE
    npm ERR! ERESOLVE unable to resolve dependency tree
    npm ERR! 
    npm ERR! While resolving: my-app@1.0.0
    npm ERR! Found: @sandbox/plugin@undefined
    npm ERR! node_modules/@sandbox/plugin
    npm ERR!   dev @sandbox/plugin@"file:../plugin/sandbox-plugin-1.0.0.tgz" from the root project
    npm ERR! 
    npm ERR! Could not resolve dependency:
    npm ERR! peer @sandbox/plugin@"^1" from third-party@1.0.0
    npm ERR! node_modules/third-party
    npm ERR!   third-party@"file:../third-party/third-party-1.0.0.tgz" from the root project
    npm ERR! 
    npm ERR! Fix the upstream dependency conflict, or retry
    npm ERR! this command with --force, or --legacy-peer-deps
    npm ERR! to accept an incorrect (and potentially broken) dependency resolution.
    npm ERR! 
    npm ERR! See /home/ext/.npm/eresolve-report.txt for a full report.
     
    npm ERR! A complete log of this run can be found in:
    npm ERR!     /home/ext/.npm/_logs/2021-02-20T13_03_48_472Z-debug.log
