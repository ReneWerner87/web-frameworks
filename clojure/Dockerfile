{{#image}}
  FROM {{{.}}}
{{/image}}

{{^image}}
  FROM clojure:openjdk-11-tools-deps-slim-buster
{{/image}}

WORKDIR /usr/src/app

COPY . ./

{{#build}}
  RUN {{{.}}}
{{/build}}

{{^build}}
  RUN clojure -Auberjar
{{/build}}

FROM openjdk:11-jre-slim-buster

WORKDIR /opt/bin

{{#environment}}
  ENV {{{.}}}
{{/environment}}

{{#files}}
  COPY --from=0 /usr/src/app/{{{.}}} /opt/bin/{{{.}}} 
{{/files}}

{{#command}}
  CMD {{{.}}}
{{/command}}
