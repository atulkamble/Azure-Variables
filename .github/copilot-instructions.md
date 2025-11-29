# Azure DevOps Variables - AI Agent Instructions

## Project Overview
This repository demonstrates Azure DevOps variable management patterns across different pipeline types and referencing methods. Focus on practical examples that showcase real-world variable usage scenarios.

## Key Concepts to Understand
- **Variable Scopes**: Release pipeline, build pipeline, variable groups, and library variables
- **Variable Types**: Secret variables, counter variables, and standard variables
- **Reference Methods**: 
  - Macro syntax: `$(variableName)` - expanded before execution
  - Template expressions: `${{ variables.variableName }}` - compile-time expansion
  - Runtime expressions: `$[variables.variableName]` - runtime evaluation

## Content Structure Patterns
When adding examples, organize by:
1. **Classic Editor Examples** (`/classic-editor/`) - UI-based pipeline configurations
2. **YAML Pipeline Examples** (`/yaml-pipelines/`) - Code-based pipeline definitions
3. **Variable Group Examples** (`/variable-groups/`) - Shared variable collections
4. **Advanced Scenarios** (`/advanced/`) - Complex variable referencing patterns

## Azure DevOps Specific Conventions
- Use realistic environment names: `dev`, `staging`, `prod` (not generic placeholder names)
- Include proper Azure subscription and resource group naming patterns
- Show variable precedence and override scenarios
- Demonstrate security best practices for secrets and sensitive variables

## Example Requirements
- **YAML Files**: Include complete, runnable pipeline definitions
- **Screenshots**: When documenting Classic Editor, include UI screenshots with annotations
- **Variable References**: Show both working and non-working examples to highlight common mistakes
- **Documentation**: Each example should explain WHEN to use specific variable types/methods

## Common Pitfalls to Address
- Variable scope conflicts between pipeline and variable group levels
- Incorrect syntax usage leading to literal string expansion
- Security leaks through improper secret variable handling
- Template expression limitations in certain pipeline contexts

## Testing Approach
- Validate YAML syntax using Azure DevOps pipeline validation
- Test variable expansion in different execution contexts
- Verify variable group permissions and library access patterns
- Document expected behavior vs actual behavior for edge cases

## Integration Context
This project serves as a reference for:
- DevOps engineers learning Azure Pipelines variable management
- Teams standardizing variable naming and usage patterns
- Training materials for Azure DevOps adoption
- Troubleshooting guides for common variable-related issues