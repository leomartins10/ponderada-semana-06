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
# Documentação dos Testes de Criptografia e Hash

Esta documentação foi desenvolvida com base nos seguintes critérios:

- Descrição completa do método utilizado para garantir a reprodutibilidade;
- Resultados obtidos em uma tabela com 10 testes diferentes;
- Comparação com análise textual entre AES-256 e SHA-256;
- Análise baseada nos resultados obtidos.

## Parte 1: Descrição do Método Utilizado

### SHA-256 (Hash)
- Biblioteca: Utilizamos a biblioteca nativa `hashlib` do Python.
- Procedimento: 
  - Cada entrada de texto é convertida para bytes (caso seja uma string).  
  - A função `sha256()` processa a entrada e gera um digest hexadecimal de 256 bits (ou seja, 64 caracteres em hexadecimal).  
- Propriedade:  
  - O método é unidirecional, isto é, não há um processo de "descriptografia".  
  - Serve para verificação de integridade dos dados, já que qualquer modificação na entrada gera um hash completamente diferente.

### AES-256 (Criptografia Simétrica)
- Biblioteca: Utilizamos a biblioteca “PyCryptodome”.
- Procedimento:  
  - Geração de chave: Uma chave aleatória de 256 bits (32 bytes) é gerada e utilizada para todas as operações.  
  - IV (Vetor de Inicialização): Para cada texto, é gerado um IV de 16 bytes. Este valor garante que mesmo a mesma mensagem criptografada com a mesma chave produza resultados diferentes (devido ao modo CBC).  
  - Processo:
    - O texto é convertido para bytes e recebe o padding necessário (para que seu tamanho seja múltiplo do tamanho do bloco, 16 bytes).  
    - A criptografia é realizada com AES no modo CBC.  
    - A operação de descriptografia utiliza a mesma chave e IV, removendo o padding para recuperar o texto original.
- Medição de Tempo:  
  - As operações de criptografia e descriptografia são temporizadas usando `time.perf_counter()`, que oferece alta resolução e precisão para as medições, permitindo comparar o desempenho dos algoritmos.

Esta metodologia detalhada possibilita a replicação dos testes em diferentes ambientes, garantindo consistência e confiabilidade dos resultados.

