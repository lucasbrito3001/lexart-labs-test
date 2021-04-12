# <strong>Documentação e Instruções do Projeto!</strong>

## <strong style="color: orange">Documentação:</strong>
<hr/>
<br/>

### <strong style="border-bottom: 2px solid orange">App.vue</strong>
- O componente App é a alma do projeto, é nele que está centralizada todas as REQUESTS que são feitas, basicamente centralizei o que se refere a API nele.
- Ele é responsável por enviar variáveis aos props dos componentes filhos para determinar as linhas da Table e os campos de input do Form

- <strong style="border-bottom: 2px solid orange">Funções:</strong>
    - <strong style="border-bottom: 1px solid orange">getProduct( ):</strong> Responsável por pegar todos os produtos do estoque no 'crudcrud' para atualizar a tabela. (ela preenche o array que coloca os itens na tabela)
   
    - <strong style="border-bottom: 1px solid orange">postProduct( ):</strong> Responsável por postar/adicionar os produtos no estoque, e depois chamar a função getProduct para atualizar a tabela.
    
    - <strong style="border-bottom: 1px solid orange">getSelectedProduct( ):</strong> Responsável por pegar o item selecionado (pelo click no botão 'select') e colocar suas informações no form para ser atualizado.
    
    - <strong style="border-bottom: 1px solid orange">updateProduct( ):</strong> Responsável por fazer a atualização de um item selecionado, e depois chamar a função getProduct para atualizar a tabela.
    
    - <strong style="border-bottom: 1px solid orange">deleteProduct( ):</strong> Responsável por deletar um determinado item (selecionado pelo click no botão 'delete'), e depois chamar a função getProduct para atualizar a tabela.

    - <strong style="border-bottom: 1px solid orange">clearFormInputs( ):</strong> Responsável por limpar os campos input do formulário quando se realiza alguma ação nele pelo botão submit.

- <strong style="border-bottom: 2px solid orange">Variáveis:</strong>
    - <strong style="border-bottom: 1px solid orange">formValues:</strong> Objeto que armazena os valores dos inputs do formulário, ele é enviado para o componente <strong>Form</strong> por props.
    
    - <strong style="border-bottom: 1px solid orange">idToUpdate:</strong> Armazena o código do id do produto que será atualizado, foi definido no 'data' do componente para não incluir o ID no formValues, foi uma solução para um possível conflito.

    - <strong style="border-bottom: 1px solid orange">actionForm:</strong> Define qual ação vai ser realizada quando se apertar o botão de submit no componente Form (Add Product ou Update Product).

    - <strong style="border-bottom: 1px solid orange">crudcrudURL:</strong> Simples, nessa variável fica o link do crudcrud que vai ser utilizada nas requests, quando precisar de alguma alteração faça aqui.

    - <strong style="border-bottom: 1px solid orange">arrayTableHead:</strong> É onde fica os dados da linha do cabeçalho da tabela, se quiser adicionar algum atributo ou excluir, é só mudar aqui.

    - <strong style="border-bottom: 1px solid orange">arrayTableBody:</strong> Esse array é passado por pros para o componente Table, é nele que fica armazeado os itens do estoque, sempre que ocorre alguma alteração no estoque ele é alterado e a tabela se atualiza. Diretamente ligado a função getProduct( ).

<br/>

### <strong style="border-bottom: 2px solid orange">Form.vue</strong>

- Componente onde se encontra o fomuláro, responsável pela emissão das suas ações (add e update).

- <strong style="border-bottom: 2px solid orange">Função:</strong>

    - <strong style="border-bottom: 1px solid orange">sendFormAction( ):</strong> Responsável por enviar um evento que determina a REQUEST que será realizada (POST ou PUT) para o componente App.vue

- <strong style="border-bottom: 2px solid orange">Props:</strong>

    - <strong style="border-bottom: 1px solid orange">propsForms:</strong> É a variável objeto enviada pelo componente App.vue para preencher os inputs do formulário, inicialmente vem com os atributos do objeto vazios, e se altera conforme a necessidade: 
        - quando se digita algo nos iputs ele se altera
        - quando se seleciona um item pelo botao 'select' ele se altera.

### <strong style="border-bottom: 2px solid orange">Table.vue</strong>

- Componente onde se encontra a tabela, ele se atualiza conforme o estoque se modifica.

- <strong style="border-bottom: 2px solid orange">Data:</strong>

    - <strong style="border-bottom: 1px solid orange">tableHeadDatas:</strong> Array que contém os atributos da tabela, é utilizado para definir o seu cabeçalho, o conteúdo pode ser modificado que o cabeçalho irá mudar junto.
        - obs: caso vá mudar o número de atributos no cabeçalho, vá no style do componente e mude a divisão do width em 'thead tr th' e 'tbody tr td'

- <strong style="border-bottom: 2px solid orange">Props:</strong>

    - <strong style="border-bottom: 1px solid orange">tableBodyDatas:</strong> Array que contém todos os itens do estoque, ele é atualizado e enviado por props do componente App.vue sempre que a função getProduct( ) é executada. É responsável por colocar os itens do estoque na tabela, por meio de sua manipulação.

<hr/>
