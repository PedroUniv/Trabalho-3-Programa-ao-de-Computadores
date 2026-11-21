Trabalho – Implementação de um Sistema de Registro e Gestão de Contas Bancárias (ETAPA 3)

2. Etapa 3 – Descrição
Nesta etapa, o sistema deverá ser aprimorado para permitir que os dados cadastrados e as movimentações realizadas sejam armazenados permanentemente em arquivos.
Até a Etapa 2, todas as informações ficavam armazenadas apenas na memória do computador, por meio de arrays. Isso significa que, ao encerrar o programa, todas as contas cadastradas,
os saldos e o histórico de movimentações eram perdidos.
Agora, o sistema deverá utilizar arquivos para armazenar essas informações, permitindo
que os dados sejam recuperados automaticamente quando o programa for executado novamente.
O aluno deverá utilizar os recursos de manipulação de arquivos da linguagem C++, apresentados no material da disciplina, especialmente:
 Biblioteca fstream;
o ofstream: para gravação de dados em arquivos;
o ifstream: para leitura de dados em arquivos;
o is_open(): para verificar se um arquivo foi aberto corretamente;
o getline(): para leitura de linhas;
o close(): para fechar arquivos;
o ios::app: para acrescentar informações ao final de um arquivo, quando necessário.
Também deverão ser utilizadas funções próprias para organizar as operações de leitura e gravação
dos dados.

2.1 Arquivos do Sistema
O sistema deverá trabalhar com dois arquivos de texto:

1. contas.txt
Deverá armazenar os dados de todas as contas cadastradas no sistema.
Para cada conta, deverão ser armazenadas as seguintes informações:
 Número da conta;
 Nome do cliente;
 CPF;
 Tipo da conta;
 Saldo;
 Situação da conta (ativa ou inativa).

Exemplo de conteúdo do arquivo:
1001;Ana Silva;12345678900;1;700.00;1
1002;Bruno Souza;98765432100;2;800.00;1
1003;Carlos Lima;11122233344;1;1500.00;1

Cada linha representa uma conta bancária. Os campos estão separados por ponto e vírgula.

2. movimentacoes.txt
Deverá armazenar o histórico de todas as movimentações realizadas no sistema.
Para cada movimentação, deverão ser armazenadas:
 Número da conta;
 Tipo da movimentação;
 Valor da movimentação.

Exemplo de conteúdo do arquivo:
1001;D;500.00
1001;S;300.00
1002;D;300.00
1003;D;1500.00

Os códigos utilizados continuam sendo:
Código Movimentação
D Depósito
S Saque
Nas transferências, deverão ser mantidos dois registros: um de saída (S) na conta de origem e outro de entrada (D) na conta de destino.
Observação: Os arquivos deverão preservar os dados mesmo depois que o programa for encerrado.

2.2 Carregamento dos dados ao iniciar o programa
Ao iniciar a execução, o sistema deverá verificar se os arquivos existem e realizar a leitura dos
dados armazenados.

O programa deverá:
1. Abrir o arquivo contas.txt para leitura.
2. Ler os registros armazenados.
3. Recuperar os dados de cada conta.
4. Armazenar os dados nos arrays utilizados na Etapa 2.
5. Atualizar a variável quantidadeContas.
6. Realizar o mesmo procedimento para o arquivo movimentacoes.txt.
7. Atualizar a variável quantidadeMovimentacoes.

Caso os arquivos ainda não existam (primeira execução do programa), o sistema deverá iniciar
normalmente, considerando que ainda não existem contas ou movimentações cadastradas.
Exemplo de funcionamento:
Imagine que o aluno cadastrou três contas e realizou algumas movimentações. Ao encerrar o programa e executá-lo novamente, o sistema deverá recuperar automaticamente essas três contas,
seus respectivos saldos e todo o histórico de movimentações.
Não será necessário cadastrar novamente as contas.

2.3 Salvamento dos dados das contas
Sempre que uma conta for cadastrada ou tiver alguma informação alterada, os dados deverão ser
armazenados no arquivo contas.txt.
O programa deverá percorrer os arrays de contas e gravar os registros no arquivo.

Exemplo:
ofstream arquivo("contas.txt");
if (arquivo.is_open()) {
 for (int i = 0; i < quantidadeContas; i++) {
 arquivo << numeroConta[i] << ";"
 << nomeCliente[i] << ";"
 << cpf[i] << ";"
 << tipoConta[i] << ";"
 << saldo[i] << ";"
 << contaAtiva[i] << endl;
 }
 arquivo.close();
}

Atenção: Na gravação completa dos arrays, a abertura do arquivo com ofstream sem ios::app
substitui o conteúdo anterior. Isso é adequado neste exemplo porque o programa percorre todas as
contas e grava novamente os registros atualizados.

2.4 Salvamento do histórico de movimentações
O histórico de movimentações também deverá ser armazenado permanentemente.
Sempre que ocorrer um depósito, saque ou transferência, o sistema deverá atualizar o arquivo movimentacoes.txt.
O arquivo deverá preservar todas as movimentações realizadas, inclusive aquelas registradas em
execuções anteriores do programa.

Exemplo:
ofstream arquivo("movimentacoes.txt");
if (arquivo.is_open()) {
 for (int i = 0; i < quantidadeMovimentacoes; i++) {
 arquivo << contaMovimentacao[i] << ";"
 << tipoMovimentacao[i] << ";"
 << valorMovimentacao[i] << endl;
 }
 arquivo.close();
}

Assim como no arquivo de contas, o exemplo realiza a gravação completa do histórico existente
nos arrays.

2.5 Transferências e persistência dos dados
A transferência entre contas deverá continuar funcionando conforme implementado na Etapa 2.
Considere novamente o exemplo:
 Conta 1001 – Ana: saldo de R$ 1.000,00.
 Conta 1002 – Bruno: saldo de R$ 500,00.

Ana transfere R$ 300,00 para Bruno.

Após a operação:
Conta Saldo anterior Saldo atualizado
1001 – Ana R$ 1.000,00 R$ 700,00
1002 – Bruno R$ 500,00 R$ 800,00

O histórico deverá registrar:
Conta Tipo Valor
1001 S R$ 300,00
1002 D R$ 300,00

Nesta etapa, além de atualizar os arrays, o programa deverá garantir que as alterações sejam gravadas nos arquivos correspondentes.

2.6 Funcionalidades obrigatórias

O sistema deverá manter todas as funcionalidades desenvolvidas na Etapa 2 e acrescentar a persistência dos dados, que é o salvamento em arquivos.
As funcionalidades esperadas são:
1. Cadastrar contas bancárias.
2. Listar as contas cadastradas.
3. Consultar uma conta pelo número.
4. Realizar depósitos.
5. Realizar saques, verificando se existe saldo suficiente.
6. Realizar transferências entre duas contas.
7. Exibir o extrato de uma conta.

Importante: Todas as operações de cadastro de contas, depósitos, saques e transferência deverão
atualizar os saldos e preservar o histórico de movimentações nos arquivos correspondentes (contas.txt e movimentações.txt) .

2.7 Utilização de funções próprias
Nesta etapa, deverão ser utilizadas funções próprias para organizar a leitura e a gravação dos arquivos. Se você já fez este procedimento, aceitando o desafio na ETAPA 2, não precisará fazer
novamente:
Sugestões de funções:
void carregarContas();
void salvarContas();
void carregarMovimentacoes();
void salvarMovimentacoes();

2.8 Sugestões de testes.
Para comprovar que a persistência dos dados está funcionando corretamente, o aluno deverá realizar os os testes a seguir. Estes testes poderão ser questionados na apresentação do dia 25/11:
Teste 1 – Cadastro e recuperação de contas
1. Executar o programa.
2. Cadastrar pelo menos três contas bancárias.
3. Encerrar o programa.
4. Executar novamente.
5. Listar as contas cadastradas.

Resultado esperado: as três contas deverão aparecer com todos os dados anteriormente cadastrados.

Teste 2 – Persistência dos saldos
1. Realizar um depósito em uma conta.
2. Realizar um saque em outra conta.
3. Encerrar o programa.
4. Executar novamente.
5. Consultar os saldos das duas contas.

Resultado esperado: os saldos deverão permanecer iguais aos valores existentes após as operações.

Teste 3 – Persistência das transferências
1. Realizar uma transferência entre duas contas.
2. Encerrar o programa.
3. Executar novamente.
4. Consultar as duas contas envolvidas.
5. Consultar o extrato de cada conta.

Resultado esperado: os saldos deverão estar atualizados e o extrato deverá apresentar os registros
de saída e entrada da transferência.

Teste 4 – Histórico de movimentações
1. Realizar diferentes depósitos, saques e transferências.
2. Encerrar o programa.
3. Executar novamente.
4. Consultar o extrato de uma conta que possua movimentações anteriores.

Resultado esperado: o sistema deverá apresentar todas as movimentações realizadas, inclusive
aquelas registradas antes do último encerramento do programa.
ATENÇÃO: O principal objetivo desta etapa é demonstrar que o sistema consegue armazenar informações permanentemente, recuperá-las em uma nova execução e continuar funcionando normalmente, sem perder as contas cadastradas, os saldos e o histórico de movimentações.
