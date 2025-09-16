Diário de bordo
---

Criei um diretório vazio para organizar o que for implementado por curso, logo adicionei um diretório e o rastreei no git.

```bash
mkdir continuous-integration
```

O git não consegue rastrear diretórios vazios, é uma pratica comum quando se quer colocar um diretório vazio no repositório colocar um arquivo com o nome `.gitkeep`. Então:

```bash
touch continuous-integration/.gitkeep
```

Agora o git pode rastrear o diretório:

````bash
git add continuous-integration/
```

Estou utilizando um padrão específico de commit <incluir_depois_o_link_da_documentacao_deste_padrão>, este tipo de operação, estará na categoria `chore` portanto:

```bash
git commit -m "chore: Add course directory"
```

Por ser um projeto apenas para estudo esta padronização  de commits é desnecessária, mas quis colocar mesmo assim 🤷🏻.

Dentro do diretório criado, clonei o projeto disponibilizado no curso, a forma recomendada de se rastrear repositórios git dentro de outro repositório é utilizando o comando `git add submodule`.

```bash
git add submodule git@github.com:CViniciusSDias/projeto_go_alura.git
```

Com o repositório devidamente clonado, entramos no próprio para então executar o comando docker compose para inicializar a composição de containers configurada no projeto:

Primeiro, utilizando a flag `-d` para rodar em segundo plano
```bash
docker compose up -d
```

Por estar utilizando o notebook da empresa que tem o Windows com WSL, houveram algumas coisas a mais que tive que fazer. Apareceu um erro, falando que não tenho o docker compose instalado, o que achei estranho (infelizmente não tirei prints das mensagens). Logo me lembrei que talvez o docker, por algum motivo, só estava aceitando o comando `docker-compose` (não confundir com o comando separado: `docker compose` sem o hífen). Ao executar o comando, retornou uma mensagem relacionada à integração do docker com o WSL2, logo me lembrei que o docker desktop não estava ativado no meu Windows, tinha desativado uns meses atrás por algum mal funcionamento que não vou me lembrar dos detalhes agora.

<inserir_imagem_da_configuracao_que_fiz_no_docker_desktop>



