# fokus_alura2

### Manipulando dados com o DOM

- **Capturando os dados da tela**
    
    ```jsx
    const taskListContainer = document.querySelector('app__section-task-list')
    ```
    

Para iniciarmos a nova versão do Fokus, criamos um arquivo JavaScript chamado `script-crud.js`, linkamos ele ao HTML e já começamos selecionando o elemento de lista `ul` do HTML identificado como `app__section-task-list`.

- **Criando tarefas estáticas**
    
    ```jsx
    const taskListContainer = document.querySelector('app__section-task-list');
    
    let tarefas = [
        {
            descricao: 'Tarefa Concluída',
            concluida: true
        },
        {
            descricao: 'Tarefa Pendente',
            concluida: false
        }
        
    ]
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </`
    ```
    

Dando prosseguimento ao código, criamos um `array` que será armazenado na variável de nome `tarefas`, esse array contém uma lista de dois `objetos` que possuem as propriedades de descrição e concluída, se observarmos o designer do projeto, existe um ícone de “conclusão de tarefa”, sabendo disso já importamos o `icon.svg` no JavaScript. 

- **Implementando uma função**
    
    ```jsx
    const taskListContainer = document.querySelector('app__section-task-list');
    
    let tarefas = [
        {
            descricao: 'Tarefa Concluída',
            concluida: true
        },
        {
            descricao: 'Tarefa Pendente',
            concluida: false
        }
        
    ]
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </`
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    ```
    

Nessa etapa, foi criada uma função chamada `createTask` que recebe como parametro `tarefa`, dentro dessa função criamos elementos como `li`, `icon` e `p` com `createElement`, passamos a ele um identificador classe com `class.list.add` e em exceção ao `icon` que ao invés de passarmos o `classList` passamos um `innerHTML` e buscamos a imagem `svg` que está guardada na variável `taskIconSvg`. Depois disso reunimos, esses elementos la no HTML, todos dentro do li com o `appenChild`.

- **Mostrando os dados na tela**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    let tarefas = [
        {
            descricao: 'Tarefa Concluída',
            concluida: true
        },
        {
            descricao: 'Tarefa Pendente',
            concluida: false
        }
        
    ]
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    ```
    

Nessa etapa, criamos uma `arrow function` também conhecida como função anônima, puxamos o `array tarefas` onde adicionamos dois objetos e passamos ao `array` um `forEach`, responsável por acessar o array e “viajar” sobre seus objetos, nessa `arrow function`, criamos uma variável com nome `taskItem`, que recebe a função `createTask` e passamos o `task` como parâmetro dessa função. E pra finalizar essa etapa, utilizamos o `appendChild` juntoamente com a variável `taskListContainer` que foi criada no inicio do código e adicionamos a elas o `taskItem`.

### Trabalhando com formulário

- **Adicionando um formulário**
    
    ```
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    let tarefas = [
        {
            descricao: 'Tarefa Concluída',
            concluida: true
        },
        {
            descricao: 'Tarefa Pendente',
            concluida: false
        }
        
    ]
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    ```
    

Para iniciarmos essa etapa do código, começamos com a criação das variáveis e nela armazenamos os elemento a de vindo do `HTML` através do método do `DOM` `querySelector`. Após isso criamos uma `arrow function` que será adicionada através de um evento de `click` implementado por meio do `addEventListener` e quando o evento `click` for executado no botão “Adicionar nova tarefa” que está armazenado na variável `toggleFormTaskBtn`, após a execução do evento `click`, temos mais tarefas a ser executada como o `textContent` contendo a frase “Adicionando tarefa” que será adicionado na variável `formLabel`, e também através do `classList` será adicionado uma class `“hidden”` na variável `formTask`, essa class já está pré-definida no `CSS` para esconder o formulário de modo que ele será exibido, apenas quando o evento de `click` for acionado.

- **Criando tarefas dinâmicas**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    let tarefas = [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    ```
    

> O método `preventDefault()` cancela o evento se for cancelável, o que significa que a ação padrão que pertence ao evento não ocorrerá.
> 

Nessa etapa do código, a missão é deixar o código dinâmico, e para isso utilizamos a variável `formTask` que será acompanhada do `addEventListener` com o evento submit, ou seja, com esse evento iremos receber informações do usuário, assim criaremos uma `arrow function` que terá como parâmetro o `evento` e dentro da `arrow function` iremos passar ao parâmetro `evento` o `preventDefault` tornando-o padrão e iremos recriar o `array` que foi criado acima, zerando o anterior, pois aqui nesse novo array, ao ivés de adicionarmos a informação, iremos receber a informação, deixando o código dinâmico. Dentro do `array` temo as propriedades `descrição` onde iremos receber o `textarea.value`, ou seja, o valor que será adicionado no formulario (a tarefa) e na propriedade `concluida` iremos atribuir o valor de `false`, pois não faz sentido adicionar uma tarefa que já foi concluída.

Seguindo o código, puxaremos o `array tarefas` e com o comando `push`, iremos adicionar o novo `array task` dentro do tarefas que já está vazio, logo após criaremos uma variável chamada `taskItem`, que recberá a função `createTask` juntamente com o parâmetro `task` e depois utilizamos o `appendChild`, adicionando o `taskItem` ao `taskListContainer`.

- **Limpando o form**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel')
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel')
    
    let tarefas = [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    const limparForm = () => {
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        limparForm()
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm)
    ```
    

Anteriormente resolvi o desafio de manipular o botão de cancelar, porém se observarmos a execução do `Fokus`, veremos que o `form` precisa de ter seu valor zerado, e é essa a missão dessa etapa, para isso criamos uma nova função com o nome `limparForm` e essa função passará um valor vazio para o `textarea` no qual recebe o valor do formulário e adicionamos uma `class` `“hiden”` por meio do `classList`, fazendo com que oculte o formulário e o texto. Com isso, agora basta chamar essa função dentro do `formTask` e do `btnCancelar`.

- **Conhecendo o localStorage**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel')
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel')
    
    let tarefas = [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    const limparForm = () => {
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        limparForm()
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    
    localStorage.setItem('quantidade', 10);
    console.log(localStorage.getItem('quantidade'))
    ```
    

> O `localStorage` é uma forma de armazenar dados diretamente no navegador.
> 

> `setItem` enviará uma informação externa para dentro do nosso `localStorage`. O `getItem` faz o fluxo oposto, enviando algo do `localStorage` para o nosso código
> 

Nessa etapa do código, nós começamos a interagir com o “banco de dados” do navegador, mais conhecido como `localStorage`, nele podemos armazenar informações localmente. Então, de inicio a gente chama o `localStorage` ao código e utilizamos o `setItem` para enviar informação para ser armazenada no `localStorage`, no `localStorage` também temos uma `variável`, porém nesse caso ela é conhecida como `key` demos o nome ao `key` de `“quantidade”` e a essa “variável” adicionamos o valor 10. Logo após, utilizamos o `console.log` para imprimir essa informação na ferramenta do desenvolvedor e dentro desse comando de impressão chamamos o `localStorage`, e com o `getItem` pegamos o `key` quantidade e apresentamamos ao `console.log` para ser imprimido no `console` do `DevTools`.

### Interagindo com o localStorage

- **Selecionando tarefas**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : []
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    const limparForm = () => {
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        updateLocalStorage();
        limparForm();
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    ```
    

> **`JSON.parse()`**método estático analisa uma string JSON, construindo o valor ou objeto JavaScript descrito pela string.
> 

> **`JSON.stringify()`**método estático converte um valor JavaScript em uma string JSON, substituindo opcionalmente valores se uma função substituta for especificada ou incluindo opcionalmente apenas as propriedades especificadas se uma matriz substituta for especificada.
> 

Dando inicio a alocação de tarefas ao “banco de dados” do navegador ou mais conhecido como `localStorage`, criamos uma variável chamada `localStorageTarefas` que receberá o `key` “tarefas” que será adicionado ao `localStorage`. Logo após, substituiremos um `array` vazio, por um operador ternário que Se `localStorageTarefas` possuir alguma tarefa o `JSON.parse` executara o seguinte comando:

> Pegará a tarefa que estará em forma de *string* no `LocalStorage`. Lembre-se, o `LocalStorage` só trabalha com *`strings`*, então ele pegará essa *`string`* e a transformará de volta para um `objeto` JavaScript.
> 

Se não tiver nada ocupando, ai sim passaremos um `array` vazio.

Fizemos toda a manipulação para receber a tarefa e guarda-la, agora partiremos para a criação da variável que irá inserir as tarefas ao `localStorage`. Chamamos a função de `updateLocalStorage` e aqui, passaremos ao `localStorage` o `setItem` que como já vimos ele é utilizado para enviar informações ao `localStorage` e com o `setItem` enviaremos a informação adicionada pelo usuário especificamente para o `key` “tarefas” e usaremos também o `JSON.stringify` que executará o seguinte comando:

> `JSON.stringify()` para transformar um objeto JavaScript em uma string.
> 
- **Selecionando tarefas**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : []
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        document.querySelectorAll('app__section-task-list-item').forEach(function (button) {
            button.classList.remove('app__section-task-list-item');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item')
    }
    
    const limparForm = () => {
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        updateLocalStorage();
        limparForm();
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    ```
    

Para iniciarmos essa etapa de seleção de tarefas, criaremos uma variável e chamaremos de `taskAtiveDescription`, ou seja, descrição da tarefa que está ativa e com o elemento do `DOM` `queryselector` buscaremos o elemento `HTML` identificado pela `class` `app__section-active-task-description`.

Seguindo com código inicializaremos duas variáveis que serão muito importante para essa etapa de seleção de tarefas, serão chamadas de `tarefaSelecionada` e `itemTarefaSelecionada` e terão como valor `null` de forma inicial.

Logo após, dentro da função `createTask`, criaremos uma `arrow function`, onde passaremos um evento de `onclick` ao `li` ou seja, quando o `item` de `lista (li)` for clicado a função `selecionaTarefa` será chamada e já terá como parâmetro `tarefa` e `li`.

- **Manipulando o ícone SVG**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path
            d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z"
            fill="#01080E" />
    </svg>
    `
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        document.querySelectorAll('.app__section-task-list-item-active').forEach(function (button) {
            button.classList.remove('app__section-task-list-item-active');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item-active')
    }
    
    const limparForm = () => {
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        const button = document.createElement('button')
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        svgIcon.addEventListener('click', (event) => {
            event.stopPropagation();
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        })
    
        if(tarefa.concluida) {
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        updateLocalStorage();
        limparForm();
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    ```
    

> O `stopPropagation()`método evita que a propagação do mesmo evento seja chamada.
> 

> O `setAttribute()`método define um novo valor para um atributo.
> 

Chegou a hora de marcarmos a tarefa como concluída e para isso, inicializamos uma variável nome `button` e nela adicionamos um `createElement`. Seguindo com o código, criamos uma função com `addEventListener` e o evento utilizado foi o de `click` na variável `svgIcon` que tem como parametro `event`, e dentro dessa função será executado o seguinte:

> Primeiro, declaramos que o evento criará um `stopPropagation`. Em seguida, criaremos uma nova classe para essa tarefa, quando ela for concluída. Esta classe ainda não existe no nosso HTML, será criada com o `classList.add`, e com nome`app__section-task-list-item-complete`.
> 

Agora, devemos criar uma condicional `if` para quando a tarefa for concluida `tarefa.concluida`, passaremos ao botão `button` um `setAttribute` e passaremos o valor `true` ao `‘disable’` e adicionaremos uma `class` chamada `app__section-task-list-item-complete` ao `li`, a mesma `class` que foi utilizada acima e já que utilizamos o `setAttribute` aqui, devemos subi-lo pra cima também.

### Atualizando tarefas

- **Integrando o botão de edição**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z" fill="#01080E" />
    </svg>
    `
    
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    let tarefaEmEdicao = null;
    let paragraphEmEdição = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        document.querySelectorAll('.app__section-task-list-item-active').forEach(function (button) {
            button.classList.remove('app__section-task-list-item-active');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item-active')
    }
    
    const limparForm = () => {
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    const selecionaTarefaParaEditar = () => {
        
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        const button = document.createElement('button');
    
        button.classList.add('app__button-edit');
        const editIcon = document.createElement('img');
        editIcon.setAttribute('src', '/imagens/edit.png')
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        svgIcon.addEventListener('click', (event) => {
            event.stopPropagation();
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        })
    
        if(tarefa.concluida) {
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
        li.appendChild(button);
        li.appendChild(editIcon);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        updateLocalStorage();
        limparForm();
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    ```
    

Novamente, de inicio inicializamos as variáveis que chamamos de `tarefaEmEdicao` e `paragraphEmEdicão` e demos um valor de `null` a elas. Logo após, criamos também uma função com nome de `selecionaTarefaParaEditar`, mas antes de adicionar códigos a essa função devemos implantar o botão que dará acesso ao editar e o botão será criado dentro da função `createTask`, adicionaremos na variável `button` uma `class` através do `classList.add` e daremos o nome de `app__button-edit`, para adicionar o ícone do botão editar criamos mais uma variável chamada `editIcon` e com o `createElement` adicionaremos um elemento de imagem, já temos o ícone salvo na pasta `./imagens` para adicionarmos ao código devemos passar um `setAttribute` com dois valor o primeiro `src` que buscará a imagem e o segundo valor o caminho da imagem.

- **Criando a função de edição**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z" fill="#01080E" />
    </svg>
    `
    
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    let tarefaEmEdicao = null;
    let paragraphEmEdicão = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        document.querySelectorAll('.app__section-task-list-item-active').forEach(function (button) {
            button.classList.remove('app__section-task-list-item-active');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item-active')
    }
    
    const limparForm = () => {
        tarefaEmEdicao = null;
        paragraphEmEdicão = null;
    
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    const selecionaTarefaParaEditar = (tarefa, elemento) => {
        if(tarefaEmEdicao == tarefa) {
            limparForm();
            return;
        }
    
        formLabel.textContent = 'Editando tarefa';
        tarefaEmEdicao = tarefa;
        paragraphEmEdicão = elemento;
        textarea.value = tarefa.descricao;
        formTask.classList.remove('hidden')
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        const button = document.createElement('button');
    
        button.classList.add('app_button-edit');
        const editIcon = document.createElement('img');
        editIcon.setAttribute('src', '/imagens/edit.png');
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        svgIcon.addEventListener('click', (event) => {
            event.stopPropagation();
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        })
    
        if(tarefa.concluida) {
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
        li.appendChild(button);
        li.appendChild(editIcon);
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
        updateLocalStorage();
        limparForm();
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    ```
    

Vamos a vante, já temos a função `selecionaTarefa` criada, agora precisamos adicionar códigos a ela, para que de fato ela execute a edição. Começamos passando dois `parâmetros` para a função que são a `tarefa` e o `elemento`, e dentro da função criamos uma `condicional if (se)`, então quando a `tarefaEmEdição` receber `tarefa` irá executar a função `limparForm`, que já foi criada, ou seja, ela limpará o formulário, para que seja editado e retornará em branco com o comando `return`.

Seguindo com o código da função, adicionaremos um texto ao `formLabel` “Editando tarefa” com o `textContent`, logo após a variável`tarefaEmEdicao` vai receber `tarefa`, `paragraphEmEdicao` vai receber `elemento`, o valor do `textarea` vai receber um novo valor e ao `formTask` removeremos a `class` `‘hidden’`, ou seja, não haverá ocultação.

- **Editando tarefas e salvando localmente**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z" fill="#01080E" />
    </svg>
    `
    
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    let tarefaEmEdicao = null;
    let paragraphEmEdicao = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        document.querySelectorAll('.app__section-task-list-item-active').forEach(function (button) {
            button.classList.remove('app__section-task-list-item-active');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item-active')
    }
    
    const limparForm = () => {
        tarefaEmEdicao = null;
        paragraphEmEdicao = null;
    
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    const selecionaTarefaParaEditar = (tarefa, elemento) => {
        if(tarefaEmEdicao == tarefa) {
            limparForm();
            return;
        }
    
        formLabel.textContent = 'Editando tarefa';
        tarefaEmEdicao = tarefa;
        paragraphEmEdicao = elemento;
        textarea.value = tarefa.descricao;
        formTask.classList.remove('hidden')
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        const button = document.createElement('button');
    
        button.classList.add('app_button-edit');
        const editIcon = document.createElement('img');
        editIcon.setAttribute('src', '/imagens/edit.png');
    
        button.appendChild(editIcon);
    
        // li.appendChild(editIcon);
    
        button.addEventListener('click', (event) => {
            event.stopPropagation();
            selecionaTarefaParaEditar(tarefa, paragraph);
        })
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        svgIcon.addEventListener('click', (event) => {
            event.stopPropagation();
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        })
    
        if(tarefa.concluida) {
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
        li.appendChild(button);
        
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        
        if(tarefaEmEdicao) {
            tarefaEmEdicao.descricao = textarea.value;
            paragraphEmEdicao.textContent = textarea.value;
        } else {
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
    }
        updateLocalStorage();
        limparForm();
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    ```
    

> O método`stopPropagation()`evita que a propagação do mesmo evento seja chamada.
> 

Se executarmos o projeto, perceberemos que o botão de editar ainda está inacessível. Nessa etapa, temos como missão integrar o botão de editar a sua função. Para isso, precisamos criar um evento de `click` com `addEventListener` ao `button` e quando clicado teremos como parâmetro o `event` e uma `arrow function,` dentro dessa `arrow function` teremos um `stopPropagation` juntamente ao `event` e passamos os parâmetros `tarefa` e `paragraph` para a função `selecionaTarefaParaEditar`.

Pra finalizar essa integração, fomos para o evento de `submit` localizado no `formTask` e adicionamos uma `condicional if`, `se` tarefa estiver em edição `(tarefaEmEdição = true)`, a descrição da `tarefaEmEdicao` receberá um novo valor, assim também o `paragraphEmEdicao` receberá um novo valor, e com o `else`, nesse caso `se não` estiver em edição o código percorrerá o mesmo caminho de antes.

<aside>
📌 **Para saber mais: desvendando o LocalStorage**

Agora que você já sabe que o localStorage é uma ferramenta importante para armazenar alguns dados localmente. Porém, como aprendemos até aqui, precisamos tomar alguns cuidados ao manipular os dados que vão para o localStorage ou que estão saindo dele. Como isso acontece? Para ilustrar esse conceito, vou utilizar um exemplo prático e explicar as etapas:

```jsx
// Dados de exemplo
let pessoa = {nome: 'João', idade: 23};

 // Armazena os dados no localStorage
localStorage.setItem('pessoa', JSON.stringify(pessoa));

// Recupera os dados do localStorage
let pessoaString = localStorage.getItem('pessoa');
let pessoaObjeto = JSON.parse(pessoaString);
COPIAR CÓDIGO
```

Ao considerar a importação de dados para o localStorage, o método `localStorage.setItem()` é empregado em conjunto com `JSON.stringify()`, que converte um objeto em uma string. Isso permite armazenar informações complexas em uma forma que o localStorage possa compreender:

```jsx
let pessoa = {nome: 'João', idade: 23};
localStorage.setItem('pessoa', JSON.stringify(pessoa)); // Transforma o objeto em string
COPIAR CÓDIGO
```

Por outro lado, para recuperar dados do localStorage e incorporá-los de volta em nossa página, usamos o método `.getItem()`. O processo inverso ao que ocorreu anteriormente é executado: a string armazenada é convertida de volta para um objeto por meio do `JSON.parse()`:

```jsx
let pessoaString = localStorage.getItem('pessoa'); // Obtém a string do localStorage
let pessoa = JSON.parse(pessoaString); // Transforma a string em objeto novamente
COPIAR CÓDIGO
```

Nesse exemplo, o objeto pessoa é convertido em uma string usando `JSON.stringify()` e armazenado no localStorage por meio do método `localStorage.setItem()`. Posteriormente, a string é recuperada do localStorage usando `localStorage.getItem()` e então é convertida de volta para um objeto usando `JSON.parse()`.

</aside>

### Removendo tarefas

- **Concluindo as tarefas**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z" fill="#01080E" />
    </svg>
    `
    
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    let tarefaEmEdicao = null;
    let paragraphEmEdicao = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        if(tarefa.concluida) {
            return
        }
    
        document.querySelectorAll('.app__section-task-list-item-active').forEach(function (button) {
            button.classList.remove('app__section-task-list-item-active');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item-active')
    }
    
    const limparForm = () => {
        tarefaEmEdicao = null;
        paragraphEmEdicao = null;
    
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    const selecionaTarefaParaEditar = (tarefa, elemento) => {
        if(tarefaEmEdicao == tarefa) {
            limparForm();
            return;
        }
    
        formLabel.textContent = 'Editando tarefa';
        tarefaEmEdicao = tarefa;
        paragraphEmEdicao = elemento;
        textarea.value = tarefa.descricao;
        formTask.classList.remove('hidden')
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        const button = document.createElement('button');
    
        button.classList.add('app_button-edit');
        const editIcon = document.createElement('img');
        editIcon.setAttribute('src', '/imagens/edit.png');
    
        button.appendChild(editIcon);
    
        // li.appendChild(editIcon);
    
        button.addEventListener('click', (event) => {
            event.stopPropagation();
            selecionaTarefaParaEditar(tarefa, paragraph);
        })
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        svgIcon.addEventListener('click', (event) => {
            if(tarefa == tarefaSelecionada) {
                event.stopPropagation();
                button.setAttribute('disabled', true);
                li.classList.add('app__section-task-list-item-complete');
                tarefaSelecionada.concluida = true;
                updateLocalStorage();
            }
            
        })
    
        if(tarefa.concluida) {
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
        li.appendChild(button);
        
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        
        if(tarefaEmEdicao) {
            tarefaEmEdicao.descricao = textarea.value;
            paragraphEmEdicao.textContent = textarea.value;
        } else {
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
    }
        updateLocalStorage();
        limparForm();
    })
    
    document.addEventListener('TarefaFinalizada', function (e) {
        if(tarefaSelecionada) {
            tarefaSelecionada.concluida = true;
            itemTarefaSelecionada.classList.add('app__section-task-list-item-complete');
            itemTarefaSelecionada.querySelector('button').setAttribute('disable', true);
        }
        updateLocalStorage()
    })
    ```
    

> Para isso, voltamos no VS Code e abrimos o arquivo `script.js`. Vamos diminuir o tempo de foco para conseguir fazer esses testes, certo?. Então, na variável `tempoDecorridoEmSegundos`, definimos o valor `3`. Depois, em `tempoDecorridoEmSegundos`, também definimos o valor `3`. Fazemos isso somente na função de foco.
> 
- Retornando ao `script-crud.js`

> No fim do código, começaremos a criar essa função que concluirá primeiro a parte de foco. Depois implementaremos essa funcionalidade no botão de check.
> 
> 
> Escrevemos `document.addEventListener()`. Como parâmetro, passamos entre aspas simples o evento que será executado `TarefaFinalizada`. Assim, quando a tarefa chegar ao fim do cronômetro será marcada como finalizada. Adicionamos vírgula seguido de uma `function ()`.
> 
> Na mesma linha abrimos chaves para criarmos a função. Dentro dela, passamos `if(tarefaSelecionada)` seguido de chaves. Dentro dessas chaves, passamos `tarefaSelecionada.concluida` que receberá `true`, ou seja, se foi concluída é verdadeira.
> 
> Na linha seguinte, dentro de `if()`, passamos `itemTarefaSelecionada.classList.add()`. Como parâmetro passaremos o mesmo `app` localizado acima, então subimos o código, copiamos e colamos.
> 
> Logo abaixo, passamos `itemTarefaSelecionada.querySelector()`. Como parâmetro e dentro de aspas simples, passamos `button`. Fora dos parênteses escrevemos `.setAttribute('disabled', true)`.
> 
> Por fim, passamos `update LocalStorage()`
> 

> Mas, repare que, mesmo com a Tarefa 1 concluída, conseguimos selecioná-la. Isso não deveria acontecer, pois se selecionamos ela aparece como "Em andamento". Então, antes de desenvolvermos a parte de concluir pelo SVGIcon, faremos essa correção no código.
> 
> 
> No arquivo `script-crud.js`, vamos até a função `selecionaTarefa`, na linha 34. Na linha abaixo, escrevemos `if(tarefa.concluida)`, na linha abaixo `return`. Dessa forma, se a tarefa estiver concluída, saímos das função e quebramos as linhas seguintes. Sendo assim, se a tarefa for concluída não será possível selecionar.
> 

> Na função `createTask()`. Queremos que se clicarmos no botão a tarefa seja considerada como concluída. Então,  em `svgIcon`, adicionamos uma nova linha dentro das chaves. Passamos `if(tarefa==tarefaSelecionada) {}`.
> 
> 
> > Sempre passaremos esse parâmetro da tarefa selecionada. Isso é importante porque, se marcarmos alguma tarefa errada e ela não estiver selecionada, ela não será concluída. É como um protocolo de segurança para a página.
> > 
> 
> Dentro das chaves, vamos criar o bloco de código, ou seja, copiaremos o que já está feito e colamos dentro do novo bloco. Em seguida, na linha abaixo, criamos o `tarefaSelecionada.concluida` igual à `true`.
> 
> Então, se a tarefa selecionada foi marcada no `svgIcon`, queremos que essa tarefa tenha o atributo `concluída` igual a verdadeiro. Por fim, passamos `updateLocalStorage`.
> 
- **Deletando as tarefas**
    
    ```jsx
    const taskListContainer = document.querySelector('.app__section-task-list');
    
    const formTask = document.querySelector('.app__form-add-task');
    const toggleFormTaskBtn = document.querySelector('.app__button--add-task');
    const formLabel = document.querySelector('.app__form-label');
    
    const textarea = document.querySelector('.app__form-textarea');
    
    const cancelFormBtn = document.querySelector('.app__form-footer__button--cancel');
    const btnCancelar = document.querySelector('.app__form-footer__button--cancel');
    
    const btnDeletar = document.querySelector('.app__form-footer__button--delete');
    
    const localStorageTarefas = localStorage.getItem('tarefas');
    
    const taskAtiveDescription = document.querySelector('.app__section-active-task-description');
    
    let tarefas = localStorageTarefas ? JSON.parse(localStorageTarefas) : [];
    
    const taskIconSvg =  `
    <svg class="app__section-task-icon-status" width="24" height="24" viewBox="0 0 24 24"
        fill="none" xmlns="http://www.w3.org/2000/svg">
        <circle cx="12" cy="12" r="12" fill="#FFF" />
        <path d="M9 16.1719L19.5938 5.57812L21 6.98438L9 18.9844L3.42188 13.4062L4.82812 12L9 16.1719Z" fill="#01080E" />
    </svg>
    `
    
    let tarefaSelecionada = null;
    let itemTarefaSelecionada = null;
    
    let tarefaEmEdicao = null;
    let paragraphEmEdicao = null;
    
    const selecionaTarefa = (tarefa, elemento) => {
        if(tarefa.concluida) {
            return
        }
    
        document.querySelectorAll('.app__section-task-list-item-active').forEach(function (button) {
            button.classList.remove('app__section-task-list-item-active');
        })
    
        if (tarefaSelecionada == tarefa) {
            taskAtiveDescription.textContent = null;
            itemTarefaSelecionada = null;
            tarefaSelecionada = null;
            return;
        }
    
        tarefaSelecionada = tarefa;
        itemTarefaSelecionada = elemento;
        taskAtiveDescription.textContent = tarefa.descricao;
        elemento.classList.add('app__section-task-list-item-active')
    }
    
    const limparForm = () => {
        tarefaEmEdicao = null;
        paragraphEmEdicao = null;
    
        textarea.value = '';
        formTask.classList.add('hidden');
    }
    
    const selecionaTarefaParaEditar = (tarefa, elemento) => {
        if(tarefaEmEdicao == tarefa) {
            limparForm();
            return;
        }
    
        formLabel.textContent = 'Editando tarefa';
        tarefaEmEdicao = tarefa;
        paragraphEmEdicao = elemento;
        textarea.value = tarefa.descricao;
        formTask.classList.remove('hidden')
    }
    
    function createTask(tarefa) {
        const li = document.createElement('li');
        li.classList.add('app__section-task-list-item');
    
        const svgIcon = document.createElement('svg');
        svgIcon.innerHTML = taskIconSvg;
    
        const paragraph = document.createElement('p');
        paragraph.classList.add('app__section-task-list-item-description');
    
        paragraph.textContent = tarefa.descricao;
    
        const button = document.createElement('button');
    
        button.classList.add('app_button-edit');
        const editIcon = document.createElement('img');
        editIcon.setAttribute('src', '/imagens/edit.png');
    
        button.appendChild(editIcon);
    
        // li.appendChild(editIcon);
    
        button.addEventListener('click', (event) => {
            event.stopPropagation();
            selecionaTarefaParaEditar(tarefa, paragraph);
        })
    
        li.onclick = () => {
            selecionaTarefa(tarefa, li);
        }
    
        svgIcon.addEventListener('click', (event) => {
            if(tarefa == tarefaSelecionada) {
                event.stopPropagation();
                button.setAttribute('disabled', true);
                li.classList.add('app__section-task-list-item-complete');
                tarefaSelecionada.concluida = true;
                updateLocalStorage();
            }
            
        })
    
        if(tarefa.concluida) {
            button.setAttribute('disabled', true);
            li.classList.add('app__section-task-list-item-complete');
        }
    
        li.appendChild(svgIcon);
        li.appendChild(paragraph);
        li.appendChild(button);
        
    
        return li
    }
    
    tarefas.forEach(task => {
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    })
    
    cancelFormBtn.addEventListener('click', () => {
        formTask.classList.add('hidden');
    })
    
    btnCancelar.addEventListener('click', limparForm);
    
    btnDeletar.addEventListener('click', () => {
        if(tarefaSelecionada) {
            const index = tarefas.indexOf(tarefaSelecionada);
    
            if(index != -1) {
                tarefas.splice(index, 1);
            }
    
            itemTarefaSelecionada.remove()
            tarefas.filter(t => t != tarefaSelecionada)
            itemTarefaSelecionada = null
            tarefaSelecionada = null
        }
    
        updateLocalStorage();
        limparForm();
    })
    
    toggleFormTaskBtn.addEventListener('click', () => {
        formLabel.textContent = 'Adicionando tarefa';
        formTask.classList.toggle('hidden');
    })
    
    const updateLocalStorage = () => {
        localStorage.setItem('tarefas', JSON.stringify(tarefas));
    }
    
    formTask.addEventListener('submit', (evento) => {
        evento.preventDefault();
        
        if(tarefaEmEdicao) {
            tarefaEmEdicao.descricao = textarea.value;
            paragraphEmEdicao.textContent = textarea.value;
        } else {
        const task = {
            descricao: textarea.value,
            concluida: false
        }
    
        tarefas.push(task);
        const taskItem = createTask(task);
        taskListContainer.appendChild(taskItem);
    
    }
        updateLocalStorage();
        limparForm();
    })
    
    document.addEventListener('TarefaFinalizada', function (e) {
        if(tarefaSelecionada) {
            tarefaSelecionada.concluida = true;
            itemTarefaSelecionada.classList.add('app__section-task-list-item-complete');
            itemTarefaSelecionada.querySelector('button').setAttribute('disable', true);
        }
        updateLocalStorage()
    })
    ```
    

> Começando pela construção da constante `btnDeletar` igual à `document.querySelector()`. Como parâmetro, passamos, dentro de aspas simples, `.app__form-footer__button--delete`.
> 

> Assim, capturamos no HTML o que será responsável pelo botão deletar. Para realizarmos a implementação, descemos o código até o `btnCancelar.addEventListener()`.
> 
> 
> Pulamos duas linhas. Começaremos a criar o evento de clique e o que acontecerá quando clicarmos no botão de deletar. Escrevemos `btnDeletar.addEventListener()`. Nos parênteses, entre aspas simples, passamos `click, () => {}`.
> 
> Nas chaves, definiremos que se a tarefa estiver selecionada, então `if(tarefaSelecionada)`. Adicionamos chaves, no bloco, passamos `const index = tarefas.indexOf()` que recebe como parâmetro `tarefaSelecionada`.
> 
> > Passamos o index, pois queremos encontrar a posição da tarefa dentro da lista de tarefas, para podermos removê-la corretamente sem causar nenhum erro no código.
> > 
> 
> Dentro desse `if()`, criaremos outro, nele passaremos `index !== -1`. Essa é uma confirmação, ou seja, se isso for verdadeiro, significa que existe uma tarefa selecionada.
> 
> Na linha abaixo, passamos `tarefas.splice(index, 1)`, assim, removeremos a tarefa do `index`.
> 

> Agora, fora do bloco `splice`, na linha 149, vamos continuar construindo a função deletar. Escrevemos `itemTarrefaSelecionada.remove()`.
> 
> 
> > Com esse remove, removeremos esse elemento que estava lidado a essa tarefa tanto do JavaScript como HTML.
> > 
> 
> Na linha baixo, passamos `tarefas.filter(t=> t!= tarefaSelecionada)`. Assim, criamos um novo *array* sem a tarefa que removemos. Portanto, é uma maneira reutilizarmos o *array* existente, a lista de tarefas que criamos no início do código.
> 
> Para finalizar, na linha abaixo, passamos o `itemTarefaSelecionada` igual à `null`, seguido de `tarefaSelecionada`, que também recebe `null`. Isso porque queremos um comportamento no qual, ao deletar algo, nenhuma tarefa seja selecionada automaticamente, ou seja, como se tivéssemos acabado de entrar na página.
> 
> Fora de todos os `ifs`, ainda dentro da nossa função `btnDeletar`, passamos o `updateLocalStorage()` para removermos essa tarefa. Abaixo, passamos o `limparForm()` para resetar o bloco do formulário.
>
