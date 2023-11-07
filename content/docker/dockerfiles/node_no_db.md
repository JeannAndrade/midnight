---
layout: internal
---

# Exemplo de *dockerfile* para uma aplicação Node.js, sem acesso a banco de dados

```docker
FROM alpine
LABEL maintainer="<nigelpoulton@hotmail.com>"
RUN apk add --update nodejs nodejs-npm
COPY . /src
WORKDIR /src
RUN  npm install
EXPOSE 8080
ENTRYPOINT ["node", "./app.js"]
```
