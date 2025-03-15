# amigosecretomashanovo
Escolhi o nome Masha para homenagear uma pessoa que eu admiro.  Participar do desafio me fez pensar na amizade e nos "códigos" que cada relacionamento traz, e como vamos escrevendo esse código que trocamos e lemos, ao longo da vida, com as pessoas com quem a amizade acontece.
Foram várias tentativas de integrar o html com o javascript, colocar e recolocar arrays, onclick, math ramdom e muita pesquisa no ChatGpt e DeepSeek para conseguir algum resultado.
<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@100;400;700;900&family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&display=swap" rel="stylesheet">
    <title>Amigo Secreto</title>
</head>

<body>
    <main class="main-content">
        <header class="header-banner">
            <h1 class="main-title">Amigo Secreto</h1>
            <img src="assets/amigo-secreto.png" alt="Imagem representativa de amigo secreto">
        </header>
        
        <section class="input-section">
            <h2 class="section-title">Digite o nome dos seus amigos</h2> 
            <div class="input-wrapper">
                <input type="text" id="amigo" class="input-name" placeholder="Digite um nome">
                <button class="button-add" onclick="adicionarAmigo()">Adicionar</button>
            </div>
           
            <ul id="listaAmigos" class="name-list" aria-labelledby="listaAmigos" role="list">
                <!-- Lista de amigos vai aparecer aqui -->
            </ul>
            
            <ul id="resultado" class="result-list" aria-live="polite"></ul>
        
            <div class="button-container">
                <button class="button-draw" onclick="sortearAmigo()" aria-label="Sortear amigo secreto">
                    <img src="assets/play_circle_outline.png" alt="Ícone para sortear">
                    Sortear amigo
                </button>
            </div>
        </section>
    </main>

    <script>
        let amigos = []; // Array para armazenar os nomes dos amigos
        
        // Função para adicionar amigos à lista
        function adicionarAmigo() {
            const inputNome = document.getElementById('amigo');
            const nome = inputNome.value.trim();
            
            if (nome !== "") {
                amigos.push(nome);
                atualizarListaAmigos();
                inputNome.value = ""; // Limpar o campo de entrada
            }
        }
        
        // Função para atualizar a lista de amigos na interface
        function atualizarListaAmigos() {
            const listaAmigos = document.getElementById('listaAmigos');
            listaAmigos.innerHTML = ''; // Limpar lista antes de atualizar
            amigos.forEach(amigo => {
                const li = document.createElement('li');
                li.textContent = amigo;
                listaAmigos.appendChild(li);
            });
        }

        // Função para sortear amigos secretos
        function sortearAmigo() {
            if (amigos.length < 2) {
                alert("É necessário pelo menos 2 amigos para fazer o sorteio!");
                return;
            }
            
            let sorteio = [...amigos];
            let resultados = [];

            // Embaralhar a lista de amigos
            while (sorteio.length) {
                let sorteado = sorteio.splice(Math.floor(Math.random() * sorteio.length), 1)[0];
                let amigoSorteado = sorteio[Math.floor(Math.random() * sorteio.length)];
                resultados.push(`${sorteado} -> ${amigoSorteado}`);
            }

            exibirResultados(resultados);
        }

        // Função para exibir os resultados do sorteio
        function exibirResultados(resultados) {
            const listaResultado = document.getElementById('resultado');
            listaResultado.innerHTML = ''; // Limpar resultados anteriores
            resultados.forEach(resultado => {
                const li = document.createElement('li');
                li.textContent = resultado;
                listaResultado.appendChild(li);
            });
        }
    </script>
</body>
</html>
