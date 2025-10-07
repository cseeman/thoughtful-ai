# Testing Prompts

AI prompts for generating Ruby and Rails tests with RSpec.

## Overview

Testing is a top AI use case for Ruby developers, but it needs the right context. Specify your framework versions, available gems, and routing conventions to avoid common pitfalls.

## Quick Tips

- Specify testing framework and versions ("RSpec 3.12", "FactoryBot 6.4")
- List available tools (shoulda-matchers, VCR, FactoryBot)
- Mention routing conventions (Rails 7 uses full path helpers)
- Request edge cases explicitly
- Indicate dependencies to mock

## What Works and What Doesn't

Based on community feedback and experience.

### Example 1: Basic Method Tests

**❌ No Context**
```
Write tests for this method
```

Why it fails: No framework specified, no context, no available tools mentioned. Testing is a top use case for AI, but needs complete context.

**✅ Complete Context**
```
Context: Rails 7.1, RSpec 3.12, FactoryBot 6.4

Generate comprehensive RSpec tests for this method:

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
- Follow RSpec conventions
- Test all code paths (all user types)
- Test edge cases (zero/negative values, nil inputs, boundary conditions)
- Test float precision (currency calculations)
- Use descriptive describe/context/it structure

Context: E-commerce discount calculator. Premium users get 1.2x, VIP users get 1.5x.
```

Why it works: Exact versions, actual code shown, edge cases specified, business context provided.

Result (partial):
```ruby
RSpec.describe '#calculate_discount' do
  describe 'with valid inputs' do
    context 'when user_type is standard' do
      it 'returns base discount' do
        expect(calculate_discount(100, 10, 'standard')).to eq(10.0)
      end
    end

    context 'when user_type is premium' do
      it 'returns 1.2x multiplier' do
        expect(calculate_discount(100, 10, 'premium')).to eq(12.0)
      end
    end
  end

  describe 'edge cases' do
    it 'returns 0 for negative price' do
      expect(calculate_discount(-100, 10, 'standard')).to eq(0)
    end
  end
end
```

### Example 2: Controller Tests (Routing Pitfall)

**❌ No Routing Conventions**
```
Generate controller tests for UsersController
```

Why it fails: Common AI mistake - uses outdated syntax like `get :index` or `get :create`. No authentication context.

**✅ Routing Conventions Specified**
```
Context: Rails 7.1, RSpec 3.12, Devise authentication

Generate RSpec controller tests for UsersController#index and #create.

IMPORTANT routing conventions:
- Use full path helpers: users_path, NOT get :index
- Use HTTP verb methods: get users_path, NOT get :index
- This is a Rails 7 application

Controller code:
```ruby
class UsersController < ApplicationController
  before_action :authenticate_user!

  def index
    @users = User.where.not(confirmed_at: nil).order(created_at: :desc)
  end

  def create
    @user = User.new(user_params)
    if @user.save
      redirect_to users_path, notice: 'User created'
    else
      render :new, status: :unprocessable_entity
    end
  end

  private

  def user_params
    params.require(:user).permit(:email, :name)
  end
end
```

Requirements:
- Use FactoryBot (assume :user factory exists)
- Test authentication (signed in vs signed out)
- Test successful and failure paths
- Test flash messages and redirects
- Use full path helpers (users_path, new_user_path)
```

Why it works: Explicit routing syntax prevents AI's common mistake. Shows actual controller, lists test scenarios.

Community quote: "For controller tests, I always specify: 'Use full routes like api_v1_birds_path, not get :create'"

### Example 3: Model Tests with shoulda-matchers

**✅ Tool-Specific**
```
Context: Rails 7.1, RSpec 3.12, shoulda-matchers 5.3, FactoryBot 6.4

Generate RSpec tests for this User model:

```ruby
class User < ApplicationRecord
  has_many :posts, dependent: :destroy
  has_many :comments, dependent: :nullify

  validates :email, presence: true, uniqueness: true, format: { with: URI::MailTo::EMAIL_REGEXP }
  validates :name, presence: true, length: { minimum: 2, maximum: 100 }
  validates :age, numericality: { greater_than_or_equal_to: 13 }, allow_nil: true

  scope :confirmed, -> { where.not(confirmed_at: nil) }
  scope :recent, ->(days = 7) { where('created_at >= ?', days.days.ago) }

  def full_name
    "#{first_name} #{last_name}".strip
  end

  def confirmed?
    confirmed_at.present?
  end
end
```

Requirements:
- Use shoulda-matchers for validations and associations
- Use FactoryBot (assume :user factory exists)
- Test all validations, associations, scopes, and methods
- Test edge cases for custom methods
- Follow RSpec best practices (one assertion per test where possible)
```

Why it works: Specifies shoulda-matchers for concise validation tests. Lists all test areas. Tool-specific instructions reduce verbosity significantly.

Result (partial):
```ruby
RSpec.describe User, type: :model do
  describe 'associations' do
    it { is_expected.to have_many(:posts).dependent(:destroy) }
    it { is_expected.to have_many(:comments).dependent(:nullify) }
  end

  describe 'validations' do
    it { is_expected.to validate_presence_of(:email) }
    it { is_expected.to validate_uniqueness_of(:email) }
    it { is_expected.to validate_length_of(:name).is_at_least(2).is_at_most(100) }
  end

  describe 'scopes' do
    describe '.confirmed' do
      let!(:confirmed_user) { create(:user, confirmed_at: Time.current) }
      let!(:unconfirmed_user) { create(:user, confirmed_at: nil) }

      it 'returns only confirmed users' do
        expect(User.confirmed).to include(confirmed_user)
        expect(User.confirmed).not_to include(unconfirmed_user)
      end
    end
  end

  describe '#full_name' do
    context 'with trailing spaces' do
      let(:user) { build(:user, first_name: 'Jane ', last_name: ' Doe') }

      it 'strips whitespace' do
        expect(user.full_name).to eq('Jane Doe')
      end
    end
  end
end
```

### Example 4: Service Object with Mocking

**❌ Missing Dependency Info**
```
Test this service object
```

Why it fails: No dependency information, missing expected behavior, no failure scenarios, doesn't indicate Result pattern.

**✅ Dependencies Specified**
```
Context: Rails 7.1, RSpec 3.12, dry-monads Result pattern

Generate RSpec tests for this service object:

```ruby
class UserRegistrationService
  def initialize(params, mailer: UserMailer)
    @params = params
    @mailer = mailer
  end

  def call
    user = User.new(@params)

    if user.save
      @mailer.welcome_email(user).deliver_later
      Success(user)
    else
      Failure(user.errors)
    end
  end
end
```

Requirements:
- Use RSpec mocks/stubs for UserMailer
- Test both Success and Failure paths
- Verify mailer is called on success
- Verify mailer is NOT called on failure
- Test that user is saved correctly
- Use let blocks for setup

Dependencies to mock:
- UserMailer.welcome_email (should return mock with deliver_later)

Assume FactoryBot :user factory exists.
```

Why it works: Shows full service code, specifies dry-monads, lists dependencies, both paths specified.

Result (partial):
```ruby
RSpec.describe UserRegistrationService do
  let(:mailer_double) { double('mailer', deliver_later: true) }
  let(:mailer_class) { class_double(UserMailer, welcome_email: mailer_double) }
  let(:valid_params) { attributes_for(:user) }
  let(:service) { described_class.new(valid_params, mailer: mailer_class) }

  describe '#call' do
    context 'with valid parameters' do
      it 'creates a user' do
        expect { service.call }.to change(User, :count).by(1)
      end

      it 'sends welcome email' do
        service.call
        expect(mailer_class).to have_received(:welcome_email)
      end

      it 'returns Success with user' do
        result = service.call
        expect(result).to be_success
        expect(result.value!).to be_a(User)
      end
    end

    context 'with invalid parameters' do
      let(:invalid_params) { { email: nil } }
      let(:service) { described_class.new(invalid_params, mailer: mailer_class) }

      it 'does not send email' do
        service.call
        expect(mailer_class).not_to have_received(:welcome_email)
      end

      it 'returns Failure with errors' do
        result = service.call
        expect(result).to be_failure
      end
    end
  end
end
```

## Community Insights

### What Works
- Basic RSpec tests - Model validations, associations with shoulda-matchers
- Happy path scenarios - AI generates good success case tests
- Standard Rails patterns - Controller CRUD tests with proper authentication

### Common Pitfalls
- **Outdated routing syntax** - AI uses `get :index` instead of `get users_path`
- **Missing edge cases** - AI focuses on happy paths, forgets boundary conditions
- **Insufficient mocking** - External dependencies not properly stubbed
- **Generic test names** - Non-descriptive "it works" style tests

### Pro Tips

> "Always specify: 'use shoulda_matchers and assume FactoryBot factories exist'"

> "For routing, be explicit: 'use full path helpers like users_path, not controller action shortcuts'"

> "Request edge cases explicitly - AI won't think of them on its own"

> "Specify your Result pattern (dry-monads, custom) so AI knows return types"

Key takeaway: Testing is a strong use case for AI, but requires context - specify framework versions, available gems, routing conventions, dependencies to mock, and edge cases to cover.

## Prompt Templates

### Model Tests
```
Context: Rails [version], RSpec [version], shoulda-matchers [version], FactoryBot [version]

Generate RSpec tests for [Model]:

[Model code]

Requirements:
- Use shoulda-matchers for validations/associations
- Use FactoryBot (assume factory exists)
- Test all validations, associations, scopes, methods
- Test edge cases
- Follow RSpec best practices
```

### Controller Tests
```
Context: Rails [version], RSpec [version], [Auth framework]

Generate RSpec controller tests for [Controller]#[actions].

IMPORTANT: Use full path helpers (users_path), not shortcuts

[Controller code]

Requirements:
- Test authentication (signed in vs out)
- Test success and failure paths
- Test flash messages and redirects
- Use FactoryBot
```

### Service Object Tests
```
Context: Rails [version], RSpec [version], [Result pattern if applicable]

Generate RSpec tests for [Service]:

[Service code]

Requirements:
- Test Success and Failure paths
- Mock external dependencies
- Verify side effects
- Use let blocks

Dependencies to mock:
- [List dependencies]
```

## Related Resources

- [RSpec Documentation](https://rspec.info/)
- [Rails Testing Guide](https://guides.rubyonrails.org/testing.html)
- [shoulda-matchers](https://github.com/thoughtbot/shoulda-matchers)
- [FactoryBot](https://github.com/thoughtbot/factory_bot)

---

Good tests are readable, maintainable, and comprehensive. AI can help generate them - always review and validate.
