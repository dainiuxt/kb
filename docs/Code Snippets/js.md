# JavaScript

### Alert/Prompt

Gauti atsakymą į klausimą iš `prompt` ir jį pateikti, jei `true`, pakeisti į priešingą ir patekti, jei `false`:

``` js
let answer = confirm('Ar tavo PGR testas yra teigiamas?')
 
if (answer) {
    alert(answer + ' Sveikiname! tu sergi Covid ;)');
} 
if (!answer) {
    answer = !answer;
    alert(answer + ' Sveikiname - tu pasveikai!')
}
```
Patikrinti, ar į `prompt` atsakymą pateikstas skaičius, ar kito tipo `string`:

```js
let answer = prompt('Įveskite bet ką: ')
 
if (isNaN(Number(answer))) {
    alert('Jūs įvedėte "' + answer + '", tačiau tai - ne skaičius.')
} 
if (!isNaN(answer)) {
    alert('Jūs įvedėte skaičių ' + answer); 
}
//veikia ir su console.log()
```

### Programa 'Pilnametis'

1. Paprastas variantas:

```js
let answer = prompt('Kiek tau metų: ')
 
if (Number(answer) < 18) {
    alert('Iki 18 tau liko ' + (18 - answer));
} else if (Number(answer) < 21) {
    alert('Iki 21 tau liko ' + (21 - answer)); 
} else {
    alert('Tu jau visiškai pilnametis!')
}
```

2. `switch` variantas:

```js
let answer = prompt('Kiek tau metų: ')
 
switch(answer) {
 case '1':
 case '2':
 case '3':
 case '4':
 case '5':
 case '6':
 case '7':
 case '8':
 case '9':
 case '10':
 case '11':
 case '12':
 case '13':
 case '14':
 case '15':
 case '16':
 case '17':
    alert('Iki 18 tau liko ' + (18 - Number(answer)));
 break;
 case '18':
 case '19':
 case '20':
    alert('Iki 21 tau liko ' + (21 - Number(answer)));
 break;
 default:
    alert('Tu jau visiškai pilnametis!')
}
```
3. "Pilnametis" parenkant `array` elementą:

```js
let answer = prompt('Kiek tau metų: ')
let i;
if (Number(answer) < 18) {i = 0}
else if (Number(answer) < 21) {i = 1}
else i = 2;
let list = [`Iki 18 tau liko ${18-answer}`,
            `Iki 21 tau liko ${21-answer}`,
            'Tu jau visiškai pilnametis'];
alert(list[i]);
```

### Namų darbai - sukurti objektą, jį užpildyti ir išvesti viską į kosolę ar alertą

```js
let vardas = prompt('Koks tavo vardas: ');
let amzius = prompt('Kiek tau metų: ');
let miestas = prompt('Iš kokio miesto esi: ');

let person = {};
person.vardas = vardas;
person.amzius = amzius;
person.miestas = miestas;

let i;
if (Number(amzius) < 18) {i = 0}
else if (Number(amzius) < 21) {i = 1}
else i = 2;

let list = [`Iki 18 tau liko ${18-amzius}`,
            `Iki 21 tau liko ${21-amzius}`,
            'Tu jau visiškai pilnametis'];

let answer = `Tavo vardas - ${person.vardas}.
Tavo miestas - ${person.miestas}.
Tavo amžius - ${person.amzius}.
${list[i]}.`;

console.log(answer);
alert(answer);
```

### `Array` and `Object` manipulation

```js
let kiek = prompt('Kelių asmenų duomenis norite įvesti: ');
let counter = 0;
let persons = [];

while (counter < kiek) {
    let name = prompt('Koks tavo vardas: ');
    let amzius = prompt('Kiek tau metų: ');
    let obj = {
        vardas: name,
        amzius: amzius,
    };
    persons.push(obj);
    counter++;
}

console.log(persons);
```
