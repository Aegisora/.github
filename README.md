# 🛡️ Aegisora

**Aegisora** is a modular PHP validation ecosystem built around reusable rules, structured validation results, and predictable execution flow.

The ecosystem is designed for applications that need validation logic to be:

* explicit
* reusable
* framework-agnostic
* easy to test
* easy to compose
* safe to execute

Aegisora separates validation into small independent packages. Each rule focuses on one validation concern, while Guardian provides a fluent way to execute multiple rules in sequence.

---

## 🧭 Core Idea

Aegisora follows a simple validation flow:

```text
Value → Context → Rule → Result → Exception or Success
```

Rules do not return raw booleans.

Instead, every rule receives a `Context` object and returns a standardized `Result` object. This makes validation behavior consistent across packages and applications.

---

## 🧩 Ecosystem Packages

### ⚙️ Core Packages

| Package                                             | Description                                                             |
| --------------------------------------------------- | ----------------------------------------------------------------------- |
| [`aegisora/rule-contract`](/Aegisora/rule-contract) | Defines the core abstractions for building validation rules.            |
| [`aegisora/guardian`](/Aegisora/guardian)           | Provides a fluent validation orchestrator for executing rule pipelines. |

### 🧪 Validation Rules

| Package                                                           | Description                                     |
| ----------------------------------------------------------------- | ----------------------------------------------- |
| [`aegisora/email-rule`](/Aegisora/email-rule)                     | Validates email values.                         |
| [`aegisora/in-array-rule`](/Aegisora/in-array-rule)               | Validates that a value exists in a given array. |
| [`aegisora/instanceof-rule`](/Aegisora/instanceof-rule)           | Validates object type using `instanceof`.       |
| [`aegisora/is-callable-rule`](/Aegisora/is-callable-rule)         | Validates callable values.                      |
| [`aegisora/is-array-rule`](/Aegisora/is-array-rule)               | Validates array values.                         |
| [`aegisora/boolean-rule`](/Aegisora/boolean-rule)                 | Validates boolean values.                       |
| [`aegisora/emptiness-rule`](/Aegisora/emptiness-rule)             | Validates empty or non-empty values.            |
| [`aegisora/scalar-equality-rule`](/Aegisora/scalar-equality-rule) | Validates scalar value equality.                |

---

## 📦 Installation

Install the core validation orchestrator:

```shell
composer require aegisora/guardian
```

Install individual rules as needed:

```shell
composer require aegisora/email-rule
composer require aegisora/is-array-rule
composer require aegisora/in-array-rule
```

You can combine only the packages your application actually needs.

---

## 🚀 Example Usage

Aegisora rules can be executed directly through `rule-contract`, or composed into validation pipelines through `guardian`.

```php
<?php

use Aegisora\Guardian\Guardian;
use Aegisora\Rules\EmailRule;
use App\Exceptions\InvalidEmailException;

$guardian = new Guardian();

$guardian->check(
    'user@example.com',
    EmailRule::create(),
    new InvalidEmailException()
);
```

For more complex scenarios, multiple rules can be chained together:

```php
<?php

use Aegisora\Guardian\Guardian;
use Aegisora\Rules\EmailRule;
use Aegisora\Rules\EmptinessRule;
use App\Exceptions\EmailIsEmptyException;
use App\Exceptions\InvalidEmailException;

$guardian = new Guardian();

$guardian
    ->that('user@example.com')
    ->must(
        EmptinessRule::notEmpty(),
        new EmailIsEmptyException()
    )
    ->must(
        EmailRule::create(),
        new InvalidEmailException()
    )
    ->validate();
```

If validation passes, execution continues normally.

If validation fails, Guardian stops on the first failed rule and throws the exception attached to that rule.

---

## 📜 Rule Contract

All validation rules are built on top of `aegisora/rule-contract`.

A rule receives a `Context` and returns a `Result`:

```php
<?php

use Aegisora\RuleContract\Models\Context;
use Aegisora\RuleContract\Models\Result;
use Aegisora\RuleContract\Rule;

final class AdultAgeRule extends Rule
{
    protected function executeValidate(Context $context): Result
    {
        $age = $context->getValue();

        if ($age < 18) {
            return Result::invalid('adult_age');
        }

        return Result::valid();
    }
}
```

This contract keeps all rules predictable and compatible with the rest of the ecosystem.

---

## 🛡️ Guardian

`aegisora/guardian` is the validation execution engine.

It is responsible for:

* accepting a value
* creating a validation context
* executing rules sequentially
* stopping on the first failed rule
* throwing default or custom exceptions
* isolating rule execution errors

Guardian does not contain validation logic itself. Validation logic belongs to independent rule packages.

---

## 🧱 Design Principles

Aegisora packages follow a few core principles.

### 🎯 One Rule — One Responsibility

Each rule should validate one specific thing.

This keeps validation logic small, reusable, and easy to test.

### 🧰 Framework Agnostic

Aegisora does not depend on Laravel, Symfony, Slim, or any other framework.

Packages can be used in:

* web applications
* APIs
* CLI tools
* microservices
* domain-driven projects
* custom PHP applications

### 📊 Structured Results

Rules return `Result` objects instead of raw booleans.

This allows each failed validation to expose a rule code and makes validation failures easier to handle consistently.

### 🔒 Safe Execution

Unexpected rule execution errors are isolated through the rule contract and can be converted by Guardian into dedicated execution exceptions.

This keeps validation failures separate from rule implementation failures.

---

## 🏷️ Package Naming Convention

Rule packages follow a simple naming convention:

```text
*-rule
```

Examples:

```text
email-rule
is-array-rule
in-array-rule
instanceof-rule
emptiness-rule
```

This makes packages easy to discover and keeps the ecosystem consistent.

---

## 🧠 When to Use Aegisora

Aegisora is useful when validation logic needs to be shared across multiple parts of an application or across multiple projects.

Typical use cases:

* validating DTOs and commands
* validating API input
* validating domain values
* building reusable business rules
* creating validation pipelines
* replacing scattered `if` checks with explicit rules

---

## 🤝 Contributing

Contributions are welcome.

You can contribute by:

* reporting issues
* improving documentation
* adding tests
* suggesting new rule packages
* creating new reusable validation rules

Before contributing, please check the contribution guidelines in the corresponding repository.

---

## 🛡️ Security

If you discover a security issue, please follow the security policy of the affected repository.

---

## ⚖️ License

Aegisora packages are open-source and released under the MIT License.

See the `LICENSE` file in each repository for details.

---

## ⭐ Support

If you find Aegisora useful, consider giving the repositories a star.

It helps the ecosystem grow and makes the packages easier for other developers to discover.
