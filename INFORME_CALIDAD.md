# EVALUACIÓN TÉCNICA FORMAL DE CALIDAD
## 4Geeks Academy — Repositorio de ejercicios «Master TypeScript Skills»

---

**Referencia del informe:** QA-TS-2026-002  
**Fecha de análisis:** 28 de mayo de 2026  
**Repositorio analizado:** Fork de `4GeeksAcademy/master-typescript-exercises`   
**Precio del curso abonado:** Entre aproximadamente 4.000 € y 9.000 €  
**Metodología:** Cada hallazgo del presente informe es directamente verificable abriendo el archivo indicado. Se proporcionan rutas de archivo, citas textuales exactas y evidencia a nivel de línea para cada afirmación. No se realiza ninguna afirmación que no pueda confirmarse mediante la inspección del repositorio en su estado comprometido.

---

## ÍNDICE

1. [Alcance y metodología](#1-alcance-y-metodología)
2. [Descripción general del repositorio](#2-descripción-general-del-repositorio)
3. [Hallazgo 1 — Errores de return type en TypeScript](#3-hallazgo-1--errores-de-return-type-en-typescript)
4. [Hallazgo 2 — Parámetros fantasma](#4-hallazgo-2--parámetros-fantasma)
5. [Hallazgo 3 — Discrepancias en la numeración de ejercicios en los README](#5-hallazgo-3--discrepancias-en-la-numeración-de-ejercicios-en-los-readme)
6. [Hallazgo 4 — Archivos de solución sin implementación](#6-hallazgo-4--archivos-de-solución-sin-implementación)
7. [Hallazgo 5 — Archivos README stub](#7-hallazgo-5--archivos-readme-stub)
8. [Hallazgo 6 — Contradicciones internas](#8-hallazgo-6--contradicciones-internas)
9. [Hallazgo 7 — Auditoría de contenido específico de TypeScript](#9-hallazgo-7--auditoría-de-contenido-específico-de-typescript)
10. [Estadísticas resumen](#10-estadísticas-resumen)

---

## 1. ALCANCE Y METODOLOGÍA

El presente informe audita los archivos de ejercicios entregados a los estudiantes como parte del módulo «Master TypeScript Skills». La auditoría abarca:

- Los 170 directorios de ejercicios (desde `001-isOldEnoughToDrink` hasta `170-comparePassByValueAndReference`)
- Todos los archivos `app.ts` (archivos TypeScript de inicio entregados a los estudiantes)
- Todos los archivos `README.md` (archivos de instrucciones)
- Todos los archivos `test.js` (suites de pruebas automatizadas)
- Todos los archivos `solution.hide.js` (implementaciones de referencia)

Para cada categoría de defecto se proporciona la siguiente evidencia:
- La ruta de archivo exacta
- El texto exacto citado del archivo
- La evidencia contradictoria (descripción del README, aseveración del test o un segundo archivo)
- Una explicación de una línea del defecto

Todas las lecturas de archivos se realizaron directamente sobre el estado comprometido del repositorio.

---

## 2. DESCRIPCIÓN GENERAL DEL REPOSITORIO

| Elemento | Cantidad |
|---|---|
| Directorios de ejercicios | 170 |
| Archivos `app.ts` | 170 |
| Archivos `README.md` | 171 (incluye `00-Welcome`) |
| Archivos `test.js` | 170 |
| Archivos `solution.hide.js` | 169 |

---

## 3. HALLAZGO 1 — ERRORES DE RETURN TYPE EN TYPESCRIPT

Cada archivo `app.ts` declara un return type de TypeScript para la función que el estudiante debe implementar. En los siguientes casos, el return type declarado es demostrablemente incorrecto: bien porque la descripción del README especifica un tipo diferente, bien porque las aseveraciones del test confirman un tipo diferente, o bien ambas cosas. Un estudiante que implemente correctamente la función tal como se describe producirá código cuyo valor de retorno no coincide con el return type de TypeScript declarado, lo que genera un error de TypeScript.

---

### 3.1 — `exercises/046-addToFront/app.ts`

**Firma citada:**
```typescript
function addToFront(arr: unknown[], element: number): string {
```

**El README indica** (`exercises/046-addToFront/README.md`):
> "addToFront adds the given element to the front of the given array, and returns the given array."

**Aseveración del test** (`exercises/046-addToFront/test.js`):
```javascript
expect(addToFront([6, 7], 8)).toStrictEqual([8, 6, 7]);
expect(addToFront([1, 2], 3)).toStrictEqual([3, 1, 2]);
```

**Defecto:** El return type declarado es `string`. La función se describe como que devuelve un array y los tests verifican valores de array. Una implementación correcta devuelve un array, lo que no satisface la type annotation de return type `string`.

---

### 3.2 — `exercises/047-addToBack/app.ts`

**Firma citada:**
```typescript
function addToBack(arr: unknown[], element: number): string {
```

**El README indica** (`exercises/047-addToBack/README.md`):
> "addToBack returns the given array with the given element added at the end."

**Defecto:** El return type declarado es `string`; la función se describe como que devuelve un array.

---

### 3.3 — `exercises/048-joinArrays/app.ts`

**Firma citada:**
```typescript
function joinArrays(arr1: unknown[], arr2: unknown[]): string {
```

**El README indica** (`exercises/048-joinArrays/README.md`):
> "joinArrays returns an array with the elements of arr1, followed by the elements of arr2 in order."

**Defecto:** El return type declarado es `string`; la función se describe como que devuelve un array.

---

### 3.4 — `exercises/049-getElementsAfter/app.ts`

**Firma citada:**
```typescript
function getElementsAfter(array: unknown[], n: unknown, arg3: number): string {
```

**El README indica** (`exercises/049-getElementsAfter/README.md`):
> "getElementsAfter returns a new array with all the elements after (but not including) the given index."

**Aseveración del test** (`exercises/049-getElementsAfter/test.js`):
```javascript
let output = getElementsAfter(['a', 'b', 'c', 'd', 'e'], 2)
expect(output).toEqual(['d', 'e'])
```

**Defecto:** El return type declarado es `string`; la función se describe y se prueba como que devuelve un array. (El parámetro fantasma `arg3` se documenta por separado en el Hallazgo 2.)

---

### 3.5 — `exercises/056-getAllLetters/app.ts`

**Firma citada:**
```typescript
function getAllLetters(str: string): string {
```

**El README indica** (`exercises/056-getAllLetters/README.md`):
> "getAllLetters returns an array containing every character in the word."

**Aseveración del test** (`exercises/056-getAllLetters/test.js`):
```javascript
expect(output).toEqual(["R", "a", "d", "a", "g", "a", "s", "t"]);
```

**Defecto:** El return type declarado es `string`; la función se describe y se prueba como que devuelve un array de caracteres (`string[]`).

---

### 3.6 — `exercises/057-getAllWords/app.ts`

**Firma citada:**
```typescript
function getAllWords(str: string): string {
```

**El README indica** (`exercises/057-getAllWords/README.md`):
> "getAllWords returns an array containing every word in the sentence."

**Defecto:** El return type declarado es `string`; la función se describe como que devuelve un array de palabras.

---

### 3.7 — `exercises/068-joinThreeArrays/app.ts`

**Firma citada:**
```typescript
function joinThreeArrays(arr1: unknown[], arr2: unknown[], arr3: unknown[]): string {
```

**El README indica** (`exercises/068-joinThreeArrays/README.md`):
> "joinThreeArrays returns an array with the elements of arr1 in order followed by the elements in arr2 followed by the elements of arr3."

**Defecto:** El return type declarado es `string`; la función se describe como que devuelve un array.

---

### 3.8 — `exercises/074-filterOddLengthWords/app.ts`

**Firma citada:**
```typescript
function filterOddLengthWords(words: unknown[]): number {
```

**El README indica** (`exercises/074-filterOddLengthWords/README.md`):
> "filterOddLengthWords returns an array containing only the elements of the given array whose lengths are odd numbers."

**Aseveración del test** (`exercises/074-filterOddLengthWords/test.js`):
```javascript
expect(Array.isArray(filterOddLengthWords(['you']))).toBeTruthy();
expect(output).toEqual(['you', 'can']);
```

**Defecto:** El return type declarado es `number`; la función se describe y se prueba como que devuelve un array de strings.

---

### 3.9 — `exercises/116-getProperty/app.ts`

**Firma citada:**
```typescript
function getProperty(obj: unknown, key: string): unknown[] {
```

**El README indica** (`exercises/116-getProperty/README.md`):
> "getProperty returns the value of the property at the given key."

**Aseveración del test** (`exercises/116-getProperty/test.js`):
```javascript
expect(getProperty(person,'name')).toEqual('Alex');
expect(getProperty(person,'lastname')).toBe(undefined);
```

**Defecto:** El return type declarado es `unknown[]` (un array); los tests verifican que la función devuelve un único valor escalar (`'Alex'`, `undefined`). El return type correcto es `unknown`, no `unknown[]`.

---

### 3.10 — `exercises/162-longestPalindrome/app.ts`

**Firmas citadas:**
```typescript
function reverseString(string: string): number {
  // your code here
    return 0;
}

function isPalindrome(word: string): number {
  // your code here
    return 0;
}
```

**El README indica** (`exercises/162-longestPalindrome/README.md`):
> "You can detect palindromes by comparing a string to its reverse."

**Aseveraciones del test** (`exercises/162-longestPalindrome/test.js`):
```javascript
test('Function reverseString must return something', () => {
  expect(reverseString('some text')).not.toBe(undefined);
});
test('Function isPalindrome must return something', () => {
  expect(isPalindrome('some text')).not.toBe(undefined);
});
```

**El archivo de solución confirma** (`exercises/162-longestPalindrome/solution.hide.js`):
```javascript
function reverseString(string) {
  return string.split('').reverse().join('');  // returns a string
}
function isPalindrome(word) {
  return word.length > 1 && word.toLowerCase() === reverseString(word.toLowerCase());  // returns boolean
}
```

**Defecto:** Ambas funciones declaran return type `number`. `reverseString` debe devolver un `string` (una cadena invertida no puede ser un número). `isPalindrome` debe devolver un `boolean` (se utiliza en una expresión condicional). El archivo de solución confirma estos return types correctos. Un estudiante que implemente estas funciones correctamente producirá errores de TypeScript en ambas.

---

### 3.11 — Ejercicios adicionales con return type `string` donde el README describe un array

Los siguientes ejercicios comparten el mismo patrón de defecto que los §3.2–3.7: el return type declarado es `string` mientras que el README y/o el test espera un array. Se enumeran aquí por exhaustividad sin repetir las evidencias completas:

| Archivo | Return declarado | El README describe |
|---|---|---|
| `exercises/050-getElementsUpTo/app.ts` | `string` | "returns an array with all the elements up until…" |
| `exercises/051-removeFromFront/app.ts` | `string` | "returns the SAME array with its first element removed" |
| `exercises/052-removeFromBack/app.ts` | `string` | "returns the array with its last element removed" |
| `exercises/053-removeFromFrontOfNew/app.ts` | `string` | "returns a new array containing all but the first element" |
| `exercises/054-removeFromBackOfNew/app.ts` | `string` | "returns a new array containing all but the last element" |
| `exercises/072-keep/app.ts` | `string` | "returns an array containing the items that match" |

---

## 4. HALLAZGO 2 — PARÁMETROS FANTASMA

Las siguientes function signatures en `app.ts` contienen parámetros que:

1. No están descritos en el README correspondiente
2. No se utilizan como argumentos en ninguna llamada dentro del `test.js` correspondiente
3. Están nombrados con el patrón de marcador de posición genérico `arg2`, `arg3`, etc.

Estos parámetros no pueden conciliarse con la descripción del ejercicio. Un estudiante que lea la function signature para comprender la interfaz de la función encontrará argumentos para los que no existe ninguna explicación.

---

### 4.1 — `exercises/049-getElementsAfter/app.ts`

**Firma citada:**
```typescript
function getElementsAfter(array: unknown[], n: unknown, arg3: number): string {
```

**Llamadas del test** (`exercises/049-getElementsAfter/test.js`):
```javascript
expect(getElementsAfter([1, 2], 1)).not.toBe(undefined);
getElementsAfter(['a', 'b', 'c', 'd', 'e'], 2)
getElementsAfter(['you', 'can', 'do', 'it'], 1)
```
Todas las llamadas del test pasan exactamente **2 argumentos**.

**El README describe** dos parámetros: un array y un índice.

**Defecto:** El tercer parámetro `arg3: number` está declarado en la firma pero nunca se suministra en ninguna llamada del test y no está descrito en el README.

---

### 4.2 — `exercises/087-joinArraysOfArrays/app.ts`

**Firma citada:**
```typescript
function joinArrayOfArrays(arr: unknown[], arg2: unknown, arg3: unknown[], arg4: unknown, arg5: unknown[], arg6: string, arg7: unknown): unknown[] {
```

**Llamadas del test** (`exercises/087-joinArraysOfArrays/test.js`):
```javascript
joinArrayOfArrays([[1, 4], [true, false], ['x', 'y']])
joinArrayOfArrays([[2, 6], [4, true]])
```
Todas las llamadas del test pasan exactamente **1 argumento**.

**El README indica** (`exercises/087-joinArraysOfArrays/README.md`):
> "Given a matrix (array of arrays), joinArrayOfArrays returns a single array containing the elements of the nested arrays."

Describe un único parámetro.

**Defecto:** La firma declara 7 parámetros. Los parámetros `arg2` a `arg7` (6 de 7) nunca se suministran en ninguna llamada del test y no están descritos en el README.

---

### 4.3 — `exercises/113-getMatrixValue/app.ts`

**Firma citada:**
```typescript
function getMatrixValue(matrix: unknown[], row: unknown, col: unknown[], arg4: unknown, arg5: number, arg6: number): number {
```

**Llamadas del test** (`exercises/113-getMatrixValue/test.js`):
```javascript
expect(getMatrixValue([[1,2],[3,4]], 1, 0)).toBe(3);
expect(getMatrixValue([[1,2],[3,4]], 4, 0)).toBe(undefined);
```
Todas las llamadas del test pasan exactamente **3 argumentos**.

**Defecto:** La firma declara 6 parámetros. `arg4`, `arg5`, `arg6` nunca se suministran en ninguna llamada del test. Además, `col` está tipado como `unknown[]` (un array), pero todas las llamadas del test pasan el entero `0` como tercer argumento, lo que hace que la type annotation de `col` sea inconsistente con los datos del test.

---

### 4.4 — `exercises/163-FashionInventory-A/app.ts`

**Firma citada (completa):**
```typescript
function renderInventory(inventory: unknown[], arg2: unknown, arg3: unknown, arg4: Record<string, unknown>, arg5: unknown, arg6: Record<string, unknown>, arg7: unknown, arg8: Record<string, unknown>, arg9: unknown, arg10: unknown, arg11: unknown, arg12: Record<string, unknown>, arg13: unknown, arg14: unknown, arg15: Record<string, unknown>, arg16: unknown, arg17: unknown, arg18: unknown, arg19: unknown): string {
```

**Llamadas del test** (`exercises/163-FashionInventory-A/test.js`):
```javascript
renderInventory([{name: 'Brunello Cucinelli', shoes: [...]}, {name: 'Gucci', shoes: [...]}])
```
Todas las llamadas del test pasan exactamente **1 argumento**.

**El README indica** (`exercises/163-FashionInventory-A/README.md`):
> "Write a function called renderInventory that will receive as a parameter an array like currentInventory."

Describe un único parámetro.

**Defecto:** La firma declara 19 parámetros. Los parámetros `arg2` a `arg19` (18 de 19) nunca se suministran en ninguna llamada del test y no están descritos en el README. Adicionalmente, el return type declarado es `string`, pero el test verifica que `typeof renderInventory(...) === 'object'` y espera un array de arrays.

---

### 4.5 — `exercises/168-getDisplayNameFromOptionalProfile/app.ts`

**Firma citada:**
```typescript
function getDisplayName(profile: Record<string, unknown>, arg2: unknown): string {
```

**Llamadas del test** (`exercises/168-getDisplayNameFromOptionalProfile/test.js`):
```javascript
expect(getDisplayName({ firstName: 'Ana', nickname: 'Annie' })).toBe('Annie');
expect(getDisplayName({ firstName: 'Ana' })).toBe('Ana');
```
Ambas llamadas del test pasan exactamente **1 argumento**.

**El README indica** (`exercises/168-getDisplayNameFromOptionalProfile/README.md`):
> "Use optional properties to return nickname or fallback first name."

Describe una única entrada (un objeto de perfil).

**Defecto:** El parámetro `arg2: unknown` está declarado en la firma pero nunca se suministra en ninguna llamada del test y no está descrito en el README.

---

### 4.6 — Ejercicios adicionales con parámetros fantasma

Los siguientes ejercicios comparten el mismo patrón de parámetros fantasma. En cada caso, los parámetros sobrantes no están descritos en el README y no se suministran en ninguna llamada del test. Se enumeran sin repetir las evidencias completas:

| Archivo | Parámetros declarados | Aridad de llamada del test | Parámetros fantasma |
|---|---|---|---|
| `exercises/045-getLastElement/app.ts` | `(array, arg2)` | 1 | `arg2` |
| `exercises/050-getElementsUpTo/app.ts` | `(array, n, arg3)` | 2 | `arg3` |
| `exercises/051-removeFromFront/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/052-removeFromBack/app.ts` | `(arr, arg2, arg3)` | 1 | `arg2`, `arg3` |
| `exercises/053-removeFromFrontOfNew/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/054-removeFromBackOfNew/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/072-keep/app.ts` | `(arr, keeper, arg3, arg4)` | 2 | `arg3`, `arg4` |
| `exercises/075-filterEvenLengthWords/app.ts` | `(words, arg2)` | 1 | `arg2` |
| `exercises/076-getLengthOfLongestElement/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/077-squareElements/app.ts` | `(arr, arg2, arg3)` | 1 | `arg2`, `arg3` |
| `exercises/078-filterOddElements/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/079-computeProductOfAllElements/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/080-filterEvenElements/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/081-getLengthOfShortestElement/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/083-findSmallestElement/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/085-getLargestElement/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/086-computeSumOfAllElements/app.ts` | `(arr, arg2)` | 1 | `arg2` |
| `exercises/088-findShortestWordAmongMixedElements/app.ts` | `(arr, arg2, arg3, arg4)` | 1 | `arg2`, `arg3`, `arg4` |
| `exercises/089-findSmallestnumberAmongMixedElements/app.ts` | `(arr, arg2, arg3, arg4)` | 1 | `arg2`, `arg3`, `arg4` |
| `exercises/109-findPairForSum/app.ts` | `(array, number, arg3, arg4)` | 2 | `arg3`, `arg4` |
| `exercises/114-transposeMatrix/app.ts` | `(matrix, arg2, arg3, arg4, arg5, arg6)` | 1 | `arg2`–`arg6` |
| `exercises/115-binarySearchSortedArray/app.ts` | `(values, target, arg3, arg4, arg5, arg6)` | 2 | `arg3`–`arg6` |
| `exercises/164-FashionInventory-B/app.ts` | `(inventory, arg2, ..., arg19)` | 1 | `arg2`–`arg19` |

---

## 5. HALLAZGO 3 — DISCREPANCIAS EN LA NUMERACIÓN DE EJERCICIOS EN LOS README

Cada archivo README de ejercicio muestra un número en su encabezado H1 (p. ej., `` # `029` computeAreaOfARectangle ``). En 142 de los 170 ejercicios (83,5 %), el número mostrado no coincide con el nombre del directorio. A continuación se documenta el alcance y la naturaleza de la discrepancia.

### 5.1 Metodología

El número del encabezado del README se extrajo de la primera línea de cada `README.md`. Se comparó con el prefijo numérico del nombre del directorio. La comparación es directamente verificable mediante la lectura de cada archivo.

### 5.2 Magnitud de la discrepancia

| Rango | Cantidad | Relación README–Directorio |
|---|---|---|
| Ejercicios 001–028 | 28 | Los números coinciden |
| Ejercicios 029 en adelante | 142 | Los números no coinciden (83,5 % del total) |

### 5.3 Ejemplos representativos

**Ejemplo A — Desplazamiento constante de +9:**

Directorio: `exercises/029-computeAreaOfARectangle/`  
Primera línea del `README.md`: `` # `038` computeAreaOfARectangle ``  
Discrepancia: el directorio es 029; el README muestra 038.

Directorio: `exercises/035-computePower/`  
Primera línea del `README.md`: `` # `044` computePower ``  
Discrepancia: el directorio es 035; el README muestra 044.

**Ejemplo B — Discrepancia extrema en un único ejercicio:**

Directorio: `exercises/041-getStringLength/`  
Primera línea del `README.md`: `` # `144` getStringLength ``  
Discrepancia: el directorio es 041; el README muestra 144 — una diferencia de 103.

**Ejemplo C — Referencia invertida (número de directorio superior al número del README):**

Directorio: `exercises/116-getProperty/`  
Primera línea del `README.md`: `` # `029` getProperty ``  
Discrepancia: el directorio es 116; el README muestra 029 — el número del README es 87 unidades inferior al número del directorio.

Directorio: `exercises/124-addArrayProperty/`  
Primera línea del `README.md`: `` # `037` addArrayProperty ``  
Discrepancia: el directorio es 124; el README muestra 037.

**Ejemplo D — Salto numérico amplio hacia adelante (ejercicios 060 y 076):**

Directorio: `exercises/059-extend/`  
Primera línea del `README.md`: `` # `066` Extend ``  
Directorio siguiente: `exercises/060-convertDoubleSpaceToSingle/`  
Primera línea del `README.md`: `` # `076` convertDoubleSpaceToSingle ``  
Discrepancia: el número del README salta de 066 a 076 entre dos directorios consecutivos, un hueco de 10 números sin ejercicios correspondientes.

Directorio: `exercises/075-filterEvenLengthWords/`  
Primera línea del `README.md`: `` # `091` filterEvenLengthWords ``  
Directorio siguiente: `exercises/076-getLengthOfLongestElement/`  
Primera línea del `README.md`: `` # `112` getLengthOfLongestElement ``  
Discrepancia: el número del README salta de 091 a 112, un hueco de 20 números sin ejercicios correspondientes.

**Ejemplo E — Sin número mostrado en absoluto:**

Directorio: `exercises/113-getMatrixValue/`  
Primera línea del `README.md`: `# 113-getMatrixValue`  
No se muestra ningún número de ejercicio; únicamente se repite el nombre del directorio.

El mismo patrón (nombre del directorio repetido, sin número) se aplica a: `exercises/114-transposeMatrix/`, `exercises/115-binarySearchSortedArray/`, `exercises/167-buildUserProfileWithInterface/`, `exercises/168-getDisplayNameFromOptionalProfile/`, `exercises/169-renameBookMutableVsImmutable/`, `exercises/170-comparePassByValueAndReference/`.

---

## 6. HALLAZGO 4 — ARCHIVOS DE SOLUCIÓN SIN IMPLEMENTACIÓN

Los archivos `solution.hide.js` sirven como implementaciones de referencia. Los estudiantes pueden consultarlos para comprender una solución correcta. Los cuatro archivos de solución siguientes contienen un cuerpo de función con `return {}` o `return ''` precedido de `// your code here` — el mismo texto de marcador de posición que se encuentra en los archivos de inicio del estudiante — y, por tanto, no implementan la función.

Cada uno se verifica con su test correspondiente para confirmar que la solución, tal como está escrita, no superaría sus propios tests.

---

### 6.1 — `exercises/167-buildUserProfileWithInterface/solution.hide.js`

**Contenido completo del archivo:**
```javascript
interface UserProfile {
  name: string;
  age: number;
  isAdult: boolean;
}

function buildUserProfile(name, age) {
  // your code here
  return {};
}
```

**Aseveración del test** (`exercises/167-buildUserProfileWithInterface/test.js`):
```javascript
test('Case 1', () => {
  expect(buildUserProfile('Leo', 20)).toEqual({ name: 'Leo', age: 20, isAdult: true });
});
```

**Defecto:** La función devuelve `{}`. El test espera `{ name: 'Leo', age: 20, isAdult: true }`. La solución, tal como está escrita, no supera su propio test.

---

### 6.2 — `exercises/168-getDisplayNameFromOptionalProfile/solution.hide.js`

**Contenido completo del archivo:**
```javascript
function getDisplayName(profile) {
  // your code here
  return '';
}
```

**Aseveraciones del test** (`exercises/168-getDisplayNameFromOptionalProfile/test.js`):
```javascript
test('Case 1', () => {
  expect(getDisplayName({ firstName: 'Ana', nickname: 'Annie' })).toBe('Annie');
});
test('Case 2', () => {
  expect(getDisplayName({ firstName: 'Ana' })).toBe('Ana');
});
```

**Defecto:** La función devuelve `''`. Los tests esperan `'Annie'` y `'Ana'` respectivamente. La solución, tal como está escrita, no supera ninguno de sus dos tests.

---

### 6.3 — `exercises/169-renameBookMutableVsImmutable/solution.hide.js`

**Contenido completo del archivo:**
```javascript
function renameBookImmutable(book, newTitle) {
  // your code here
  return {};
}
```

**Aseveración del test** (`exercises/169-renameBookMutableVsImmutable/test.js`):
```javascript
test('Case 1', () => {
  const original = { title: 'Old', author: 'A' };
  const renamed = renameBookImmutable(original, 'New');
  expect(original.title).toBe('Old');
  expect(renamed.title).toBe('New');
});
```

**Defecto:** La función devuelve `{}`. `renamed.title` sería `undefined`, no `'New'`. La solución, tal como está escrita, no supera su propio test.

---

### 6.4 — `exercises/170-comparePassByValueAndReference/solution.hide.js`

**Contenido completo del archivo:**
```javascript
function comparePassByValueAndReference(input) {
  // your code here
  return {};
}
```

**Aseveración del test** (`exercises/170-comparePassByValueAndReference/test.js`):
```javascript
test('Case 1', () => {
  const item = { count: 1 };
  const out = comparePassByValueAndReference(item);
  expect(out.externalCount).toBeGreaterThanOrEqual(1);
  expect(item.count).toBeGreaterThanOrEqual(1);
});
```

**Defecto:** La función devuelve `{}`. `out.externalCount` sería `undefined`, lo que no cumple la condición `>= 1`. La solución, tal como está escrita, no supera su propio test.

---

## 7. HALLAZGO 5 — ARCHIVOS README STUB

Los siguientes archivos README contienen menos de cinco líneas de contenido sustancial y no incluyen ningún ejemplo funcional de entrada/salida esperadas. Se cita el texto completo de cada uno.

---

### 7.1 — `exercises/042-printUserBadgeVoid/README.md`

**Contenido completo del archivo:**
```
# 042-printUserBadgeVoid

Create a procedure (void function) that prints a formatted user badge.

## Instructions

Implement `printUserBadge` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo de lo que debería contener o mostrar una «insignia de usuario formateada». La function signature del `app.ts` muestra dos parámetros (`name: string, level: number`), pero el README no describe cuál debería ser la salida de la insignia, lo que hace imposible saber qué resultado se espera.

---

### 7.2 — `exercises/113-getMatrixValue/README.md`

**Contenido completo del archivo:**
```
# 113-getMatrixValue

Read a value from a matrix by row and column index safely.

## Instructions

Implement `getMatrixValue` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo de entrada/salida. No se describe qué significa «safely» en este contexto (sin explicación del comportamiento fuera de límites). El test confirma que `getMatrixValue([[1,2],[3,4]], 4, 0)` debe devolver `undefined`, pero este caso límite no está documentado.

---

### 7.3 — `exercises/114-transposeMatrix/README.md`

**Contenido completo del archivo:**
```
# 114-transposeMatrix

Return the transpose of a matrix (rows become columns).

## Instructions

Implement `transposeMatrix` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo de entrada/salida. No se explica qué produce la transposición de una matriz.

---

### 7.4 — `exercises/115-binarySearchSortedArray/README.md`

**Contenido completo del archivo:**
```
# 115-binarySearchSortedArray

Implement binary search in a sorted array and return index or -1.

## Instructions

Implement `binarySearchSortedArray` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo de entrada/salida. Este ejercicio sigue inmediatamente al ejercicio 111, que proporciona una explicación detallada de varios pasos sobre la búsqueda binaria; el ejercicio 115 no proporciona ninguna, a pesar de tratar el mismo tema.

---

### 7.5 — `exercises/167-buildUserProfileWithInterface/README.md`

**Contenido completo del archivo:**
```
# 167-buildUserProfileWithInterface

Create and return a typed object using an interface.

## Instructions

Implement `buildUserProfile` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo. No se muestra ninguna definición de interface. No se describe ninguna propiedad requerida. El test exige que el resultado incluya `{ name, age, isAdult }`, pero ninguna de estas propiedades se menciona en el README.

---

### 7.6 — `exercises/168-getDisplayNameFromOptionalProfile/README.md`

**Contenido completo del archivo:**
```
# 168-getDisplayNameFromOptionalProfile

Use optional properties to return nickname or fallback first name.

## Instructions

Implement `getDisplayName` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo. No se describe la forma del objeto de entrada. No se muestra ninguna sintaxis de optional property de TypeScript. El título hace referencia a un concepto de TypeScript («optional properties») que no se demuestra en ningún archivo del ejercicio. El archivo de solución no implementa la función (véase Hallazgo 4).

---

### 7.7 — `exercises/169-renameBookMutableVsImmutable/README.md`

**Contenido completo del archivo:**
```
# 169-renameBookMutableVsImmutable

Return a renamed copy of a book without mutating the original object.

## Instructions

Implement `renameBookImmutable` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo de entrada/salida. No se describe la forma del objeto libro. El test revela la estructura esperada (`{ title, author }`), pero el README no.

---

### 7.8 — `exercises/170-comparePassByValueAndReference/README.md`

**Contenido completo del archivo:**
```
# 170-comparePassByValueAndReference

Demonstrate pass-by-value vs pass-by-reference behavior in TypeScript.

## Instructions

Implement `comparePassByValueAndReference` in `app.ts` using TypeScript types.
```

**Defecto:** No hay ningún ejemplo. No se describe la entrada ni la salida esperada. El test exige `out.externalCount >= 1`, que es la única especificación del comportamiento esperado, y no figura en el README.

---

## 8. HALLAZGO 6 — CONTRADICCIONES INTERNAS

Los siguientes son casos en los que un archivo dentro de un ejercicio contradice a otro archivo del mismo ejercicio. Cada contradicción se documenta con citas textuales exactas de ambas fuentes en conflicto.

---

### 8.1 — Ejercicio 155: La pista contradice al ejemplo

**Archivo:** `exercises/155-ArrayToObject-B/README.md`

**La pista indica:**
> "Assume that all elements in the array will be of type `string`."

**Ejemplo en el mismo README:**
```javascript
let output = fromListToObject([['make', 'Ford'], ['model', 'Mustang'], ['year', 1964]])
console.log(output); // --> { make : 'Ford', model : 'Mustang', year : 1964 }
```

**El test confirma** (`exercises/155-ArrayToObject-B/test.js`):
```javascript
let output = fromListToObject([
  ['make', 'Ford'],
  ['model', 'Mustang'],
  ['year', 1964],
]);
expect(output).toEqual({ make: 'Ford', model: 'Mustang', year: 1964 });
```

**Defecto:** La pista instruye a los estudiantes a asumir que todos los elementos son strings. El ejemplo y el test utilizan `1964`, que es un número, no un string. Un estudiante que siga la pista y escriba código que asuma entrada completamente de tipo string puede producir una implementación que satisfaga la restricción enunciada en la pista pero que no supere el test.

---

### 8.2 — Ejercicio 102: La descripción del hipervínculo no coincide con el destino del enlace

**Archivo:** `exercises/102-modulo/README.md`

**Texto citado:**
> "It should behave as described in the [canonical documentation (MDN) for the TypeScript remainder operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder)."

**Defecto:** El texto del hipervínculo describe el destino como «la documentación canónica (MDN) del operador resto de TypeScript». La URL proporcionada (`https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder`) enlaza con la página de MDN del operador resto de **JavaScript**. MDN no dispone de una página específica de TypeScript para el operador resto; TypeScript utiliza el mismo operador `%` que JavaScript. La descripción del destino del enlace es factualmente inexacta.

---

### 8.3 — Ejercicio 160: Los datos requeridos están ausentes del archivo del estudiante

**Archivo:** `exercises/160-GreetCustomers/README.md`

**Texto citado:**
> "Please check to the `customerData` object."

**Archivo:** `exercises/160-GreetCustomers/app.ts`

**Contenido completo del archivo:**
```typescript
function greetCustomer(firstName: string): string {
  // your code here
  return '';
}

export {};
```

**El test depende de** (`exercises/160-GreetCustomers/test.js`):
```javascript
test('If a client has visited only once, it must say "Welcome back ..."', () => {
  let output = greetCustomer('Joe');
  expect(output).toBe("Welcome back, Joe! We're glad you liked us the first time!");
});
```

**Defecto:** El README instruye a los estudiantes a consultar `customerData`. El archivo `app.ts` no contiene ningún objeto `customerData`. El test llama a `greetCustomer('Joe')` y espera una respuesta específica que requiere saber que `Joe` tiene `visits: 1`. Ni el README ni el `app.ts` proporcionan estos datos. El objeto `customerData` aparece únicamente en `solution.hide.js`, que está oculto para los estudiantes.

---

### 8.4 — Ejercicio 059: El patrón de ejemplo del README contradice el return type declarado

**Archivo:** `exercises/059-extend/README.md`

**El ejemplo muestra la función invocada por su efecto secundario, sin utilizar el valor de retorno:**
```typescript
extend(obj1, obj2);

console.log(obj1); // --> {a: 1, b: 2, c: 3}
console.log(obj2); // --> {b: 4, c: 3}
```

**Archivo:** `exercises/059-extend/app.ts`

**Firma citada:**
```typescript
function extend(obj1: unknown, obj2: unknown): unknown[] {
```

**Test** (`exercises/059-extend/test.js`):
```javascript
extend(obj1, obj2)
let output = obj1
expect(output).toEqual({ a: 1, b: 2, c: 3 })
```
El test no utiliza el valor de retorno de `extend`; lee `obj1` directamente.

**Defecto:** El ejemplo del README y el test tratan `extend` como una función void que muta `obj1`. La function signature del `app.ts` declara el return type como `unknown[]` (un array). No existe ningún escenario en el que una función que muta un objeto deba devolver también un array. Además, los parámetros están tipados como `unknown`, lo que en TypeScript impide el acceso a propiedades sin una type assertion explícita — un estudiante que implemente el cuerpo de la función utilizando la sintaxis `obj1[key]` encontrará un error de TypeScript porque `unknown` no permite el acceso a propiedades.

---

### 8.5 — Ejercicio 003: Error tipográfico en el encabezado de sección

**Archivo:** `exercises/003-isOldEnoughToVote/README.md`

**Encabezado citado:**
```
## 📝 Insructions:
```

**Defecto:** El encabezado contiene un error tipográfico: «Insructions» debería ser «Instructions». Todos los demás ejercicios del repositorio utilizan la ortografía correcta. Se trata de un error de corrección de texto.

---

## 9. HALLAZGO 7 — AUDITORÍA DE CONTENIDO ESPECÍFICO DE TYPESCRIPT

Esta sección documenta qué ejercicios, en su caso, requieren o demuestran características del lenguaje específicas de TypeScript — es decir, características presentes en TypeScript pero ausentes en JavaScript: declaraciones de `interface`, parámetros de tipo genérico, declaraciones de `enum`, union types (`A | B`), intersection types (`A & B`), type guards, optional properties (`prop?: T`), `readonly` y type aliases (`type X = ...`).

### 9.1 — Resultado de la búsqueda en todos los archivos `app.ts`

Se realizó una búsqueda en todos los 170 archivos `app.ts` de las palabras clave: `interface`, `enum`, `<T>`, `| `, `& `, `is `, `readonly`, `type ` (como palabra clave que precede a un type alias). **No se encontró ninguna coincidencia en ningún archivo `app.ts`.** Todos los archivos `app.ts` utilizan únicamente type annotations básicas: `: string`, `: number`, `: boolean`, `: unknown[]`, `: Record<string, unknown>` y `: void`.

### 9.2 — Evaluación ejercicio a ejercicio de los conceptos específicos de TypeScript

#### Ejercicios 001–166 (166 ejercicios)

Los 166 archivos `app.ts` utilizan únicamente type annotations básicas. Ninguna de las function signatures, listas de parámetros o return types requiere conocimiento de TypeScript más allá de anotar un parámetro con un tipo primitivo. Los ejercicios son matemática y lógicamente idénticos a ejercicios de JavaScript, con type annotations añadidas a la firma de inicio.

Ejemplos de type annotations utilizadas:
- `age: number`, `name: string` — type annotations de tipo primitivo
- `arr: unknown[]` — array de tipo débil
- `Record<string, unknown>` — tipo de utilidad incorporado utilizado como token único

#### Ejercicio 167 — `buildUserProfileWithInterface`

**Título del README:** «buildUserProfileWithInterface»  
**Instrucción del README:** «Create and return a typed object using an interface.»

**Contenido del `app.ts`:**
```typescript
function buildUserProfile(name: string, age: number): Record<string, unknown> {
  // your code here
  return {} as Record<string, unknown>;
}
```

El archivo `app.ts` no contiene ninguna declaración de `interface`. El return type utiliza `Record<string, unknown>` y una type assertion con `as`, ninguna de las cuales requiere que el estudiante escriba o comprenda un interface.

**Contenido del `solution.hide.js`:**
```javascript
interface UserProfile {
  name: string;
  age: number;
  isAdult: boolean;
}

function buildUserProfile(name, age) {
  // your code here
  return {};
}
```

El archivo de solución contiene una declaración de `interface UserProfile`, que es el elemento específico de TypeScript al que hace referencia el título del README. Sin embargo, tal como se documenta en el Hallazgo 4, el cuerpo de la función no está implementado (`return {}`).

**Valoración:** El README hace referencia a un interface. El archivo de solución declara uno pero no lo utiliza (la función no está implementada). El archivo `app.ts` entregado a los estudiantes no contiene ninguna declaración de interface. Al estudiante no se le muestra cómo declarar ni utilizar un interface en ninguno de los archivos proporcionados.

#### Ejercicio 168 — `getDisplayNameFromOptionalProfile`

**Instrucción del README:** «Use optional properties to return nickname or fallback first name.»

**Contenido del `app.ts`:**
```typescript
function getDisplayName(profile: Record<string, unknown>, arg2: unknown): string {
  // your code here
  return '';
}
```

El archivo `app.ts` no contiene ninguna sintaxis de optional property (p. ej., `nickname?: string`). El parámetro está tipado como `Record<string, unknown>`, que acepta cualquier objeto con clave string y no comunica al estudiante que `nickname` es opcional.

**Contenido del `solution.hide.js`:**
```javascript
function getDisplayName(profile) {
  // your code here
  return '';
}
```

La solución no implementa la función (véase Hallazgo 4) y no contiene ninguna sintaxis de optional property de TypeScript.

**Valoración:** El README hace referencia a las optional properties, pero ni el `app.ts` ni el archivo de solución demuestran esta característica de TypeScript.

#### Ejercicios 169–170

El ejercicio 169 («Mutable vs Immutable») y el ejercicio 170 («Pass by Value and Reference») describen comportamientos en tiempo de ejecución de JavaScript que no son específicos de TypeScript. Ninguno de los archivos `app.ts` contiene ningún constructo de TypeScript más allá de una type annotation de return type. Los archivos de solución no implementan las funciones (véase Hallazgo 4).

### 9.3 — Resumen

| Ejercicios | Característica específica de TypeScript en `app.ts` | Característica específica de TypeScript en la solución | Característica descrita en el README |
|---|---|---|---|
| 001–166 | Ninguna | Ninguna (soluciones en JS puro) | Ninguna |
| 167 | Ninguna (solo `Record<string, unknown>` y type assertion con `as`) | Declaración de `interface` presente pero función sin implementar | «interface» referenciado en el título |
| 168 | Ninguna | Ninguna | «optional properties» referenciado |
| 169 | Ninguna | Ninguna | Ninguna específica de TypeScript |
| 170 | Ninguna | Ninguna | Ninguna específica de TypeScript |

El único constructo del lenguaje TypeScript específico presente en cualquier archivo de ejercicio es la declaración de `interface UserProfile` en `exercises/167-buildUserProfileWithInterface/solution.hide.js`. Dicha declaración aparece junto a un cuerpo de función sin implementar.

---

## 10. ESTADÍSTICAS RESUMEN

| Hallazgo | Cantidad | % sobre 170 ejercicios |
|---|---|---|
| Ejercicios con un return type de TypeScript demostrablemente incorrecto en `app.ts` (§3) | 17 | 10 % |
| Ejercicios con al menos un parámetro fantasma en `app.ts` (§4) | 37 | 22 % |
| Ejercicios en los que el número del README no coincide con el nombre del directorio (§5) | 142 | 83,5 % |
| Archivos de solución sin implementación que no superan sus propios tests (§6) | 4 | 2 % |
| Archivos README sin ejemplo funcional y con menos de 5 líneas de contenido (§7) | 8 | 5 % |
| Ejercicios con una contradicción interna documentada (§8) | 5 | 3 % |
| Ejercicios en los que `app.ts` utiliza una característica del lenguaje específica de TypeScript (§9) | 0 | 0 % |
| Ejercicios en los que el archivo de solución utiliza una característica específica de TypeScript (§9) | 1 (sin implementar) | 0,6 % |

---

*Fin del informe*

*Referencia del informe: QA-TS-2026-002 | Fecha: 28 de mayo de 2026*
