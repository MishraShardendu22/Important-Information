## 1. What is Cobra?
Cobra is a library in Go that helps you create command-line applications. Think of it as a framework that lets you add commands like start, check, or status to your Go program, and each command can do something specific. Cobra is especially useful when you want to run your Go program from the command line and have it do specific tasks based on commands you give.

## 2. How Cobra Works (Basics)
### Commands: Cobra lets you create commands, like “check website health” or “start server.”
### Flags: Flags are options you can pass to commands to change how they work, like --url to specify a website to check.
### Root Command: This is the main command, and every other command you add will be a subcommand of this root command.

## Example :

### Commands: Main actions your application can perform, like run, build, or test.
### Flags: Options or parameters you can pass to commands to modify their behavior, like --verbose or --output=file.txt.
### Subcommands: Commands that are part of a main command, allowing for more structured functionality, like having git commit as a subcommand of git.

``` go
func init() {
    CheckCommand.Flags().StringVarP(&url, "url", "u", "", "URL of the website to check")
    CheckCommand.MarkFlagRequired("url")
    RootCommand.AddCommand(CheckCommand)
}
```

## Syntax of Flags:
### <command>.Flags().StringVarP(<variable>, "<full-flag-name>", "<short-flag-name>", "<default-value>", "<description>")

## MarkFlagRequired("url") is used to specify that the url flag is mandatory when executing the CheckCommand. If the user tries to run the command without providing this flag, the program will display an error message and show the correct usage instructions instead of proceeding with the command's execution.

### Here's how it works:

Enforcement: This ensures that users cannot run the command without specifying a URL. It's a way to enforce that the command has all the necessary information to perform its task.
User Feedback: If the required flag is missing, Cobra automatically handles it by informing the user about the missing flag and showing how to use the command correctly.

So, using MarkFlagRequired enhances the usability and robustness of the command-line tool by preventing incomplete or incorrect command usage.

## Use of Use in RootCommand: The Use field should typically be a command name rather than a description. For your base command, you might want to name it something like "checker" or "health-checker" instead of a description.

Here's a breakdown of how setting the GOOS and GOARCH environment variables helped in creating a working executable:

Understanding GOOS and GOARCH
GOOS: This variable specifies the target operating system for which you want to build your application. By setting GOOS=windows, you instructed the Go compiler to create a binary that is compatible with Windows.

GOARCH: This variable specifies the target architecture. By setting GOARCH=amd64, you ensured that the compiled binary would be for 64-bit architecture, which is standard for most modern Windows systems.
