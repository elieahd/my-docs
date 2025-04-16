The `AAA` patterns provides a simple structure for all tests. It advocates for splitting each test into three parts:

- `arrange` : bring the `SUT` (system under test aka the class you are testing) and its dependencies to a desired states
- `act` : calls the method, pass the prepared dependencies and capture the output value (if any)
- `assert` : verify the outcome

Once u get used to the uniformity of this pattern, it will help you to easily read and understand any test.

`Given`-`When`-`Then` pattern is similar to `AAA` pattern, it advocates to break down tests into similar 3 parts: 

* `Given` corresponds to the `arrange` section
* `When` corresponds to the `act` section
* `Then` corresponds to the `assert` section

The only distinction is that the `Given`-`When`-`Then` structure is more readable to non-programmers.

## Guidelines 

* avoid multiple `arrange`/`act`/`assert` sections 
* distinguish the SUT in tests by naming it `sut`
* differentiate the three test sections either by putting Arrange, Act, and Assert comments before them or by introducing empty lines between these sections
* `act` section is normally a single line code
* avoid if statements in tests
