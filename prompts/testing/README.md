# Testing Prompts

*AI prompts for generating comprehensive Ruby and Rails tests with RSpec*

## 🎯 Overview

Testing with AI requires careful prompting to ensure comprehensive coverage, proper test structure, and Ruby testing best practices. These prompts help you generate tests that are maintainable, readable, and effective.

## 📋 Best Practices

- **Specify testing framework**: Always mention RSpec, Minitest, etc.
- **Include edge cases**: Request tests for boundary conditions
- **Mock external dependencies**: Specify what should be mocked
- **Follow testing conventions**: Use proper describe/context/it structure
- **Request explanations**: Ask AI to explain test strategy

## 🚀 Prompt Templates

### RSpec Test Generation

**Basic Model Tests:**
```
Generate comprehensive RSpec tests for this Ruby model:

[Paste model code here]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all validations
- Test all associations
- Test all public methods
- Include edge cases and error scenarios
- Use descriptive test names
- Add proper setup and teardown
- Include YARD documentation for test methods

Context: [describe the model's purpose and business logic]
Testing Framework: RSpec
```

**Complex Model Tests:**
```
Generate comprehensive RSpec tests for this complex Ruby model:

[Paste model code here]

Model Features:
- [feature 1]
- [feature 2]
- [feature 3]

Business Rules:
- [rule 1]
- [rule 2]
- [rule 3]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all validations and custom validators
- Test all associations and dependent options
- Test all callbacks and their effects
- Test all scopes and class methods
- Test all instance methods
- Include edge cases and error scenarios
- Test performance considerations
- Use factories for test data
- Add proper setup and teardown
- Include YARD documentation

Context: [describe the model's purpose and business logic]
Testing Framework: RSpec
Factory: [specify factory library if used]
```

### Controller Tests

**RESTful Controller Tests:**
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
Authentication: [specify authentication method]
```

**API Controller Tests:**
```
Generate comprehensive RSpec tests for this Rails API controller:

[Paste API controller code here]

API Endpoints:
- [list all endpoints]

Authentication: [specify authentication method]
Response Format: JSON

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all API endpoints
- Test request/response formats
- Test HTTP status codes
- Test error responses
- Test authentication and authorization
- Test parameter validation
- Include edge cases and error scenarios
- Test pagination if applicable
- Use proper test data setup
- Add YARD documentation

Context: [describe the API's purpose and business logic]
Testing Framework: RSpec
Authentication: [specify authentication method]
```

### Service Object Tests

**Basic Service Tests:**
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

**Complex Service Tests:**
```
Generate comprehensive RSpec tests for this complex Ruby service object:

[Paste service code here]

Service Purpose: [describe what the service does]
Dependencies: [list all dependencies]
Input: [describe input parameters]
Output: [describe expected output]

Business Logic:
- [step 1]
- [step 2]
- [step 3]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test successful execution path
- Test all error scenarios
- Test input validation
- Test output format
- Test side effects
- Test dependency interactions
- Include edge cases and boundary conditions
- Mock all external dependencies
- Test performance considerations
- Use descriptive test names
- Add YARD documentation

Context: [describe the service's purpose and business logic]
Testing Framework: RSpec
Dependencies: [list external dependencies to mock]
```

### Integration Tests

**Feature Tests:**
```
Generate comprehensive RSpec feature tests for this user workflow:

[Describe the user workflow]

Workflow Steps:
- [step 1]
- [step 2]
- [step 3]

User Roles: [specify user roles involved]
Authentication: [specify authentication requirements]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test complete user workflow
- Test different user roles
- Test error scenarios
- Test edge cases
- Use proper test data setup
- Include accessibility considerations
- Add YARD documentation

Context: [describe the feature's purpose and business logic]
Testing Framework: RSpec
Browser: [specify browser testing tool if used]
```

**System Tests:**
```
Generate comprehensive RSpec system tests for this application feature:

[Describe the application feature]

Feature Components:
- [component 1]
- [component 2]
- [component 3]

User Journey: [describe the user journey]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test complete user journey
- Test different scenarios
- Test error handling
- Test edge cases
- Use proper test data setup
- Include performance considerations
- Add YARD documentation

Context: [describe the feature's purpose and business logic]
Testing Framework: RSpec
Browser: [specify browser testing tool]
```

## 🔧 Specific Testing Scenarios

### Edge Case Testing

**Boundary Condition Tests:**
```
Generate RSpec tests for boundary conditions and edge cases for this Ruby code:

[Paste code here]

Boundary Conditions:
- [condition 1]
- [condition 2]
- [condition 3]

Edge Cases:
- [case 1]
- [case 2]
- [case 3]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all boundary conditions
- Test all edge cases
- Test error scenarios
- Test performance limits
- Use descriptive test names
- Add YARD documentation

Context: [describe the code's purpose and business logic]
Testing Framework: RSpec
```

### Performance Testing

**Performance Test Generation:**
```
Generate RSpec performance tests for this Ruby code:

[Paste code here]

Performance Requirements:
- [requirement 1]
- [requirement 2]

Load Scenarios:
- [scenario 1]
- [scenario 2]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test performance under load
- Test memory usage
- Test response times
- Include benchmarking
- Test scalability
- Add YARD documentation

Context: [describe the code's purpose and performance requirements]
Testing Framework: RSpec
```

### Security Testing

**Security Test Generation:**
```
Generate RSpec security tests for this Ruby code:

[Paste code here]

Security Concerns:
- [concern 1]
- [concern 2]

Attack Vectors:
- [vector 1]
- [vector 2]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test input validation
- Test authorization
- Test data sanitization
- Test SQL injection prevention
- Test XSS prevention
- Add YARD documentation

Context: [describe the code's purpose and security requirements]
Testing Framework: RSpec
```

## 🎨 Test Organization

### Test Structure

**Well-Organized Test Suite:**
```
Generate a well-organized RSpec test suite for this Ruby class:

[Paste class code here]

Test Organization:
- Group related tests
- Use descriptive describe/context blocks
- Include proper setup and teardown
- Use shared examples where appropriate

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Organize tests logically
- Use descriptive test names
- Include proper setup and teardown
- Use shared examples for common patterns
- Add YARD documentation

Context: [describe the class's purpose and business logic]
Testing Framework: RSpec
```

### Shared Examples

**Shared Example Generation:**
```
Generate RSpec shared examples for this common pattern:

[Describe the common pattern]

Pattern Usage:
- [usage 1]
- [usage 2]
- [usage 3]

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Create reusable shared examples
- Include proper parameterization
- Add comprehensive documentation
- Make it easily testable

Context: [describe the pattern's purpose and usage]
Testing Framework: RSpec
```

## 🔍 Test Quality Assurance

### Test Coverage

**Comprehensive Test Coverage:**
```
Generate tests with comprehensive coverage for this Ruby code:

[Paste code here]

Coverage Requirements:
- 100% line coverage
- 100% branch coverage
- All edge cases
- All error scenarios

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Achieve comprehensive coverage
- Test all code paths
- Include edge cases
- Test error scenarios
- Add YARD documentation

Context: [describe the code's purpose and business logic]
Testing Framework: RSpec
```

### Test Maintainability

**Maintainable Test Suite:**
```
Generate maintainable RSpec tests for this Ruby code:

[Paste code here]

Maintainability Requirements:
- Easy to understand
- Easy to modify
- Well-documented
- Properly organized

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Create maintainable tests
- Use descriptive names
- Include comprehensive documentation
- Organize logically
- Add YARD documentation

Context: [describe the code's purpose and business logic]
Testing Framework: RSpec
```

## 📝 Example Testing Prompts

### Before (Ineffective)
```
Write tests for this method
```

### After (Effective)
```
Generate comprehensive RSpec tests for this Ruby method:

```ruby
def calculate_discount(price, discount_percentage, user_type)
  return 0 if price <= 0 || discount_percentage <= 0
  
  base_discount = price * (discount_percentage / 100.0)
  
  case user_type
  when 'premium'
    base_discount * 1.2
  when 'vip'
    base_discount * 1.5
  else
    base_discount
  end
end
```

Requirements:
- Follow RSpec conventions and Ruby Style Guide
- Test all code paths
- Test edge cases (zero/negative values)
- Test different user types
- Test error scenarios
- Use descriptive test names
- Add YARD documentation

Context: This method calculates discounts for e-commerce orders based on price, discount percentage, and user type. Premium and VIP users get additional multipliers.
Testing Framework: RSpec
```

## 🎯 Pro Tips

1. **Be Specific**: Include all requirements and constraints
2. **Request Edge Cases**: Always ask for boundary condition tests
3. **Mock Dependencies**: Specify what should be mocked
4. **Validate Output**: Review generated tests for completeness
5. **Iterate**: Use follow-up prompts to add missing test cases

## 🔗 Related Resources

- [RSpec Documentation](https://rspec.info/)
- [Rails Testing Guide](https://guides.rubyonrails.org/testing.html)
- [Ruby Style Guide](https://rubystyle.guide/)
- [Factory Bot](https://github.com/thoughtbot/factory_bot)
- [VCR](https://github.com/vcr/vcr) - HTTP interaction recording

---

*Remember: Good tests are readable, maintainable, and comprehensive. AI can help generate them, but you should always review and validate!* 💎
