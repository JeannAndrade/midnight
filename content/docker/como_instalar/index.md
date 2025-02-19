---
layout: internal
---

# Como instalar o Docker

## Docker Desktop

Baixe o software [aqui](https://hub.docker.com/) e, depois de instalado, você terá um ambiente Docker totalmente funcional, ótimo para desenvolvimento, teste e aprendizado. Inclui Docker Compose e você pode até habilitar um cluster Kubernetes de nó único se precisar aprender Kubernetes. No mesmo site vc encontra o software para Windows ou Mac. No Windows o Docker vai rodar no WSL 2. No Mac o Docker é instalado em um Linux rodando dentro de uma VM.

## Através do Multipass

Multipass é uma ferramenta gratuita para criar VMs Linux no estilo nuvem em sua máquina Linux, Mac ou Windows.

## Docker no Linux

Siga a série de comandos do livro para fazer a instalação no Linux 22.04 LTS. Segui o roteiro de instalação no Linux 23.04 e foi também, tudo certo.

## Play with Docker

[Play with Docker](https://labs.play-with-docker.com/) (PWD) é um playground Docker totalmente funcional baseado na Internet que dura até 4 horas. Você pode adicionar vários nós e até mesmo agrupá-los em um swarm.

## Problemas comuns na instalação

### O docker reclama de falta de permissão para o usuário non-root quando alguns commandos são executados

Esse [link](https://phoenixnap.com/kb/docker-permission-denied) mostra como resolver:

```bash
# Enter the command below to create the docker group on the system.
sudo groupadd -f docker
# Type the following usermod command to add the active user to the docker group.
sudo usermod -aG docker $USER
# Apply the group changes to the current terminal session by typing:
newgrp docker
# Check if the docker group is in the list of user groups.
groups
```

[top](/content/docker/index.html#docker-table-of-contents)
