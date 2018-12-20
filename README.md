# lane-next
v5 of the lane platform.  Biggest changes are

- migrating from MongoDB to postgresql
- migrating from Rest API to GraphQL
- moving a mono-repo format
- collapsing all web portals into one project
- moving to experimental modules so that lane-shared can be used in NodeJS


#### Projects

- import
    - migrates the Lane v4 MongoDB to Postgres
- lane-graphql
    - a wrapper over the graphql-js implementation to allow using the new module import
- lane-mobile
    - the mobile app in React Native.
- lane-portal
    - the web app in React
- lane-server
    - the NodeJS server with the GraphQL API


## Coding style guide
### 1. File Naming/Structure
#### File Structure
- Most files should live in `src/`, except for config files and index.js.
- The general file structure should follow this:
    ```javascript
    src/
        config/
        views/
            feature/
        global-state-manager/backend stuff/
            api/db calls/
            ...
        shared-components/
        utils/
        constants/
        assets/
    ```
- Every feature should have its own directory i.e
    ```javascript
    src/
        views/ //scenes/screens
            login/
                index.js
                login.test.js
                components/
                    successModal.js
    ```

#### File Naming

- all files should be camelCased.
- **we should stick to either jsx or js (let's discuss this)**

### 2. File Formatting

#### General
- Each presentational component should have all the styling on an external file (stored in the same dir). **We should not have any inline style**.
- We should only be exporting one react class per file.
- For directories containing multiple files that export classes, we should have a `index.js` that exports everything.

#### Brackets, Parenthesis and Blocks
- No unnecessary parenthesis i.e
    ```javascript
    (1 === true) ? 2 : 5 //oh no no no *the voice of the bitconnect dude*
    1 === true ? 2 : 5
    ```
- Space after bracket i.e

    ```javascript
        export class ClassTest {
            someFunction = () => {

            }

            function anotherFunction () {

            }
        }
    ```

- If empty blocks are required, let's keep them inline:

    ```javascript
        if(true) { }
    ```
- One liners are encouraged when readable i.e don't nest ternary functions

#### Variables

- Name should be camelCased.
- We should stick to `let` and `const` (ES7).
- We should destructure objects when possible.
- One variable per declaration:
    ```javascript
        let a = 1, b = 2 // no
        let a = 1;
        let b = 2; //yas
    ```
- Don’t chain variable assignments.
- Avoid linebreaks before or after = in an assignment.
- No unused variables.
- Do not use trailing or leading underscores.

#### Constants

- Enums are highly encouraged.
- Let's keep a file for each kind of constants (colors, size, etc).
- Constants can be snaked_case.

#### Arrays and Objects

- Do not use the variadic `Array` or `Object` constructor.
- Use computed names for arrays/objects properties. i.e
    ```javascript
        let obj = {
            name : 'dev'
            id : 1
        }

        obj['food'] = 'pasta' //no
    ```
- Only quote properties that are invalid identifiers.
- Prefer the object and array spread operator (`...`) over Object.assign to shallow-copy objects/arrays.
- Use Array.push instead of direct assignment to add items to an array
- Use line breaks after open and before close array brackets if an array has multiple lines.
- Use array destructuring
- If possible, use dot notation when accessing properties. Use bracket notation [] when accessing properties with a variable


#### Strings

- Use single quotes for strings.
- Strings that cause the line to go over 100 characters should not be written across multiple lines using string concatenation.
    ```javascript
        const errorMessage = 'This is a super long error that was thrown because \
        of Batman. When you stop to think about how Batman had anything to do \
        with this, you would get nowhere \
        fast.';

        // bad
        const errorMessage = 'This is a super long error that was thrown because ' +
        'of Batman. When you stop to think about how Batman had anything to do ' +
        'with this, you would get nowhere fast.';

        // good
        const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast'
    ```
-  When programmatically building up strings, use template strings instead of concatenation.

    ```javascript
    // bad
    function sayHi(name) {
    return 'How are you, ' + name + '?';
    }

    // bad
    function sayHi(name) {
    return ['How are you, ', name, '?'].join();
    }

    // bad
    function sayHi(name) {
    return `How are you, ${ name }?`;
    }

    // good
    function sayHi(name) {
    return `How are you, ${name}?`;
    }
    ```

#### Functions

- Function names should be camelCasedd.
- We should use arrow syntax (except for lifecycle functions).
- Never declare a function in a non-function block (if, while, etc).
- Never use arguments, opt to use rest syntax ... instead.
- Use default parameter syntax rather than mutating function arguments.
- Always put default parameters last.
- Let's add spacing in a function signature.
- Never reassign parameters.

#### Comparisons Operators & Equality

- Use `===` and `!==` over `==` and `!=`.
- Use shortcuts for booleans, but explicit comparisons for strings and numbers.
- Ternaries should not be nested and generally be single line expressions.
- Avoid unneeded ternary statements.
    ```javascript
        1 === true ? 'hello' : null //no
        1 === true && 'hello' //yes
        let a = 1;
        return a ? a : null //no
        return a || null //yes
    ```
- When mixing operators, enclose them in parentheses.

#### Control Statements

- In case your control statement (if, while etc.) gets too long or exceeds the maximum line length, each (grouped) condition could be put into a new line. The logical operator should begin the line.


#### React Classes

- Class Names should be PascalCased
- Class files should be structured like this:
    ```javascript
        class {
            constructor() {} //if needed
            lifecycle {}
            other()
            render()
        }
    ```
- We should only have 2-3 functions max per class (not including lifecycle).
- **let's discuss if we want to extends classes like React.Component or Component and import it**

#### Imports/Exports

- Only import from a path in one place.
- Do not export mutable bindings.
- Multiline imports should be indented just like multiline array and object literals
- Exports should be placed at the bottom of class files.

#### Comments

- Use /** ... */ for multi-line comments
- Start all comments with a space to make it easier to read
- Prefix your comments with FIXME or TODO

#### Spacing

- Place 1 space before the leading brace.
- Place 1 space before the opening parenthesis in control statements (if, while etc.)
    ```javascript
        if (true) {
            doSomething()
        }
    ```
- Set off operators with spaces
    ```javascript
        1 + 2 + 3
    ```
- Leave a blank line after blocks and before the next statement.
- Do not pad your blocks with blank lines.
- Add spaces inside curly braces.
- Do not add spaces inside brackets.
- Avoid having lines of code that are longer than 100 characters.
- Avoid spaces before commas and require a space after commas.
- Enforce spacing inside of computed property brackets.
- Avoid spaces between functions and their invocations.
- Avoid trailing spaces at the end of lines.

#### Prettier
- Tab with 2 spaces
- Single Quotes
- Semicolons
- No Trailing comma
- Bracket Spacing
- Line limit 80

**References:**

- [Airbnb's style guide](https://github.com/airbnb/javascript)
- [Google's style guide](https://google.github.io/styleguide/jsguide.html)
- [Medium article on file structure](https://medium.com/@alexmngn/how-to-better-organize-your-react-applications-2fd3ea1920f1)