# VitrineProduto.PHP
Criação da pagina de vitrineproduto.php

<?php
// Inclui arquivos de segurança, cabeçalho da página e conexão com o banco de dados //
include('segurancazero.php');
include('cabecalho.php');
include('conn.php');

// Verifica se o parâmetro 'id' foi passado via GET //
if(!isset($_GET['id'])){
    // Se não houver ID, redireciona para a página inicial //
    header('Location: index.php');
    exit();
}

// Captura o ID do produto //
$id = $_GET['id'];

// Consulta os dados do produto com base no ID //
$sql = "SELECT * FROM tb_produtos WHERE id_produto = $id";
$result = mysqli_query($link, $sql);
$tbl = mysqli_fetch_array($result); // Armazena os dados do produto //

// Fecha a conexão com o banco //
mysqli_close($link);

// Se o produto não for encontrado, redireciona para a página inicial //
if(!$tbl){
    header('Location: index.php');
    exit();
}
?>

<!DOCTYPE html>
<html lang="pt-br">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="lista.css">
    <title>Minhas Aventuras</title>
</head>
<body>
    <div>
        <!-- Imagem do produto -->
        <img src="imagens/<?=$tbl[6]?>" height="250">
        <h1>Detalhes do Produto</h1>
        <!-- Exibe o título do produto, preço e formulário para adicionar ao carrinho -->
        <span class="titulo"><?=$tbl[1]?></span>
        <br>
        <span class="product-price">
        R$ <?=number_format($tbl[5], 2, ',', '.')?>
        </span>
        <br><br>
        <!-- Formulário para adicionar o produto ao carrinho -->
        <form action="carrinho.php" method="post">
            <input type="hidden" name="id_produto" value="<?=$tbl[0]?>">
            <select name="quantidade">
                <option value="1">1</option> <!-- Opções de quantidade de produtos -->
                <option value="2">2</option>
                <option value="3">3</option>
                <option value="4">4</option>
                <option value="5">5</option>
                <option value="6">6</option>
                <option value="7">7</option>
                <option value="8">8</option>
                <option value="9">9</option>
                <option value="10">10</option>
            </select>
            <br>
            <a href="index.php">
                <input type="button" value="Voltar">
            </a>
            <input type="submit" value="Adicionar ao Carrinho"> <!-- Botão para adicionar ao carrinho -->
        </form>
        <p>Descrição: <?=$tbl[2]?></p> <!-- Exibe a descrição do produto -->
        <p>Caracteristicas: <?=$tbl[3]?></p> <!-- Exibe as características do produto -->
        <p>Codigo de Barras: <?=$tbl[7]?></p> <!-- Exibe o código de barras do produto -->
    </div>

</body>
</html>
