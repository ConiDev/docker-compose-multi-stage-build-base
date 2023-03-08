ARG VERSION_NODE=${VERSION_NODE}

FROM node:${VERSION_NODE} AS base

USER node
WORKDIR /srv/app


FROM base AS development

ENV NODE_ENV="development"
CMD npm ci && npm run dev -- -p ${PORT_NODE}



FROM base AS production

ENV NODE_ENV="production"
CMD npm ci && npm run build && npm run start -- -p ${NEXT_PORT}