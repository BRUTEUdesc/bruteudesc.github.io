# Site BRUTE UDESC

## Rodando localmente

### Instale o Ruby e o Bundler

Instale o `rbenv`. Isso vai facilitar sua vida em termos de lidar com versões.
[Link](https://github.com/rbenv/rbenv#installation)

```bash
# Clonando a aplicação
git clone https://github.com/rbenv/rbenv.git ~/.rbenv

# Adicionando ao PATH (troque para o seu shell)
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bash_profile

# Iniciando instalação
~/.rbenv/bin/rbenv init

# Reiniciando shell
exec $SHELL

# Checkando se está OK
curl -fsSL https://github.com/rbenv/rbenv-installer/raw/master/bin/rbenv-doctor | bash

# Instalando scrip para usar rbenv instal
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```

Agora instale a versão Ruby do projeto. 

`rbenv install 2.7.0`

E por fim, o bundler

`gem install bundler`

### Instalando dependências

Na pasta do repositório, execute

`bundle install`

### Subindo o servido localmente

`bundle exec jekyll serve`

### Testando

Pronto, agora é só acessar [localhost:4000](localhost:4000)