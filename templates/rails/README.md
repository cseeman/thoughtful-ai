# Rails Prompt Templates

*Reusable prompt templates for common Rails development tasks*

## 🎯 Overview

These templates provide ready-to-use prompts for common Rails development scenarios. Customize them with your specific requirements and context.

## 🚀 Model Templates

### Basic Model Generation
```
Create a Rails model for [ModelName] with the following attributes:
- [attribute1]: [type] (required/optional)
- [attribute2]: [type] (required/optional)
- [attribute3]: [type] (required/optional)

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include appropriate validations
- Add any necessary associations
- Use descriptive method names
- Include YARD documentation

Example usage: [describe how the model will be used]
```

### Model with Business Logic
```
Create a Rails model for [ModelName] that handles [business requirement].

Attributes:
- [attribute1]: [type] (required/optional)
- [attribute2]: [type] (required/optional)

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

### Model with Associations
```
Create a Rails model for [ModelName] with the following associations:
- [association1]: [type] with [ModelName]
- [association2]: [type] with [ModelName]

Attributes:
- [attribute1]: [type] (required/optional)
- [attribute2]: [type] (required/optional)

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include appropriate validations
- Add proper association options (dependent, foreign_key, etc.)
- Include scopes for common queries
- Add YARD documentation

Context: [describe the relationship and business logic]
```

## 🎮 Controller Templates

### RESTful Controller
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

### API Controller
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

### Custom Controller Action
```
Create a custom Rails controller action for [ActionName] that [describes what it does].

Input: [describe input parameters]
Output: [describe expected output]

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include proper error handling
- Use strong parameters
- Add appropriate before_action filters
- Include flash messages
- Handle edge cases gracefully
- Add YARD documentation

Context: [describe the action's purpose and business logic]
```

## 🔧 Service Object Templates

### Basic Service Object
```
Create a Ruby service object for [BusinessOperation].

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

### Service Object with Dependencies
```
Create a Ruby service object for [BusinessOperation] that integrates with [external services].

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

## 🧪 Test Templates

### Model Tests
```
Generate comprehensive RSpec tests for this Rails model:

[Paste model code here]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all validations
- Test all associations
- Test all public methods
- Include edge cases and error scenarios
- Use descriptive test names
- Add proper setup and teardown
- Include YARD documentation

Context: [describe the model's purpose and business logic]
Testing Framework: RSpec
```

### Controller Tests
```
Generate comprehensive RSpec controller tests for this Rails controller:

[Paste controller code here]

Controller Actions:
- [list all actions]

Authentication: [specify authentication requirements]
Authorization: [specify authorization rules]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all controller actions
- Test authentication and authorization
- Test parameter handling
- Test response formats and status codes
- Test error handling
- Test flash messages
- Include edge cases and error scenarios
- Use proper test data setup
- Add YARD documentation

Context: [describe the controller's purpose and business logic]
Testing Framework: RSpec
```

### Service Object Tests
```
Generate comprehensive RSpec tests for this Ruby service object:

[Paste service code here]

Service Purpose: [describe what the service does]
Input: [describe input parameters]
Output: [describe expected output]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test successful execution
- Test error scenarios
- Test input validation
- Test output format
- Test side effects
- Include edge cases
- Mock external dependencies
- Use descriptive test names
- Add YARD documentation

Context: [describe the service's purpose and business logic]
Testing Framework: RSpec
Dependencies: [list external dependencies to mock]
```

## 🔄 Refactoring Templates

### Method Refactoring
```
Refactor this Ruby method to improve readability and follow Ruby Style Guide while maintaining exact functionality:

[Paste method code here]

Requirements:
- Maintain exact same behavior
- Follow Ruby Style Guide
- Improve readability
- Use idiomatic Ruby patterns
- Add YARD documentation
- Explain the changes made

Context: [describe the method's purpose and current issues]
```

### Controller Refactoring
```
Refactor this Rails controller to follow best practices and improve maintainability:

[Paste controller code here]

Current Issues:
- [specific issues you've identified]

Requirements:
- Maintain exact same functionality
- Follow Rails conventions and Ruby Style Guide
- Extract business logic to service objects where appropriate
- Improve error handling
- Add proper before_action filters
- Use strong parameters correctly
- Add YARD documentation
- Explain the refactoring strategy

Context: [describe the controller's purpose and current usage]
```

### Model Refactoring
```
Refactor this Rails model to improve organization and follow best practices:

[Paste model code here]

Current Issues:
- [specific issues you've identified]

Requirements:
- Maintain exact same functionality
- Follow Rails conventions and Ruby Style Guide
- Organize methods logically
- Extract complex logic to private methods
- Improve validation organization
- Add comprehensive YARD documentation
- Make it more maintainable
- Explain the refactoring approach

Context: [describe the model's purpose and relationships]
```

## 📝 Documentation Templates

### YARD Documentation
```
Add comprehensive YARD documentation to this Ruby code:

[Paste code here]

Requirements:
- Follow YARD documentation standards
- Include method descriptions
- Add parameter documentation
- Include return value documentation
- Add usage examples
- Include edge case documentation
- Add version information if applicable

Context: [describe the code's purpose and usage]
```

### README Generation
```
Generate a comprehensive README for this Rails application:

Application Purpose: [describe what the application does]
Key Features: [list main features]
Tech Stack: [list technologies used]

Requirements:
- Include installation instructions
- Include usage examples
- Include API documentation if applicable
- Include contribution guidelines
- Include license information
- Use clear, professional language

Context: [describe the application's purpose and target audience]
```

## 🚀 Migration Templates

### Basic Migration
```
Create a Rails migration to [describe what the migration does].

Requirements:
- Follow Rails conventions
- Include proper rollback functionality
- Add appropriate indexes
- Include data migration if needed
- Add comments explaining the purpose
- Follow Ruby Style Guide

Context: [describe the migration's purpose and business logic]
```

### Complex Migration
```
Create a Rails migration to [describe what the migration does] with the following requirements:

Changes:
- [change 1]
- [change 2]
- [change 3]

Data Migration:
- [describe any data migration needed]

Requirements:
- Follow Rails conventions
- Include proper rollback functionality
- Add appropriate indexes
- Handle data migration safely
- Add comments explaining the purpose
- Follow Ruby Style Guide
- Include error handling

Context: [describe the migration's purpose and business logic]
```

## 🔧 Custom Templates

### Form Object
```
Create a Rails form object for [FormPurpose] that handles multiple models.

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

### Background Job
```
Create a Sidekiq background job for [JobPurpose].

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

## 🎯 Usage Tips

### 1. Customize for Your Needs
- Replace placeholders with your specific requirements
- Add context about your application
- Include your team's conventions

### 2. Combine Templates
- Use multiple templates for complex features
- Combine model, controller, and test templates
- Add refactoring templates as needed

### 3. Iterate and Improve
- Start with basic templates
- Add more specific requirements
- Refine based on results

### 4. Save Effective Prompts
- Keep track of what works
- Build your own template library
- Share with your team

---

*Remember: These templates are starting points. Always customize them for your specific needs and context!* 💎
