# array-plugin-construct2
Adicionei uma nova condição através do js dentro prototype js no plugin array da Scirra para a engine construct 2.

(Atualização do plugin com a condição: "Contains value column y" e a expressão:  "Index Y of".)

Condição adicionada ao plugin:
- (ContainsConvertLowercase):

Oque faz: busca (elemento a elemento) na array convertendo cada elemento em minúsculo para verificar se o valor existe.
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
Atualização do plugin com a condição: "Contains value column y" e a expressão:  "Index Y of".

Condição adicionada ao plugin:
- (ContainsColumnY):

Oque faz: Vai procurar na coluna y declarada, pelo valor declarado como parâmetro para a busca somente naquela coluna y. O valor procurado não tem que ser no mesmo tipo, se for string (texto) vai procurar pelo valor no tipo de string, se for numero vai procurar o valor como numero.

Exemplo: Tenho uma array com 3 colunas y e quero procurar pelo valor "teste" na coluna Y informada.
  
Código usado no runtime:
```  
		Cnds.prototype.ContainsColumnY = function(y,val)
	{
		if(y < this.cy && y >= 0){ //A condição irá verificar se o Y colocado é menor que a quantidade de elemento no eixo y, pois o índice começa com zero, e se o número for maior que zero para não colocar um valor negativo.
		var x, z;
		
		for (x = 0; x < this.cx; x++)
		{
			for (z = 0; z < this.cz; z++)
				{
					if (this.arr[x][y][z] === val) // comparação nao converte os tipos para os 2 serem iguais, entao coloquei o valor no tipo de string (texto) ou número.
						return true;
				}
		}
		
		return false;
	} else {
	return false
	}
	};
``` 
