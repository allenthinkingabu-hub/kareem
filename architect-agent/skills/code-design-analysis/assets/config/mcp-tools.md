# MCP Tools — SA-ANA-001 Code Design Analysis

## Overview

Defines the MCP (Model Context Protocol) tools a qualified Code Design Analysis AI Agent must use.

## MCP Tool Reference

### MCP-01: context7
**Purpose**: Authoritative documentation lookup for frameworks and libraries used by the analysis target.

**Use Cases**:
- Look up official API documentation for detected frameworks (Spring, Django, Express, Rails, etc.)
- Verify design pattern implementation conventions for the target language/framework
- Look up correct usage of architectural constructs
- Verify security best practices for identified vulnerabilities

**Invocation Trigger**:
- When a framework-specific annotation, decorator, or convention is identified and its behavior must be verified
- When a design pattern is detected and canonical implementation must be confirmed
- When security-sensitive code is found and best practice documentation is needed

---

### MCP-02: IDE Diagnostics (`mcp__ide__getDiagnostics`)
**Purpose**: Type analysis and symbol resolution within the target scope.

**Use Cases**:
- Identify type errors, unresolved symbols, and type mismatches
- Detect methods called with wrong argument types
- Confirm method signatures and return types in strongly-typed languages
- Identify unused imports and dead code

**Invocation Trigger**:
- When static type information is ambiguous from source reading alone
- When verifying that identified interfaces are correctly implemented
- When assessing code quality (type safety as a quality indicator)

---

### MCP-03: Code Intelligence Tools
**Purpose**: Call graph traversal and cross-reference analysis beyond Grep capability.

**Use Cases**:
- Construct accurate call graphs for complex inbound/outbound dependency mapping
- Find all implementations of a specific interface across the codebase
- Identify all event listeners for a specific event type
- Trace dependency injection chains in IoC containers

**Invocation Trigger**:
- When Grep-based search is insufficient for accurate caller analysis
- When dealing with dynamic dispatch or polymorphism
- When tracing cross-module dependencies in large codebases

## Modifying MCP Tools

To add a new MCP tool, append a new `MCP-N` section following the format above.
