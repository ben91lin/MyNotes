# Cucumber
https://www.npmjs.com/package/@cucumber/cucumber
https://www.npmjs.com/package/@cucumber/pretty-formatter
https://www.npmjs.com/package/multiple-cucumber-html-reporter

https://github.com/cucumber/cucumber-js/blob/HEAD/docs/cli.md

## Output Report
[CAUTION!] If '.feature' is empty, gherkinDocument will not have property 'feature'. Will got the TypeError: Cannot read property 'name' of null.
    cucumber-js <feature-path> --format message:<path>
    cucumber-js <feature-path> --format json:<path>
    cucumber-js <feature-path> --format html:<path>