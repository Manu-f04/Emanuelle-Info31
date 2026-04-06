<?php


$arquivo =$_FILES ["arquivo"];

$nome = $arquivo["name"];
$tamanho = $arquivo["size"];
$tmp_name = $arquivo["tmp_name"];

$tamanhoMax = 2 * 1024 * 1024;

if($arquivo["error"] != 0) {
    echo "Erro ao enviar o arquivo.";
exit;
    }
 
    if ($tamanho > $tamanhoMax) {
        echo "O arquivo é muito grande. O tamanho máximo permitido é de 2MB.";
        exit;
    }

    $nomeUnico = time() . "_" . $nome;

    $destino = "upload/" . $nomeUnico;

    if (move_uploaded_file($tmp_name, $destino)) {
       
    $texto = "Arquivo " . $nomeUnico . " - Tamanho: " . $tamanho . " bytes\n";
    file_put_contents("registro.txt", $texto, FILE_APPEND);

    echo "Nome Original: " . $nome . "<br>";
    echo "Nome salvo: " . $nomeUnico . "<br>";
    echo "Arquivo enviado com sucesso!";

    echo "<a href='index.php'>voltar</a>";
    
    } else {
        echo "Erro ao enviar o arquivo .";

    }
    
