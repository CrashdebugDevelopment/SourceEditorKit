
```markdown
<details>
  <summary><strong>MARK: Using 'SourceEditor' with a string binding</strong></summary>

```swift
@State private var source = "Hello, World! // This is a comment!"

// Initializing the SourceEditor with a string binding.
// The tokenizer is configured for Python syntax,
// and the default light theme is applied.
SourceEditor(source: $source)
   .tokenizerConfiguration(for: .python)
   .themeConfiguration(for: .defaultLight)
```
</details>

<details>
  <summary><strong>MARK: Using 'SourceEditor' with an editor controller</strong></summary>

```swift
@StateObject private var controller = SourceEditorController()

// Initializing the SourceEditor with a controller object.
// The language and theme configurations are set for Python,
// and an overlay displays the current cursor position.
SourceEditor(controller: controller)
   .languageConfiguration(for: .python)
   .themeConfiguration(for: .defaultLight)
   .overlay {
       Text("Line: \(controller.cursorSelection.line) Char: \(controller.cursorSelection.character)")
           .frame(maxWidth: .infinity, maxHeight: .infinity, alignment: .bottomTrailing)
           .padding()
   }
```
</details>

<details>
  <summary><strong>MARK: Defining custom languages including custom themes</strong></summary>

```swift
// Define all the available tokens for the Swift language.
// These tokens will be used by the tokenizer to identify
// and style different elements of the code.
enum SwiftConfiguration: TokenConfiguration {
   case comment, string, number, keyword
}

// Defining the language configuration for the tokenizer.
// This configuration tells the tokenizer how to identify
// comments, strings, numbers, and keywords in Swift code.
let languageConfiguration: LanguageConfiguration(SwiftConfiguration) = [
   .comment: .regex("//.*$"),  // Regex to match single-line comments
   .string: .regex("\"[^\"]*\""),  // Regex to match strings
   .number: .regex("\\d+"),  // Regex to match numbers
   .keyword: .list(["let", "var", "func", "return"])  // List of Swift keywords
]

// Defining the theme configuration for the tokenizer.
// This configuration assigns colors to the different tokens.
let themeConfiguration: ThemeConfiguration(SwiftConfiguration) = [
   .comment: UIColor.gray,  // Gray color for comments
   .string: UIColor.red,  // Red color for strings
   .number: UIColor.blue,  // Blue color for numbers
   .keyword: UIColor.purple  // Purple color for keywords
]

// Defining the overall theme for the editor.
// This includes the text color, background color,
// and styles for line numbers and selected lines.
let theme = Theme (
   textColor: UIColor.black,  // Black color for the main text
   backgroundColor: UIColor.white,  // White background
   lineNumberColor: UIColor.gray,  // Gray color for line numbers
   lineNumberColorSelected: UIColor.black,  // Black color for selected line numbers
   lineBackgroundSelected: UIColor.lightGray,  // Light gray background for selected lines
   
   configuration: themeConfiguration  // Applying the previously defined theme configuration
)
```
</details>

<details>
  <summary><strong>MARK: Usage</strong></summary>

```swift
// Applying the custom language and theme configurations
// to the SourceEditor for Swift syntax highlighting.
SourceEditor(...)
   .languageConfiguration(for: languageConfiguration)
   .themeConfiguration(for: theme)
```
</details>
```

This version uses `<details>` and `<summary>` HTML tags to create collapsible sections for each "MARK" in your code, which helps organize the code when viewed on GitHub.
