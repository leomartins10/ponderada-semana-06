## Parte 1: Descrição do Método Utilizado

### SHA-256 (Hash)

- Utilizamos a biblioteca nativa `hashlib` do Python.

#### Procedimento
- **Conversão de Dados:**  
  Cada entrada de texto é convertida para bytes (caso seja uma string), garantindo que a função possa processar a informação corretamente.
- **Processamento do Hash:**  
  A função `sha256()` processa a entrada e gera um digest hexadecimal de 256 bits, resultando em uma saída fixa de 64 caracteres em hexadecimal.

#### Propriedades
- **Unidirecionalidade:**  
  - O método é unidirecional, ou seja, não há um processo de "descriptografia" do hash.
- **Verificação de Integridade:**  
  - Qualquer modificação, mesmo mínima, na entrada resulta em um hash completamente diferente, facilitando a verificação da integridade dos dados.

#### Pontos Positivos
- **Consistência:**  
  - Gera sempre uma saída de tamanho fixo (64 caracteres), independentemente do tamanho da entrada.
- **Segurança:**  
  - Devido à sua natureza unidirecional e ao design robusto, é resistente a colisões em condições ideais.
- **Rapidez:**  
  - O cálculo do hash é geralmente rápido e eficiente em termos de desempenho computacional.

#### Pontos Negativos
- **Irreversibilidade:**  
  - Uma vez gerado, o hash não pode ser revertido para recuperar a entrada original, o que limita seu uso a funções de verificação.
- **Sensibilidade a Alterações:**  
  - Pequenas alterações na entrada geram mudanças drásticas no hash, o que pode ser um desafio se for necessária uma análise de similaridade entre entradas.
- **Aplicabilidade Limitada:**  
  - Não pode ser utilizado para aplicações que requerem a recuperação dos dados originais, apenas para verificação e autenticação.



### AES-256 (Criptografia Simétrica)

#### Biblioteca
- Utilizamos a biblioteca **PyCryptodome**.

#### Procedimento
- **Geração de Chave:**  
  - Uma chave aleatória de 256 bits (32 bytes) é gerada e utilizada para todas as operações de criptografia e descriptografia.
- **Geração do IV (Vetor de Inicialização):**  
  - Para cada texto a ser criptografado, é gerado um IV de 16 bytes.  
  - Esse IV garante que mesmo a mesma mensagem criptografada com a mesma chave produza resultados diferentes (devido ao modo CBC).

#### Processo
- **Preparação dos Dados:**  
  - O texto é convertido para bytes e recebe o padding necessário para que seu tamanho seja múltiplo do tamanho do bloco (16 bytes).
- **Criptografia:**  
  - A operação de criptografia é realizada utilizando o algoritmo AES no modo CBC.
- **Descriptografia:**  
  - A operação de descriptografia utiliza a mesma chave e IV, removendo o padding para recuperar o texto original.

#### Medição de Tempo
- As operações de criptografia e descriptografia são temporizadas utilizando `time.perf_counter()`, que oferece alta resolução e precisão para as medições. Essa abordagem permite uma comparação detalhada do desempenho dos algoritmos.

#### Pontos Positivos
- **Reversibilidade:**  
  - Permite a recuperação exata do texto original, o que é essencial para aplicações que exigem tanto a proteção quanto a posterior leitura dos dados.
- **Segurança:**  
  - Utilizando uma chave de 256 bits e um IV aleatório, o método oferece um alto nível de segurança contra ataques, desde que os parâmetros sejam gerenciados corretamente.
- **Versatilidade:**  
  - Adequado para diversos cenários que requerem proteção da confidencialidade dos dados, como comunicação segura e armazenamento de informações sensíveis.

#### Pontos Negativos
- **Complexidade na Gestão de Parâmetros:**  
  - Requer um gerenciamento seguro da chave e do IV. Se esses elementos forem comprometidos, a segurança da criptografia pode ser seriamente afetada.
- **Custo Computacional:**  
  - Embora os tempos de processamento sejam baixos, a operação de criptografia e, especialmente, de descriptografia, pode ser mais custosa computacionalmente do que o cálculo de um hash simples como o SHA-256.
- **Sensibilidade ao Reuso de IV:**  
  - O uso repetido do mesmo IV com a mesma chave pode comprometer a segurança, exigindo cuidado na implementação para garantir a geração de IVs únicos para cada operação.

#### Considerações Gerais
- A metodologia empregada para ambos os métodos (SHA-256 e AES-256) permite a replicação dos testes em diferentes ambientes, garantindo consistência e confiabilidade dos resultados.
- A escolha entre SHA-256 e AES-256 depende da finalidade:
  - **SHA-256:** Ideal para verificação de integridade e autenticação.
  - **AES-256:** Essencial quando a confidencialidade e a possibilidade de recuperar os dados originais são requisitos.

