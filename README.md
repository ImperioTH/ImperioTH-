<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Império TH - Loja de Pratas</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #000;
            color: #fff;
        }
        header {
            background-color: #222;
            padding: 20px;
            text-align: center;
        }
        header h1 {
            color: #c0c0c0;
            font-size: 2rem;
            margin: 0;
        }
        header p {
            text-align: center;
            margin: 0;
            padding: 5px;
        }
        nav {
            background-color: #333;
            text-align: center;
            padding: 10px;
        }
        nav a {
            color: #c0c0c0;
            margin: 0 15px;
            text-decoration: none;
            font-size: 1.2rem;
        }
        .container {
            padding: 20px;
            text-align: center;
        }
        .product-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }
        .product {
            border: 1px solid #555;
            margin: 10px;
            padding: 15px;
            width: 100%; /* Tornando os produtos 100% do espaço disponível */
            max-width: 300px; /* Limite de largura para desktop */
            border-radius: 10px;
            background-color: #111;
            box-sizing: border-box;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .product img {
            width: 100%;
            border-radius: 10px;
        }
        .btn {
            margin-top: 10px;
            padding: 10px;
            background-color: #555;
            color: #fff;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .btn:hover {
            background-color: #777;
        }
        #carrinho-container {
            margin-top: 30px;
            padding: 20px;
            background-color: #222;
            border-radius: 10px;
            text-align: left;
        }
        #carrinho-container ul {
            list-style: none;
            padding: 0;
        }
        #carrinho-container li {
            margin: 10px 0;
            padding: 10px;
            background-color: #111;
            border-radius: 5px;
        }
        .btn-finalizar, .btn-limpar {
            margin-top: 10px;
            padding: 10px;
            background-color: #c00;
            color: #fff;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        .btn-finalizar:hover, .btn-limpar:hover {
            background-color: #f33;
        }
        #total-carrinho {
            margin-top: 10px;
            font-size: 1.2rem;
        }

        /* Responsivo: Para telas menores (celulares) */
        @media (max-width: 768px) {
            header h1 {
                font-size: 1.5rem;
            }
            nav a {
                display: block;
                margin: 10px 0;
                font-size: 1rem;
            }
            .container {
                padding: 10px;
            }
            .product-container {
                justify-content: space-evenly;
            }
            .product {
                width: 100%; /* Garante que os produtos ocupem toda a largura disponível em telas menores */
                max-width: 90%; /* Limita o tamanho para não ficar gigantesco */
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Bem-vindo ao Império TH</h1>
        <p>A prata que fala por você!</p>
    </header>
    <nav>
        <a href="#">Home</a>
        <a href="#">Produtos</a>
        <a href="#">Contato</a>
    </nav>
    <div class="container">
        <h2>Promoções Especiais</h2>
        <!-- Produtos -->
        <div class="product-container">
            <div class="product">
                <img src="https://via.placeholder.com/200" alt="Produto 1">
                <h3>Corrente Prata 925</h3>
                <p>R$ 149,90</p>
                <button class="btn" onclick="adicionarAoCarrinho('Corrente Prata 925', 149.90)">Adicionar ao Carrinho</button>
            </div>
            <div class="product">
                <img src="https://via.placeholder.com/200" alt="Produto 2">
                <h3>Anel Prata Masculino</h3>
                <p>R$ 89,90</p>
                <button class="btn" onclick="adicionarAoCarrinho('Anel Prata Masculino', 89.90)">Adicionar ao Carrinho</button>
            </div>
            <div class="product">
                <img src="https://via.placeholder.com/200" alt="Produto 3">
                <h3>Pulseira Prata 925</h3>
                <p>R$ 129,90</p>
                <button class="btn" onclick="adicionarAoCarrinho('Pulseira Prata 925', 129.90)">Adicionar ao Carrinho</button>
            </div>
        </div>
    </div>

    <!-- Carrinho -->
    <div id="carrinho-container" class="container">
        <h2>Seu Carrinho</h2>
        <ul id="carrinho-itens"></ul>
        <p id="total-carrinho">Total: R$ 0,00</p>
        <button class="btn-finalizar" onclick="finalizarCompra()">Finalizar Compra</button>
        <button class="btn-limpar" onclick="limparCarrinho()">Limpar Carrinho</button>
    </div>

    <!-- Script do Carrinho -->
    <script>
        let carrinho = [];

        function adicionarAoCarrinho(nome, preco) {
            const produto = { nome, preco };
            carrinho.push(produto);
            atualizarCarrinho();
            alert(`${nome} foi adicionado ao carrinho!`);
        }

        function atualizarCarrinho() {
            const carrinhoItens = document.getElementById('carrinho-itens');
            const totalCarrinho = document.getElementById('total-carrinho');
            carrinhoItens.innerHTML = '';
            let total = 0;

            carrinho.forEach((produto, index) => {
                carrinhoItens.innerHTML += `<li>${produto.nome} - R$ ${produto.preco.toFixed(2)} 
                <button onclick="removerDoCarrinho(${index})" style="margin-left: 10px; color: red;">Remover</button></li>`;
                total += produto.preco;
            });

            totalCarrinho.innerText = `Total: R$ ${total.toFixed(2)}`;
        }

        function removerDoCarrinho(index) {
            carrinho.splice(index, 1); // Remove o item pelo índice
            atualizarCarrinho();
        }

        function finalizarCompra() {
            if (carrinho.length > 0) {
                alert('Compra finalizada com sucesso!');
                carrinho = [];
                atualizarCarrinho();
            } else {
                alert('Seu carrinho está vazio!');
            }
        }

        function limparCarrinho() {
            carrinho = [];
            atualizarCarrinho();
        }
    </script>
</body>
</html>
