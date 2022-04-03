- [S.O.L.I.D](#solid)
  - [Single Responsability Principle](#single-responsability-principle)
    - [Exemplo:](#exemplo)
  - [Open/Closed Principle](#openclosed-principle)
    - [Exemplo:](#exemplo-1)
  - [Liskov Substitution Principle](#liskov-substitution-principle)
    - [Exemplo:](#exemplo-2)
  - [Interface Segregation Principle](#interface-segregation-principle)
    - [Exemplo:](#exemplo-3)
  - [Dependency Inversion Principle](#dependency-inversion-principle)
    - [Exemplo:](#exemplo-4)

# S.O.L.I.D

SOLID é um acrônimo que consolida 5 itens que são considerados como boas práticas no mundo do desenvolvimento
orientado a objetos.

## Single Responsability Principle

- Cada classe deve ter apenas uma responsabilidade.
- Uma classe deve ter um, e apenas um, motivo para mudar.

### Exemplo:

```ts
/** Note que a classe curso está extrapolando suas responsabilidades,
 * lidando com conexão e criação de categorias.
 *
 * A forma correta seria remover métodos que não pertencem a responsabilidade
 * da classe e criá-los dentro das classes corretas
**/
class Course {
  constructor(
    private name: string,
    private category: string,
    private description: string
  ) {}

  public function connection() {}

  public function createCategory() {}

  public function createCourse() {}
}

```

## Open/Closed Principle

- Toda classe deve ser aberta a extensão mas fechada para modificação
- Quando eu tenho uma classe e preciso adicionar um novo requisito devo extender uma nova classe a partir de uma classe base a estas e criar esse novo comportamento.

### Exemplo:

```ts
/**
 * Note que para cada comportamento, nova categoria, eu preciso adicionar uma nova regra de negócio
 * O modo correto de fazer isso é criar uma classe base de vídeo, e estendê-la para as classes
 * Movie, TVShow e outras que possam surgir.
**/
class Video {
  constructor(
    private type: string;
  ) {}

  public function calculaInteresse() {
    if(this.type == "Movie") {
      // calcula
    } else if(this.type == "TVShow") {
      // faz outro cálculo
    }
  }
}
```

## Liskov Substitution Principle

- Subclasses podem ser substituídas por suas classes pais.

### Exemplo:

```ts
/**
 * Note que para cada comportamento, nova categoria, eu preciso adicionar uma nova regra de negócio
 * O modo correto de fazer isso é criar uma classe base de vídeo, e estendê-la para as classes
 * Movie, TVShow e outras que possam surgir.
**/
class Movie {
  public function play() {
    // play on video
  }

  public function increaseVolume() {

  }
}

class SomeRandomMovie extends Movie {

}

// Filme mudo, logo não pode estender de Movie pois não utiliza increaseVolume
class ModernTimes extends Movie {
  public function increaseVolume() {}
}

```

## Interface Segregation Principle

- Uma classe não é obrigada a implementar interfaces que ela não utilizará.

### Exemplo:

```ts
/**
 * Note que para cada comportamento, nova categoria, eu preciso adicionar uma nova regra de negócio
 * O modo correto de fazer isso é criar uma classe base de vídeo, e estendê-la para as classes
 * Movie, TVShow e outras que possam surgir.
**/
class Movie {
  public function play() {...}
}

class AudioControl {
  public function increaseVolume() {...}
}

class TheLionKing implements Movie, AudioControl {}
class ModernTimes implements Movie {}
```

## Dependency Inversion Principle

- Deve-se depender de abstrações e não de implementações

### Exemplo:

```ts
class ICategory {}
class DramaCategory implements ICategory {}

class Movie {
  constructor(private name: string, private category: ICategory) {
    this.name = name;
    this.category = category;
  }

  function getName(): string {
    return this.name;
  }

  function setName(name: string): void {
    this.name = name;
  }

  function getCategory(): string {
    return this.category;
  }

  function setCategory(category: ICategory): void {
    this.category = category;
  }
}
```
