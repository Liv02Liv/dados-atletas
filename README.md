# 🏆 Projeto de Certificação 2 – Dados dos Atletas

Este projeto foi desenvolvido como parte da certificação do curso DEVstart.  
O objetivo é criar uma aplicação em **JavaScript** capaz de receber informações de um atleta, calcular e exibir **categoria**, **IMC** e **média válida** das notas.

---

## 📋 Funcionalidades

A aplicação permite:

- Cadastrar um atleta com:
  - Nome  
  - Idade  
  - Peso  
  - Altura  
  - Notas (array de números)
- Calcular automaticamente:
  - **Categoria** (com base na idade)
  - **IMC (Índice de Massa Corporal)**
  - **Média válida** (excluindo a menor e a maior nota)
- Exibir todas as informações no console.

---

## 🧠 Regras do sistema

### 🧩 Categorias
| Faixa etária | Categoria |
|---------------|------------|
| 9 a 11 anos   | Infantil   |
| 12 a 13 anos  | Juvenil    |
| 14 a 15 anos  | Intermediário |
| 16 a 30 anos  | Adulto     |
| Outras idades | Sem categoria |

### ⚖️ Cálculo do IMC
\[
IMC = \frac{peso}{(altura \times altura)}
\]

### 🧮 Cálculo da média válida
1. Ordenar as notas em ordem crescente;  
2. Remover a menor e a maior nota;  
3. Calcular a média das notas restantes.

---

## 💻 Código principal (`dados-atletas.js`)

```javascript
class Atleta {
  constructor(nome, idade, peso, altura, notas) {
    this.nome = nome;
    this.idade = idade;
    this.peso = peso;
    this.altura = altura;
    this.notas = notas;
  }

  calculaCategoria() {
    if (this.idade >= 9 && this.idade <= 11) return "Infantil";
    else if (this.idade >= 12 && this.idade <= 13) return "Juvenil";
    else if (this.idade >= 14 && this.idade <= 15) return "Intermediário";
    else if (this.idade >= 16 && this.idade <= 30) return "Adulto";
    else return "Sem categoria";
  }

  calculaIMC() {
    return this.peso / (this.altura * this.altura);
  }

  calculaMediaValida() {
    let notasOrdenadas = this.notas.sort((a, b) => a - b);
    let notasValidas = notasOrdenadas.slice(1, notasOrdenadas.length - 1);
    let soma = notasValidas.reduce((total, nota) => total + nota, 0);
    return soma / notasValidas.length;
  }

  obtemNomeAtleta() { return this.nome; }
  obtemIdadeAtleta() { return this.idade; }
  obtemPesoAtleta() { return this.peso; }
  obtemAlturaAtleta() { return this.altura; }
  obtemNotasAtleta() { return this.notas; }
  obtemCategoria() { return this.calculaCategoria(); }
  obtemIMC() { return this.calculaIMC(); }
  obtemMediaValida() { return this.calculaMediaValida(); }
}

// Exemplo de uso
const atleta = new Atleta("Cesar Abascal", 30, 80, 1.70, [10, 9.34, 8.42, 10, 7.88]);

console.log(`Nome: ${atleta.obtemNomeAtleta()}`);
console.log(`Idade: ${atleta.obtemIdadeAtleta()}`);
console.log(`Peso: ${atleta.obtemPesoAtleta()}`);
console.log(`Altura: ${atleta.obtemAlturaAtleta()}`);
console.log(`Notas: ${atleta.obtemNotasAtleta().join(",")}`);
console.log(`Categoria: ${atleta.obtemCategoria()}`);
console.log(`IMC: ${atleta.obtemIMC()}`);
console.log(`Média válida: ${atleta.obtemMediaValida()}`);

