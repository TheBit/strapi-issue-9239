# Strapi
This repo is for reproducing this bug: https://github.com/strapi/strapi/issues/9239 (I wish it wouldn't happen...)

Was initialized with command:

`yarn create strapi-app my-project-3.5.2 --quickstart`

Super Admin:
```
thebit@i.ua
Qwerty123
```
## Steps to reproduce
1. git clone https://github.com/TheBit/strapi-issue-9239.git
1. cd my-project-3.5.2
1. yarn install
1. yarn build
1. yarn develop
1. open http://localhost:1337/graphql
1. send query:
```
TBD
```
