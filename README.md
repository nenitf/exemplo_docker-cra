# exemplo_docker-cra

## Motivação

- Facilitar troca de contexto de projetos (versões de ferramentas)
- Simplificar criação de ambiente

## Criação do projeto

1. Crie a pasta do projeto
    ```sh
    mkdir projectName
    cd projectName
    ```

2. Crie a estrutura com template cra
    ```sh
    docker container run --rm -t -v $(pwd):/app/ -w /app node:16 yarn create react-app .
    ```

    > **Linux**: Garantir permissões da pasta ao usuário do host ``sudo chown -R $USER:$USER .``

3. Remova `node_modules` do host
    ```sh
    rm -r node_modules
    ```

4. Crie a pasta `docker`
    > Exclua arquivos referentes ao `cypress` caso queira

## Execução

### Desenvolvimento

1. Suba o ambiente
    ```sh
    docker-compose -f docker/docker-compose.yml up -d
    ```

2. Inicie o servidor
    ```sh
    docker-compose -f docker/docker-compose.yml exec app yarn start
    ```

### Adição de dependências

1. Suba o ambiente

2. Adicione as dependências
    ```sh
    docker-compose -f docker/docker-compose.yml exec app yarn add <dependencia>
    ```

3. Quando parar o ambiente, na próxima vez que subi-lo *rebuilde*
    ```sh
    docker-compose -f docker/docker-compose.yml up -d --build
    ```

### Testes

#### Jest

1. Suba o ambiente

2. Execute os testes
    ```sh
    docker-compose -f docker/docker-compose.yml exec app yarn test
    ```

#### Cypress

- Suba o ambiente configurado e execute os testes
    ```sh
    docker-compose -f docker/docker-compose.yml -f docker/cy-docker-compose.yml up
    ```

## Instruções

- Pare o container com ``docker-compose -f docker/docker-compose.yml down`` caso ele tenha subido com ``-d``, do contrário tecle <Ctrl><C>
- Acesse o container com ``docker-compose -f docker/docker-compose.yml exec app sh``
- Utilize outras definições do docker-compose para complementar o base, assim como `docker/cy-docker-compose.yml` serve para definir comando ao subir o container de `docker/docker-compose.yml`
