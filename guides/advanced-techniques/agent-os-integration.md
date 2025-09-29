# Agent OS Integration for Ruby Development

*Structured workflows for consistent, high-quality AI code generation*

## 🎯 What is Agent OS?

Agent OS is an open-source system that transforms AI coding agents into productive developers by providing structured workflows that capture your standards, stack, and codebase details. Instead of random prompting, it provides a systematic approach to AI-assisted development.

## 🏗️ Core Components

### 1. Standards Layer

The Standards Layer defines your technical stack, coding conventions, and quality requirements.

**Example: `config/agent-os-standards.yml`**
```yaml
# Technical Stack
tech_stack:
  framework: "Rails 7.1"
  ruby_version: "3.3.0"
  database: "PostgreSQL 15"
  cache: "Redis 7"
  background_jobs: "Sidekiq 7"
  api: "GraphQL with Apollo"
  testing: "RSpec, FactoryBot, Capybara"
  deployment: "Docker, AWS ECS"

# Coding Standards
coding_standards:
  style_guide: "Ruby Style Guide (rubystyle.guide)"
  documentation: "YARD with examples"
  error_handling: "comprehensive with structured logging"
  performance: "N+1 query prevention, eager loading"
  security: "OWASP guidelines, input validation"
  testing: "TDD approach, 90%+ coverage"

# Naming Conventions
conventions:
  methods: "snake_case, descriptive names"
  classes: "PascalCase, single responsibility"
  constants: "SCREAMING_SNAKE_CASE"
  files: "snake_case.rb"
  directories: "snake_case/"

# Code Organization
organization:
  models: "app/models with concerns in app/models/concerns"
  controllers: "app/controllers with API in app/controllers/api"
  services: "app/services with subdirectories by domain"
  jobs: "app/jobs with queue-specific subdirectories"
  serializers: "app/serializers for API responses"
```

### 2. Product Layer

The Product Layer documents your application's purpose, architecture, and strategic decisions.

**Example: `config/agent-os-product.yml`**
```yaml
# Product Mission
mission: "Build a comprehensive project management platform for remote teams"

# Architecture Decisions
architecture:
  pattern: "Modular monolith with clear domain boundaries"
  api_design: "RESTful primary, GraphQL for complex queries"
  data_strategy: "Event sourcing for audit trails, CQRS for read models"
  authentication: "JWT with refresh tokens, OAuth for integrations"
  authorization: "Role-based with resource-level permissions"

# Technology Choices
technology_choices:
  - choice: "Rails over other frameworks"
    rationale: "Rapid development, strong ecosystem, team expertise"
    date: "2024-01-01"
  - choice: "PostgreSQL over MySQL"
    rationale: "Better JSON support, advanced indexing, ACID compliance"
    date: "2024-01-01"
  - choice: "GraphQL overlay on REST"
    rationale: "Flexible queries for mobile, backward compatibility"
    date: "2024-02-15"

# Roadmap Context
roadmap:
  q1_2024: "Core user management and project creation"
  q2_2024: "Task management and team collaboration"
  q3_2024: "Advanced reporting and analytics"
  q4_2024: "Integrations and mobile app"

# Domain Knowledge
domains:
  user_management:
    concepts: ["User", "Profile", "Authentication", "Authorization"]
    business_rules: ["Email verification required", "Password complexity rules"]
  
  project_management:
    concepts: ["Project", "Task", "Milestone", "Team", "Assignment"]
    business_rules: ["Projects have owners", "Tasks belong to projects", "Team members have roles"]
```

### 3. Specs Layer

The Specs Layer provides detailed specifications for current features and tasks.

**Example: `config/agent-os-specs.yml`**
```yaml
# Current Feature
current_feature: "User Project Assignment with Role-Based Permissions"

# Feature Requirements
requirements:
  functional:
    - "Users can be assigned to multiple projects"
    - "Each assignment has a specific role (admin, member, viewer)"
    - "Role determines permissions within the project"
    - "Assignment history is tracked for audit purposes"
  
  non_functional:
    - "Assignment operations must be atomic"
    - "Permission checks must be performant (< 10ms)"
    - "Audit trail must be immutable"

# Technical Specifications
technical_specs:
  models:
    - name: "ProjectAssignment"
      attributes:
        - "user_id: references users(id)"
        - "project_id: references projects(id)"
        - "role: enum [admin, member, viewer]"
        - "assigned_at: timestamp"
        - "assigned_by_id: references users(id)"
      validations:
        - "unique combination of user_id and project_id"
        - "role must be present"
        - "assigned_by must be project admin or system admin"
      associations:
        - "belongs_to :user"
        - "belongs_to :project"
        - "belongs_to :assigned_by, class_name: 'User'"
  
  controllers:
    - name: "ProjectAssignmentsController"
      actions: ["index", "create", "update", "destroy"]
      authorization: "project admin or system admin"
      response_format: "JSON with proper HTTP status codes"
  
  services:
    - name: "ProjectAssignmentService"
      methods: ["assign_user", "update_role", "remove_assignment"]
      error_handling: "Custom exceptions with user-friendly messages"

# Implementation Tasks
tasks:
  - task: "Create ProjectAssignment model"
    acceptance_criteria:
      - "Model created with all required attributes"
      - "Validations implemented and tested"
      - "Associations properly defined"
  
  - task: "Implement ProjectAssignmentService"
    acceptance_criteria:
      - "Service handles all assignment operations"
      - "Proper error handling and logging"
      - "Comprehensive test coverage"
  
  - task: "Create API endpoints"
    acceptance_criteria:
      - "RESTful endpoints for CRUD operations"
      - "Proper authorization checks"
      - "JSON responses with appropriate status codes"
```

## 🔧 Implementation Guide

### Step 1: Setup Agent OS Context

**Create the context loader:**
```ruby
# lib/agent_os/context_loader.rb
module AgentOS
  class ContextLoader
    CONFIG_DIR = Rails.root.join('config', 'agent-os')
    
    def self.load_all_context
      {
        standards: load_standards,
        product: load_product,
        specs: load_specs
      }
    end
    
    def self.load_standards
      YAML.load_file(CONFIG_DIR.join('standards.yml'))
    rescue Errno::ENOENT
      Rails.logger.warn "Agent OS standards file not found"
      {}
    end
    
    def self.load_product
      YAML.load_file(CONFIG_DIR.join('product.yml'))
    rescue Errno::ENOENT
      Rails.logger.warn "Agent OS product file not found"
      {}
    end
    
    def self.load_specs
      YAML.load_file(CONFIG_DIR.join('specs.yml'))
    rescue Errno::ENOENT
      Rails.logger.warn "Agent OS specs file not found"
      {}
    end
  end
end
```

### Step 2: Create Enhanced Prompts

**Base prompt generator:**
```ruby
# lib/agent_os/prompt_generator.rb
module AgentOS
  class PromptGenerator
    def initialize(context = nil)
      @context = context || ContextLoader.load_all_context
    end
    
    def generate_prompt(task_description, additional_context = {})
      <<~PROMPT
        You are a senior Ruby developer working on a Rails application. Use the following context to generate high-quality, production-ready code.
        
        ## Technical Standards
        #{format_standards}
        
        ## Product Context
        #{format_product_context}
        
        ## Current Specifications
        #{format_current_specs}
        
        ## Task
        #{task_description}
        
        ## Additional Context
        #{format_additional_context(additional_context)}
        
        ## Requirements
        - Follow all standards and conventions defined above
        - Generate code that integrates with the existing architecture
        - Include comprehensive error handling
        - Add appropriate logging
        - Make it easily testable
        - Include YARD documentation
        - Consider performance implications
        - Follow security best practices
        
        Generate code that meets these requirements and follows Ruby/Rails best practices.
      PROMPT
    end
    
    private
    
    def format_standards
      return "No standards defined" if @context[:standards].empty?
      
      standards = @context[:standards]
      <<~STANDARDS
        **Tech Stack:** #{standards.dig('tech_stack')&.values&.join(', ')}
        **Style Guide:** #{standards.dig('coding_standards', 'style_guide')}
        **Documentation:** #{standards.dig('coding_standards', 'documentation')}
        **Testing:** #{standards.dig('coding_standards', 'testing')}
        **Naming Conventions:** #{standards.dig('conventions')&.values&.join(', ')}
      STANDARDS
    end
    
    def format_product_context
      return "No product context defined" if @context[:product].empty?
      
      product = @context[:product]
      <<~PRODUCT
        **Mission:** #{product['mission']}
        **Architecture Pattern:** #{product.dig('architecture', 'pattern')}
        **API Design:** #{product.dig('architecture', 'api_design')}
        **Current Focus:** #{product.dig('roadmap', 'current_quarter')}
      PRODUCT
    end
    
    def format_current_specs
      return "No current specifications" if @context[:specs].empty?
      
      specs = @context[:specs]
      <<~SPECS
        **Current Feature:** #{specs['current_feature']}
        **Key Requirements:** #{specs.dig('requirements', 'functional')&.join(', ')}
        **Technical Specs:** #{specs.dig('technical_specs')&.keys&.join(', ')}
      SPECS
    end
    
    def format_additional_context(additional_context)
      return "None" if additional_context.empty?
      
      additional_context.map { |key, value| "**#{key}:** #{value}" }.join("\n")
    end
  end
end
```

### Step 3: Integration with AI Models

**OpenAI integration:**
```ruby
# lib/agent_os/ai_client.rb
module AgentOS
  class AIClient
    def initialize(model: 'gpt-4', temperature: 0.1)
      @client = OpenAI::Client.new(access_token: ENV['OPENAI_API_KEY'])
      @model = model
      @temperature = temperature
    end
    
    def generate_code(prompt, max_tokens: 2000)
      response = @client.chat(
        parameters: {
          model: @model,
          messages: [
            {
              role: "system",
              content: "You are a senior Ruby developer with expertise in Rails, clean code, and best practices. Generate production-ready code that follows all specified standards and conventions."
            },
            {
              role: "user",
              content: prompt
            }
          ],
          max_tokens: max_tokens,
          temperature: @temperature
        }
      )
      
      response.dig("choices", 0, "message", "content")
    end
    
    def generate_with_context(task_description, additional_context = {})
      prompt_generator = PromptGenerator.new
      prompt = prompt_generator.generate_prompt(task_description, additional_context)
      
      generate_code(prompt)
    end
  end
end
```

### Step 4: Rake Tasks for Agent OS

**Create management tasks:**
```ruby
# lib/tasks/agent_os.rake
namespace :agent_os do
  desc "Initialize Agent OS configuration files"
  task :init => :environment do
    config_dir = Rails.root.join('config', 'agent-os')
    FileUtils.mkdir_p(config_dir)
    
    # Create default files if they don't exist
    create_default_standards(config_dir) unless File.exist?(config_dir.join('standards.yml'))
    create_default_product(config_dir) unless File.exist?(config_dir.join('product.yml'))
    create_default_specs(config_dir) unless File.exist?(config_dir.join('specs.yml'))
    
    puts "Agent OS configuration files created in #{config_dir}"
  end
  
  desc "Generate code using Agent OS context"
  task :generate, [:task_description] => :environment do |t, args|
    task_description = args[:task_description]
    
    if task_description.blank?
      puts "Usage: rails agent_os:generate['Create a user service object']"
      exit 1
    end
    
    client = AgentOS::AIClient.new
    code = client.generate_with_context(task_description)
    
    puts "Generated code:"
    puts "=" * 50
    puts code
    puts "=" * 50
  end
  
  desc "Validate Agent OS configuration"
  task :validate => :environment do
    context = AgentOS::ContextLoader.load_all_context
    
    puts "Validating Agent OS configuration..."
    
    if context[:standards].empty?
      puts "⚠️  Warning: No standards defined"
    else
      puts "✅ Standards loaded successfully"
    end
    
    if context[:product].empty?
      puts "⚠️  Warning: No product context defined"
    else
      puts "✅ Product context loaded successfully"
    end
    
    if context[:specs].empty?
      puts "⚠️  Warning: No current specifications defined"
    else
      puts "✅ Current specifications loaded successfully"
    end
  end
  
  private
  
  def create_default_standards(config_dir)
    # Implementation for creating default standards file
  end
  
  def create_default_product(config_dir)
    # Implementation for creating default product file
  end
  
  def create_default_specs(config_dir)
    # Implementation for creating default specs file
  end
end
```

## 🎯 Usage Examples

### Example 1: Generate a Service Object

```bash
rails agent_os:generate['Create a ProjectAssignmentService that handles user assignment to projects with role-based permissions']
```

**Generated output will include:**
- Proper service object structure following your standards
- Error handling with custom exceptions
- Logging for audit purposes
- YARD documentation
- Integration with your existing models

### Example 2: Generate a Model with Complex Validations

```bash
rails agent_os:generate['Create a ProjectAssignment model with validations for unique user-project combinations and role-based assignment permissions']
```

**Generated output will include:**
- Model with all required attributes and associations
- Custom validations following your business rules
- Proper error messages
- Database constraints
- Test factories

### Example 3: Generate API Controller

```bash
rails agent_os:generate['Create a RESTful API controller for ProjectAssignment with proper authorization and JSON responses']
```

**Generated output will include:**
- RESTful actions with proper HTTP status codes
- Authorization checks using your existing patterns
- Strong parameters
- Error handling with meaningful messages
- JSON serialization

## 🔄 Workflow Integration

### Development Workflow

1. **Start with Agent OS context**
   ```bash
   rails agent_os:init
   ```

2. **Update context as needed**
   - Modify `config/agent-os/standards.yml` for technical changes
   - Update `config/agent-os/product.yml` for architectural decisions
   - Edit `config/agent-os/specs.yml` for current feature specifications

3. **Generate code with context**
   ```bash
   rails agent_os:generate['Your task description']
   ```

4. **Review and refine**
   - Review generated code for Ruby idiomaticity
   - Test the generated code
   - Refine prompts based on results

### Team Workflow

1. **Shared context files**
   - Commit Agent OS configuration files to version control
   - Ensure all team members use the same context
   - Review context changes in pull requests

2. **Code review integration**
   - Include Agent OS context in code review discussions
   - Verify generated code follows established standards
   - Document any deviations from the context

3. **Continuous improvement**
   - Regularly update context based on new learnings
   - Refine prompts based on team feedback
   - Share effective prompt patterns

## 📊 Benefits

### Consistency
- All generated code follows the same standards
- Consistent naming conventions across the codebase
- Uniform error handling and logging patterns

### Quality
- Production-ready code from the start
- Comprehensive error handling
- Proper documentation and testing considerations

### Efficiency
- Faster development with structured prompts
- Reduced need for code review iterations
- Clear context for AI models

### Maintainability
- Well-documented architectural decisions
- Clear separation of concerns
- Easy to onboard new team members

## 🚀 Advanced Features

### Dynamic Context Loading

```ruby
# Load context based on current branch or environment
def load_context_for_branch
  branch = `git branch --show-current`.strip
  
  case branch
  when /feature\/user-management/
    load_user_management_context
  when /feature\/project-management/
    load_project_management_context
  else
    load_default_context
  end
end
```

### Context Validation

```ruby
# Validate context completeness
def validate_context
  required_sections = %w[tech_stack coding_standards conventions]
  missing_sections = required_sections - @context[:standards].keys
  
  if missing_sections.any?
    raise "Missing required context sections: #{missing_sections.join(', ')}"
  end
end
```

### Context Templates

```ruby
# Template system for different project types
def load_template(template_name)
  template_path = Rails.root.join('config', 'agent-os', 'templates', "#{template_name}.yml")
  YAML.load_file(template_path)
end
```

---

*Agent OS transforms AI code generation from random prompting to systematic, high-quality development. Start with the basics and gradually add complexity as your team becomes comfortable with the workflow.* 🚀

