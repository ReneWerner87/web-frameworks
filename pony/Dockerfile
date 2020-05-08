FROM ponylang/ponyc:0.34.1-alpine

RUN apk add clang openssl-dev

WORKDIR /src/main

COPY bundle.json .

RUN stable fetch

{{#sources}}
  COPY {{{.}}} {{{.}}}
{{/sources}}

{{#environment}}
  ENV {{{.}}}
{{/environment}}

{{#before_command}}
  RUN {{{.}}}
{{/before_command}}

RUN stable env ponyc -Dopenssl_1.1.x -Dstatic

FROM alpine 

RUN apk add libatomic libgcc libexecinfo

WORKDIR /opt/web

{{#binaries}}
  COPY --from=0 /src/main/main {{{.}}}
{{/binaries}}

CMD ./web
