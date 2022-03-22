# array-plugin-construct2
Adicionei uma nova condição através do js dentro prototype js no plugin array da Scirra para a engine construct2.

Condição adicionada ao plugin:
- (ContainsConvertLowercase):

Oque faz: busca (elemento a elemento) na array convertendo cada elemento em minúsculo para verificar se o valor existe.
Desta forma não importa a composição do valor do elemento na array, sempre retornará o valor em minúsculo facilitando expressões e comparações.

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
