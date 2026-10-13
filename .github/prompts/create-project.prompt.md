# Create Standard .NET Project Structure

## Objective

Create a standardized set of five .NET projects using a project name supplied by the user.

The user will provide one input:

- `ProjectName`: The base name for all projects and directories.

Example input: `Scada.Driver.Modbus`

Use the provided name exactly as the naming prefix. Do not hardcode the example name.

## Directory and Solution Structure

Create a root directory named `{ProjectName}`.

Inside this directory, create the following main solution:

`{ProjectName}/{ProjectName}.sln`

The main solution must contain exactly these five projects:

1. `{ProjectName}` — .NET 8 class library.
2. `{ProjectName}.Composition` — .NET 8 class library.
3. `{ProjectName}.Interface` — .NET 8 class library.
4. `{ProjectName}.Interface.External` — .NET Standard 2.1 class library.

Create a separate test directory:

`{ProjectName}/{ProjectName}.Test/{ProjectName}.Test.sln`

5. `{ProjectName}.Test.Unit` — .NET 8 class library, configured as a unit-test project.

The unit-test project must be located at:

`{ProjectName}/{ProjectName}.Test/{ProjectName}.Test.Unit/`

## Required Project Configuration

Use these target frameworks:

| Project | Target framework |
|---|---|
| `{ProjectName}` | `net8.0` |
| `{ProjectName}.Composition` | `net8.0` |
| `{ProjectName}.Interface` | `net8.0` |
| `{ProjectName}.Interface.External` | `netstandard2.1` |
| `{ProjectName}.Test.Unit` | `net8.0` |

Use the standard SDK-style `.csproj` format.

Disable nullable reference types and disable implicit usings for the projects or do not add them.

Do not change target frameworks or project names.

## Project Responsibilities

Keep the projects initially minimal and ready for future implementation.

- **Core project (`{ProjectName}`):** Main implementation and domain functionality.
- **Composition project (`{ProjectName}.Composition`):** Composition root, dependency registration and wiring of implementations.
- **Interface project (`{ProjectName}.Interface`):** Internal abstractions and contracts.
- **External interface project (`{ProjectName}.Interface.External`):** Public or integration-facing contracts intended to remain compatible with .NET Standard 2.1 consumers.
- **Unit-test project (`{ProjectName}.Test.Unit`):** Unit tests for the implementation.

Do not create unnecessary business logic, placeholder classes, services or interfaces.

## Project References and Dependencies

Inspect the existing repository and follow any applicable Copilot instructions and architecture documentation.

Do not create circular dependencies.

Only add project references that are justified by the documented architecture. In particular, do not assume that the .NET Standard project can reference a .NET 8 project.

The unit-test project should reference the implementation project or projects that it needs to test.

Configure the unit-test project so that it can be discovered and executed by `dotnet test`. Configure for NUnit testing

Use compatible, stable package versions. Do not add unrelated NuGet packages.

## Naming and File Structure

- Use the exact project names specified above.
- Name each project file after its project.
- Use standard Visual Studio solution and project conventions.
- Place each project in a directory with the same name as the project.
- Keep the main solution at the root of `{ProjectName}`.
- Keep the test solution inside `{ProjectName}.Test`.
- Do not create an additional solution file or an extra nesting level.

## Execution Workflow

1. Ask the user for `ProjectName` if it has not been provided.
2. Inspect the current workspace, existing solutions, repository instructions and architecture documentation.
3. Determine the intended output location. Do not overwrite existing files or projects without permission.
4. Create the root directory and four main class-library projects.
5. Create the nested test directory, unit-test project and test solution.
6. Add the five main projects to the main solution.
7. Configure only the necessary project references and test dependencies.
8. Build the main solution in Release configuration.
9. Run the unit tests using the test solution.
10. Report the created directory structure, target frameworks, project references, build results and test results.

Use the .NET CLI when appropriate, and verify that each command succeeds before proceeding to dependent operations.

If a command fails, investigate and fix the cause instead of claiming that project generation succeeded.

## Completion Criteria

The task is complete only when:

- All five project files exist at the required locations.
- All target frameworks match the specification.
- The main solution contains all the created projects.
- The test project is discoverable by `dotnet test`.
- The main solution builds successfully, or any build failure is explicitly reported.
- The test command has been executed, or any reason it could not run is explicitly reported.