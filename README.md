- [Optional Chaining](#optional-chaining)

# Optional Chaining
O operador de encadeamento opcional provê uma forma de simplificar o acesso a valores através de objetos conectados, quando é possível que uma referência ou função possa ser undefined ou null.

Por exemplo, considere um objeto obj que possui uma estrutura aninhada. Sem o encadeamento opcional, verificar proriedades profundamente aninhadas requer uma validação de referências intermediárias, algo como:

```javascript
let nestedProp = obj.first && obj.first.second;
```

O valor de obj.first é confirmadamente não-null (e não-undefined) antes de acessar o valor de obj.first.second. Isso previne o erro que ocorreria se você simplesmente acessasse obj.first.second diretamente sem testar obj.first.

Com o operador de encadeamento opcional (?.), entretanto, você não precisa explicitamente testar e aplicar curto-circuito baseado no estado de obj.first antes de tentar acessar obj.first.second:

```javascript
let nestedProp = obj.first?.second;
```

Ao utilizar o operador ?. ao invés de apenas ., o JavaScript sabe que deve implicitamente checar e ter certeza que obj.first não é null ou undefined antes de tentar acessar obj.first.second. Se obj.first é null ou undefined, a expressão automaticamente sofrerá curto-circuito, retornando undefined.

Isso é equivalente ao seguinte, exceto que a variável temporária, de fato, não é criada:

```javascript
let temp = obj.first;
let nestedProp = ((temp === null || temp === undefined) ? undefined : temp.second);
```

Outros exemplos:

Encadeamento opcional com chamadas de funções
```javascript
let result = someInterface.customMethod?.();
```

Lidando com callbacks opcionais ou manipuladores de eventos

```javascript
function doSomething(onContent, onError) {
  try {
   // ... faz algo com os dados
  }
  catch (err) {
    onError?.(err.message); // Nenhuma exceção se onError for undefined
  }
}
```

Encadeamento opcional com expressões
```javascript
let nestedProp = obj?.['prop' + 'Name'];
```

[Fonte - MDN Web Docs](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Optional_chaining "Fonte - MDN Web Docs")
