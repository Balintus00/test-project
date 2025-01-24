# Train of thought

- in a custom folder (like with SQLDelight) for each source set
- should generate based on gherkin file
- should generate kotlin code using that uses the official test library
- need to set some rules with the syntax, like allowed characters and maximum character count (based
  on the test library)
- publishing
- if two steps are the same in the gherkin file, they have common name
- should generate a Kotlin method for each gherkin steps, and the user should be able to fill the
  content of these generated functions
- coroutine support
- grammarKit, kotlin poet
- Basically it would be really similar to SpecFlow
- I could use Kotlin DSL instead of a GrammarKit based solution
    - Would be much more less complex this way both for me (developer) and the user
    - this makes portability worse, but the measure of that can be controlled with the syntax of the
      DSL
- https://cucumber.io/docs/gherkin/reference
- in that case a DSL is needed to define and group steps into scenarios, and also there needs to be
  a way to define what each step exactly does
- it should be lightweight and easily customisable
- for each step an object could be generated, that identifies the step, then the definition to the
  step could be added using an annotation
    - pretty much the same as other libraries' step definition syntax, but because of the generated
      objects, typos are not possible
- probably custom gradle tasks will be needed for the code generation
- another way could be generating an abstract class for the feature, and there for each step an
  abstract method could be generated, the user could override
- Also it should be kept in mind, that the steps might need to use some common, feature related
  variables, e.g. like given steps setting mock behaviour
- regarding the test execution where scenarios have multiple then steps, a setting should be
  available to run a test case for each step, or run the previous non-then steps and then execute
  the then steps after each other
- parameterizable steps should be considered
- the specflow descendant project reqnroll and cucumber documentation might give more ideas and
  insights
    - https://docs.reqnroll.net/latest/
    - https://cucumber.io/
- would be nice to support instrumented tests too
    - like Kotest does not work out of the box with Android instrumented tests, because Kotest uses
      JUnit5 and the instrumented test runner JUnit4
- Kotlin Test library seems a good library to build on
    - supports the most important platforms, can be integrated with multiple JVM frameworks (JUnit4,
      JUnit5, TestNG)
    - is maintained by Jetbrains, official library
- https://www.jetbrains.com/help/kotlin-multiplatform-dev/multiplatform-run-tests.html#test-a-simple-multiplatform-project
- https://www.jetbrains.com/help/kotlin-multiplatform-dev/compose-test.html#writing-and-running-tests-with-compose-multiplatform
- if I'll choose to use Kotlin DSL for the test definitions, it seems a good idea to first implement
  a prototype of the library, then add the code generation implementation
- I should probably go with SemVer

# Case Studies

## 1. Cucumber

- it's really cool that the undefined steps are printed in the test output in way, that the function
  declarations can be copied to the codebase
- it uses the class that contains the step definition implementation, to store the state of the test
  case (variables)
- Gherkin language's examples can make the feature much more readable, and Cucumber works really
  well with it, that it generates the test cases based on that
- there is an possibility to allow parallel execution with junit5, though I don't really like
  that the gherkin code needs to modified to handle concurrency in some cases
- ob JUnit4 parallel execution for scenarios is allowed, which is cool
- the arguments are interestingly well resolved with Kotlin, its implementation is probably worth
  investigating
- data tables
- step definitions are matched to the code using regexp and similar methods. Would be nice if I
  could avoid this using code generation or some other solution, because it seems error prone.
- Cucumber has step results, this might not be needed for my goal
- hooks seems really useful, and I think it would worth implementing them
- conditional hooks seems interesting, though I'm not sure about using tags in the DSL
- tags probably won't be supported, at least in the first version
- [cucumber junit platform engine documentation](https://github.com/cucumber/cucumber-jvm/tree/main/cucumber-junit-platform-engine)
- parameter types are interesting, and seems useful
- [cucumber expressions](https://github.com/cucumber/cucumber-expressions#readme) - alternative to
  regexp, would be nice to avoid the need for this by constructing the DSL properly
- would be nice to avoid customising reporting, and instead just depend on the used test framework's
  abilities
- the asterisk (*) syntax is interesting for steps, might consider supporting it
- scenario outlines with data tables is really useful
