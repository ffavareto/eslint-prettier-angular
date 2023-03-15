# ESLint - Angular

<aside>
🗣 O que nós programadores fazemos: escrevemos letrinhas coloridas em algum editor de código.

</aside>

É cotidiano trabalhar em um mesmo projeto com mais pessoas, ou seja, mais de um jeito de programar em um mesmo projeto, alguns usam ; outros não, alguns usam espaço aqui ou ali e outros não, o que acaba gerando uma falta de padrão na escrita do código, como no exemplo abaixo:

```jsx
function multiplicarPorDez(numero){
  return numero*10
}
```

```jsx
function multiplicarPorDez(numero) {
  return numero * 10;
}
```

A diferença entre um código e outra não é tão grande, ambos funcionam, mas ver essas diferenças em um mesmo projeto não fica lega, e é sempre bom lembrar que devemos cuidar do código com muito carinho, nem sempre é possível no meio da correria, mas sempre que puder melhorar é ótimo, e o que será apresentado aqui não vai custar quase nada de esforço e deixará seu código e dos seus colegas de trabalho bem mais padronizado, por mais que cada um tenha suas particularidades na hora de escrever as letrinhas coloridas na tela.

---

Você já deve ter ouvido falar bem do ESLint ou do Prettier, mas assim como eu, embora sabendo dos benefícios sempre teve preguiça de configura-los em seus projetos, o foco aqui é Angular, mas o ESLint + Prettier pode ser usado em vários cenários, e é bem fácil de faze-lo.

> A ideia é que você escreva o código do jeito que quiser, mas assim que você executar o famoso **ctrl + s** o código “magicamente” será formatado de um jeito bonito e organizado em questão de espaçamentos, quebrar de linha, linhas em branco, ponto e vírgula…
> 

---

Após ter seu projeto criado, execute os seguintes comandos abaixo em ordem:

- `npm install --save-dev eslint`
- `npm install --save-dev @typescript-eslint/eslint-plugin eslint-plugin-prettier`
- `npm install --save-dev prettier prettier-eslint eslint-config-prettier`

---

Feito isso, crie um arquivo `.eslintrc.json` na raiz do projeto e insira o seguinte:

```json
{
  "parser": "@typescript-eslint/parser", // Especifica o analisador ESLint
  "extends": ["prettier", "plugin:prettier/recommended"],
  "parserOptions": {
    "ecmaVersion": 2020, // Permite a análise de recursos ECMAScript modernos
    "sourceType": "module" // Permite o uso de importações
  },
  "rules": {
    // Local para especificar regras ESLint.
		// Pode ser usado para substituir regras especificadas nas configurações estendidas.
		// Com o tempo e pesquisando você aprende a colocar regras aqui
  }
}
```

Uma boa ideia é ignorar alguns arquivos, algo parecido com o `.gitignore`, mas nesse caso os arquivos ignorados não sofrerão formatações causadas pelas configurações que estamos fazendo, para isso crie na raiz do projeto o arquivo `.eslintignore` e coloque o seguinte:

```json
package.json
package-lock.json
dist
```

---

O próximo passo é mexer no `package.json`, dentro de scripts você deve criar o comando `lint`, então o seu scripts ficará parecido com o abaixo:

```json
"scripts": {
    "ng": "ng",
    "start": "ng serve",
    "build": "ng build",
    "watch": "ng build --watch --configuration development",
    "test": "ng test",
    **"lint": "tsc --noEmit && eslint . --ext js,ts,json --quiet --fix"**
  },
```

---

Agora, também na raiz do projeto crie o arquivo `.prettierrc.json` e adicione o seguinte:

```json
{
    "singleQuote": true,
    "trailingComma": "none",
    "endOfLine": "auto"
}
```

E nesse arquivo ai é onde você pode definir as regras que quiser, para saber o que pode ser feito ai e ter mais ideias [veja a documentação](https://prettier.io/docs/en/configuration.html).

Outro exemplo de configuração bacana é o seguinte:

```json
{
    "singleQuote": true,
    "trailingComma": "none",
    "endOfLine": "auto",
    "tabWidth": 4,
    "printWidth": 100
}
```

---

No Visual Studio Code é possível instalar extensões que nos ajudam muito na produtividade e em outros aspectos, e existem duas extensões que você deve instalar para essa ideia do ESLint e Prettier funcionar corretamente, são as seguintes:

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
- [Prettier - Code formatter](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

---

Por fim, entre no arquivo JSON das configurações do seu Visual Studio Code e adicione o seguinte:

```json
"[javascript]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint",
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    "editor.formatOnSave": false
  },
  "[typescript]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint",
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    "editor.formatOnSave": false
  },
  "[json]": {
    "editor.defaultFormatter": "dbaeumer.vscode-eslint",
    "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
    },
    "editor.formatOnSave": false
  }
```

---

E caso você tenha feito tudo isso em um projeto que já existe, execute o comando `npm run lint`, se der algum erro pesquise sobre (com isso nós já estamos acostumados 😂), esse comando vai formatar todos os arquivos de acordo com as regras estabelecidas no arquivo `.prettierrc.json`, por isso é ali que você define o que quer e é esse arquivo que deve ser igual entre você e seus colegas do projeto, pois todos terão o mesmo padrão de código.

---

[Using ESLint and Prettier with VScode in an Angular Project 🚀(outdated)](https://dev.to/dreiv/using-eslint-and-prettier-with-vscode-in-an-angular-project-42ib)

[Configuration File · Prettier](https://prettier.io/docs/en/configuration.html)