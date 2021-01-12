1. Instalação do 'material for mkdocs'

> ~$ docker pull squidfunk/mkdocs-material

2. Iniciar a documentação do projeto

> ~$ docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .

_será criada uma pasta docs (com o arquivo index.md) e um arquivo mkdocs.yml_

3. Par ativar o tema, o mkdocs.yml começará assim:

theme:
  name: material