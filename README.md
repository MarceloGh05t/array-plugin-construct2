# array-plugin-construct2
Adicionei uma nova condição através do js dentro prototype js no plugin array da Scirra para a engine construct 2.

(Atualização do plugin com a condição: "Contains value column y" e a expressão:  "Index Y of".)

Condição adicionada ao plugin:
- (ContainsConvertLowercase):

O que faz: busca (elemento a elemento) na array convertendo cada elemento em minúsculo para verificar se o valor existe.
Desta forma não importa a composição do valor do elemento na array, sempre retornará o valor em minúsculo facilitando expressões e comparações.

Exemplo: quero localizar a palavra valor. Vai localizar mesmo que a palavra estiver escrita na array, como: Valor, vAlor, vaLor, valOr, VAlor, etc...

Código usado no runtime:
```
Cnds.prototype.ContainsConvertLowercase = function(val)
	{
		var x, y, z;
	  	
		for (x = 0; x < this.cx; x++)
		{
			for (y = 0; y < this.cy; y++)
			{
				for (z = 0; z < this.cz; z++)
				{
						
					if (this.arr[x][y][z].toString().toLowerCase() === val)
						return true;
				}
			}
		}
		
		return false;
	};
  ```
========================

Atualização do plugin com a condição: "Contains value column y" e a expressão:  "Index Y of".

Condição adicionada ao plugin:

- Contains value column y (ContainsColumnY):

O que faz: Vai procurar na coluna y declarada, pelo valor declarado como parâmetro para a busca somente naquela coluna y. O valor procurado tem que ser no mesmo tipo do declarado, se for string (texto) vai procurar pelo valor no tipo de string, se for numero vai procurar o valor como numero.

Exemplo: Tenho uma array com 3 colunas y e quero procurar pelo valor "teste" na coluna Y informada.
  
Código usado no runtime:
```  
		Cnds.prototype.ContainsColumnY = function(y,val)
	{
		if(y < this.cy && y >= 0){ //A condição irá verificar se o Y colocado é menor, que a quantidade de elemento no eixo y, pois o índice começa com zero, e se o número for maior, que zero para não colocar um valor negativo.
		var x, z;
		
		for (x = 0; x < this.cx; x++)
		{
			for (z = 0; z < this.cz; z++)
				{
					if (this.arr[x][y][z] === val) // comparação não converte os tipos para os 2 serem iguais, entao coloquei o valor no tipo de string (texto) ou número.
						return true;
				}
		}
		
		return false;
	} else {
	return false
	}
	};
``` 

Expressão adicionada ao plugin:

- Index Y of (IndexYOf):

O que faz: vai verificar todas as colunas y de uma linha x da array, se tem o valor declarado. O valor passsado já é convertido para string para não tem problemas de valores iguais, mas tipos diferentes e retonar o valor da coluna y, que em o valor infomado naquela linha x.

Exemplo: IndexYOf(1,"valor_teste") vai procurar pelo "valor_teste" em todas as colunas y co x infomado, que no caso foi a linha 1.

Código usado no runtime:
``` 
Exps.prototype.IndexYOf = function (ret,x,value)
	{
		if(x < this.cx && x >= 0){ //A condição irá verificar se o x colocado é menor, que a quantidade de elemento no eixo x, pois o índice começa com zero, e se o número for maior, que zero para não colocar um valor negativo.

		for (var i = 0; i < this.cy; i++)
		{
			if (this.arr[x][i][0].toString() === value.toString())
			{
				ret.set_int(i);
				return;
			}
		}
		}
		ret.set_int(-1);
	};

``` 
