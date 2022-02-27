# PHPTest

## Como funciona
Este pacote serve para gerar teste a partir de comentários no código.
Uma alternativa mais simplista ao PHPUnit.

A idéia é diminuir o trabalho por trás da tarefa massante que é criar testes.

## Como usar

Você pode clonar o repositorio ou então instalar utilizando o composer:

```bash
composer require albreis/phptest
```

Para utilizar está suite de teste basta utilizar o padrão:

@test return [codigo php para executar]

O valor retornado precisa ser true ou false

Veja abaixo algums exemplos de utilização da ferramenta

### Exemplo 1

```php
<?php namespace Albreis;

class Calculadora {
    /**
     * @test return (new Albreis\Calculadora)->soma(1, 2) == 3
     * @test return (new Albreis\Calculadora)->soma(1, 2) == 4
     */
    public function soma($num1, $num2) {
        return ($num1 + $num2);
    }
}
```

Salve o arquivo acima em uma pasta e rode o comando abaixo, indicando a pasta onde existem os arquivos para teste

```bash
php vendor/bin/phptest {diretorio}
```

ou

```bash
php vendor/albreis/test/phptest {diretorio}
```

### Exemplo 2

```php
<?php namespace Albreis;

class Anime {
    /**
     * @test return isset(json_decode((new Albreis\Anime)->getRandom())->anime)
     * @test return !isset(json_decode((new Albreis\Anime)->getRandom())->anime)
     */
    public function getRandom() {
        return file_get_contents('https://animechan.vercel.app/api/random');
    }
}
```

```bash
php vendor/albreis/test/phptest {diretorio}
```

### Escrevendo testes em arquivos externos

Quando o teste for muito complexo é precisa de várias linhas o ideal é escrever em um arquivo externo.

Basta utilizar o padrão: @test_using [caminho relativo do arquivo externo]

Arquivo de teste: SomaTest.php
```php
<?php 
return (new Albreis\Soma)->soma(2, 3) == 5;
```

Classe para testar:

```php
<?php namespace Albreis;

class Soma {
    /**
     * @test return (new Albreis\Soma)->soma(9,9) == 89
     * @test_using SomaTest.php
     */
    public function soma($num1, $num2) {
        return ($num1 + $num2);
    }
}
```

### Testando um bloco de código
```php
/**
 * @test return ($num1 + $num2) == 4
 */
$num1 = 1;
$num2 = 3;
```

Retornará:
```bash
File: /home/public_html/bin/examples/tests.php
Line: 4
Test: return ($num1 + $num2) == 4
Return: bool(true)
Status: Success

Congratulations! All tests are passed.
```

### Testando uma função
```php
/**
 * @test return soma(1, 1) == 2
 */
function soma($n, $n2) {
    return ($n + $n2);
}
```

Retornará:
```bash
File: /home/public_html/bin/examples/tests.php
Line: 10
Test: return soma(1, 1) ==2
Return: bool(true)
Status: Success

Congratulations! All tests are passed.
```


### **Finalizado!**
Todos os testes serão executados