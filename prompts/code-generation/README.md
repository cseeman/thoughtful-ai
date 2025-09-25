# Code Generation Prompts

*AI prompts for generating Ruby and Rails code with intention and purpose*

## 🎯 Overview

These prompts help you generate Ruby code that follows Rails conventions, Ruby style guides, and maintains readability. The key is providing context and specific instructions to get idiomatic Ruby output.

## 📋 Best Practices

- **Always specify the framework**: "Rails 7", "Ruby 3.x"
- **Include style guide references**: "Follow Ruby Style Guide"
- **Provide context**: Explain the business logic or requirements
- **Specify constraints**: "Use only standard library methods"
- **Request explanations**: "Explain your approach"

## 🚀 Prompt Templates

### Rails Model Generation

**Basic Model:**
```
Create a Rails model for [Entity] with the following attributes:
- [attribute1]: [type] (required/optional)
- [attribute2]: [type] (required/optional)

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include appropriate validations
- Add any necessary associations
- Use descriptive method names
- Include YARD documentation

Example usage: [describe how the model will be used]
```

**Advanced Model with Business Logic:**
```
Create a Rails model for [Entity] that handles [business requirement].

Attributes:
[list attributes with types and constraints]

Business Rules:
- [rule 1]
- [rule 2]
- [rule 3]

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include appropriate validations and callbacks
- Add scopes for common queries
- Include error handling
- Use descriptive method names
- Add YARD documentation with examples

Consider edge cases: [mention specific edge cases]
```

### Controller Generation

**RESTful Controller:**
```
Create a Rails controller for [Resource] with standard RESTful actions.

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include proper error handling
- Use strong parameters
- Add before_action filters where appropriate
- Include flash messages
- Handle edge cases gracefully
- Add YARD documentation

Authentication: [specify if authentication is required]
Authorization: [specify any authorization rules]
```

**API Controller:**
```
Create a Rails API controller for [Resource] that returns JSON.

Requirements:
- Follow Rails API conventions
- Include proper HTTP status codes
- Add error handling with meaningful messages
- Use strong parameters
- Include pagination for index action
- Add request/response examples
- Follow Ruby Style Guide

Authentication: [specify authentication method]
Version: [API version if applicable]
```

### Service Object Generation

**Basic Service:**
```
Create a Ruby service object for [Business Operation].

Input: [describe input parameters]
Output: [describe expected output]

Requirements:
- Follow Ruby Style Guide
- Use descriptive method names
- Include error handling
- Add YARD documentation
- Make it testable
- Handle edge cases

Business Logic:
- [describe the main business logic]
- [include any specific requirements]
```

**Complex Service with Dependencies:**
```
Create a Ruby service object for [Complex Business Operation] that integrates with [external services].

Dependencies:
- [dependency 1]: [purpose]
- [dependency 2]: [purpose]

Input: [describe input parameters]
Output: [describe expected output]

Requirements:
- Follow Ruby Style Guide
- Use dependency injection
- Include comprehensive error handling
- Add logging for important operations
- Make it easily testable
- Include YARD documentation with examples

Business Logic:
- [step 1]
- [step 2]
- [step 3]

Error Scenarios:
- [scenario 1]
- [scenario 2]
```

## 🔧 Specific Use Cases

### CRUD Operations

**Complete CRUD with Validations:**
```
Generate a complete CRUD implementation for [Model] with:

Model:
- Attributes: [list with types]
- Validations: [specific validation requirements]
- Associations: [relationships with other models]

Controller:
- Standard RESTful actions
- Proper error handling
- Strong parameters
- Flash messages

Views (if needed):
- Form helpers
- Error display
- Success messages

Requirements:
- Follow Rails conventions
- Use Ruby Style Guide
- Include YARD documentation
- Make it production-ready
```

### Background Jobs

**Sidekiq Job:**
```
Create a Sidekiq background job for [Job Purpose].

Input: [describe job parameters]
Output: [describe expected outcome]

Requirements:
- Follow Ruby Style Guide
- Include proper error handling and retry logic
- Add logging for monitoring
- Handle job failures gracefully
- Include YARD documentation
- Make it idempotent if possible

Business Logic:
- [describe what the job does]
- [include any specific requirements]
```

### Form Objects

**Complex Form:**
```
Create a Rails form object for [Form Purpose] that handles multiple models.

Models involved:
- [Model 1]: [attributes]
- [Model 2]: [attributes]

Validation requirements:
- [validation 1]
- [validation 2]

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include proper validation
- Handle nested attributes
- Add error handling
- Include YARD documentation
- Make it easily testable

Business Logic:
- [describe form processing logic]
```

## 🎨 Style and Convention Prompts

### Ruby Style Guide Compliance

**Style-Aware Generation:**
```
Generate [code type] following the Ruby Style Guide:

Requirements:
- Use 2-space indentation
- Prefer single quotes for strings
- Use descriptive variable names
- Avoid unnecessary parentheses
- Use guard clauses where appropriate
- Follow naming conventions
- Include YARD documentation

Context: [describe the specific use case]
```

### Rails Conventions

**Convention-Compliant Code:**
```
Generate [Rails component] following Rails conventions:

Requirements:
- Follow Rails naming conventions
- Use Rails helpers and methods
- Include proper error handling
- Use Rails conventions for associations
- Follow RESTful patterns
- Include appropriate callbacks
- Add YARD documentation

Framework: Rails [version]
Context: [describe the specific use case]
```

## 🔍 Quality Assurance Prompts

### Code Review Preparation

**Review-Ready Code:**
```
Generate [code type] that's ready for code review:

Requirements:
- Follow Ruby Style Guide and Rails conventions
- Include comprehensive error handling
- Add meaningful comments and YARD documentation
- Use descriptive method and variable names
- Handle edge cases
- Include examples in documentation
- Make it easily testable

Context: [describe the specific use case]
Review Criteria: [mention specific review criteria]
```

### Production-Ready Code

**Production Standards:**
```
Generate production-ready [code type] with:

Requirements:
- Follow Ruby Style Guide and Rails conventions
- Include comprehensive error handling and logging
- Add proper validation and sanitization
- Include performance considerations
- Add security best practices
- Include monitoring and observability
- Add YARD documentation with examples
- Make it easily maintainable

Context: [describe the specific use case]
Performance Requirements: [mention any performance constraints]
Security Requirements: [mention any security considerations]
```

## 📝 Example Prompts

### Before (Ineffective)
```
Write a method to get users
```

### After (Effective)
```
Write a Ruby method following Rails conventions to find a user by ID. Use idiomatic Ruby patterns, avoid explicit nil checks, and follow the Ruby Style Guide. The method should integrate well with Rails controllers and handle the ActiveRecord::RecordNotFound exception appropriately.

Context: This is for a Rails 7 application with User model that has standard attributes (id, email, name, created_at, updated_at).

Requirements:
- Use Rails conventions
- Follow Ruby Style Guide
- Include YARD documentation
- Handle edge cases
- Make it easily testable
```

## 🎯 Pro Tips

1. **Be Specific**: The more context you provide, the better the output
2. **Mention Constraints**: Specify what you don't want as well as what you do
3. **Request Explanations**: Ask AI to explain its approach
4. **Iterate**: Use follow-up prompts to refine the output
5. **Validate**: Always review generated code for Ruby idiomaticity

## 🔗 Related Resources

- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Style Guide](https://rails.rubystyle.guide/)
- [YARD Documentation](https://yardoc.org/)
- [Rails Guides](https://guides.rubyonrails.org/)

---

*Remember: AI generates code, but you're the Ruby expert. Always review and validate the output!* 💎
