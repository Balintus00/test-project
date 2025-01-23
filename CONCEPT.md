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
