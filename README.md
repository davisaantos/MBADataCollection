# MBADataCollection

# Manual do Projeto de Coleta de Dados e Armazenamento com Kafka em Ubuntu

Este manual fornece instruções detalhadas para configurar e executar um projeto de coleta e armazenamento de dados que utiliza o Apache Kafka como ferramenta de streaming em uma máquina virtual (VM) rodando Ubuntu. O projeto permite a coleta de diversos tipos de dados, incluindo eventos, PDFs, imagens, vídeos e documentos do Office, e armazena-os localmente.

## Sumário

1. [Pré-requisitos](#pré-requisitos)
2. [Instalação e Configuração](#instalação-e-configuração)
   - [Configuração da Máquina Virtual](#configuração-da-máquina-virtual)
   - [Instalação do Java](#instalação-do-java)
   - [Instalação do Apache Kafka](#instalação-do-apache-kafka)
3. [Configuração do Projeto](#configuração-do-projeto)
   - [Clonar o Repositório](#clonar-o-repositório)
   - [Estrutura do Projeto](#estrutura-do-projeto)
4. [Execução do Kafka](#execução-do-kafka)
   - [Iniciando o ZooKeeper](#iniciando-o-zookeeper)
   - [Iniciando o Servidor Kafka](#iniciando-o-servidor-kafka)
5. [Execução do Produtor e Consumidor](#execução-do-produtor-e-consumidor)
   - [Produtor de Dados](#produtor-de-dados)
   - [Consumidor de Dados](#consumidor-de-dados)
6. [Armazenamento Local](#armazenamento-local)
7. [Testes e Validação](#testes-e-validação)
8. [Contribuições](#contribuições)
9. [Licença](#licença)

---

## Pré-requisitos

- Máquina virtual com Ubuntu instalado.
- Acesso ao terminal com permissões de administrador.
- Git instalado para clonar o repositório.
- Conhecimento básico de comandos Linux.

## Instalação e Configuração

### Configuração da Máquina Virtual

1. **Atualize os pacotes do sistema**:

   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```

### Instalação do Java

O Apache Kafka requer Java instalado no sistema.

1. **Instale o OpenJDK**:

   ```bash
   sudo apt install default-jdk -y
   ```

2. **Verifique a instalação do Java**:

   ```bash
   java -version
   ```

### Instalação do Apache Kafka

1. **Baixe a última versão do Kafka**:

   ```bash
   wget https://downloads.apache.org/kafka/3.5.1/kafka_2.13-3.5.1.tgz
   ```

2. **Extraia o arquivo baixado**:

   ```bash
   tar -xzf kafka_2.13-3.5.1.tgz
   ```

3. **Mova o diretório extraído para `/usr/local/kafka`**:

   ```bash
   sudo mv kafka_2.13-3.5.1 /usr/local/kafka
   ```

## Configuração do Projeto

### Clonar o Repositório

Clone o repositório do projeto no GitHub:

```bash
git clone https://github.com/seu_usuario/seu_projeto.git
```

Substitua `seu_usuario` e `seu_projeto` pelo nome de usuário e nome do repositório.

### Estrutura do Projeto

- `/producer`: Contém o código fonte do produtor de dados.
- `/consumer`: Contém o código fonte do consumidor de dados.
- `/data_storage`: Diretório onde os dados serão armazenados localmente.
- `README.md`: Documentação do projeto.

## Execução do Kafka

Antes de iniciar o produtor e o consumidor, é necessário iniciar o ZooKeeper e o servidor Kafka.

### Iniciando o ZooKeeper

1. **Navegue até o diretório do Kafka**:

   ```bash
   cd /usr/local/kafka
   ```

2. **Inicie o ZooKeeper**:

   ```bash
   bin/zookeeper-server-start.sh config/zookeeper.properties
   ```

   **Nota**: Recomenda-se executar este comando em uma janela de terminal separada.

### Iniciando o Servidor Kafka

1. **Em uma nova janela de terminal, inicie o servidor Kafka**:

   ```bash
   cd /usr/local/kafka
   bin/kafka-server-start.sh config/server.properties
   ```

## Execução do Produtor e Consumidor

### Produtor de Dados

O produtor envia os dados (eventos, PDFs, imagens, vídeos, documentos do Office) para um tópico Kafka.

1. **Navegue até o diretório do produtor**:

   ```bash
   cd seu_projeto/producer
   ```

2. **Instale as dependências necessárias** (se aplicável):

   ```bash
   pip install -r requirements.txt
   ```

3. **Configure o produtor**:

   Verifique o arquivo `config/producer_config.json` e ajuste as configurações conforme necessário (por exemplo, endereço do servidor Kafka, tópico).

4. **Execute o produtor**:

   ```bash
   python producer.py
   ```

### Consumidor de Dados

O consumidor recebe os dados do tópico Kafka e os armazena localmente.

1. **Navegue até o diretório do consumidor**:

   ```bash
   cd seu_projeto/consumer
   ```

2. **Instale as dependências necessárias** (se aplicável):

   ```bash
   pip install -r requirements.txt
   ```

3. **Configure o consumidor**:

   Verifique o arquivo `config/consumer_config.json` e ajuste as configurações conforme necessário.

4. **Execute o consumidor**:

   ```bash
   python consumer.py
   ```

## Armazenamento Local

Os dados consumidos serão armazenados no diretório `/data_storage`. Certifique-se de que este diretório existe:

```bash
mkdir -p seu_projeto/data_storage
```

## Testes e Validação

1. **Teste de Envio de Dados**:

   - Utilize o produtor para enviar diferentes tipos de dados.
   - Verifique os logs para confirmar o envio bem-sucedido.

2. **Verificação do Armazenamento**:

   - Confirme que os dados estão sendo armazenados corretamente no diretório `data_storage`.
   - Verifique a integridade dos arquivos armazenados.

3. **Monitoramento**:

   - Use ferramentas como o Kafka Monitor ou o Kafka Manager para monitorar os tópicos e as mensagens.

## Contribuições

Contribuições são bem-vindas! Para contribuir:

1. Faça um fork do repositório.
2. Crie uma nova branch com a sua feature ou correção de bug:

   ```bash
   git checkout -b minha-feature
   ```

3. Faça commit das suas alterações:

   ```bash
   git commit -m "Minha nova feature"
   ```

4. Envie para o branch principal:

   ```bash
   git push origin minha-feature
   ```

5. Abra um Pull Request no GitHub.

## Licença

Este projeto está licenciado sob a [Licença MIT](LICENSE).

---

**Observação**: Certifique-se de que todas as dependências e versões das ferramentas estejam compatíveis. Para mais detalhes, consulte a documentação oficial do [Apache Kafka](https://kafka.apache.org/documentation/) e das bibliotecas utilizadas no projeto.
