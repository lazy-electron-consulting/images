ARG NODE_TAG=16-alpine3.12
FROM node:${NODE_TAG}

ARG APOLLO_VERSION=2.33.8
ARG GRAPHQL_VERSION=15

WORKDIR /app

# reduce npm output
ENV npm_config_audit=false \
    npm_config_update_notifier=false \
    npm_config_fund=false

# install and hack dependencies to a workable state for codegen (https://github.com/apollographql/apollo-tooling/issues/2422)
# - `apollo` says it works with `graphql@14`, but it does not
# - `apollo-language-server` says it does not work with `graphql@15`, but it does
RUN npm install "graphql@${GRAPHQL_VERSION}" && \
    npm install "apollo@${APOLLO_VERSION}" && \
    rm -rf node_modules/apollo-language-server/node_modules/graphql

ENTRYPOINT ["/app/node_modules/.bin/apollo", "client:codegen"]
