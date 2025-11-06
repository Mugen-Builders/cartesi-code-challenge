# Cartesi Rollups Code Challenge

## Descrição

Este desafio de código é parte do workshop do @cartesiproject no Brasil, realizado no Inteli. Os participantes devem documentar todo o processo em um README e compartilhar um vídeo no Twitter|X.

## Instruções do Desafio

1.  **Encontrar os Valores Corretos**:
    
    -   Utilize o código fornecido para identificar o valor correto que deve ser adivinhado (guess), bem como outro valor que advém de uma "charada" (birth_year). Assim que você conseguir gerar o output correto, faça o "decode" da payload (hex) e mostre a string gerada. Corra! Você precisa ser o primeiro a postar no Twitter|X juntamente com um README.md e um vídeo refazendo os inputs até o decode da string para ganhar o prêmio.

2.  **Documentar o Processo**:
    
    -   Crie um README documentando cada passo que você tomou para encontrar o guess correto. Se possível, use referências para a documentação da Cartesi: https://docs.cartesi.io/.

3.  **Postagem no Twitter|X**:
    
    -   Faça uma postagem no Twitter|X com um vídeo demonstrando a resolução do desafio e o link para o README.md com a explicação. Use o template de mensagem fornecido abaixo e sinta-se à vontade para comentar sobre a experiência do workshop.


## Message Template
```text
I'm participating in the @cartesiproject workshop in Brazil, taking place at Inteli.
Here's a video demonstrating the resolution of the code challenge presented by @henrimarlon_.
```

**Você precisa submeter o link de uma thread criada com os requsitos de submissão no X como comentário nesse [post](https://x.com/henrimarlon_/status/1985729322900942968).**

## Passo a Passo

### 1. Configuração do Ambiente

#### Pré-requisitos

Antes de começar, certifique-se de ter instalado:

1. **Foundry**: https://getfoundry.sh/

2. **Docker Desktop**: https://www.docker.com/products/docker-desktop/

3. **Cartesi CLI**:
```bash
npm install -g @cartesi/cli@2.0.0-alpha.20
cartesi --help
```

#### Verificando a Instalação

Após instalar os pré-requisitos, verifique se tudo está configurado corretamente:

```bash
cartesi doctor
```

**Output esperado:**
```bash
✔ Your system is ready.
```

#### Clonando o Repositório

Clone o repositório do desafio:

```bash
git clone https://github.com/Mugen-builders/cartesi-code-challenge.git
```

### 2. Rodando o Código

```bash
cd challenge
cartesi build
cartesi run
```

**Anote o endereço da aplicação que será exibido no output:**
```
✔ challenge contract deployed at <endereço-da-aplicação>
```

Você precisará deste endereço para verificar os outputs posteriormente.

### 3. Interaja com o dApp:

Em outro terminal, envie um input com seus valores de guess e birth_year:

```bash
cartesi send '{"guess": <valor-aqui>, "birth_year": <valor-aqui>}' --application=<endereço-da-aplicação> --rpc-url="http://127.0.0.1:6751/anvil"
```

**Exemplo:**
```bash
cartesi send '{"guess": 1234, "birth_year": 2004}'
```

Envie quantas inputs achar necessário para encontrar os valores certos!

### 4. Verificando os Outputs (Notices)

Após enviar o input, verifique se você recebeu um notice de sucesso (use o endereço da aplicação anotado anteriormente):

```bash
curl -X POST http://127.0.0.1:6751/rpc \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "method": "cartesi_listOutputs",
    "params": {
      "application": "<endereço-da-aplicação>",
      "limit": 10,
      "offset": 0
    },
    "id": 1
  }'
```

**Exemplo com endereço:**
```bash
curl -X POST http://127.0.0.1:6751/rpc \
  -H "Content-Type: application/json" \
  -d '{
    "jsonrpc": "2.0",
    "method": "cartesi_listOutputs",
    "params": {
      "application": "0xc0f6c529e869e9e9f9ea2b2b38dd7a343ad6a0dd",
      "limit": 10,
      "offset": 0
    },
    "id": 1
  }'
```

### 5. Decodificando a Payload

Se você recebeu um notice, copie o valor do campo `payload` e decodifique usando o comando `cast`:

```bash
cast to-ascii <payload-em-hex>
```

**Exemplo:**
```bash
cast to-ascii 0x436f6e67726174756c6174696f6e73203078663339666436653531616164383866366634636536616238383237323739636666666239323236362120596f75206861766520736f6c76656420746865206368616c6c656e676521
```

**Output esperado quando você acertar:**

```text
Congratulations <seu-endereço-de-carteira>! You have solved the challenge!
```

*Nota: O endereço da carteira na mensagem pode variar dependendo da conta que você está usando.*

### 6. Dicas:

Leia o código!
O output esperado é um notice! ;)

### 5. Postagem no Twitter

Grave um vídeo demonstrando o processo e poste no Twitter|X utilizando o template fornecido, junto a um link para um README.md com a explicação da resolução.

## Suporte

Se você tiver dúvidas durante o desafio, junte-se ao Discord oficial da Cartesi:

**Discord da Cartesi**: https://discord.com/invite/pfXMwXDDfW

**Nota importante**: O suporte no Discord é fornecido em inglês. Prepare suas dúvidas em inglês para obter ajuda da comunidade.

## Observações Finais

Boa sorte, Cartesians!
