# Un aperçu de Swift

Explorez les fonctionnalités et la syntaxe de Swift.

La tradition veut que le premier programme dans un nouveau langage devrait afficher les mots "Hello, world!" à l'écran. En Swift, cela peut être fait en une seule ligne :

```swift
print("Hello, world!")
// Affiche "Hello, world!"
```

Si vous avez écrit du code en C ou en Objective-C, cette syntaxe vous sera familière — en Swift, cette ligne de code constitue un programme complet. Vous n'avez pas besoin d'importer une bibliothèque séparée pour des fonctionnalités telles que l'*input*/*output* ou la manipulation de chaînes de caractères (*string*). Le code écrit à la portée globale est utilisé comme point d'entrée pour le programme, vous n'avez donc pas besoin d'une fonction `main()`. Vous n'avez pas non plus besoin d'écrire des points-virgules à la fin de chaque instruction. 

Cet aperçu vous fournit suffisamment d'informations pour commencer à écrire du code en Swift en vous montrant comment accomplir diverses tâches de programmation. Ne vous inquiétez pas si vous ne comprenez pas quelque chose — tout ce qui est présenté dans cet aperçu est expliqué en détail dans le reste de ce livre.

## Valeurs simples

Utilisez `let` pour définir une constante et `var` pour créer une variable. La valeur d'une constante n'a pas besoin d'être connue au moment de la compilation, mais vous devez lui attribuer une valeur exactement une fois. Cela signifie que vous pouvez utiliser des constantes pour nommer une valeur que vous choisissez une fois, mais que vous utiliserez à plusieurs endroits.

```swift
myVariable = 42
myVariable = 50
let myConstant = 42
```

Une constante ou une variable doit être du même type que la valeur que vous souhaitez lui attribuer. Cependant, il n'est pas toujours nécessaire d'expliciter le type. En fournissant une valeur lors de la création d'une constante ou d'une variable, le compilateur peut en déduire le type. Dans l'exemple ci-dessus, le compilateur conclut que `myVariable` est un entier parce que sa valeur initiale est un entier.

Si la valeur initiale ne fournit pas suffisamment d'informations (ou s'il n'y a pas de valeur initiale), précisez le type en l'écrivant après la variable, séparé par deux-points.

```swift
let implicitInteger = 70
let implicitDouble = 70.0
let explicitDouble: Double = 70
```

> Expérimentez : Créez une constante avec un type explicite de `Float` et une valeur de `4`.

Les valeurs ne sont jamais converties implicitement en un autre type. Si vous avez besoin de convertir une valeur en un type différent, créez explicitement une instance du type souhaité.

```swift
let label = "The width is "
let width = 94
let widthLabel = label + String(width)
```

> Expérimentez : Essayez de supprimer de la dernièere ligne la conversion en `String`. Quelle erreur obtenez-vous ?

Il existe une manière encore plus simple d'inclure des valeurs dans les chaînes de caractères : écrivez la valeur entre parenthèses et placez une barre oblique inversée (`\`) avant les parenthèses. Par exemple :

```swift
let apples = 3
let oranges = 5
let appleSummary = "I have \(apples) apples."
let fruitSummary = "I have \(apples + oranges) pieces of fruit."
```

> Expérimentez : Utilisez `\()` pour inclure un calcul en virgule flottante dans une chaîne de caractères et pour inclure le nom de quelqu'un dans une salutation.

Utilisez trois doubles guillemets (`"""`) pour les chaînes de caractères qui occupent plusieurs lignes. L'indentation au début de chaque ligne citée est supprimée, tant qu'elle correspond à l'indentation des guillemets de fermeture. Par exemple :

```swift
let quotation = """
        Bien qu'il y ait de l'espace à gauche,
        en réalité les lignes ne sont pas indentées.
            Sauf pour cette ligne.
        Les guillemets doubles (") peuvent apparaître sans nécessiter une barre oblique inversée.

        J'ai toujours \(pommes + oranges) morceaux de fruits.
        """
```

Créez des tableaux (*arrays*) et des dictionnaires (*dictionaries*) en utilisant des crochets (`[]`) et accédez à leurs éléments en écrivant l'index ou la clé entre crochets. Une virgule est autorisée après le dernier élément.

```swift
var fruits = ["strawberries", "limes", "tangerines"]
fruits[1] = "grapes"
var occupations = [
    "Malcolm": "Captain",
    "Kaylee": "Mechanic",
]
occupations["Jayne"] = "Public Relations"
```

Les tableaux s'agrandissent automatiquement lorsque vous ajoutez des éléments.

```swift
fruits.append("blueberries")
print(fruits)
// Affiche "["strawberries", "grapes", "tangerines", "blueberries"]"
```

Des crochets sont également utilisés pour écrire un tableau ou un dictionnaire vide. Pour un tableau, écrivez `[]`, et pour un dictionnaire, écrivez `[:]`.

```swift
fruits = []
occupations = [:]
```

Si vous assignez un tableau vide ou un dictionnaire à une nouvelle variable, ou à un autre endroit où il n'y a aucune information sur le type, vous devez spécifier le type.

```swift
let emptyArray: [String] = []
let emptyDictionary: [String: Float] = [:]
```

## Contrôle de flux

Utilisez `if` et `switch` pour créer des conditions, et utilisez `for`-`in`, `while` et `repeat`-`while` pour créer des boucles. Les parenthèses autour de la condition ou de la variable de boucle sont facultatives. Les accolades autour du corps sont obligatoires.

```swift
let individualScores = [75, 43, 103, 87, 12]
var teamScore = 0
for score in individualScores {
    if score > 50 {
        teamScore += 3
    } else {
        teamScore += 1
    }
}
print(teamScore)
// Affiche "11"
```

Dans une instruction conditionnelle `if`, la condition doit être une expression booléenne. Cela signifie que du code tel que `if score { ... }` est une erreur, et non une comparaison implicite à zéro.

Vous pouvez écrire `if` ou `switch` après le signe égal (`=`) d'une assignation ou après `return` pour choisir une valeur en fonction de la condition.

```swift
let scoreDecoration = if teamScore > 10 {
    "🎉"
} else {
    ""
}
print("Score:", teamScore, scoreDecoration)
// Affiche "Score: 11 🎉"
```

Vous pouvez utiliser `if` et `let` ensemble pour travailler avec des valeurs qui pourraient être manquantes. Ces valeurs sont représentées sous forme optionnelle. Une valeur optionnelle contient soit une valeur, soit `nil` pour indiquer qu'une valeur est manquante. Écrivez un point d'interrogation (`?`) après le type d'une valeur pour marquer la valeur comme optionnelle.

```swift
var optionalString: String? = "Hello"
print(optionalString == nil)
// Affiche "false"
var optionalName: String? = "John Appleseed"
var greeting = "Hello!"
if let name = optionalName {
    greeting = "Hello, \(name)"
}
```

> Expérimentez : Changez `optionalName` pour `nil`. Quelle salutation recevez-vous ? Ajoutez une clause `else` qui définit une salutation différente si `optionalName` est `nil`.

Si la valeur optionnelle est `nil`, la condition est `false` et le code entre accolades est ignoré. Sinon, la valeur optionnelle est déballée et assignée à la constante après le mot-clé `let`, ce qui rend la valeur déballée disponible à l'intérieur du bloc de code.

Une autre façon de gérer les valeurs optionnelles est de fournir une valeur par défaut en utilisant l'opérateur `??`. Si la valeur optionnelle est absente, la valeur par défaut est utilisée à la place.

```swift
let nickname: String? = nil
let fullName: String = "John Appleseed"
let informalGreeting = "Hi \(nickname ?? fullName)"
```

Vous pouvez utiliser une orthographe plus courte pour déballer une valeur, en utilisant le même nom pour cette valeur déballée.

```swift
if let nickname {
    print("Hey, \(nickname)")
}
// N'affiche rien, parce que nickname est nil
```

Les *switch* prennent en charge tout type de données et une grande variété d'opérations de comparaison. Il ne se limite pas aux entiers et aux tests d'égalité.

```swift
let vegetable = "red pepper"
switch vegetable {
case "celery":
    print("Add some raisins and make ants on a log.")
case "cucumber", "watercress":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pepper"):
    print("Is it a spicy \(x)?")
default:
    print("Everything tastes good in soup.")
}
// Affiche "Is it a spicy red pepper?"
```

> Expérimentez : Essayez de supprimer le cas `default`. Quelle erreur obtenez-vous ?

Remarquez comment `let` peut être utilisé dans un motif pour attribuer la valeur qui correspond au motif à une constante.

Après l'exécution du code à l'intérieur du cas switch qui correspond, le programme sort de l'instruction switch. L'exécution ne se poursuit pas jusqu'au cas suivant, donc vous n'avez pas besoin de sortir explicitement du switch à la fin du code de chaque cas.

`for`-`in` est utilisé pour itérer sur les éléments d'un dictionnaire en fournissant une paire de noms à utiliser pour chaque paire clé-valeur. Les dictionnaires sont une collection non ordonnée, donc leurs clés et valeurs sont itérées dans un ordre arbitraire.

```swift
let interestingNumbers = [
    "Prime": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Square": [1, 4, 9, 16, 25],
]
var largest = 0
for (_, numbers) in interestingNumbers {
    for number in numbers {
        if number > largest {
            largest = number
        }
    }
}
print(largest)
// Affiche "25"
```

> Expérimentez : Remplacez le `_` par un nom de variable et observez quelle sorte de nombre était le plus grand.

Utilisez `while` pour répéter un bloc de code jusqu'à ce qu'une condition change. La condition d'une boucle peut également être à la fin, garantissant que la boucle est exécutée au moins une fois.

```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Affiche "128"
var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Affiche "128"
```

> Expérimentez : Modifiez la condition de `m < 100` à `m < 0` pour voir comment les boucles `while` et `repeat`-`while` se comportent différemment lorsque la condition de la boucle est déjà vraie.

Vous pouvez maintenir un index dans une boucle en utilisant `..<` pour créer une plage d'index.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Affiche "6"
```

Utilisez `..<` pour créer une plage qui exclut sa valeur supérieure, et utilisez `...` pour créer une plage qui inclut les deux valeurs.

## Fonctions et closures

Utilisez `func` pour déclarer une fonction. Appelez une fonction en écrivant son nom suivi d'une liste d'arguments entre parenthèses. Utilisez `->` pour séparer les noms et types des paramètres du type de retour de la fonction.

```swift
func greet(person: String, day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet(person: "Bob", day: "Tuesday")
```

> Expérimentez : Supprimez le paramètre `day`. Ajoutez un paramètre pour inclure la spécialité du déjeuner d'aujourd'hui dans la salutation.

Par défaut, les fonctions utilisent les noms de leurs paramètres comme étiquettes pour leurs arguments. Écrivez une étiquette d'argument personnalisée avant le nom du paramètre, ou écrivez `_` pour ne pas utiliser d'étiquette d'argument.

```swift
func greet(_ person: String, on day: String) -> String {
    return "Hello \(person), today is \(day)."
}
greet("John", on: "Wednesday")
```

Utilisez un tuple pour créer une valeur composite, par exemple, pour renvoyer plusieurs valeurs à partir d'une fonction. Les éléments d'un tuple peuvent être référencés soit par leur nom, soit par leur numéro.

```swift
func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
    var min = scores[0]
    var max = scores[0]
    var sum = 0
    for score in scores {
        if score > max {
            max = score
        } else if score < min {
            min = score
        }
        sum += score
    }
    return (min, max, sum)
}
let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
print(statistics.sum)
// Affiche "120"
print(statistics.2)
// Affiche "120"
```

Les fonctions peuvent être imbriquées. Les fonctions imbriquées ont accès aux variables qui ont été déclarées dans la fonction externe. Vous pouvez utiliser des fonctions imbriquées pour organiser le code dans une fonction qui est longue ou complexe.

```swift
func returnFifteen() -> Int {
    var y = 10
    func add() {
        y += 5
    }
    add()
    return y
}
returnFifteen()
```

Les fonctions sont de première classe. Cela signifie qu'une fonction peut renvoyer une autre fonction comme valeur.

```swift
func makeIncrementer() -> ((Int) -> Int) {
    func addOne(number: Int) -> Int {
        return 1 + number
    }
    return addOne
}
var increment = makeIncrementer()
increment(7)
```

Une fonction peut prendre une autre fonction comme l'un de ses arguments.

```swift
func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
    for item in list {
        if condition(item) {
            return true
        }
    }
    return false
}
func lessThanTen(number: Int) -> Bool {
    return number < 10
}
var numbers = [20, 19, 7, 12]
hasAnyMatches(list: numbers, condition: lessThanTen)
```

Les fonctions sont en réalité un cas particulier de closures : des blocs de code qui peuvent être appelés ultérieurement. Le code dans une closure a accès à des éléments tels que des variables et des fonctions qui étaient disponibles dans la portée où la closure a été créée, même si la closure se trouve dans une portée différente lors de son exécution — vous avez déjà vu un exemple de cela avec des fonctions imbriquées. Vous pouvez écrire une closure sans nom en entourant le code avec des accolades (`{}`). Utilisez `in` pour séparer les arguments et le type de retour du corps.

```swift
numbers.map({ (number: Int) -> Int in
    let result = 3 * number
    return result
})
```

> Expérimentez : Réécrivez la closure pour renvoyer zéro pour tous les nombres impairs.

Plusieurs options s'offrent à vous pour écrire des closures de manière plus concise. Lorsque le type d'une closure est déjà connu, comme le rappel pour un délégué, vous pouvez omettre le type de ses paramètres, son type de retour, ou les deux. Les closures à une seule instruction retournent implicitement la valeur de leur seule instruction.

```swift
let mappedNumbers = numbers.map({ number in 3 * number })
print(mappedNumbers)
// Affiche "[60, 57, 21, 36]"
```

Vous pouvez vous référer aux paramètres par numéro plutôt que par nom. Cette approche est particulièrement utile dans les closures très courtes. Une closure passée en dernier argument à une fonction peut apparaître immédiatement après les parenthèses. Lorsqu'une closure est le seul argument d'une fonction, vous pouvez omettre les parenthèses entièrement.

```swift
typealias AudioSample = UInt16let sortedNumbers = numbers.sorted { $0 > $1 }
print(sortedNumbers)
// Affiche "[20, 19, 12, 7]"
```

## Objets et classes

Utilisez `class` suivie du nom de la classe pour créer une classe. Une déclaration de propriété dans une classe est écrite de la même manière qu'une déclaration de constante ou de variable, à la seule différence qu'elle est dans le contexte d'une classe. De même, les déclarations de méthode et de fonction sont écrites de la même manière.

```swift
class Shape {
    var numberOfSides = 0
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

> Expérimentez : Ajoutez une propriété constante avec `let` et ajoutez une autre méthode qui prend un argument.

Créez une instance d'une classe en plaçant des parenthèses après le nom de la classe. Utilisez la syntaxe avec un point pour accéder aux propriétés et méthodes de l'instance.

```swift
var shape = Shape()
shape.numberOfSides = 7
var shapeDescription = shape.simpleDescription()
```

Il manque quelque chose d'important à cette version de la classe `Shape` : un initialiseur pour configurer la classe lorsqu'une instance est créée. Utilisez `init` pour en créer un.

```swift
class NamedShape {
    var numberOfSides: Int = 0
    var name: String
    init(name: String) {
        self.name = name
    }
    func simpleDescription() -> String {
        return "A shape with \(numberOfSides) sides."
    }
}
```

Remarquez comment `self` est utilisé pour distinguer la propriété `name` de l'argument `name` de l'initialiseur. Les arguments de l'initialiseur sont transmis comme un appel de fonction lorsque vous créez une instance de la classe. Chaque propriété doit avoir une valeur attribuée, soit dans sa déclaration (comme avec `numberOfSides`), soit dans l'initialiseur (comme avec `name`).

Utilisez `deinit` pour créer un désinitialiseur si vous avez besoin d'effectuer un certain nettoyage avant que l'objet ne soit désalloué.

Les sous-classes incluent le nom de leur superclasse après leur nom de classe, séparé par deux-points. Il n'y a aucune obligation pour les classes de sous-classer une classe racine standard, donc vous pouvez inclure ou omettre une superclasse selon vos besoins.

Les méthodes d'une sous-classe qui remplacent l'implémentation de la superclasse sont marquées avec `override` - remplacer une méthode par accident, sans `override`, est détecté par le compilateur comme une erreur. Le compilateur détecte également les méthodes avec `override` qui ne remplacent effectivement aucune méthode de la superclasse.

```swift
class Square: NamedShape {
    var sideLength: Double
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 4
    }
    func area() -> Double {
        return sideLength * sideLength
    }
    override func simpleDescription() -> String {
        return "A square with sides of length \(sideLength)."
    }
}
let test = Square(sideLength: 5.2, name: "my test square")
test.area()
test.simpleDescription()
```

> Expérimentez : Créez une autre sous-classe de `NamedShape` appelée `Circle` qui prend un rayon et un nom en tant qu'arguments pour son initialisateur. Implémentez une méthode `area()` et une méthode `simpleDescription()` dans la classe `Circle`.

En plus des propriétés simples qui sont stockées, les propriétés peuvent avoir un *getter* et un *setter*.

```swift
class EquilateralTriangle: NamedShape {
    var sideLength: Double = 0.0
    init(sideLength: Double, name: String) {
        self.sideLength = sideLength
        super.init(name: name)
        numberOfSides = 3
    }
    var perimeter: Double {
        get {
            return 3.0 * sideLength
        }
        set {
            sideLength = newValue / 3.0
        }
    }
    override func simpleDescription() -> String {
        return "An equilateral triangle with sides of length \(sideLength)."
    }
}
var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")
print(triangle.perimeter)
// Affiche "9.3"
triangle.perimeter = 9.9
print(triangle.sideLength)
// Affiche "3.3000000000000003"
```

Pour le `set` de `perimeter`, la nouvelle valeur a le nom implicite `newValue`. Vous pouvez fournir un nom explicite entre parenthèses après `set`.

Notez que l'initialiseur de la classe `EquilateralTriangle` comporte trois étapes différentes :

1. Définition de la valeur des propriétés déclarées par la sous-classe.
2. Appel de l'initialiseur de la superclasse.
3. Modification de la valeur des propriétés définies par la superclasse. Tout travail supplémentaire de configuration utilisant des méthodes, des *getters* ou des *setters* peuvent également être effectués à ce stade.

Si vous n'avez pas besoin de calculer la propriété mais que vous devez quand même fournir du code qui s'exécute avant et après la définition d'une nouvelle valeur, utilisez `willSet` et `didSet`. Le code que vous fournissez s'exécute à chaque fois que la valeur change en dehors d'un initialiseur. Par exemple, la classe ci-dessous garantit que la longueur du côté de son triangle est toujours la même que la longueur du côté de son carré.

```swift
class TriangleAndSquare {
    var triangle: EquilateralTriangle {
        willSet {
            square.sideLength = newValue.sideLength
        }
    }
    var square: Square {
        willSet {
            triangle.sideLength = newValue.sideLength
        }
    }
    init(size: Double, name: String) {
        square = Square(sideLength: size, name: name)
        triangle = EquilateralTriangle(sideLength: size, name: name)
    }
}
var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")
print(triangleAndSquare.square.sideLength)
// Affiche "10.0"
print(triangleAndSquare.triangle.sideLength)
// Affiche "10.0"
triangleAndSquare.square = Square(sideLength: 50, name: "larger square")
print(triangleAndSquare.triangle.sideLength)
// Affiche "50.0"
```

Lorsque vous travaillez avec des valeurs optionnelles, vous pouvez écrire `?` avant des opérations telles que les méthodes, les propriétés et l'indexation. Si la valeur avant le `?` est `nil`, tout ce qui se trouve après le `?` est ignoré et la valeur de toute l'expression est `nil`. Sinon, la valeur optionnelle est déballée, et tout ce qui se trouve après le `?` agit sur la valeur déballée. Dans les deux cas, la valeur de toute l'expression est une valeur optionnelle.

```swift
let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
let sideLength = optionalSquare?.sideLength
```

## Énumérations et Structures

Utilisez `enum` pour créer une énumération. Comme les classes et tous les autres types nommés, les énumérations peuvent avoir des méthodes qui leur sont associées.

```swift
enum Rank: Int {
    case ace = 1
    case two, three, four, five, six, seven, eight, nine, ten
    case jack, queen, king
    func simpleDescription() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .queen:
            return "queen"
        case .king:
            return "king"
        default:
            return String(self.rawValue)
        }
    }
}
let ace = Rank.ace
let aceRawValue = ace.rawValue
```

> Expérimentez : Écrivez une fonction qui compare deux valeurs `Rank` en comparant leurs valeurs brutes.

Par défaut, Swift attribue les valeurs brutes en commençant par zéro et en les incrémentant d'un à chaque fois, mais vous pouvez modifier ce comportement en spécifiant explicitement des valeurs. Dans l'exemple ci-dessus, `Ace` se voit explicitement attribuer une valeur brute de `1`, et le reste des valeurs brutes est assigné dans l'ordre. Vous pouvez également utiliser des chaînes de caractères ou des nombres à virgule flottante comme type brut d'une énumération. Utilisez la propriété `rawValue` pour accéder à la valeur brute d'un cas d'énumération.

Utilisez l'initialiseur `init?(rawValue:)` pour créer une instance d'une énumération à partir d'une valeur brute. Il renvoie soit le cas d'énumération correspondant à la valeur brute, soit `nil` s'il n'y a pas de correspondance avec `Rank`.

```swift
if let convertedRank = Rank(rawValue: 3) {
    let threeDescription = convertedRank.simpleDescription()
}
```

Les valeurs de cas d'une énumération sont des valeurs réelles, et non simplement une autre manière d'écrire leurs valeurs brutes. En fait, dans les cas où il n'y a pas de valeur brute significative, vous n'êtes pas obligé d'en fournir une.

```swift
enum Suit {
    case spades, hearts, diamonds, clubs
    func simpleDescription() -> String {
        switch self {
        case .spades:
            return "spades"
        case .hearts:
            return "hearts"
        case .diamonds:
            return "diamonds"
        case .clubs:
            return "clubs"
        }
    }
}
let hearts = Suit.hearts
let heartsDescription = hearts.simpleDescription()
```

> Expérimentez : Ajoutez une méthode `color()` à la classe `Suit` qui renvoie "black" pour les piques et les trèfles, et renvoie "red" pour les cœurs et les carreaux.

Remarquez les deux façons dont le cas `hearts` de l'énumération est mentionné ci-dessus : Lors de l'attribution d'une valeur à la constante `hearts`, le cas d'énumération `Suit.hearts` est référencé par son nom complet car la constante n'a pas de type explicite spécifié. À l'intérieur du bloc switch, le cas d'énumération est référencé par la forme abrégée `.hearts` car la valeur de `self` est déjà connue comme étant de type suit. Vous pouvez utiliser la forme abrégée chaque fois que le type de la valeur est déjà connu.

Si une énumération a des valeurs brutes, ces valeurs sont déterminées dans le cadre de la déclaration, ce qui signifie que chaque instance d'un cas particulier de l'énumération a toujours la même valeur brute. Une autre option pour les cas d'énumération est d'avoir des valeurs associées au cas - ces valeurs sont déterminées lors de la création de l'instance et peuvent être différentes pour chaque instance d'un cas d'énumération. Vous pouvez considérer les valeurs associées comme se comportant comme des propriétés stockées de l'instance du cas d'énumération. Par exemple, pensez au cas de la demande des heures de lever et de coucher du soleil auprès d'un serveur. Le serveur répond soit avec les informations demandées, soit avec une description de ce qui s'est mal passé.

```swift
enum ServerResponse {
    case result(String, String)
    case failure(String)
}
let success = ServerResponse.result("6:00 am", "8:09 pm")
let failure = ServerResponse.failure("Out of cheese.")
switch success {
case let .result(sunrise, sunset):
    print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
case let .failure(message):
    print("Failure...  \(message)")
}
// Affiche "Sunrise is at 6:00 am and sunset is at 8:09 pm."
```

> Expérimentez : Ajoutez un troisième cas à `ServerResponse` et au switch.

Remarquez comment les heures de lever et de coucher du soleil sont extraites de la valeur `ServerResponse` dans le cadre de la correspondance de la valeur avec les cas switch.

Utilisez `struct` pour créer une structure. Les structures prennent en charge de nombreux comportements similaires à ceux des classes, y compris les méthodes et les initialiseurs. Une des différences les plus importantes entre les structures et les classes est que les structures sont toujours copiées lorsqu'elles sont transmises dans votre code, tandis que les classes sont transmises par référence.

```swift
struct Card {
    var rank: Rank
    var suit: Suit
    func simpleDescription() -> String {
        return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
    }
}
let threeOfSpades = Card(rank: .three, suit: .spades)
let threeOfSpadesDescription = threeOfSpades.simpleDescription()
```

> Expérimentez : Écrivez une fonction qui renvoie un tableau contenant un jeu complet de cartes, avec une carte de chaque combinaison de rang et de couleur.

## Concurrence

Utilisez `async` pour marquer une fonction qui s'exécute de manière asynchrone.

```swift
func fetchUserID(from server: String) async -> Int {
    if server == "primary" {
        return 97
    }
    return 501
}
```

Vous marquez un appel à une fonction asynchrone en écrivant `await` devant celle-ci.

```swift
func fetchUsername(from server: String) async -> String {
    let userID = await fetchUserID(from: server)
    if userID == 501 {
        return "John Appleseed"
    }
    return "Guest"
}
```

Utilisez `async let` pour appeler une fonction asynchrone, lui permettant de s'exécuter en parallèle avec d'autres codes asynchrones. Lorsque vous utilisez la valeur qu'elle retourne, écrivez `await`.

```swift
func connectUser(to server: String) async {
    async let userID = fetchUserID(from: server)
    async let username = fetchUsername(from: server)
    let greeting = await "Hello \(username), user ID \(userID)"
    print(greeting)
}
```

Utilisez `Task` pour appeler des fonctions asynchrones à partir de code synchrone, sans attendre leur retour.

```swift
Task {
    await connectUser(to: "primary")
}
// Affiche "Hello Guest, user ID 97"
```

Utilisez des groupes de tâches pour structurer le code concurrent.

```swift
let userIDs = await withTaskGroup(of: Int.self) { taskGroup in
    for server in ["primary", "secondary", "development"] {
        taskGroup.addTask {
            return await fetchUserID(from: server)
        }
    }
    var results: [Int] = []
    for await result in taskGroup {
        results.append(result)
    }
    return results
}
```

Les acteurs (*actor*) sont similaires aux classes, sauf qu'ils veillent à ce que différentes fonctions asynchrones puissent interagir en toute sécurité avec une instance du même acteur en même temps.

```swift
actor ServerConnection {
    var server: String = "primary"
    private var activeUsers: [Int] = []
    func connect() async -> Int {
        let userID = await fetchUserID(from: server)
        // ... communicate with server ...
        activeUsers.append(userID)
        return userID
    }
}
```

Quand vous appelez une méthode sur un acteur ou accédez à l'une de ses propriétés, vous marquez ce code avec `await` pour indiquer qu'il pourrait devoir attendre que d'autres codes déjà en cours d'exécution sur l'acteur se terminent.

```swift
let server = ServerConnection()
let userID = await server.connect()
```

## Protocoles et extensions

Utilisez `protocol` pour déclarer un protocole.

```swift
protocol ExampleProtocol {
    var simpleDescription: String { get }
    mutating func adjust()
}
```

Les classes, énumérations et structures peuvent toutes adopter des protocoles.

```swift
class SimpleClass: ExampleProtocol {
    var simpleDescription: String = "A very simple class."
    var anotherProperty: Int = 69105
    func adjust() {
        simpleDescription += "  Now 100% adjusted."
    }
}
var a = SimpleClass()
a.adjust()
let aDescription = a.simpleDescription
struct SimpleStructure: ExampleProtocol {
    var simpleDescription: String = "A simple structure"
    mutating func adjust() {
        simpleDescription += " (adjusted)"
    }
}
var b = SimpleStructure()
b.adjust()
let bDescription = b.simpleDescription
```

> Expérimentez : Ajoutez une autre exigence à `ExampleProtocol`. Quels changements devez-vous apporter à `SimpleClass` et `SimpleStructure` pour qu'ils continuent de respecter le protocole ?

Remarquez l'utilisation du mot-clé `mutating` dans la déclaration de `SimpleStructure` pour marquer une méthode qui modifie la structure. La déclaration de `SimpleClass` n'a pas besoin que ses méthodes soient marquées comme `mutating`, car les méthodes d'une classe peuvent toujours modifier la classe.

Utilisez `extension` pour ajouter des fonctionnalités à un type existant, telles que de nouvelles méthodes et propriétés calculées. Vous pouvez utiliser une extension pour ajouter la conformité à un protocole à un type déclaré ailleurs, ou même à un type que vous avez importé à partir d'une bibliothèque ou d'un framework.

```swift
extension Int: ExampleProtocol {
    var simpleDescription: String {
        return "The number \(self)"
    }
    mutating func adjust() {
        self += 42
    }
}
print(7.simpleDescription)
// Affiche "The number 7"
```

> Expérimentez : Écrivez une extension pour le type `Double` qui ajoute une propriété `absoluteValue`.

Vous pouvez utiliser un nom de protocole de la même manière que tout autre type nommé, par exemple, pour créer une collection d'objets de types différents mais qui tous se conforment à un seul protocole. Lorsque vous travaillez avec des valeurs dont le type est un type de protocole empaqueté, les méthodes en dehors de la définition du protocole ne sont pas disponibles.

```swift
let protocolValue: ExampleProtocol = a
print(protocolValue.simpleDescription)
// Affiche "A very simple class.  Now 100% adjusted."
// print(protocolValue.anotherProperty)  // Enlever le commentaire pour voir l'erreur
```

Bien que la variable `protocolValue` ait un type d'exécution de `SimpleClass`, le compilateur la traite comme le type donné de `ExampleProtocol`. Cela signifie que vous ne pouvez pas accidentellement accéder à des méthodes ou propriétés que la classe implémente en plus de sa conformité au protocole.

## Gestion des erreurs

Vous représentez les erreurs en utilisant n'importe quel type qui adopte le protocole `Error`.

```swift
enum PrinterError: Error {
    case outOfPaper
    case noToner
    case onFire
}
```

Utilisez `throw` pour déclencher une erreur et `throws` pour indiquer une fonction susceptible de déclencher une erreur. Si vous lancez une erreur dans une fonction, la fonction se termine immédiatement et le code appelant la fonction gère l'erreur.

```swift
func send(job: Int, toPrinter printerName: String) throws -> String {
    if printerName == "Never Has Toner" {
        throw PrinterError.noToner
    }
    return "Job sent"
}
```

Il existe plusieurs façons de gérer les erreurs. Une manière consiste à utiliser la structure `do`-`catch`. À l'intérieur du bloc `do`, vous marquez le code susceptible de générer une erreur en écrivant `try` devant. À l'intérieur du bloc `catch`, l'erreur est automatiquement nommée `error` à moins que vous ne lui donniez un nom différent.

```swift
do {
    let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
    print(printerResponse)
} catch {
    print(error)
}
// Affiche "Job sent"
```

> Expérimentez : Changez le nom de l'imprimante en `"Never Has Toner"`, de sorte que la fonction `send(job:toPrinter:)` génère une erreur.

Vous pouvez fournir plusieurs blocs `catch` qui gèrent des erreurs spécifiques. Vous écrivez un motif après `catch`, tout comme vous le faites après `case` dans une instruction `switch`.

```swift
do {
    let printerResponse = try send(job: 1440, toPrinter: "Gutenberg")
    print(printerResponse)
} catch PrinterError.onFire {
    print("I'll just put this over here, with the rest of the fire.")
} catch let printerError as PrinterError {
    print("Printer error: \(printerError).")
} catch {
    print(error)
}
// Affiche "Job sent"
```

> Expérimentez : Ajoutez du code pour générer une erreur à l'intérieur du bloc `do`. Quel type d'erreur devez-vous générer pour que l'erreur soit traitée par le premier bloc `catch` ? Et pour les deuxième et troisième blocs ?

```swift
if let definiteString = assumedString {
    print(definiteString)
}
// Affiche "An implicitly unwrapped optional string."
```

Une autre façon de gérer les erreurs est d'utiliser `try?` pour convertir le résultat en optionnel. Si la fonction lance une erreur, l'erreur spécifique est ignorée et le résultat est `nil`. Sinon, le résultat est un optionnel contenant la valeur que la fonction a renvoyée.

```swift
let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")
```

Utilisez `defer` pour écrire un bloc de code qui s'exécute après tout autre code dans la fonction, juste avant le retour de la fonction. Le code est exécuté indépendamment de savoir si la fonction génère une erreur. Vous pouvez utiliser `defer` pour écrire du code de configuration et de nettoyage côte à côte, même s'ils doivent être exécutés à des moments différents.

```swift
var fridgeIsOpen = false
let fridgeContent = ["milk", "eggs", "leftovers"]
func fridgeContains(_ food: String) -> Bool {
    fridgeIsOpen = true
    defer {
        fridgeIsOpen = false
    }
    let result = fridgeContent.contains(food)
    return result
}
fridgeContains("banana")
print(fridgeIsOpen)
// Affiche "false"
```

## Génériques

Écrivez un nom à l'intérieur de crochets angulaires pour créer une fonction ou un type générique.

```swift
func makeArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
    var result: [Item] = []
    for _ in 0..<numberOfTimes {
        result.append(item)
    }
    return result
}
makeArray(repeating: "knock", numberOfTimes: 4)
```

Vous pouvez créer des formes génériques de fonctions et de méthodes, ainsi que des classes, des énumérations et des structures.

```swift
// Réimplémente le type optionnel de la bibliothèque standard de Swift.
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var possibleInteger: OptionalValue<Int> = .none
possibleInteger = .some(100)
```

Utilisez `where` juste avant le corps pour spécifier une liste d'exigences, par exemple, pour exiger que le type implémente un protocole, pour exiger que deux types soient identiques, ou pour exiger qu'une classe ait une superclasse particulière.

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])
```

> Expérimentez : Modifier la fonction `anyCommonElements(_:_:)` pour créer une fonction qui renvoie un tableau des éléments communs à deux séquences quelconques.

Écrire `<T: Equatable>` revient au même que d'écrire `<T> ... where T: Equatable`.
