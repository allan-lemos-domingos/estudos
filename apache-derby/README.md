# Apache Derby - Versão 10.17

Site do projeto: https://db.apache.org/derby/

Site da documentação: https://db.apache.org/derby/docs/10.17/ 

## Ferramenta

- A IDE escolhida para o estudo foi o VS Code.
- O Terminal utilizado foi o gitbash.
- Java 19 ou superior conforme solicitado na documentação, seção: [System requirements](https://db.apache.org/derby/docs/10.17/getstart/cgsintsr.html.) 

## Instalação

Para usar o Apache Derby e necessário baixar o projeto e descompactado-lo dentro da pasta de estudo do projeto.

Afim de aprender cada modo de utilização do Apache Derby, inicialmente será utilizado a linha de comando para a sua utilização.

Assim sendo, o comando abaixo efetuar o download do Apache Derby.

:warning: Todo e qualquer comando deve ser executando dentro da pasta de estudo  `apache-derby` localizada na raiz do repositório de estudos.

```bash
wget https://dlcdn.apache.org//db/derby/db-derby-10.17.1.0/db-derby-10.17.1.0-bin.tar.gz && \
tar -zxf db-derby-10.17.1.0-bin.tar.gz && \
rm db-derby-10.17.1.0-bin.tar.gz
```

Para verificar a instalação iremos usar a ferramente `sysinfo` para obter informações sobre o java environment a versão do Derby.

```bash
./db-derby-10.17.1.0-bin/bin/sysinfo
```

## Get Start 

Nesta seção é iniciado o básico do aprendizado sobre o os tipo de conexão com o Derby, seguiremos conforme o get start do site oficial, na seção: [Self-study tutorial for users new to Derby](https://db.apache.org/derby/docs/10.17/getstart/cgstutorialintro.html)

:warning: Todos os passo para este tutorial ficarão dentro da pasta `getstart`, assim todos os comandos apresentados no tutorial serão ajustados para a organização deste repositório e serão apresentado na mesma ordem conforme o tutorial. Algumas pastas adicionais serão criadas para uma melhor organização.

:warning: Para facilitar todo o aprendizado, utilizaremos sempre os scripts fornecidos no projeto, estes já configuram temporariamente as variáveis necessárias para a utilização do Apache Derby.

### Atividade 1: Rodando SQL usando o drive integrado.

#### Criando um diretório e copiando scripts

Vamos criar um novo diretório e copiar os scripts de exemplo já contido no projeto, conforme comando abaixo: 

```bash
mkdir -p getstart/DERBYTUTOR && \
cp db-derby-10.17.1.0-bin/demo/programs/toursdb/*.sql ./getstart/DERBYTUTOR/ 
```
Agora vamos iniciar o Apache Derby em modo integrado usando a ferramente `ij`.

```bash
./db-derby-10.17.1.0-bin/bin/ij
``` 
Criando o banco de dados e abrindo a conexão.

```bash
connect 'jdbc:derby:getstart/derbytutordb;create=true';
```
Criando a primeira tabela:

```bash
CREATE TABLE FIRSTTABLE(
ID INT PRIMARY KEY,
NAME VARCHAR(12));
```

Inserindo alguns registros na tabela:

```bash
INSERT INTO FIRSTTABLE VALUES 
(10,'TEN'),(20,'TWENTY'),(30,'THIRTY');
```
Efetuando select de todas os registros:

```bash
SELECT * FROM FIRSTTABLE;
```

Efetuando select com restrição ao registro de `id` 20.

```bash
SELECT * FROM FIRSTTABLE WHERE ID=20;
```

Criando novas tabelas em um outro schema a partir de um arquivo de script sql:

```bash
run 'getstart/DERBYTUTOR/ToursDB_schema.sql';
```
Populando as novas tabelas a partir de um arquivo de script sql:

```bash
run 'getstart/DERBYTUTOR/loadCOUNTRIES.sql';
run 'getstart/DERBYTUTOR/loadCITIES.sql';
run 'getstart/DERBYTUTOR/loadAIRLINES.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTS1.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTS2.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTAVAILABILITY1.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTAVAILABILITY2.sql';
```
### Atividade 2: Rodando SQL usando o driver cliente.

Para demonstrar o uso Apache Derby no modo cliente/servidor será utlizado dois terminais, um para iniciar-lo em modo servidor de rede, e outro para acessa-lo como cliente.

#### Iniciando Derby como Servidor.

Para iniciar o Apache Derby em modo servidor de rede, deve ser executado o seguindo comando:

```bash
./db-derby-10.17.1.0-bin/bin/NetworkServerControl start
```

Após o iniciar, será apresentado no terminal o número de ip e porta para se conectar ao servidor.

Agora deve abrir o segundo terminal e iniciar o cliente usando a ferramenta `ij` diponível junto ao distribuição, também na pasta bin, conforme abaixo: 

```bash
./db-derby-10.17.1.0-bin/bin/ij
```

Apó iniciar o cliente no segundo terminal, devemos informa em qual host e porta conectar, o exemplo abaixo considera que o servidor esta rodando em localhost na porta padrão 1527, o banco será utilizado o mesmo criado na [Atividade 1](#atividade-1-rodando-sql-usando-o-drive-integrado):

```bash
connect 'jdbc:derby://localhost:1527/getstart/derbytutordb;create=true';
```

Para finalizar terminar a conexão do com servidor pode-se usar o comando asseguir: 

```bash
exit;
```
E para parar o servidor, deve abrir um terceiro terminal e executar o comandando baixo finaliza sua execução.

```bash
./db-derby-10.17.1.0-bin/bin/NetworkServerControl shutdown
```








 


