# 🐽 Code Hog - Your Friendly Code Smell Companion

A friendly truffle pig that sniffs out design principle violations in your codebase.

Code Hog is a [Claude Code](https://docs.anthropic.com/en/docs/claude-code) plugin that analyzes your source files against established software design principles and reports findings with actionable suggestions — all in a constructive, encouraging tone.

## What It Checks

| Principle | What it catches |
|-----------|----------------|
| **Law of Demeter** | Excessive method chaining and deep property access |
| **Single Responsibility** | Classes juggling too many concerns |
| **Open/Closed** | Rigid if/else and switch statements on types |
| **Liskov Substitution** | Unsupported operation errors and runtime type-checking |
| **Interface Segregation** | Overly broad god interfaces |
| **Dependency Inversion** | Hardcoded concrete dependencies |
| **DRY** | Duplicate code blocks and magic numbers |
| **KISS** | Excessive nesting, complex booleans, too many parameters |
| **YAGNI** | Unused code and unreachable branches |
| **Tell, Don't Ask** | Querying state then making decisions externally |
| **Composition over Inheritance** | Deep inheritance hierarchies |

## Install

### From GitHub

In Claude Code, run:

```
/plugin marketplace add ivannovosad/codehog
/plugin install codehog
```

### Local install

```
git clone https://github.com/ivannovosad/codehog.git
```

Then in Claude Code, run:

```
/plugin install ./codehog
```

## Usage

```
/codehog
```

Code Hog will scan your project, identify the language(s), and produce a report organized by principle with impact levels (High / Medium / Low) and concrete suggestions for each finding.

## Example Output

```
🐽 Code Hog is happily rooting through your codebase...

## 🐽 app/services/order_processor.rb

✅ Nice work: Clean method naming and good use of service objects!

### 💎 Opportunity | Law of Demeter (line ~42)
Impact: High — deep coupling makes this fragile when internals change

  order.customer.address.country.tax_rate

What's happening: This chain reaches through 4 objects — any change
in the middle breaks this code.
Quick win: Add a delegated method like order.tax_rate or pass the
rate directly.

### 💡 Suggestion | Single Responsibility (context)
Impact: Medium — mixing concerns makes the class harder to test

What's happening: This service handles payment processing, inventory
updates, and email notifications — three distinct responsibilities.
Quick win: Extract PaymentHandler and InventoryUpdater, keep this
class as the orchestrator.

### ✨ Polish | KISS (line ~87)
Impact: Low — small change, nice readability boost

  if !order.nil? && !order.cancelled? && order.items.any? && order.payment_status != :failed

Quick win: Extract to a descriptive method like order.processable?

---

## Summary

📊 What You're Doing Well
- Consistent service object pattern across the app
- Good test coverage in models
- Clear naming conventions

Files sniffed: 12 | Opportunities: 8
  💎 High: 2 | 💡 Medium: 4 | ✨ Low: 2

Recommended Starting Points:
1. app/services/order_processor.rb — highest concentration of findings
2. app/models/user.rb — SRP violation easy to fix
3. app/controllers/api/v1/products_controller.rb — deep nesting

Cleanest Files: app/models/product.rb, app/services/auth_service.rb

🙂 Solid foundation! A handful of improvements would take this from good to great.
```

## Language Support

Ruby, JavaScript, TypeScript, Python, Java, Go, Rust, C#, and more.

## License

[MIT](LICENSE)
