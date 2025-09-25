# Before/After Examples

*Real-world examples showing the difference between ineffective and effective AI prompting*

## 🎯 Overview

These examples demonstrate how thoughtful prompting can dramatically improve AI output quality. Each example shows a "before" (ineffective) prompt and an "after" (effective) prompt with the resulting code differences.

## 📋 How to Use These Examples

1. **Study the patterns**: Notice what makes prompts effective
2. **Adapt to your needs**: Modify the effective prompts for your specific use cases
3. **Practice**: Try the effective prompts with your own code
4. **Iterate**: Use follow-up prompts to refine the output

## 🚀 Code Generation Examples

### Example 1: User Model Generation

#### ❌ Before (Ineffective)
```
Create a user model
```

**AI Output:**
```ruby
class User < ApplicationRecord
  validates :name, presence: true
  validates :email, presence: true
end
```

#### ✅ After (Effective)
```
Create a Rails model for User with the following attributes:
- name: string (required)
- email: string (required, unique)
- password_digest: string (required)
- role: string (default: 'user')
- created_at: datetime
- updated_at: datetime

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include appropriate validations
- Add secure password functionality
- Include role-based functionality
- Use descriptive method names
- Include YARD documentation

Example usage: This model will be used for authentication and authorization in a Rails application.
```

**AI Output:**
```ruby
# frozen_string_literal: true

# User model for authentication and authorization
#
# @example Creating a new user
#   user = User.create!(name: "John Doe", email: "john@example.com", password: "secret123")
#   user.authenticate("secret123") # => user
#
# @example Checking user role
#   user.admin? # => false
#   user.update!(role: "admin")
#   user.admin? # => true
class User < ApplicationRecord
  has_secure_password

  validates :name, presence: true, length: { minimum: 2, maximum: 100 }
  validates :email, presence: true, 
            uniqueness: { case_sensitive: false },
            format: { with: URI::MailTo::EMAIL_REGEXP }
  validates :role, presence: true, 
            inclusion: { in: %w[user admin moderator] }

  scope :admins, -> { where(role: 'admin') }
  scope :moderators, -> { where(role: ['admin', 'moderator']) }

  # @return [Boolean] true if user is an admin
  def admin?
    role == 'admin'
  end

  # @return [Boolean] true if user is a moderator or admin
  def moderator?
    %w[admin moderator].include?(role)
  end

  # @return [String] user's display name
  def display_name
    name.presence || email.split('@').first
  end
end
```

### Example 2: Controller Action Generation

#### ❌ Before (Ineffective)
```
Write a controller action to create a post
```

**AI Output:**
```ruby
def create
  @post = Post.new(post_params)
  if @post.save
    redirect_to @post
  else
    render :new
  end
end
```

#### ✅ After (Effective)
```
Create a Rails controller action for creating a blog post with the following requirements:

Input: Post parameters (title, content, author_id, published_at)
Output: Redirect to post show page on success, render new form on failure

Business Rules:
- Only authenticated users can create posts
- Posts must have a title and content
- Author is automatically set to current user
- Published_at is optional (draft if not set)

Requirements:
- Follow Rails conventions and Ruby Style Guide
- Include proper error handling
- Use strong parameters
- Add flash messages
- Handle edge cases gracefully
- Include YARD documentation

Context: This is for a blog application where users can create and manage their own posts.
```

**AI Output:**
```ruby
# Creates a new blog post
#
# @example Successful creation
#   POST /posts
#   # => redirects to /posts/123 with success message
#
# @example Failed creation
#   POST /posts
#   # => renders :new with error messages
#
# @return [void]
def create
  @post = current_user.posts.build(post_params)
  
  if @post.save
    flash[:success] = "Post '#{@post.title}' was successfully created."
    redirect_to @post
  else
    flash.now[:error] = "There was a problem creating your post."
    render :new, status: :unprocessable_entity
  end
rescue StandardError => e
  Rails.logger.error "Post creation failed: #{e.message}"
  flash[:error] = "An unexpected error occurred. Please try again."
  redirect_to new_post_path
end

private

# Strong parameters for post creation
#
# @return [ActionController::Parameters] permitted post parameters
def post_params
  params.require(:post).permit(:title, :content, :published_at)
end
```

## 🔧 Refactoring Examples

### Example 3: Method Refactoring

#### ❌ Before (Ineffective)
```
Make this method better
```

**Original Code:**
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

#### ✅ After (Effective)
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

**AI Output:**
```ruby
# Finds a user by ID
#
# @param user_id [Integer, String] the ID of the user to find
# @return [User, nil] the user if found, nil otherwise
#
# @example Finding an existing user
#   find_user(123) # => #<User id: 123, name: "John">
#
# @example Finding a non-existent user
#   find_user(999) # => nil
def find_user(user_id)
  User.find_by(id: user_id)
end
```

**Explanation of Changes:**
- Removed explicit nil checks (Ruby handles this automatically)
- Used `find_by` instead of `where.first` (more idiomatic)
- Removed unnecessary `return` statements
- Simplified method name to be more descriptive
- Added comprehensive YARD documentation
- Reduced from 11 lines to 1 line while maintaining functionality

### Example 4: Complex Refactoring

#### ❌ Before (Ineffective)
```
Refactor this code
```

**Original Code:**
```ruby
class OrderProcessor
  def process_order(order)
    if order.valid?
      if order.payment.valid?
        if order.inventory.available?
          order.status = 'processing'
          order.save!
          
          # Send confirmation email
          UserMailer.order_confirmation(order.user, order).deliver_now
          
          # Update inventory
          order.items.each do |item|
            item.product.update!(stock: item.product.stock - item.quantity)
          end
          
          # Process payment
          payment_result = PaymentGateway.charge(order.payment, order.total)
          if payment_result.success?
            order.status = 'completed'
            order.save!
            return { success: true, message: 'Order processed successfully' }
          else
            order.status = 'payment_failed'
            order.save!
            return { success: false, message: 'Payment failed' }
          end
        else
          return { success: false, message: 'Insufficient inventory' }
        end
      else
        return { success: false, message: 'Invalid payment' }
      end
    else
      return { success: false, message: 'Invalid order' }
    end
  end
end
```

#### ✅ After (Effective)
```
Refactor this OrderProcessor class to improve maintainability and readability:

```ruby
[Paste original code here]
```

Current Issues:
- Deeply nested conditionals
- Multiple responsibilities in one method
- Poor error handling
- Hard to test individual components

Requirements:
- Maintain exact same functionality
- Follow Ruby Style Guide
- Break down into smaller, focused methods
- Improve error handling
- Add comprehensive YARD documentation
- Make it more testable
- Explain the refactoring approach

Context: This is an e-commerce order processing system that handles validation, inventory, payment, and notifications.
```

**AI Output:**
```ruby
# frozen_string_literal: true

# Processes e-commerce orders through validation, inventory, and payment
#
# @example Processing a valid order
#   processor = OrderProcessor.new
#   result = processor.process_order(order)
#   # => { success: true, message: 'Order processed successfully' }
#
# @example Processing an invalid order
#   result = processor.process_order(invalid_order)
#   # => { success: false, message: 'Invalid order' }
class OrderProcessor
  # Processes an order through the complete workflow
  #
  # @param order [Order] the order to process
  # @return [Hash] result hash with success status and message
  def process_order(order)
    return validation_error('Invalid order') unless order.valid?
    return validation_error('Invalid payment') unless order.payment.valid?
    return validation_error('Insufficient inventory') unless inventory_available?(order)

    process_valid_order(order)
  rescue StandardError => e
    handle_processing_error(order, e)
  end

  private

  # Processes a validated order through completion
  #
  # @param order [Order] the validated order
  # @return [Hash] success result
  def process_valid_order(order)
    order.update!(status: 'processing')
    
    send_confirmation_email(order)
    update_inventory(order)
    
    payment_result = process_payment(order)
    handle_payment_result(order, payment_result)
  end

  # Checks if inventory is available for all order items
  #
  # @param order [Order] the order to check
  # @return [Boolean] true if inventory is available
  def inventory_available?(order)
    order.items.all? { |item| item.product.stock >= item.quantity }
  end

  # Sends order confirmation email
  #
  # @param order [Order] the order to confirm
  # @return [void]
  def send_confirmation_email(order)
    UserMailer.order_confirmation(order.user, order).deliver_now
  end

  # Updates inventory for all order items
  #
  # @param order [Order] the order to process
  # @return [void]
  def update_inventory(order)
    order.items.each do |item|
      item.product.update!(stock: item.product.stock - item.quantity)
    end
  end

  # Processes payment for the order
  #
  # @param order [Order] the order to charge
  # @return [PaymentResult] the payment processing result
  def process_payment(order)
    PaymentGateway.charge(order.payment, order.total)
  end

  # Handles payment processing result
  #
  # @param order [Order] the order being processed
  # @param payment_result [PaymentResult] the payment result
  # @return [Hash] result hash
  def handle_payment_result(order, payment_result)
    if payment_result.success?
      order.update!(status: 'completed')
      { success: true, message: 'Order processed successfully' }
    else
      order.update!(status: 'payment_failed')
      { success: false, message: 'Payment failed' }
    end
  end

  # Creates a validation error result
  #
  # @param message [String] the error message
  # @return [Hash] error result hash
  def validation_error(message)
    { success: false, message: message }
  end

  # Handles unexpected processing errors
  #
  # @param order [Order] the order being processed
  # @param error [StandardError] the error that occurred
  # @return [Hash] error result hash
  def handle_processing_error(order, error)
    Rails.logger.error "Order processing failed: #{error.message}"
    order.update!(status: 'error') if order.persisted?
    { success: false, message: 'An unexpected error occurred' }
  end
end
```

**Explanation of Refactoring:**
- **Extracted methods**: Broke down the monolithic method into focused, single-responsibility methods
- **Improved readability**: Each method has a clear purpose and is easy to understand
- **Better error handling**: Added comprehensive error handling with logging
- **Enhanced testability**: Each method can now be tested independently
- **Added documentation**: Comprehensive YARD documentation for all methods
- **Maintained functionality**: All original behavior is preserved

## 🧪 Testing Examples

### Example 5: Test Generation

#### ❌ Before (Ineffective)
```
Write tests for this method
```

**Method to Test:**
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

#### ✅ After (Effective)
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

**AI Output:**
```ruby
# frozen_string_literal: true

require 'rails_helper'

RSpec.describe DiscountCalculator, '#calculate_discount' do
  let(:calculator) { described_class.new }

  describe 'with valid inputs' do
    context 'for regular users' do
      it 'calculates standard discount' do
        result = calculator.calculate_discount(100, 10, 'regular')
        expect(result).to eq(10.0)
      end

      it 'calculates discount for larger amounts' do
        result = calculator.calculate_discount(1000, 15, 'regular')
        expect(result).to eq(150.0)
      end
    end

    context 'for premium users' do
      it 'applies 20% premium multiplier' do
        result = calculator.calculate_discount(100, 10, 'premium')
        expect(result).to eq(12.0) # 10 * 1.2
      end

      it 'calculates premium discount for larger amounts' do
        result = calculator.calculate_discount(1000, 15, 'premium')
        expect(result).to eq(180.0) # 150 * 1.2
      end
    end

    context 'for VIP users' do
      it 'applies 50% VIP multiplier' do
        result = calculator.calculate_discount(100, 10, 'vip')
        expect(result).to eq(15.0) # 10 * 1.5
      end

      it 'calculates VIP discount for larger amounts' do
        result = calculator.calculate_discount(1000, 15, 'vip')
        expect(result).to eq(225.0) # 150 * 1.5
      end
    end
  end

  describe 'with edge cases' do
    context 'when price is zero or negative' do
      it 'returns 0 for zero price' do
        result = calculator.calculate_discount(0, 10, 'regular')
        expect(result).to eq(0)
      end

      it 'returns 0 for negative price' do
        result = calculator.calculate_discount(-100, 10, 'regular')
        expect(result).to eq(0)
      end
    end

    context 'when discount percentage is zero or negative' do
      it 'returns 0 for zero discount percentage' do
        result = calculator.calculate_discount(100, 0, 'regular')
        expect(result).to eq(0)
      end

      it 'returns 0 for negative discount percentage' do
        result = calculator.calculate_discount(100, -10, 'regular')
        expect(result).to eq(0)
      end
    end

    context 'with decimal inputs' do
      it 'handles decimal prices correctly' do
        result = calculator.calculate_discount(99.99, 10, 'regular')
        expect(result).to eq(9.999)
      end

      it 'handles decimal discount percentages correctly' do
        result = calculator.calculate_discount(100, 12.5, 'regular')
        expect(result).to eq(12.5)
      end
    end
  end

  describe 'with invalid user types' do
    it 'treats unknown user types as regular users' do
      result = calculator.calculate_discount(100, 10, 'unknown')
      expect(result).to eq(10.0)
    end

    it 'handles nil user type as regular user' do
      result = calculator.calculate_discount(100, 10, nil)
      expect(result).to eq(10.0)
    end

    it 'handles empty string user type as regular user' do
      result = calculator.calculate_discount(100, 10, '')
      expect(result).to eq(10.0)
    end
  end

  describe 'with extreme values' do
    it 'handles very large prices' do
      result = calculator.calculate_discount(1_000_000, 1, 'regular')
      expect(result).to eq(10_000.0)
    end

    it 'handles very large discount percentages' do
      result = calculator.calculate_discount(100, 100, 'regular')
      expect(result).to eq(100.0)
    end

    it 'handles very large discount percentages for premium users' do
      result = calculator.calculate_discount(100, 100, 'premium')
      expect(result).to eq(120.0)
    end
  end
end
```

## 🎯 Key Takeaways

### What Makes Prompts Effective

1. **Specificity**: The more specific you are, the better the output
2. **Context**: Provide relevant background information
3. **Requirements**: List specific requirements and constraints
4. **Examples**: Include examples of expected usage
5. **Framework**: Specify the framework and version
6. **Style**: Reference style guides and conventions

### Common Patterns in Effective Prompts

- **Role-based**: "Act as a senior Ruby developer..."
- **Constraint-based**: "Use only standard library methods..."
- **Pattern-based**: "Follow the same pattern as this existing code..."
- **Style-aware**: "Write in the style of this codebase..."

### Red Flags in Ineffective Prompts

- Too vague: "Make this better"
- No context: Missing business logic explanation
- No requirements: No specific constraints or guidelines
- No examples: No usage examples or expected output
- No framework: Missing technology stack information

## 🔗 Related Resources

- [Ruby Style Guide](https://rubystyle.guide/)
- [Rails Style Guide](https://rails.rubystyle.guide/)
- [RSpec Documentation](https://rspec.info/)
- [YARD Documentation](https://yardoc.org/)

---

*Remember: The quality of your prompts directly impacts the quality of AI output. Take time to craft thoughtful, specific prompts!* 💎
