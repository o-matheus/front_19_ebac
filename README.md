# Módulo 19 - Boas práticas CSS

## **Exercício – Módulo 19: Boas Práticas no CSS**

Este exercício teve como objetivo aplicar a metodologia **BEM (Block, Element, Modifier)** em um projeto fornecido pela EBAC, reorganizando o HTML e os estilos CSS conforme as boas práticas abordadas ao longo do módulo.

---

### **Objetivos do exercício**

* Atualizar as classes do HTML com base na nomenclatura BEM.
* Refatorar o CSS (ou SCSS) utilizando blocos, elementos e modificadores.
* Aplicar as boas práticas de organização de código usando CSS puro ou pré-processador.
* Entregar o exercício através do GitHub, na branch `boas-praticas`, incluindo os arquivos `.scss` e `.css` se for usado pré-processador.

---

### **Configuração inicial do projeto**

* O projeto **não foi criado com o comando `npm init -y`**, pois o nome da pasta estava fora dos padrões exigidos pelo Node. Por isso, foi necessário rodar `npm init` e preencher manualmente cada um dos campos solicitados no terminal.

* A instalação do SASS foi feita com:

  ```bash
  npm install --save-dev sass
  ```

  > 🔎 **Explicação da diferença**:

  * `--save-dev`: adiciona o pacote como **dependência de desenvolvimento**, ou seja, só será necessária enquanto o projeto estiver sendo desenvolvido (ex.: pré-processadores, ferramentas de build, testes).
  * `--save` (ou sem nada): adiciona o pacote como **dependência de produção**, necessária para o funcionamento final do projeto.
  * Como o SASS é usado **apenas durante o desenvolvimento**, o uso de `--save-dev` está **correto e recomendado**.

* Também foi criado um `.gitignore` com `node_modules/` para evitar o envio dessa pasta para o repositório.

* A branch do exercício foi criada com:

  ```bash
  git checkout -b "boas-praticas"
  ```

---

### **Refatoração do HTML com BEM**

* O HTML original usava classes como `produto-imagem`, `produto-nome` e `em-destaque`, que **não estavam de acordo com a nomenclatura BEM**.

* As classes foram atualizadas para:

  * `.produto__imagem`
  * `.produto__nome`
  * `.produto__descricao`

* A classe de modificação `em-destaque` foi substituída pela classe **modificadora BEM**:

  * `.produto--em-destaque`

---

### **Refatoração do CSS com SASS**

* O CSS foi convertido para **SASS (SCSS)**, utilizando aninhamento com `&` para evitar repetição e melhorar a organização do código.

  ```scss
  .produto {
    &__imagem {
      width: 100%;
    }

    &__nome {
      font-size: 1.2em;
      margin: 8px 0;
    }

    &__descricao {
      color: gray;
    }

    &--em-destaque {
      border: 2px solid gold;
      padding: 8px;
      background-color: #ffff42;
    }
  }
  ```

* O container `.produtos` (plural) foi mantido para estruturar os cards com Grid Layout.

---

### **Compilação do SCSS para CSS**

* A compilação foi feita com o seguinte comando no terminal:

  ```bash
  npm run sass ./exercicio/bem/main.scss ./exercicio/bem/main.css
  ```

* Como o projeto é simples, **não foi criado um script de `watch` automatizado**. A compilação foi feita manualmente ao final.

---

### **Conclusão**

O exercício demonstrou como adaptar um código já existente para seguir a metodologia BEM, melhorando a clareza, a escalabilidade e a organização do projeto. Também reforçou as vantagens práticas do uso de pré-processadores como o SASS, especialmente em conjunto com boas práticas de nomenclatura e estruturação de estilos.