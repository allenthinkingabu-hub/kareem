# Tools — SA-ANA-001 Code Design Analysis

## Overview

Defines the tools a qualified Code Design Analysis AI Agent must use during analysis.

## Tool Reference

### T-01: Glob
**Purpose**: Locate target files and related components within the analysis scope.

**Use Cases**:
- Locate all files belonging to a class, module, or topic scope
- Identify related test files
- Find all files in a feature directory
- Discover configuration files relevant to the analysis target

**Example Patterns**:
```
src/auth/**/*.java          # All files in auth module (Java)
**/*Service*.ts             # All TypeScript service files
src/**/{ClassName}*.py      # Python files containing ClassName
**/test/**/*SessionTest*    # Session-related test files
```

---

### T-02: Grep
**Purpose**: Trace import statements, usages, callers, and cross-references.

**Use Cases**:
- Find all callers of a method or class
- Trace import/dependency chains (`import`, `require`, `@Autowired`, `@Inject`)
- Locate all usages of a constant, configuration key, or interface
- Find all implementations of an interface
- Search for annotations, decorators, injection points

**Example Patterns**:
```
"import.*ClassName"         # Imports of ClassName
"extends BaseService"       # Subclasses
"@Autowired.*Repository"    # Injection points
"ClassName\.methodName"     # Method usages
```

---

### T-03: Read
**Purpose**: Deep code reading and structural analysis of target files.

**Use Cases**:
- Read full class/interface file for responsibility analysis
- Read method body for algorithm tracing
- Read configuration files (Spring beans, DI containers, module configs)
- Read build files (pom.xml, build.gradle, package.json) for dependency analysis

**Guidance**:
- Read the full target file first, then read related files as needed
- For large files (>500 lines), read method signatures first, then method bodies
- Always read test files alongside source files for behavioral context

---

### T-04: Bash
**Purpose**: Build system commands, dependency listing, and coverage tool invocation.

**Use Cases**:
- List project dependencies
- Run static analysis tools
- Identify test coverage
- Inspect build output artifacts
- Run type-check commands

**Common Commands by Ecosystem**:
| Ecosystem | Dependency Listing | Coverage |
|-----------|-------------------|----------|
| Java/Maven | `mvn dependency:tree` | `mvn test` |
| Java/Gradle | `gradle :module:dependencies` | `gradle test` |
| Node.js | `npm ls --depth=2` | `jest --coverage` |
| Python | `pip show {package}` | `pytest --cov={target}` |
| Go | `go list -m all` | `go test -cover ./...` |
| .NET | `dotnet list package` | `dotnet test --collect` |

## Modifying Tools

To add a new tool, append a new `T-N` section following the format above.
