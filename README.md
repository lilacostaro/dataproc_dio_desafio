<<<<<<< HEAD
# Digital Innovation One - Desafio
Projeto criado através do desafio da DIO para conclusão do BootCamp de DataEnginner

## Passo-a-Passo

### Etapa 1

- Criar uma conta do Gmail para ser utilizada no projeto
- Criar uma conta no [Google Cloud Platform(CGP)](https://cloud.google.com/?utm_source=google&utm_medium=cpc&utm_campaign=latam-BR-all-pt-dr-BKWS-all-all-trial-e-dr-1009897-LUAC0010101&utm_content=text-ad-none-any-DEV_c-CRE_512285710743-ADGP_Hybrid%20%7C%20BKWS%20-%20EXA%20%7C%20Txt%20~%20GCP_General-KWID_43700062788251524-kwd-301173107504&utm_term=KW_google%20cloud%20platform-ST_Google%20Cloud%20Platform&gclid=CjwKCAiA1aiMBhAUEiwACw25MVpQ-wN9R_FX2JGM5m67FpBE_jYePmyedlcZjN78P3RljPFD4YDYbxoC4ZIQAvD_BwE&gclsrc=aw.ds)
- Criação de um projeto que será utilizado para alocar todos os recursos que serão utilizados para a conclusão do desafio. O projeto criado recebeu o nome de desafioDataProc.

### Etapa 2

- Criação de uma instancia de VM, para isso é necessário ativar a API de Compute Engine, caso ela inda não tenha sido ativada.
- A maquina criada pode ser acessada clicando no botão SSH no canto superior esquerdo da pagina da maquina, ou via Cloud Shell. 
- Os seguintes comandos foram utilizados para acessar a VM via Cloud Shell. 
- gcloud compute instances list
- gcloud compute ssh instancia-hadoop --zone=us-west1-a
- Esta etapa foi realizada apenas para uma maior conhecimento da plataforma e a maquina foi excluída em seguida.

### Etapa 3 - Criação do DataProc

- A primeira coisa a se fazer e ativar a Cloud Dataproc API.
- Também foi necessária a criação de uma credencial, atrelada a Cloud DataProc API para poder utilizar o DataProc.
- Foi criado um bucket para o armazenamento do arquivo que será executado para o projeto.
- Foi criado o cluster Hadoop via Interface e o código de linha de comando gerado para a mesma criação foi esse.

gcloud dataproc clusters create cluster-desafio-dataproc --enable-component-gateway --region us-west1 --zone us-west1-a --master-machine-type n1-standard-2 --master-boot-disk-size 500 --num-workers 3 --worker-machine-type n1-standard-2 --worker-boot-disk-size 500 --image-version 2.0-debian10 --optional-components JUPYTER,ZEPPELIN,ZOOKEEPER --project desafiodataproc-331703


### Etapa 4 - Execução do Desafio

- Clonar o repositório do Github fornecido pelo Instrutor no Cluster.
- Entrar no diretório e listar os arquivos.
- Rodar o comando: gsutil ls
- Rodar o comando: vim contador.py
- Atualizar o arquivo com as informações do bucket que foi criado.
- Copiar os arquivos para o bucket utilizando o comando: gsutil cp contador.py livro.txt gs://dataprocdesafio
- Criar um novo job com as seguintes informações:

Id do job: job-projeto \
Região: us-west1 \
Cluster: cluster-desafio-dataproc \
Tipo de Job: PySpark \
Arquivo Python Principal: gs://dataprocdesafio/contador.py

- Como resultado da execução do job foi gerado o arquivo [resultado_part-00000](https://github.com/lilacostaro/dataproc_dio_desafio/blob/main/resultado_part-00000) na pasta resultado no Cloud Storage.
- Foi criado o arquivo [resultado.txt](https://github.com/lilacostaro/dataproc_dio_desafio/blob/main/resultado.txt) e foi inserido nele as 10 primeiras linhas do arquivo **resultado_part-00000**.
