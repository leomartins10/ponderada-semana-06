# Ponderada Semana 06
## Seleção das bibliotecas
Para realizar os casos de testes dos algoritmos SHA-256 (Hash) e AES-256 (Criptografia) foram selecionadas as bibliotecas `hashlib` e `PyCryptodome`

**Hashlib**: A `hashlib` faz parte da biblioteca padrão do Python baseada no OpenSSL. Portanto, confiável e fácil de usar.

**PyCryptodome**: PyCryptodome é uma biblioteca completa, oferece diversos métodos de criptografia (simétrica, assimétrica) e possuindo uma documentação detalhada. Outra vantagem é a ausência de dependências externas, o que reduz  o consumo de memória e proporciona um processamento eficiente. 

## Planejamento dos Casos de Teste
### SHA-256
**Critérios de teste:**
- Correção do hash: Verificar se o hash gerado está de acordo com o padrão SHA-256 (64 caracteres hexadecimais).
- Tempo de execução: Verificar se o processamento ocorre em tempo razoável (especialmente em entradas grandes).
- Tamanho e complexidade da entrada: Variar desde strings vazias até dados grandes ou binários, incluindo caracteres especiais.
- Confiabilidade: Garantir que o algoritmo sempre retorne o mesmo resultado para a mesma entrada (idempotência).

**Caso de teste 1:** String vazia
- Entrada: "" (string vazia)
- Justificativa: Avaliar o comportamento da função quando não há conteúdo algum.
- Expectativa: Deve gerar um hash SHA-256 válido (64 caracteres em hexadecimal), conhecido para string vazia, e o tempo de execução deve ser praticamente instantâneo.

**Caso de teste 2:** Texto simples
- Entrada: "Hello World"
- Justificativa: Testar uma string curta, sem caracteres especiais.
- Expectativa: Deve retornar o hash conhecido para "Hello World". A saída deve ser consistente sempre que for executada, confirmando a idempotência.

**Caso de teste 3:** Texto com caracteres especiais
- Entrada: "Olá, mundo! UTF-8: çãõáê"
- Justificativa: Avaliar o comportamento da codificação em UTF-8, testando caracteres acentuados e símbolos.
- Expectativa: Deve gerar um hash válido, e o resultado não deve variar mesmo com caracteres multibyte (acentos, cedilha, etc.).

**Caso de teste 4:** String extensa ou arquivo simulado
- Entrada: Uma string bem longa (por exemplo, repetindo um trecho de texto várias vezes ou simulando um arquivo de alguns MB).
- Justificativa: Verificar o impacto de uma entrada maior tanto no tempo de processamento quanto na saída gerada.
- Expectativa: O hash deve ser calculado corretamente (sempre 64 caracteres), e o tempo de execução ainda deve ser aceitável.

**Caso de teste 5:** Dados binários
- Entrada: Conteúdo que não seja somente texto (por exemplo, bytes que simulam parte de um arquivo binário, como b'\x00\xFF\x10\x80').
- Justificativa: Garantir que a função lida corretamente com dados não UTF-8 (já que há a conversão para bytes internamente) e não falha ao processá-los.
- Expectativa: Geração de um hash SHA-256 válido, confirmando a robustez do algoritmo para qualquer tipo de dado.