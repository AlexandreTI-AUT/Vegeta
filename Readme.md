# Vegeta Teste de Perforomance #

![alt text](https://i1.wp.com/ocapacitor.com/wp-content/uploads/2018/01/5070928-1427167529-latest.jpeg?zoom=2&resize=520%2C245&ssl=1)

### Esse projeto tem como objetivo realizar Teste de Performance utilizando a ferramenta de testes Vegeta? ###

### Requisitos ####
* Homebrew instalado maquina - (https://brew.sh/index_pt-br)
* Instalar o vegeta 
    * Mac OS X:
    - - $ brew update && brew install vegeta

    * Curl (Linux)
    - - $ curl -LO https://github.com/tsenart/vegeta/releases/download/v12.8.3/vegeta-12.8.3-linux-amd64.tar.gz
    - - tar -zxvf vegeta-12.8.3-linux-amd64.tar.gz
    - - sudo mv ./vegeta /usr/bin/vegeta

    * Verficar a instalação:
    - - vegeta --version

* Instalar Plot
    * - brew install rs/tap/jplot
* Instalar o JAGGR
    * - brew install rs/tap/jaggr
* Instalar JQ
    * - brew install jq


### Estrutura do Projeto: ###

* /data é armazenado os arquivos .json com os dados que serão utilizados na requisições POST.
* /reports armazena o report gerado após finlização da execução do teste, arquivos .json e html.
* /request armazena arquivo .txt(esse arquivo pode ter qualquer titulo, no nosso caso resquest) com as requisições que serão executadas pelo Vegeta.
* /results armazena o arquivo .bin com o resultado do testes, serve para analisar o resultado no terminal.


### Comandos de execução: ###

* echo "GET http://<application_url>/some/path" | vegeta attack -rate=10 -duration=30s | vegeta report - (executa o teste e apresenta do resultado direto no terminal)
  
* vegeta attack -duration=10s -rate=10 -timeout=60s -targets=request/request.txt > results/results.bin | vegeta report -output=reports/report_execution.json && vegeta plot -title="Report HIGIA" results/results.bin > reports/reports.html - (executa o teste e gera os arquivos/relatorios .json, .html e .bin)
  
* vegeta report results/results.bin - (apresenta o resultado gerado no arquivo .bin)

### Retorno da requisição 

* Total - número de solicitações emitidas.
* Rate - taxas reais de pedidos sustentadas no período de ataque.
* Throughputd - número de solicitações bem-sucedidas durante o total período.

### A Duração:

* Attack - O tempo gasto para emitir todas as solicitações ( total- wait)
* Wait - O tempo de espera pela resposta à última solicitação emitida ( total- attack)
* Total - O tempo gasto no ataque ( attack+ wait)

### Latência

* min - é a latência mínima de todas as solicitações em um ataque.
* mean - é a média aritmética / média das latências de todas as solicitações em um ataque.
* 50, 90, 95, 99 - São os 50%, 90%, 95% e 99% percentis , respectivamente, das latências de todos os pedidos de um ataque.
* max - é a latência máxima de todas as solicitações em um ataque.

### Bytes In e Bytes Out

* total - número de bytes enviados (saída) ou recebidos (entrada) com os corpos de solicitação ou resposta.
* mean - número de bytes enviados (saída) ou recebidos (entrada) com os corpos de solicitação ou resposta.

### Outros resultados
* Success - proporção mostra a porcentagem de solicitações cujas respostas não apresentaram erros e tiveram códigos de status entre 200 e 400 (não inclusivo).

* Status Codesl - inha mostra um histograma de códigos de status. 0códigos de status significam que uma solicitação não foi enviada.

* Error Set - mostra um conjunto exclusivo de erros retornados por todas as solicitações emitidas. Isso inclui solicitações que obtiveram um código de status de resposta sem êxito.