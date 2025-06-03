# VitrineProduto.PHP
Criação da pagina de vitrineproduto.php

<?php
include('segurancazero.php');
include('cabecalho.php');
include('conn.php');

if(!isset($_GET['id'])){
    header('Location: index.php');
    exit();
}
$id = $_GET['id'];
$sql = "SELECT * FROM tb_produtos WHERE id_produto = $id";
$result = mysqli_query($link,$sql);
$tbl = mysqli_fetch_array($result);
mysqli_close($link);
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
        <img src="imagens/<?=$tbl[6]?>" height="250">
        <span class="titulo"><?=$tbl[1]?></span>
        <span class="product-price">
            R$ <?=number_format($tbl[5], 2, ',', '.')?>
        </span>
        <form action="carrinho.php" method="post">
            <input type="hidden" name="id_produto" value="<?=$tbl[0]?>">
            <select name="quantidade">
                <option value="1">1</option>
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
            <input type="submit" value="Adicionar ao Carrinho">
        </form>
        <p>Descrição: <?=$tbl[2]?></p>
        <p>Caracteristicas: <?=$tbl[3]?></p>
        <p>Codigo de Barras: <?=$tbl[7]?></p>
    </div>

</body>
</html>
