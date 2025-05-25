# Módulo 19 - Boas práticas CSS

## Menu
[Aula 1 - Determine regras CSS ](#aula-1---determine-regras-css)  
[Aula 2 - Aplique a metodologia SMACSS  ](#aula-2--aplique-a-metodologia-smacss)  
[Aula 3 - Aplique a metodologia BEM  ](#aula-3--aplique-a-metodologia-bem)  
[Aula 4 -  ](#aula-)  


## **Aula 1 – Determine regras de CSS**

### **Objetivos da aula**

* Compreender os três níveis de especificidade em CSS e como isso influencia na aplicação de estilos;
* Calcular a especificidade de seletores usando um modelo matemático;
* Aprender a escrever seletores eficientes e legíveis;
* Entender o papel do `!important` e seus impactos;
* Conhecer o comportamento do navegador ao interpretar seletores;
* Introdução ao uso de metodologias como BEM e SMACSS.

---

### **Especificidade no CSS**

#### 1. O que é especificidade?

Especificidade é um sistema de hierarquia usado pelo navegador para decidir qual regra CSS será aplicada quando várias regras conflitantes apontam para o mesmo elemento.

Os níveis mais comuns são:

| Tipo de seletor          | Valor de especificidade |
| ------------------------ | ----------------------- |
| Estilo inline            | `1000`                  |
| ID                       | `0100`                  |
| Classe, atributo, pseudo | `0010`                  |
| Tag, pseudoelemento      | `0001`                  |

Exemplo:

```css
h1 { color: blue; }         /* 0001 */
.title { color: red; }      /* 0010 */
#main-title { color: green; } /* 0100 */
```

O seletor com ID vencerá os outros, por ser mais específico.

---

### **Boa prática: evitar seletor excessivamente longo**

#### 2. Como o navegador lê os seletores

Embora escrevamos da esquerda para a direita, o navegador interpreta o seletor da **direita para a esquerda**.

Exemplo:

```css
footer.container ul li a { ... }
```

A leitura pelo navegador é:

1. Encontra todos os `a`;
2. Depois, os `li` que são pais desses `a`;
3. Depois, os `ul` que contêm os `li`;
4. Depois, `.container` que envolve os `ul`;
5. Por fim, `footer` que envolve tudo.

Por isso, **quanto mais longo o seletor, maior o custo de renderização** e mais difícil a manutenção do código.

---

### **Escrevendo seletores eficientes**

#### 3. Uso de classes específicas

Uma abordagem mais limpa e eficaz é **usar classes específicas diretamente no HTML**, evitando cadeias de seletores longas.

Exemplo ruim:

```css
footer.container ul li a { ... }
```

Exemplo recomendado:

```html
<a class="footer-link" href="#">Contato</a>
```

```css
.footer-link {
  color: #fff;
  text-decoration: none;
}
```

Vantagens:

* Aumenta a especificidade sem exageros (classe = `0010`);
* Melhora a legibilidade;
* Facilita a reutilização do estilo;
* Permite uma arquitetura CSS mais semântica e modular.

---

### **O uso do `!important`**

#### 4. Quando e por que evitar

O `!important` força uma regra a se sobrepor a qualquer outra, **quebrando a lógica da cascata** do CSS.

Exemplo:

```css
.button {
  background-color: blue !important;
}
```

Apesar de útil em casos extremos, seu uso constante **dificulta a manutenção** e a compreensão do código.

Recomenda-se:

* Usar `!important` apenas em exceções;
* Resolver conflitos com especificidade adequada;
* Evitar depender dele para sobrepor regras.

---

### **Ferramentas auxiliares**

#### 5. Calculando a especificidade

Uma ferramenta útil é o site:
🔗 [https://specificity.keegan.st](https://specificity.keegan.st)

Nele, você digita o seletor e visualiza:

* A pontuação de especificidade;
* A ordem de prioridade entre seletores;
* Como o navegador vai processar o CSS.

---

### **Resumo da aula**

* CSS possui uma hierarquia de aplicação baseada na **especificidade** dos seletores;
* A **eficiência dos seletores** afeta diretamente o desempenho e a clareza do código;
* O **uso de classes personalizadas** facilita a organização e escalabilidade do CSS;
* A leitura de seletores pelo navegador acontece da **direita para a esquerda**;
* O uso de `!important` deve ser controlado e reservado para situações específicas;
* Ferramentas online como o *specificity.keegan.st* ajudam a entender e planejar melhor os seletores.

Claro! Aqui está o **resumo final da Aula 2 – Aplique a metodologia SMACSS**, consolidado com todas as suas anotações:

---

## **Aula 2 – Aplique a metodologia SMACSS**

**Objetivos:**

* Compreender os princípios fundamentais da metodologia SMACSS e como ela pode ser aplicada para organizar o código CSS de forma mais eficiente e padronizada.
* Estruturar um projeto web usando a abordagem de categorização de estilos em Base, Layout, Module, State e Theme.
* Criar estilos modulares reutilizáveis e flexíveis usando as diretrizes do SMACSS.

---

### **Categorias do SMACSS**

O SMACSS propõe dividir o código CSS em 5 categorias principais:

1. **Base**:
   Usada para fazer o reset da página.
   Nessa seção, só são utilizadas tags HTML — sem IDs ou classes.

2. **Layout**:
   Responsável por organizar a estrutura da página (menu, barra lateral, conteúdo principal, etc).
   Quando usamos o símbolo `>` em seletores, indicamos que os elementos devem ser descendentes diretos, ou seja, as regras só se aplicam a essa hierarquia exata.

3. **Module**:
   Representa os componentes reutilizáveis da interface, como cards, blocos de conteúdo, botões etc.
   Um módulo deve manter sua aparência consistente em qualquer parte do layout.
   O professor destacou que é aqui onde passamos a maior parte do tempo aplicando o SMACSS.

   * É recomendado manter uma **padronização nos nomes das classes**.
     Exemplo:

     ```html
     <div class="mensagem">
       <h5 class="mensagem-titulo">...</h5>
       <p class="mensagem-conteudo">...</p>
     </div>
     ```

4. **State**:
   Define variações temporárias dos módulos.
   Exemplo: `mensagem is-erro`.
   Esse estado altera aspectos como cor ou borda, sem modificar a estrutura base do módulo.

5. **Theme**:
   Controla a aparência geral do site com base em temas.
   O professor mostrou os exemplos do site **G1** (tema vermelho) e **GE** (tema verde).
   Apesar das diferenças visuais, a estrutura do menu e das páginas é a mesma.
   Ele criou dois temas (tema A e tema B), aplicados diretamente ao `<body>`, mostrando como alterar a identidade visual sem mudar a estrutura do conteúdo.

---

### **Accordion com JavaScript puro**

O professor demonstrou como criar um componente **accordion** com JavaScript puro, controlando o estado visual com base em classes CSS.

1. **Estrutura HTML**:

   ```html
   <div class="accordion">
     <div class="accordion-header">Título</div>
     <div class="accordion-content">Conteúdo</div>
   </div>
   ```

2. **CSS**:

   ```css
   .accordion-content {
     display: none;
   }

   .accordion.is-open .accordion-content {
     display: block;
   }
   ```

3. **JavaScript**:

   ```javascript
   const accordions = document.querySelectorAll('.accordion-header');
   for (let i = 0; i < accordions.length; i++) {
     accordions[i].addEventListener('click', function (e) {
       e.target.parentNode.classList.toggle('is-open');
     });
   }
   ```

   * Utiliza `querySelectorAll` para selecionar todos os cabeçalhos (`.accordion-header`).
   * Um `for` percorre essa lista e adiciona o evento de clique a cada um.
   * Foi usada uma função tradicional no `addEventListener`.
   * O `toggle` alterna a classe `is-open` no elemento pai (`.accordion`), ativando ou escondendo o conteúdo com base no estado.
  * A linha `e.target.parentNode.classList.toggle('is-open')` foi utilizada na função de clique do accordion para alternar a exibição do conteúdo.
  A explicação detalhada é:

  * `e` representa o **evento de clique**.
  * `e.target` é o **elemento clicado** — no caso, o `.accordion-header`.
  * `e.target.parentNode` acessa o **elemento pai**, que é o `.accordion` (envolve o header e o conteúdo).
  * `classList.toggle('is-open')` **adiciona ou remove** a classe `is-open` no pai.

    * Se a classe estiver presente, ela é **removida**.
    * Se não estiver presente, ela é **adicionada**.

* Com isso, o accordion alterna entre **mostrar e ocultar o conteúdo** com base na presença ou ausência da classe `is-open`.

Sim, Matheus — esse já foi o conteúdo completo da aula, então agora segue o **resumo final da Aula 3 – Aplique a metodologia BEM**, consolidado e pronto para ser usado nos seus materiais:

---

## **Aula 3 – Aplique a metodologia BEM**

**Objetivos:**

* Conceituar a metodologia BEM (Block, Element, Modifier);
* Aplicar a metodologia BEM na prática;
* Assimilar as boas práticas de nomenclatura sugeridas pelo BEM.

---

### **O que é BEM?**

BEM é uma metodologia que busca organizar e nomear o CSS de forma clara, reutilizável e escalável, separando os estilos em:

* **Bloco (Block)**: o componente principal. Ex.: `.menu`, `.form`.
* **Elemento (Element)**: uma parte do bloco que depende dele para existir. Ex.: `.menu__link`, `.form__control`.
* **Modificador (Modifier)**: uma variação de aparência ou estado. Ex.: `.menu__link--active`, `.form__submit--sending`.

---

### **Exemplos práticos**

* No menu da EBAC, temos:

  * Bloco: `.menu`
  * Elemento: `.menu__link`
  * Modificador: `.menu__link--active`

* A convenção de nomenclatura:

  * Dois underlines `__` para elementos
  * Dois traços `--` para modificadores

Essa padronização melhora a clareza e evita conflitos, pois deixa evidente a hierarquia e o papel de cada classe.

---

### **Boas práticas e comparações**

* Comparado ao CSS tradicional (exemplo mostrado em aula), o BEM deixa o código:

  * Mais limpo;
  * Mais descritivo;
  * Mais fácil de manter;
  * Melhor preparado para projetos em equipe.

* O site [getbem.com](https://getbem.com) é recomendado para aprofundar os conceitos e exemplos.

* Uma das recomendações do BEM é **usar apenas seletores de classe**, evitando o uso de tags e IDs diretamente nos seletores CSS.

---

### **Uso com pré-processadores**

* Embora seja possível aplicar o BEM com CSS puro, ele **se encaixa melhor com pré-processadores como SASS ou LESS**, que permitem estruturar os estilos de forma mais enxuta e hierárquica.
* Na imagem mostrada, o código em BEM utiliza uma sintaxe típica de SASS (com `&` para elementos e modificadores dentro de blocos).

---

### **Exemplo prático (formulário)**

* O professor criou um pequeno formulário como exemplo:

  * Bloco: `.form`
  * Elementos: `.form__control`, `.form__submit`
  * Modificador: `.form__submit--sending`

  **HTML:**

  ```html
  <form class="form">
    <div class="form__control">
      <label for="nome">Seu nome:</label>
      <input id="nome" type="text" />
    </div>
    <button class="form__submit form__submit--sending" type="submit">Enviar</button>
  </form>
  ```

  **CSS:**

  ```css
  .form {
    margin: 40px;
  }

  .form__control {
    margin-bottom: 16px;
    font-family: sans-serif;
  }

  .form__submit {
    cursor: pointer;
  }

  .form__submit--sending {
    cursor: wait;
  }
  ```

* A repetição do nome do bloco nos elementos/modificadores ajuda a manter o código mais coeso e fácil de entender.
