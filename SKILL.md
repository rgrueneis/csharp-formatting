---

name: csharp-formatting
description: Format C# and .NET projects using dotnet format and the bundled templates/.editorconfig. Use this skill when asked to format, clean up, or standardize C# code.

user-invocable: true
--------------------

# C# Formatting

Use this skill when the task is to format a C# project so that `dotnet format` completes successfully and `dotnet format --verify-no-changes` reports no remaining changes.

## Intent

Use the bundled [templates/.editorconfig](templates/.editorconfig) as the formatting and style template. Copy it into the target project or solution root before running `dotnet format`.

## Template

The bundled [templates/.editorconfig](templates/.editorconfig) is the formatting template for this skill. It must be copied into the project being formatted so that the target project uses the same indentation, spacing, newline, analyzer, and naming rules.

## Procedure

1. Locate the project or solution root that should be formatted.

2. Copy the bundled [templates/.editorconfig](templates/.editorconfig) into the target project or solution root.

3. Run `dotnet format --severity info` against the solution or project that owns the C# files.

4. Format `if` statements containing a single statement without braces, for example:

   ```csharp
   if (condition) DoSomething();
   ```

5. Run `dotnet format --severity info --verify-no-changes` to confirm that the tree is clean.

6. If analyzer warnings or formatting issues remain, fix the source files rather than suppressing them.

7. Repeat until `dotnet format --severity info --verify-no-changes` completes successfully for the targeted project.

## Rules

* Treat `.editorconfig` as the governing style contract.
* Prefer formatting and code-style changes that remove analyzer messages instead of leaving them as pending suggestions.
* Do not weaken analyzers or style settings just to silence `dotnet format`.
* Keep edits minimal and localized to the files reported by `dotnet format`.
* If a project-wide rule conflicts with a file-specific exception, follow the more specific `.editorconfig` scope.
* Format `if` statements containing a single statement without braces.

## XAML Rules

`dotnet format` does not format XAML. When the target project contains XAML files, apply the following rules manually:

* Use `Name` instead of `x:Name` unless the task explicitly requires `x:Name`.
* Keep the first attribute of a XAML element on the same line as the opening tag.
* Keep attributes on a single line as long as the line does not exceed 80 characters.
* If the line would exceed 80 characters, wrap attributes onto subsequent lines and indent them consistently.
* Do not introduce additional line breaks unless required by the 80-character limit.
* Add a space before the closing `/>` of a self-closing XAML element.
* When attributes are wrapped onto multiple lines, align their names consistently.
* Place event-handler attributes last and on a separate line.

## Review Checklist

* Was the correct solution or project formatted?
* Was the bundled `.editorconfig` copied to the correct location?
* Were the `.editorconfig` rules applied consistently?
* Does `dotnet format --severity info --verify-no-changes` pass for the targeted scope?
* Were remaining analyzer or formatting issues resolved in code instead of being ignored?
* If XAML files are present, were the XAML-specific rules applied?
