1. Instalação do `material for mkdocs`

> ~$ docker pull squidfunk/mkdocs-material

2. Iniciar a documentação do projeto

> ~$ docker run --rm -it -v ${PWD}:/docs squidfunk/mkdocs-material new .

_será criada uma pasta docs (com o arquivo index.md) e um arquivo mkdocs.yml_

3. Par ativar o tema, o `mkdocs.yml` começará assim:

theme:
  name: material

4. Para ver as alterações em tempo real:

> ~$ docker run --rm -it -p 8000:8000 -v ${PWD}:/docs squidfunk/mkdocs-material

5. Para hospedar o site no GitHub pages:

- Primeiro foi necessária a criação do GitHub Actions workflow dentro do repositório: `.github/workflows/ci.yml`  
Com a pasta da maneira que está escrita [neste site](https://squidfunk.github.io/mkdocs-material/publishing-your-site/).

- Depois de dar o push para o github, ativamos no github pages nas configurações e o site foi criado!


# Configurações do site 

Dentro da pasta `mkdocs.yml` são feitas todas as alterações do site: adicionados tópicos; mudança de cores; etc

