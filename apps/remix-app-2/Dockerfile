# Setup base node image
FROM node:18-bullseye-slim as base
ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable

# Install all node_modules including dev dependencies
FROM base as deps
WORKDIR /app
ADD . .
RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm install --frozen-lockfile

# Setup production node_modules
FROM base as production-deps
WORKDIR /app
ADD package.json pnpm-lock.yaml .npmrc ./
ENV NODE_ENV production
RUN --mount=type=cache,id=pnpm,target=/pnpm/store pnpm install --prod --frozen-lockfile

# Build everything
FROM base as build
WORKDIR /app
COPY --from=deps /app/ .
ENV NODE_ENV production
RUN pnpm build:remix-app-2
RUN pnpm deploy --filter=remix-app-2 --prod /prod
RUN cp -r ./apps/remix-app-2/build /prod/build

# Finally, build the production image with minimal footprint
FROM base
ARG SOME_ENV_VAR
ENV SOME_ENV_VAR=${SOME_ENV_VAR}
WORKDIR /app
COPY --from=production-deps /app/node_modules /app/node_modules
COPY --from=build /prod/build/server /app/build/server
COPY --from=build /prod/build/client /app/build/client
COPY --from=build /prod/package.json /app/package.json

# Run the app
ENTRYPOINT [ "pnpm", "start" ]
