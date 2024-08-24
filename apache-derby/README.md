# Apache Derby - Versão 10.17

Site do projeto: https://db.apache.org/derby/

Site da documentação: https://db.apache.org/derby/docs/10.17/ 

## Ferramenta

- A IDE escolhida para o estudo foi o VS Code.
- O Terminal utilizado foi o gitbash.
- Java 19 ou maior conforme solicitado na documentação, seção: [System requirements](https://db.apache.org/derby/docs/10.17/getstart/cgsintsr.html.) 

## Instalação

Para usar o Apache Derby e necessário baixar o projeto.

Afim de aprender cada modo de utilização do Apache Derby, inicialmente será utilizado a linha de comando para a sua utilização.

Assim sendo, o comando abaixo efetuar o download do Apache Derby.

:warning: Todo e qualquer comando deve ser executando dentro da pasta de estudo  `apache-derby` localizada na raiz do repositório de estutos.

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

Nesta seção é inicado o basico do aprendizado sobre o os tipo de conexão com o Derby, seguiremos conforme o get start do site oficial, na seção: [Self-study tutorial for users new to Derby](https://db.apache.org/derby/docs/10.17/getstart/cgstutorialintro.html)

:warning: Todos os passo para esta tutorial ficarão dentro da pasta `getstart`, assim todos os comandos apresentados no tutorial serão ajustados para a organição deste repositório e serão apresentado na mesma ordem conforme o tutorial, e alguma pasta adicionais serão criadas para uma melhor organização.

 :warning: Para facilitar todo o aprendizado, utilizaremos sempre os scripts fornecidos no projeto, estes já configuram temporariamente as variáveis necessárias para a utilização do Derby.

### Atividade 1: Rodando SQL usando o drive integrado.

#### Criando um diretório e copiando scripts

Vamos criar um novo diretorio e copiar os scripts de exemplo já contido no projeto, conforme comando abaixo: 

```bash
mkdir -p getstart/DERBYTUTOR && \
cp db-derby-10.17.1.0-bin/demo/programs/toursdb/*.sql ./getstart/DERBYTUTOR/ && \
mkdir getstart/atividade1/
```
Agora vamos iniciar o Derby em modo integrado usando a ferramente `ij`.

```bash
./db-derby-10.17.1.0-bin/bin/ij
``` 
Criando o banco de dados e abrindo a conexão.

```bash
connect 'jdbc:derby:getstart/atividade1/firstdb;create=true';
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
Populando a novas tabelas a partir de um arquivo de script sql:

```bash
run 'getstart/DERBYTUTOR/loadCOUNTRIES.sql';
run 'getstart/DERBYTUTOR/loadCITIES.sql';
run 'getstart/DERBYTUTOR/loadAIRLINES.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTS1.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTS2.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTAVAILABILITY1.sql';
run 'getstart/DERBYTUTOR/loadFLIGHTAVAILABILITY2.sql';
```








