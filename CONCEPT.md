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
