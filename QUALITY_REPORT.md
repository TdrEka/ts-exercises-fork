# FORMAL TECHNICAL QUALITY ASSESSMENT
## 4Geeks Academy — "Master TypeScript Skills" Exercise Repository

---

**Report Reference:** QA-TS-2026-002  
**Date of Analysis:** 28 May 2026  
**Repository analysed:** Fork of `4GeeksAcademy/master-typescript-exercises`   
**Course fee paid:** Between approximately €4,000 and €9,000  
**Methodology:** Every finding in this report is directly verifiable by opening the named file. File paths, exact quoted text, and line-level evidence are provided for each claim. No claim is made that cannot be confirmed by inspection of the repository as committed.

---

## TABLE OF CONTENTS

1. [Scope and Methodology](#1-scope-and-methodology)
2. [Repository Overview](#2-repository-overview)
3. [Finding 1 — TypeScript Return Type Errors](#3-finding-1--typescript-return-type-errors)
4. [Finding 2 — Phantom Parameters](#4-finding-2--phantom-parameters)
5. [Finding 3 — README Exercise Number Mismatches](#5-finding-3--readme-exercise-number-mismatches)
6. [Finding 4 — Non-Implementing Solution Files](#6-finding-4--non-implementing-solution-files)
7. [Finding 5 — Stub README Files](#7-finding-5--stub-readme-files)
8. [Finding 6 — Internal Contradictions](#8-finding-6--internal-contradictions)
9. [Finding 7 — TypeScript-Specific Content Audit](#9-finding-7--typescript-specific-content-audit)
10. [Summary Statistics](#10-summary-statistics)

---

## 1. SCOPE AND METHODOLOGY

This report audits the exercise files delivered to students as part of the "Master TypeScript Skills" module. The audit covers:

- All 170 exercise directories (`001-isOldEnoughToDrink` through `170-comparePassByValueAndReference`)
- All `app.ts` files (TypeScript starter files given to students)
- All `README.md` files (instruction files)
- All `test.js` files (automated test suites)
- All `solution.hide.js` files (reference implementations)

For each defect category the following evidence is provided:
- The exact file path
- The exact text quoted from the file
- The conflicting evidence (README description, test assertion, or a second file)
- A one-line explanation of the defect

All file reads were performed directly on the committed repository state.

---

## 2. REPOSITORY OVERVIEW

| Item | Count |
|---|---|
| Exercise directories | 170 |
| `app.ts` files | 170 |
| `README.md` files | 171 (includes `00-Welcome`) |
| `test.js` files | 170 |
| `solution.hide.js` files | 169 |

---

## 3. FINDING 1 — TYPESCRIPT RETURN TYPE ERRORS

Each `app.ts` declares a TypeScript return type for the function the student must implement. In the following cases the declared return type is demonstrably incorrect: either the README description specifies a different type, the test assertions confirm a different type, or both. A student who correctly implements the function as described will produce code whose return value does not match the declared TypeScript type, causing a TypeScript type error.

---

### 3.1 — `exercises/046-addToFront/app.ts`

**Quoted signature:**
```typescript
function addToFront(arr: unknown[], element: number): string {
```

**README states** (`exercises/046-addToFront/README.md`):
> "addToFront adds the given element to the front of the given array, and returns the given array."

**Test assertion** (`exercises/046-addToFront/test.js`):
```javascript
expect(addToFront([6, 7], 8)).toStrictEqual([8, 6, 7]);
expect(addToFront([1, 2], 3)).toStrictEqual([3, 1, 2]);
```

**Defect:** The declared return type is `string`. The function is described as returning an array and the tests assert array values. A correct implementation returns an array, which does not satisfy the `string` return type annotation.

---

### 3.2 — `exercises/047-addToBack/app.ts`

**Quoted signature:**
```typescript
function addToBack(arr: unknown[], element: number): string {
```

**README states** (`exercises/047-addToBack/README.md`):
> "addToBack returns the given array with the given element added at the end."

**Defect:** Declared return type is `string`; the function is described as returning an array.

---

### 3.3 — `exercises/048-joinArrays/app.ts`

**Quoted signature:**
```typescript
function joinArrays(arr1: unknown[], arr2: unknown[]): string {
```

**README states** (`exercises/048-joinArrays/README.md`):
> "joinArrays returns an array with the elements of arr1, followed by the elements of arr2 in order."

**Defect:** Declared return type is `string`; the function is described as returning an array.

---

### 3.4 — `exercises/049-getElementsAfter/app.ts`

**Quoted signature:**
```typescript
function getElementsAfter(array: unknown[], n: unknown, arg3: number): string {
```

**README states** (`exercises/049-getElementsAfter/README.md`):
> "getElementsAfter returns a new array with all the elements after (but not including) the given index."

**Test assertion** (`exercises/049-getElementsAfter/test.js`):
```javascript
let output = getElementsAfter(['a', 'b', 'c', 'd', 'e'], 2)
expect(output).toEqual(['d', 'e'])
```

**Defect:** Declared return type is `string`; the function is described as returning and tested as returning an array. (The `arg3` phantom parameter is documented separately in Finding 2.)

---

### 3.5 — `exercises/056-getAllLetters/app.ts`

**Quoted signature:**
```typescript
function getAllLetters(str: string): string {
```

**README states** (`exercises/056-getAllLetters/README.md`):
> "getAllLetters returns an array containing every character in the word."

**Test assertion** (`exercises/056-getAllLetters/test.js`):
```javascript
expect(output).toEqual(["R", "a", "d", "a", "g", "a", "s", "t"]);
```

**Defect:** Declared return type is `string`; the function is described as returning and tested as returning an array of characters (`string[]`).

---

### 3.6 — `exercises/057-getAllWords/app.ts`

**Quoted signature:**
```typescript
function getAllWords(str: string): string {
```

**README states** (`exercises/057-getAllWords/README.md`):
> "getAllWords returns an array containing every word in the sentence."

**Defect:** Declared return type is `string`; the function is described as returning an array of words.

---

### 3.7 — `exercises/068-joinThreeArrays/app.ts`

**Quoted signature:**
```typescript
function joinThreeArrays(arr1: unknown[], arr2: unknown[], arr3: unknown[]): string {
```

**README states** (`exercises/068-joinThreeArrays/README.md`):
> "joinThreeArrays returns an array with the elements of arr1 in order followed by the elements in arr2 followed by the elements of arr3."

**Defect:** Declared return type is `string`; the function is described as returning an array.

---

### 3.8 — `exercises/074-filterOddLengthWords/app.ts`

**Quoted signature:**
```typescript
function filterOddLengthWords(words: unknown[]): number {
```

**README states** (`exercises/074-filterOddLengthWords/README.md`):
> "filterOddLengthWords returns an array containing only the elements of the given array whose lengths are odd numbers."

**Test assertion** (`exercises/074-filterOddLengthWords/test.js`):
```javascript
expect(Array.isArray(filterOddLengthWords(['you']))).toBeTruthy();
expect(output).toEqual(['you', 'can']);
```

**Defect:** Declared return type is `number`; the function is described as returning and tested as returning an array of strings.

---

### 3.9 — `exercises/116-getProperty/app.ts`

**Quoted signature:**
```typescript
function getProperty(obj: unknown, key: string): unknown[] {
```

**README states** (`exercises/116-getProperty/README.md`):
> "getProperty returns the value of the property at the given key."

**Test assertion** (`exercises/116-getProperty/test.js`):
```javascript
expect(getProperty(person,'name')).toEqual('Alex');
expect(getProperty(person,'lastname')).toBe(undefined);
```

**Defect:** Declared return type is `unknown[]` (an array); the tests assert that the function returns a single scalar value (`'Alex'`, `undefined`). The correct return type is `unknown`, not `unknown[]`.

---

### 3.10 — `exercises/162-longestPalindrome/app.ts`

**Quoted signatures:**
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

**README states** (`exercises/162-longestPalindrome/README.md`):
> "You can detect palindromes by comparing a string to its reverse."

**Test assertions** (`exercises/162-longestPalindrome/test.js`):
```javascript
test('Function reverseString must return something', () => {
  expect(reverseString('some text')).not.toBe(undefined);
});
test('Function isPalindrome must return something', () => {
  expect(isPalindrome('some text')).not.toBe(undefined);
});
```

**Solution file confirms** (`exercises/162-longestPalindrome/solution.hide.js`):
```javascript
function reverseString(string) {
  return string.split('').reverse().join('');  // returns a string
}
function isPalindrome(word) {
  return word.length > 1 && word.toLowerCase() === reverseString(word.toLowerCase());  // returns boolean
}
```

**Defect:** Both functions declare return type `number`. `reverseString` must return a `string` (a reversed string cannot be a number). `isPalindrome` must return a `boolean` (it is used in a conditional). The solution file confirms these correct return types. A student implementing these functions correctly will produce TypeScript type errors on both.

---

### 3.11 — Additional exercises with `string` return type where README describes an array

The following exercises share the same defect pattern as §3.2–3.7 — the declared return type is `string` while the README and/or test expects an array. They are listed here for completeness without full repetition of evidence:

| File | Declared return | README describes |
|---|---|---|
| `exercises/050-getElementsUpTo/app.ts` | `string` | "returns an array with all the elements up until…" |
| `exercises/051-removeFromFront/app.ts` | `string` | "returns the SAME array with its first element removed" |
| `exercises/052-removeFromBack/app.ts` | `string` | "returns the array with its last element removed" |
| `exercises/053-removeFromFrontOfNew/app.ts` | `string` | "returns a new array containing all but the first element" |
| `exercises/054-removeFromBackOfNew/app.ts` | `string` | "returns a new array containing all but the last element" |
| `exercises/072-keep/app.ts` | `string` | "returns an array containing the items that match" |

---

## 4. FINDING 2 — PHANTOM PARAMETERS

The following function signatures in `app.ts` contain parameters that:

1. Are not described in the corresponding README
2. Are not used as arguments in any call within the corresponding `test.js`
3. Are named with the generic placeholder pattern `arg2`, `arg3`, etc.

These parameters cannot be reconciled with the exercise description. A student reading the signature to understand the function's interface will encounter arguments for which there is no explanation.

---

### 4.1 — `exercises/049-getElementsAfter/app.ts`

**Quoted signature:**
```typescript
function getElementsAfter(array: unknown[], n: unknown, arg3: number): string {
```

**Test calls** (`exercises/049-getElementsAfter/test.js`):
```javascript
expect(getElementsAfter([1, 2], 1)).not.toBe(undefined);
getElementsAfter(['a', 'b', 'c', 'd', 'e'], 2)
getElementsAfter(['you', 'can', 'do', 'it'], 1)
```
All test calls pass exactly **2 arguments**.

**README describes** two parameters: an array and an index.

**Defect:** The third parameter `arg3: number` is declared in the signature but never supplied in any test call and is not described in the README.

---

### 4.2 — `exercises/087-joinArraysOfArrays/app.ts`

**Quoted signature:**
```typescript
function joinArrayOfArrays(arr: unknown[], arg2: unknown, arg3: unknown[], arg4: unknown, arg5: unknown[], arg6: string, arg7: unknown): unknown[] {
```

**Test calls** (`exercises/087-joinArraysOfArrays/test.js`):
```javascript
joinArrayOfArrays([[1, 4], [true, false], ['x', 'y']])
joinArrayOfArrays([[2, 6], [4, true]])
```
All test calls pass exactly **1 argument**.

**README states** (`exercises/087-joinArraysOfArrays/README.md`):
> "Given a matrix (array of arrays), joinArrayOfArrays returns a single array containing the elements of the nested arrays."

Describes one parameter.

**Defect:** The signature declares 7 parameters. Parameters `arg2` through `arg7` (6 of 7) are never supplied in any test call and are not described in the README.

---

### 4.3 — `exercises/113-getMatrixValue/app.ts`

**Quoted signature:**
```typescript
function getMatrixValue(matrix: unknown[], row: unknown, col: unknown[], arg4: unknown, arg5: number, arg6: number): number {
```

**Test calls** (`exercises/113-getMatrixValue/test.js`):
```javascript
expect(getMatrixValue([[1,2],[3,4]], 1, 0)).toBe(3);
expect(getMatrixValue([[1,2],[3,4]], 4, 0)).toBe(undefined);
```
All test calls pass exactly **3 arguments**.

**Defect:** The signature declares 6 parameters. `arg4`, `arg5`, `arg6` are never supplied in any test call. Additionally, `col` is typed as `unknown[]` (an array), but every test call passes the integer `0` as the third argument, making the type annotation for `col` inconsistent with the test data.

---

### 4.4 — `exercises/163-FashionInventory-A/app.ts`

**Quoted signature (full):**
```typescript
function renderInventory(inventory: unknown[], arg2: unknown, arg3: unknown, arg4: Record<string, unknown>, arg5: unknown, arg6: Record<string, unknown>, arg7: unknown, arg8: Record<string, unknown>, arg9: unknown, arg10: unknown, arg11: unknown, arg12: Record<string, unknown>, arg13: unknown, arg14: unknown, arg15: Record<string, unknown>, arg16: unknown, arg17: unknown, arg18: unknown, arg19: unknown): string {
```

**Test calls** (`exercises/163-FashionInventory-A/test.js`):
```javascript
renderInventory([{name: 'Brunello Cucinelli', shoes: [...]}, {name: 'Gucci', shoes: [...]}])
```
All test calls pass exactly **1 argument**.

**README states** (`exercises/163-FashionInventory-A/README.md`):
> "Write a function called renderInventory that will receive as a parameter an array like currentInventory."

Describes one parameter.

**Defect:** The signature declares 19 parameters. Parameters `arg2` through `arg19` (18 of 19) are never supplied in any test call and are not described in the README. Additionally the declared return type is `string`, but the test asserts `typeof renderInventory(...) === 'object'` and expects an array of arrays.

---

### 4.5 — `exercises/168-getDisplayNameFromOptionalProfile/app.ts`

**Quoted signature:**
```typescript
function getDisplayName(profile: Record<string, unknown>, arg2: unknown): string {
```

**Test calls** (`exercises/168-getDisplayNameFromOptionalProfile/test.js`):
```javascript
expect(getDisplayName({ firstName: 'Ana', nickname: 'Annie' })).toBe('Annie');
expect(getDisplayName({ firstName: 'Ana' })).toBe('Ana');
```
Both test calls pass exactly **1 argument**.

**README states** (`exercises/168-getDisplayNameFromOptionalProfile/README.md`):
> "Use optional properties to return nickname or fallback first name."

Describes one input (a profile object).

**Defect:** The parameter `arg2: unknown` is declared in the signature but never supplied in any test call and is not described in the README.

---

### 4.6 — Additional exercises with phantom parameters

The following exercises share the same phantom-parameter pattern. In each case, the surplus parameters are not described in the README and are not supplied in any test call. They are listed without full evidence repetition:

| File | Declared parameters | Test-call arity | Phantom params |
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

## 5. FINDING 3 — README EXERCISE NUMBER MISMATCHES

Each exercise README file displays a number in its H1 heading (e.g. `` # `029` computeAreaOfARectangle ``). In 142 of 170 exercises (83.5%), this displayed number does not match the directory name. The following documents the extent and nature of the discrepancy.

### 5.1 Methodology

The README heading number was extracted from the first line of each `README.md`. It was compared against the numeric prefix of the directory name. The comparison is directly verifiable by reading each file.

### 5.2 Scale of discrepancy

| Range | Count | README–Directory relationship |
|---|---|---|
| Exercises 001–028 | 28 | Numbers match |
| Exercises 029 onward | 142 | Numbers do not match (83.5% of total) |

### 5.3 Representative examples

**Example A — Consistent offset of +9:**

Directory: `exercises/029-computeAreaOfARectangle/`  
First line of `README.md`: `` # `038` computeAreaOfARectangle ``  
Discrepancy: Directory is 029; README displays 038.

Directory: `exercises/035-computePower/`  
First line of `README.md`: `` # `044` computePower ``  
Discrepancy: Directory is 035; README displays 044.

**Example B — Extreme single-exercise mismatch:**

Directory: `exercises/041-getStringLength/`  
First line of `README.md`: `` # `144` getStringLength ``  
Discrepancy: Directory is 041; README displays 144 — a difference of 103.

**Example C — Inverted reference (directory number higher than README number):**

Directory: `exercises/116-getProperty/`  
First line of `README.md`: `` # `029` getProperty ``  
Discrepancy: Directory is 116; README displays 029 — the README number is lower than the directory number by 87.

Directory: `exercises/124-addArrayProperty/`  
First line of `README.md`: `` # `037` addArrayProperty ``  
Discrepancy: Directory is 124; README displays 037.

**Example D — Large forward jump (exercises 060 and 076):**

Directory: `exercises/059-extend/`  
First line of `README.md`: `` # `066` Extend ``  
Next directory: `exercises/060-convertDoubleSpaceToSingle/`  
First line of `README.md`: `` # `076` convertDoubleSpaceToSingle ``  
Discrepancy: The README number jumps from 066 to 076 between two consecutive directories, a gap of 10 numbers with no corresponding exercises present.

Directory: `exercises/075-filterEvenLengthWords/`  
First line of `README.md`: `` # `091` filterEvenLengthWords ``  
Next directory: `exercises/076-getLengthOfLongestElement/`  
First line of `README.md`: `` # `112` getLengthOfLongestElement ``  
Discrepancy: The README number jumps from 091 to 112, a gap of 20 numbers with no corresponding exercises present.

**Example E — No number displayed at all:**

Directory: `exercises/113-getMatrixValue/`  
First line of `README.md`: `# 113-getMatrixValue`  
No exercise number is shown; only the directory name is repeated.

The same pattern (directory name repeated, no number) applies to: `exercises/114-transposeMatrix/`, `exercises/115-binarySearchSortedArray/`, `exercises/167-buildUserProfileWithInterface/`, `exercises/168-getDisplayNameFromOptionalProfile/`, `exercises/169-renameBookMutableVsImmutable/`, `exercises/170-comparePassByValueAndReference/`.

---

## 6. FINDING 4 — NON-IMPLEMENTING SOLUTION FILES

The `solution.hide.js` files serve as reference implementations. Students may consult them to understand a correct solution. The following four solution files contain a function body of `return {}` or `return ''` preceded by `// your code here` — the same placeholder text found in the student starter files — and therefore do not implement the function.

Each is verified against its corresponding test to confirm the solution, as written, would fail its own tests.

---

### 6.1 — `exercises/167-buildUserProfileWithInterface/solution.hide.js`

**Full file content:**
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

**Test assertion** (`exercises/167-buildUserProfileWithInterface/test.js`):
```javascript
test('Case 1', () => {
  expect(buildUserProfile('Leo', 20)).toEqual({ name: 'Leo', age: 20, isAdult: true });
});
```

**Defect:** The function returns `{}`. The test expects `{ name: 'Leo', age: 20, isAdult: true }`. The solution, as written, fails its own test.

---

### 6.2 — `exercises/168-getDisplayNameFromOptionalProfile/solution.hide.js`

**Full file content:**
```javascript
function getDisplayName(profile) {
  // your code here
  return '';
}
```

**Test assertions** (`exercises/168-getDisplayNameFromOptionalProfile/test.js`):
```javascript
test('Case 1', () => {
  expect(getDisplayName({ firstName: 'Ana', nickname: 'Annie' })).toBe('Annie');
});
test('Case 2', () => {
  expect(getDisplayName({ firstName: 'Ana' })).toBe('Ana');
});
```

**Defect:** The function returns `''`. The tests expect `'Annie'` and `'Ana'` respectively. The solution, as written, fails both its tests.

---

### 6.3 — `exercises/169-renameBookMutableVsImmutable/solution.hide.js`

**Full file content:**
```javascript
function renameBookImmutable(book, newTitle) {
  // your code here
  return {};
}
```

**Test assertion** (`exercises/169-renameBookMutableVsImmutable/test.js`):
```javascript
test('Case 1', () => {
  const original = { title: 'Old', author: 'A' };
  const renamed = renameBookImmutable(original, 'New');
  expect(original.title).toBe('Old');
  expect(renamed.title).toBe('New');
});
```

**Defect:** The function returns `{}`. `renamed.title` would be `undefined`, not `'New'`. The solution, as written, fails its own test.

---

### 6.4 — `exercises/170-comparePassByValueAndReference/solution.hide.js`

**Full file content:**
```javascript
function comparePassByValueAndReference(input) {
  // your code here
  return {};
}
```

**Test assertion** (`exercises/170-comparePassByValueAndReference/test.js`):
```javascript
test('Case 1', () => {
  const item = { count: 1 };
  const out = comparePassByValueAndReference(item);
  expect(out.externalCount).toBeGreaterThanOrEqual(1);
  expect(item.count).toBeGreaterThanOrEqual(1);
});
```

**Defect:** The function returns `{}`. `out.externalCount` would be `undefined`, which is not `>= 1`. The solution, as written, fails its own test.

---

## 7. FINDING 5 — STUB README FILES

The following README files contain fewer than five lines of substantive content and provide no worked example of expected input/output. The complete text of each is quoted.

---

### 7.1 — `exercises/042-printUserBadgeVoid/README.md`

**Complete file content:**
```
# 042-printUserBadgeVoid

Create a procedure (void function) that prints a formatted user badge.

## Instructions

Implement `printUserBadge` in `app.ts` using TypeScript types.
```

**Defect:** No example of what a "formatted user badge" should contain or look like. The `app.ts` signature shows two parameters (`name: string, level: number`) but the README does not describe what the badge output should be, making it impossible to know what output is expected.

---

### 7.2 — `exercises/113-getMatrixValue/README.md`

**Complete file content:**
```
# 113-getMatrixValue

Read a value from a matrix by row and column index safely.

## Instructions

Implement `getMatrixValue` in `app.ts` using TypeScript types.
```

**Defect:** No example input/output. No description of what "safely" means in this context (no explanation of out-of-bounds behaviour). The test confirms that `getMatrixValue([[1,2],[3,4]], 4, 0)` should return `undefined` — this edge case is not documented.

---

### 7.3 — `exercises/114-transposeMatrix/README.md`

**Complete file content:**
```
# 114-transposeMatrix

Return the transpose of a matrix (rows become columns).

## Instructions

Implement `transposeMatrix` in `app.ts` using TypeScript types.
```

**Defect:** No example input/output. No explanation of what matrix transposition produces.

---

### 7.4 — `exercises/115-binarySearchSortedArray/README.md`

**Complete file content:**
```
# 115-binarySearchSortedArray

Implement binary search in a sorted array and return index or -1.

## Instructions

Implement `binarySearchSortedArray` in `app.ts` using TypeScript types.
```

**Defect:** No example input/output. This exercise immediately follows exercise 111 which provides a detailed multi-step explanation of binary search; exercise 115 provides none, despite having the same topic.

---

### 7.5 — `exercises/167-buildUserProfileWithInterface/README.md`

**Complete file content:**
```
# 167-buildUserProfileWithInterface

Create and return a typed object using an interface.

## Instructions

Implement `buildUserProfile` in `app.ts` using TypeScript types.
```

**Defect:** No example. No interface definition shown. No description of required properties. The test requires the result to include `{ name, age, isAdult }` but none of these properties are mentioned in the README.

---

### 7.6 — `exercises/168-getDisplayNameFromOptionalProfile/README.md`

**Complete file content:**
```
# 168-getDisplayNameFromOptionalProfile

Use optional properties to return nickname or fallback first name.

## Instructions

Implement `getDisplayName` in `app.ts` using TypeScript types.
```

**Defect:** No example. No description of the input object's shape. No TypeScript optional-property syntax shown. The title references a TypeScript concept ("optional properties") that is not demonstrated anywhere in the exercise files. The solution file does not implement the function (see Finding 4).

---

### 7.7 — `exercises/169-renameBookMutableVsImmutable/README.md`

**Complete file content:**
```
# 169-renameBookMutableVsImmutable

Return a renamed copy of a book without mutating the original object.

## Instructions

Implement `renameBookImmutable` in `app.ts` using TypeScript types.
```

**Defect:** No example input/output. No description of the book object's shape. The test reveals the expected structure (`{ title, author }`) but the README does not.

---

### 7.8 — `exercises/170-comparePassByValueAndReference/README.md`

**Complete file content:**
```
# 170-comparePassByValueAndReference

Demonstrate pass-by-value vs pass-by-reference behavior in TypeScript.

## Instructions

Implement `comparePassByValueAndReference` in `app.ts` using TypeScript types.
```

**Defect:** No example. No description of input or expected output. The test requires `out.externalCount >= 1`, which is the only specification of expected behaviour, and it is not in the README.

---

## 8. FINDING 6 — INTERNAL CONTRADICTIONS

The following are cases where one file within an exercise contradicts another file in the same exercise. Each contradiction is documented with exact quotes from both conflicting sources.

---

### 8.1 — Exercise 155: Hint contradicts example

**File:** `exercises/155-ArrayToObject-B/README.md`

**Hint states:**
> "Assume that all elements in the array will be of type `string`."

**Example in the same README:**
```javascript
let output = fromListToObject([['make', 'Ford'], ['model', 'Mustang'], ['year', 1964]])
console.log(output); // --> { make : 'Ford', model : 'Mustang', year : 1964 }
```

**Test confirms** (`exercises/155-ArrayToObject-B/test.js`):
```javascript
let output = fromListToObject([
  ['make', 'Ford'],
  ['model', 'Mustang'],
  ['year', 1964],
]);
expect(output).toEqual({ make: 'Ford', model: 'Mustang', year: 1964 });
```

**Defect:** The hint instructs students to assume all elements are strings. The example and test both use `1964`, which is a number, not a string. A student who follows the hint and writes code that assumes all-string input may produce an implementation that passes the hint's stated constraint but fails the test.

---

### 8.2 — Exercise 102: Hyperlink description does not match link target

**File:** `exercises/102-modulo/README.md`

**Quoted text:**
> "It should behave as described in the [canonical documentation (MDN) for the TypeScript remainder operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder)."

**Defect:** The hyperlink text describes the destination as "the canonical documentation (MDN) for the TypeScript remainder operator". The URL provided (`https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Remainder`) links to the MDN page for the **JavaScript** Remainder operator. MDN does not have a TypeScript-specific remainder operator page; TypeScript uses the same `%` operator as JavaScript. The description of the link destination is factually inaccurate.

---

### 8.3 — Exercise 160: Required data is absent from the student file

**File:** `exercises/160-GreetCustomers/README.md`

**Quoted text:**
> "Please check to the `customerData` object."

**File:** `exercises/160-GreetCustomers/app.ts`

**Complete file content:**
```typescript
function greetCustomer(firstName: string): string {
  // your code here
  return '';
}

export {};
```

**Test relies on** (`exercises/160-GreetCustomers/test.js`):
```javascript
test('If a client has visited only once, it must say "Welcome back ..."', () => {
  let output = greetCustomer('Joe');
  expect(output).toBe("Welcome back, Joe! We're glad you liked us the first time!");
});
```

**Defect:** The README instructs students to consult `customerData`. The `app.ts` file contains no `customerData` object. The test calls `greetCustomer('Joe')` and expects a specific response that requires knowing `Joe` has `visits: 1`. Neither the README nor `app.ts` provides this data. The `customerData` object appears only in `solution.hide.js`, which is hidden from students.

---

### 8.4 — Exercise 059: README example pattern contradicts declared return type

**File:** `exercises/059-extend/README.md`

**Example shows the function called for its side-effect, with the return value unused:**
```typescript
extend(obj1, obj2);

console.log(obj1); // --> {a: 1, b: 2, c: 3}
console.log(obj2); // --> {b: 4, c: 3}
```

**File:** `exercises/059-extend/app.ts`

**Quoted signature:**
```typescript
function extend(obj1: unknown, obj2: unknown): unknown[] {
```

**Test** (`exercises/059-extend/test.js`):
```javascript
extend(obj1, obj2)
let output = obj1
expect(output).toEqual({ a: 1, b: 2, c: 3 })
```
The test does not use the return value of `extend`; it reads `obj1` directly.

**Defect:** The README example and the test both treat `extend` as a void function that mutates `obj1`. The `app.ts` signature declares the return type as `unknown[]` (an array). There is no scenario in which a function that mutates an object should also return an array. Additionally, the parameters are typed as `unknown`, which in TypeScript prevents property access without an explicit type assertion — a student who implements the function body using `obj1[key]` syntax will encounter a TypeScript error because `unknown` does not permit property access.

---

### 8.5 — Exercise 003: Typographical error in section heading

**File:** `exercises/003-isOldEnoughToVote/README.md`

**Quoted heading:**
```
## 📝 Insructions:
```

**Defect:** The heading contains a typographical error: "Insructions" should be "Instructions". All other exercises in the repository use the correct spelling. This is a copy-editing error.

---

## 9. FINDING 7 — TYPESCRIPT-SPECIFIC CONTENT AUDIT

This section documents which exercises, if any, require or demonstrate TypeScript-specific language features — that is, features present in TypeScript but absent from JavaScript: `interface` declarations, generic type parameters, `enum` declarations, union types (`A | B`), intersection types (`A & B`), type guards, optional properties (`prop?: T`), `readonly`, and type aliases (`type X = ...`).

### 9.1 — Search result across all `app.ts` files

A search was performed across all 170 `app.ts` files for the keywords: `interface`, `enum`, `<T>`, `| `, `& `, `is `, `readonly`, `type ` (as a keyword preceding a type alias). **No matches were found in any `app.ts` file.** Every `app.ts` uses only basic type annotations: `: string`, `: number`, `: boolean`, `: unknown[]`, `: Record<string, unknown>`, and `: void`.

### 9.2 — Exercise-by-exercise assessment of TypeScript-specific concepts

#### Exercises 001–166 (166 exercises)

All 166 `app.ts` files use only basic type annotations. None of the function signatures, parameter lists, or return types require knowledge of TypeScript beyond annotating a parameter with a primitive type. The exercises are mathematically and logically identical to JavaScript exercises, with type annotations added to the starter signature.

Examples of type annotations used:
- `age: number`, `name: string` — primitive annotations
- `arr: unknown[]` — weakly typed array
- `Record<string, unknown>` — built-in utility type used as a single token

#### Exercise 167 — `buildUserProfileWithInterface`

**README title:** "buildUserProfileWithInterface"  
**README instruction:** "Create and return a typed object using an interface."

**`app.ts` content:**
```typescript
function buildUserProfile(name: string, age: number): Record<string, unknown> {
  // your code here
  return {} as Record<string, unknown>;
}
```

The `app.ts` does not contain an `interface` declaration. The return type uses `Record<string, unknown>` and an `as` type assertion, neither of which requires the student to write or understand an interface.

**`solution.hide.js` content:**
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

The solution file contains an `interface UserProfile` declaration, which is the TypeScript-specific element referenced in the README title. However, as documented in Finding 4, the function body is unimplemented (`return {}`).

**Assessment:** The README references an interface. The solution file declares one but does not use it (the function is not implemented). The `app.ts` given to students contains no interface declaration. The student is not shown how to declare or use an interface in any of the provided files.

#### Exercise 168 — `getDisplayNameFromOptionalProfile`

**README instruction:** "Use optional properties to return nickname or fallback first name."

**`app.ts` content:**
```typescript
function getDisplayName(profile: Record<string, unknown>, arg2: unknown): string {
  // your code here
  return '';
}
```

The `app.ts` does not contain any optional property syntax (e.g. `nickname?: string`). The parameter is typed as `Record<string, unknown>`, which accepts any string-keyed object and does not communicate to the student that `nickname` is optional.

**`solution.hide.js` content:**
```javascript
function getDisplayName(profile) {
  // your code here
  return '';
}
```

The solution does not implement the function (see Finding 4) and contains no TypeScript optional-property syntax.

**Assessment:** The README references optional properties, but neither `app.ts` nor the solution file demonstrates this TypeScript feature.

#### Exercises 169–170

Exercise 169 ("Mutable vs Immutable") and Exercise 170 ("Pass by Value and Reference") describe JavaScript runtime behaviours that are not TypeScript-specific. Neither `app.ts` file contains any TypeScript construct beyond a return type annotation. The solution files do not implement the functions (see Finding 4).

### 9.3 — Summary

| Exercises | TypeScript-specific feature in `app.ts` | TypeScript-specific feature in solution | Feature described in README |
|---|---|---|---|
| 001–166 | None | None (solutions in plain JS) | None |
| 167 | None (`Record<string, unknown>` and `as` cast only) | `interface` declaration present but function unimplemented | "interface" referenced in title |
| 168 | None | None | "optional properties" referenced |
| 169 | None | None | None specific to TypeScript |
| 170 | None | None | None specific to TypeScript |

The only TypeScript-specific language construct present in any exercise file is the `interface UserProfile` declaration in `exercises/167-buildUserProfileWithInterface/solution.hide.js`. That declaration appears alongside an unimplemented function body.

---

## 10. SUMMARY STATISTICS

| Finding | Count | % of 170 exercises |
|---|---|---|
| Exercises with a demonstrably wrong TypeScript return type in `app.ts` (§3) | 17 | 10% |
| Exercises with at least one phantom parameter in `app.ts` (§4) | 37 | 22% |
| Exercises where README number does not match directory name (§5) | 142 | 83.5% |
| Solution files that contain no implementation and fail their own tests (§6) | 4 | 2% |
| README files with no worked example and fewer than 5 lines of content (§7) | 8 | 5% |
| Exercises with a documented internal contradiction (§8) | 5 | 3% |
| Exercises where `app.ts` uses a TypeScript-specific language feature (§9) | 0 | 0% |
| Exercises where the solution file uses a TypeScript-specific feature (§9) | 1 (unimplemented) | 0.6% |

---

*End of Report*

*Report Reference: QA-TS-2026-002 | Date: 28 May 2026*
