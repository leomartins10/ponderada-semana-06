# Ponderada Semana 06
### Seleção das bibliotecas
Para realizar os casos de testes dos algoritmos SHA-256 (Hash) e AES-256 (Criptografia) foram selecionadas as bibliotecas `hashlib` e `PyCryptodome`

**Hashlib**: A `hashlib` faz parte da biblioteca padrão do Python baseada no OpenSSL. Portanto, confiável e fácil de usar.

**PyCryptodome**: PyCryptodome é uma biblioteca completa, oferece diversos métodos de criptografia (simétrica, assimétrica) e possuindo uma documentação detalhada. Outra vantagem é a ausência de dependências externas, o que reduz  o consumo de memória e proporciona um processamento eficiente. 

### Planejamento dos Casos de Teste
O seguinte planejamento foi traçado para realizar os testes detelhadamente:

#### Critérios de teste:
- Correção do hash: Verificar se o hash gerado está de acordo com o padrão SHA-256 (64 caracteres hexadecimais).
- Tempo de execução: Verificar se o processamento ocorre em tempo razoável (especialmente em entradas grandes).
- Tamanho e complexidade da entrada: Variar desde strings vazias até dados grandes ou binários, incluindo caracteres especiais.
- Confiabilidade: Garantir que o algoritmo sempre retorne o mesmo resultado para a mesma entrada (idempotência).

#### Caso de teste 1: String vazia
Entrada: "" (string vazia)

Justificativa: Avaliar o comportamento da função quando não há conteúdo algum.

Expectativa: Deve gerar um hash SHA-256 válido (64 caracteres em hexadecimal), conhecido para string vazia, e o tempo de execução deve ser praticamente instantâneo.

#### Caso de teste 2: Texto simples
Entrada: "Hello World"

Justificativa: Testar uma string curta, sem caracteres especiais.

Expectativa: Deve retornar o hash conhecido para "Hello World". A saída deve ser consistente sempre que for executada, confirmando a idempotência.

#### Caso de teste 3: Texto com caracteres especiais
Entrada: "Olá, mundo! UTF-8: çãõáê"

Justificativa: Avaliar o comportamento da codificação em UTF-8, testando caracteres acentuados e símbolos.

Expectativa: Deve gerar um hash válido, e o resultado não deve variar mesmo com caracteres multibyte (acentos, cedilha, etc.).

#### Caso de teste 4: String extensa ou arquivo simulado

Entrada: Uma string bem longa (por exemplo, repetindo um trecho de texto várias vezes ou simulando um arquivo de alguns MB).

Justificativa: Verificar o impacto de uma entrada maior tanto no tempo de processamento quanto na saída gerada.

Expectativa: O hash deve ser calculado corretamente (sempre 64 caracteres), e o tempo de execução ainda deve ser aceitável.

#### Caso de teste 5: Dados binários

Entrada: Conteúdo que não seja somente texto (por exemplo, bytes que simulam parte de um arquivo binário, como b'\x00\xFF\x10\x80').

Justificativa: Garantir que a função lida corretamente com dados não UTF-8 (já que há a conversão para bytes internamente) e não falha ao processá-los.

Expectativa: Geração de um hash SHA-256 válido, confirmando a robustez do algoritmo para qualquer tipo de dado.

#### Caso de teste 1 - Criptografar e descriptografar uma string curta

Objetivo: Verificar se AES-256 consegue criptografar e descriptografar corretamente uma string curta sem perda de dados.

Método:
Utilizar uma chave de 256 bits.</br>
Criptografar uma string curta, como "Hello" ou "Teste".</br>
Descriptografar o resultado e verificar se o texto original é recuperado.

Resultado esperado:
O texto descriptografado deve ser idêntico ao original.</br>
O tempo de criptografia/descriptografia deve ser mínimo.

Observações importantes:
Pequenos textos podem precisar de preenchimento (padding), pois AES-256 trabalha com blocos de 16 bytes.

#### Caso de teste 2: Criptografar e descriptografar uma string longa

Objetivo: Avaliar o comportamento do AES-256 ao lidar com um volume maior de dados.

Método: 
Utilizar uma string longa, como "Este é um texto longo para testar a criptografia AES-256 em diferentes cenários e tamanhos de entrada."</br>
Criptografar e descriptografar o texto, comparando com o original.</br>
Medir tempo de processamento.

Resultado esperado:
A criptografia e descriptografia devem funcionar corretamente, mantendo o conteúdo original.</br>
O tempo de processamento pode ser maior do que no teste de string curta.

Observações importantes:
Tamanhos maiores de entrada aumentam o tempo de criptografia.

#### Caso de teste 3: criptografar e descriptografar um texto com caracteres especiais

Objetivo: Testar se caracteres especiais, como @#$%&*çéôñ, são preservados corretamente após a criptografia e descriptografia.

Método:
Utilizar uma string como "Senha$#@!123 é segura?".</br>
Criptografar e descriptografar, verificando se os caracteres especiais são mantidos.

Resultado esperado:
O texto recuperado deve ser idêntico ao original, sem perda de caracteres especiais.

Observações importantes:
Certificar-se de que a codificação usada no código (UTF-8) está correta para suportar todos os caracteres.

#### Caso de teste 4: Criptografar e descriptografar um arquivo pequeno

Objetivo: Testar o funcionamento do AES-256 ao criptografar um arquivo pequeno, como um .txt ou .csv.

Método:
Criar um arquivo pequeno com algumas linhas de texto.</br>
Ler o conteúdo do arquivo, criptografá-lo e salvar o resultado criptografado.</br>
Descriptografar e verificar se o conteúdo do arquivo original é recuperado corretamente.

Resultado esperado:
O arquivo descriptografado deve ser exatamente igual ao original.

Observações importantes:
Pode ser necessário dividir o conteúdo em blocos antes de criptografar.

#### Caso de teste 5: Criptografar e descriptografar um arquivo grande

Objetivo: Avaliar o desempenho do AES-256 ao processar arquivos grandes, como um PDF ou imagem de vários megabytes.

Método:
Utilizar um arquivo maior (exemplo: 5MB).</br>
Ler o arquivo em partes e criptografá-lo progressivamente.</br>
Salvar o resultado criptografado e, em seguida, descriptografá-lo.</br>
Comparar o arquivo resultante com o original para verificar a integridade dos dados.

Resultado esperado:
O arquivo original deve ser recuperado corretamente após a descriptografia.</br>
O tempo de processamento será significativamente maior do que nos testes anteriores.

Observações importantes:
O uso de memória pode aumentar dependendo do tamanho do arquivo.</br>
Deve-se testar a eficiência do algoritmo ao lidar com grandes volumes de dados.