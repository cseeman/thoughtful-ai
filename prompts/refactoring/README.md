# Refactoring Prompts

*AI prompts for improving existing Ruby code while maintaining functionality and readability*

## 🎯 Overview

Refactoring with AI requires careful prompting to ensure the output maintains Ruby's expressiveness and follows best practices. These prompts help you improve code quality while preserving the original intent.

## 📋 Best Practices

- **Preserve functionality**: Always specify that behavior must remain unchanged
- **Maintain readability**: Request explanations for complex changes
- **Follow style guides**: Reference Ruby and Rails style guides
- **Incremental changes**: Break large refactoring into smaller steps
- **Test coverage**: Ensure refactoring doesn't break existing tests

## 🚀 Prompt Templates

### Basic Refactoring

**Simple Method Refactoring:**
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

Context: [describe what the method does and its role in the application]
```

**Complex Method Refactoring:**
```
Refactor this complex Ruby method to improve maintainability and readability:

[Paste method code here]

Current Issues:
- [issue 1]
- [issue 2]
- [issue 3]

Requirements:
- Maintain exact same behavior
- Follow Ruby Style Guide
- Break down into smaller, focused methods
- Improve error handling
- Add comprehensive YARD documentation
- Make it more testable
- Explain the refactoring approach

Context: [describe the method's purpose and business logic]
```

### Rails-Specific Refactoring

**Controller Refactoring:**
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

**Model Refactoring:**
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

### Performance Refactoring

**Query Optimization:**
```
Refactor this Ruby code to improve database performance while maintaining functionality:

[Paste code here]

Current Performance Issues:
- [specific performance problems]

Requirements:
- Maintain exact same functionality
- Optimize database queries
- Follow Rails conventions and Ruby Style Guide
- Add query optimization techniques
- Include performance monitoring considerations
- Add YARD documentation
- Explain the performance improvements

Context: [describe the current performance requirements and constraints]
```

**Memory Optimization:**
```
Refactor this Ruby code to reduce memory usage while maintaining functionality:

[Paste code here]

Current Memory Issues:
- [specific memory problems]

Requirements:
- Maintain exact same functionality
- Reduce memory footprint
- Follow Ruby Style Guide
- Use efficient data structures
- Add memory monitoring considerations
- Add YARD documentation
- Explain the memory optimizations

Context: [describe the current memory constraints and usage patterns]
```

## 🔧 Specific Refactoring Scenarios

### Legacy Code Modernization

**Rails 3/4 to Rails 7:**
```
Modernize this legacy Rails code to Rails 7 standards while maintaining functionality:

[Paste legacy code here]

Legacy Issues:
- [specific legacy patterns that need updating]

Requirements:
- Maintain exact same functionality
- Update to Rails 7 conventions
- Follow current Ruby Style Guide
- Replace deprecated methods
- Improve security practices
- Add modern error handling
- Include YARD documentation
- Explain the modernization approach

Context: [describe the legacy code's purpose and current Rails version]
```

**Ruby 2.x to Ruby 3.x:**
```
Modernize this Ruby 2.x code to Ruby 3.x standards while maintaining functionality:

[Paste Ruby 2.x code here]

Legacy Issues:
- [specific Ruby 2.x patterns that need updating]

Requirements:
- Maintain exact same functionality
- Use Ruby 3.x features where appropriate
- Follow current Ruby Style Guide
- Replace deprecated syntax
- Improve performance where possible
- Add YARD documentation
- Explain the modernization approach

Context: [describe the code's purpose and current Ruby version]
```

### Code Organization

**Extract Service Objects:**
```
Refactor this controller/model code by extracting business logic into service objects:

[Paste code here]

Business Logic to Extract:
- [specific business operations]

Requirements:
- Maintain exact same functionality
- Follow Rails conventions and Ruby Style Guide
- Create focused service objects
- Improve testability
- Add comprehensive error handling
- Include YARD documentation
- Explain the extraction strategy

Context: [describe the business logic and current architecture]
```

**Extract Concerns:**
```
Refactor this model by extracting shared functionality into concerns:

[Paste model code here]

Shared Functionality:
- [specific shared behaviors]

Requirements:
- Maintain exact same functionality
- Follow Rails conventions and Ruby Style Guide
- Create focused concerns
- Improve code organization
- Add comprehensive YARD documentation
- Explain the extraction approach

Context: [describe the shared functionality and current model structure]
```

### Error Handling Improvement

**Comprehensive Error Handling:**
```
Refactor this Ruby code to improve error handling and resilience:

[Paste code here]

Current Error Handling Issues:
- [specific error handling problems]

Requirements:
- Maintain exact same functionality
- Follow Ruby Style Guide
- Add comprehensive error handling
- Use appropriate exception types
- Add logging for errors
- Include error recovery strategies
- Add YARD documentation
- Explain the error handling approach

Context: [describe the current error handling and reliability requirements]
```

## 🎨 Style and Convention Refactoring

### Ruby Style Guide Compliance

**Style Guide Refactoring:**
```
Refactor this Ruby code to strictly follow the Ruby Style Guide:

[Paste code here]

Style Issues:
- [specific style guide violations]

Requirements:
- Maintain exact same functionality
- Follow Ruby Style Guide exactly
- Improve code formatting
- Use consistent naming conventions
- Add proper spacing and indentation
- Include YARD documentation
- Explain the style improvements

Context: [describe the code's purpose and current style issues]
```

### Rails Conventions

**Rails Convention Refactoring:**
```
Refactor this Rails code to follow Rails conventions and best practices:

[Paste Rails code here]

Convention Issues:
- [specific Rails convention violations]

Requirements:
- Maintain exact same functionality
- Follow Rails conventions exactly
- Use Rails helpers and methods
- Improve RESTful patterns
- Add proper callbacks and filters
- Include YARD documentation
- Explain the convention improvements

Context: [describe the Rails component and current convention issues]
```

## 🔍 Advanced Refactoring Techniques

### Metaprogramming Refactoring

**Simplify Metaprogramming:**
```
Refactor this metaprogramming code to be more readable and maintainable:

[Paste metaprogramming code here]

Current Issues:
- [specific metaprogramming problems]

Requirements:
- Maintain exact same functionality
- Follow Ruby Style Guide
- Improve readability
- Add comprehensive documentation
- Make it more maintainable
- Include examples of usage
- Explain the metaprogramming approach

Context: [describe the metaprogramming purpose and current complexity]
```

### DSL Refactoring

**DSL Improvement:**
```
Refactor this DSL code to improve usability and maintainability:

[Paste DSL code here]

Current Issues:
- [specific DSL problems]

Requirements:
- Maintain exact same functionality
- Follow Ruby Style Guide
- Improve DSL usability
- Add comprehensive documentation
- Make it more intuitive
- Include usage examples
- Explain the DSL design approach

Context: [describe the DSL's purpose and current usability issues]
```

## 📝 Example Refactoring Prompts

### Before (Ineffective)
```
Make this code better
```

### After (Effective)
```
Refactor this Ruby method to improve readability and follow Ruby Style Guide while maintaining exact functionality:

```ruby
def get_user_by_id(user_id)
  if user_id != nil
    user = User.where(id: user_id).first
    if user != nil
      return user
    else
      return nil
    end
  else
    return nil
  end
end
```

Requirements:
- Maintain exact same behavior
- Follow Ruby Style Guide
- Improve readability
- Use idiomatic Ruby patterns
- Add YARD documentation
- Explain the changes made

Context: This method is used in a Rails controller to find users by ID. The current implementation has explicit nil checks and verbose conditional logic.
```

## 🎯 Pro Tips

1. **Start Small**: Refactor one method or class at a time
2. **Preserve Tests**: Ensure existing tests still pass
3. **Document Changes**: Ask AI to explain its refactoring approach
4. **Validate Output**: Always review refactored code for Ruby idiomaticity
5. **Iterate**: Use follow-up prompts to refine the refactoring

## 🔗 Related Resources

- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Style Guide](https://rails.rubystyle.guide/)
- [Refactoring: Improving the Design of Existing Code](https://martinfowler.com/books/refactoring.html)
- [Clean Code](https://www.oreilly.com/library/view/clean-code/9780136083238/)

---

*Remember: Refactoring should improve code quality without changing behavior. Always test thoroughly!* 💎
