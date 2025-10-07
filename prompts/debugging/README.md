# Debugging Prompts

AI prompts for debugging Ruby and Rails code.

## Overview

Debugging is one of AI's strengths for Ruby developers. AI excels at explaining stack traces, identifying common errors, and suggesting fixes. The key is providing complete error context.

## Quick Tips

- Include full error messages with stack traces
- Show focused code extracts (not entire files)
- Specify Rails/Ruby versions
- Share what you've already tried
- Request explanations of WHY, not just fixes

## What Works and What Doesn't

Based on community feedback and experience.

### Example 1: Error Message Debugging

**❌ No Context**
```
This code doesn't work, fix it

def process_users
  users.map(&:email)
end
```

Why it fails: No error message, no context about what "doesn't work" means, missing surrounding code.

**✅ Complete Error Context**
```
Context: Rails 7.1, Ruby 3.2

This method raises a NoMethodError:

```ruby
class UserMailer < ApplicationMailer
  def welcome_email(user)
    @user = user
    mail(to: @user.email, subject: 'Welcome!')
  end
end

class UsersController < ApplicationController
  def create
    @user = User.new(user_params)
    if @user.save
      UserMailer.welcome_email(@user).deliver_later
      redirect_to users_path
    end
  end
end
```

Error:
```
NoMethodError: undefined method `deliver_later' for nil:NilClass
  app/controllers/users_controller.rb:7:in `create'
```

Expected: Email should be queued
Actual: NoMethodError on deliver_later

Verified:
- User saves successfully
- ActionMailer is configured
- ActiveJob with Sidekiq set up

What's causing this?
```

Why it works: Full error message, relevant code (both mailer and controller), context provided, what was already verified listed.

AI response:
```
The issue is `UserMailer.welcome_email(@user)` returns `nil`. Rails mailers must call `mail()` and return the result.

Your `welcome_email` method is missing a return value:

```ruby
def welcome_email(user)
  @user = user
  mail(to: @user.email, subject: 'Welcome!')  # Now returns Mail::Message
end
```

Explanation: Mailer methods must return a `Mail::Message` object. The `mail()` method returns this, but if you have code after it without explicit return, Ruby returns the last expression (which might be `nil`).
```

### Example 2: Rails Console Debugging

**✅ Show the Discrepancy**
```
Context: Rails 7.1, Ruby 3.2, PostgreSQL 14

Unexpected Rails console behavior:

```ruby
irb(main):001> user = User.find(1)
  User Load (0.5ms)  SELECT "users".* FROM "users" WHERE "users"."id" = $1 LIMIT $2
=> #<User id: 1, email: "test@example.com">

irb(main):002> user.posts
=> []  # Expected to see posts

irb(main):003> Post.where(user_id: 1)
  Post Load (0.3ms)  SELECT "posts".* FROM "posts" WHERE "posts"."user_id" = $1
=> [#<Post id: 1, user_id: 1, title: "First Post">]
```

Models:
```ruby
class User < ApplicationRecord
  has_many :posts
end

class Post < ApplicationRecord
  belongs_to :user
end
```

Why does `user.posts` return empty when `Post.where(user_id: 1)` finds posts?
```

Why it works: Shows console output with SQL queries, demonstrates the discrepancy, includes model code.

AI response:
```
The association is working correctly - this is likely association caching. Try:

```ruby
irb(main):004> user.posts.reload
  Post Load (0.3ms)  SELECT "posts".* FROM "posts" WHERE "posts"."user_id" = $1
=> [#<Post id: 1, user_id: 1, title: "First Post">]
```

Rails caches association queries. If posts were created after loading the user object, they won't appear until you reload the association.
```

### Example 3: Performance Debugging

**✅ Include Metrics**
```
Context: Rails 7.1, Ruby 3.2, PostgreSQL 14, production

Controller action timing out (>30 seconds):

```ruby
class DashboardController < ApplicationController
  def index
    @users = User.includes(:profile).all
    @recent_posts = Post.order(created_at: :desc).limit(10)

    @users.each do |user|
      @user_post_counts ||= {}
      @user_post_counts[user.id] = user.posts.count
    end
  end
end
```

Environment:
- 50,000 users
- Average 10 posts per user
- Timeouts after 30s in production
- Works fine in development (<100 users)

What's causing the performance issue?
```

Why it works: Performance-specific context (timeout duration, database size), environment differences noted, code shown.

AI response:
```
N+1 query problem in the `@users.each` block. For 50,000 users:
- 1 query for users
- 50,000 queries for `user.posts.count`

Total: 50,001 queries

**Fix Option 1: Counter Cache**
```ruby
# Migration
add_column :users, :posts_count, :integer, default: 0

# Post model
class Post < ApplicationRecord
  belongs_to :user, counter_cache: true
end

# Controller
@user_post_counts = @users.index_by(&:id).transform_values(&:posts_count)
```

**Fix Option 2: Single Query**
```ruby
@user_post_counts = Post.group(:user_id).count
```

Reduces 50,001 queries to 2-3. Response time should drop from 30s to <1s.
```

### Example 4: Focused Code Extract

**❌ Too Much Code**
```
My app has a bug, here's the entire file:

[500 lines of controller code]
```

Why it fails: No specific error, too much irrelevant code, wastes AI's context window.

**✅ Focused Extract**
```
Context: Rails 7.1, Ruby 3.2

Bug: Users can access other users' private posts

Relevant code (UsersController#show, lines 45-52):

```ruby
def show
  @user = User.find(params[:id])
  @posts = Post.where(published: true)  # Line 47 - BUG HERE
end
```

Post model:
- `published` (boolean): public visibility
- `user_id` (integer): belongs to User

Expected: Show only @user's published posts
Actual: Shows ALL published posts from ALL users

Security: Data leak in production

How to fix?
```

Why it works: Isolated problem, line number hint, clear expectation vs actual, security flag indicates severity.

AI response:
```
Bug on line 47 - querying all published posts instead of scoping to user.

**Fix:**
```ruby
def show
  @user = User.find(params[:id])
  @posts = @user.posts.where(published: true)
end
```

This scopes to only the specific user's posts.

**Security note**: This is a data leak (IDOR vulnerability). Consider adding authorization checks with Pundit or CanCanCan.
```

## Community Insights

### What Works
- **Error message explanation** - AI excels at stack traces
- **Common Rails errors** - ActiveRecord, routing, validation errors
- **Performance debugging** - N+1 queries, slow queries
- **Console output analysis** - Unexpected Rails console behavior

### What Requires Human Expertise
- Complex business logic bugs
- Concurrency issues (race conditions, deadlocks)
- Infrastructure problems
- Security vulnerabilities (AI may miss subtle issues)

### Pro Tips

> "Always include full error message - AI can spot patterns in stack traces"

> "Show what you've tried - saves time and helps AI understand the problem"

> "For performance, show Rails logs or rack-mini-profiler output"

> "Ask AI to explain WHY, not just HOW to fix - helps you learn"

Key takeaway: Debugging is AI's strength with proper context - full error messages, focused code extracts, version details, expected vs actual behavior, what you've tried.

## Prompt Templates

### Error Message
```
Context: Rails [version], Ruby [version], [database]

Error message:
```
[Full error with stack trace]
```

Relevant code (file:line):
```ruby
[Minimal code showing problem area]
```

Expected: [what should happen]
Actual: [what happens]

Verified:
- [Thing 1]
- [Thing 2]

What's causing this?
```

### Performance Issue
```
Context: Rails [version], Ruby [version], [database], [environment]

Performance issue: [describe slow operation]
- Response time: [current] (expected: [target])
- Database size: [records]
- Environment: [production/development]

Code:
```ruby
[The slow code]
```

What's causing the slowness?
```

### Unexpected Behavior
```
Context: Rails [version], Ruby [version]

Unexpected behavior in [component]:

Code:
```ruby
[Relevant code]
```

Expected: [what should happen]
Actual: [what happens]

Evidence:
```
[Console output, logs, or test results]
```

Why is this happening?
```

## Related Resources

- [Rails Debugging Guide](https://guides.rubyonrails.org/debugging_rails_applications.html)
- [Pry](https://pry.github.io/) - Ruby REPL
- [Bullet](https://github.com/flyerhzm/bullet) - N+1 detection

---

AI is excellent at explaining errors and suggesting fixes, but you're the expert on your application's business logic and architecture. Always verify fixes and understand why they work.
