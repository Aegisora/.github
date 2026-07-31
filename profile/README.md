# 🛡️ Aegisora

**Aegisora** is a modular PHP validation ecosystem built around reusable rules, structured validation results, predictable execution flow, and convenient validation shortcuts.

The ecosystem is designed for applications that need validation logic to be:

* explicit
* reusable
* framework-agnostic
* easy to test
* easy to compose
* safe to execute

Aegisora separates validation into small independent packages.

Each rule focuses on one validation concern, Guardian provides a fluent way to execute rule pipelines, and Rule Guardians provide shortcut APIs for common validation scenarios.

---

## 🧭 Core Idea

Aegisora follows a simple validation flow:

```text
Value → Context → Rule → Result → Exception or Success
```

Rules do not return raw booleans.

Instead, every rule receives a `Context` object and returns a standardized `Result` object. This makes validation behavior consistent across packages and applications.

For application-level usage, rules can be executed through `aegisora/guardian` or through specialized shortcut packages called Rule Guardians.

---

## 🧩 Ecosystem Packages

### ⚙️ Core Packages

| Package                                                               | Description                                                             | Statistics                                                                                                                                                         |
| --------------------------------------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [`aegisora/rule-contract`](https://github.com/Aegisora/rule-contract) | Defines the core abstractions for building validation rules.            | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/rule-contract?style=flat-square)](https://packagist.org/packages/aegisora/rule-contract) |
| [`aegisora/guardian`](https://github.com/Aegisora/guardian)           | Provides a fluent validation orchestrator for executing rule pipelines. | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/guardian?style=flat-square)](https://packagist.org/packages/aegisora/guardian)      |

### 🧪 Validation Rules

| Package                                                                               | Description                                     | Statistics                                                                                                                                                                |
| ------------------------------------------------------------------------------------- | ----------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`aegisora/email-rule`](https://github.com/Aegisora/email-rule)                       | Validates email values.                         | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/email-rule?style=flat-square)](https://packagist.org/packages/aegisora/email-rule)                       |
| [`aegisora/in-array-rule`](https://github.com/Aegisora/in-array-rule)                 | Validates that a value exists in a given array. | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/in-array-rule?style=flat-square)](https://packagist.org/packages/aegisora/in-array-rule)                 |
| [`aegisora/instanceof-rule`](https://github.com/Aegisora/instanceof-rule)             | Validates object type using `instanceof`.       | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/instanceof-rule?style=flat-square)](https://packagist.org/packages/aegisora/instanceof-rule)             |
| [`aegisora/is-callable-rule`](https://github.com/Aegisora/is-callable-rule)           | Validates callable values.                      | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/is-callable-rule?style=flat-square)](https://packagist.org/packages/aegisora/is-callable-rule)           |
| [`aegisora/is-array-rule`](https://github.com/Aegisora/is-array-rule)                 | Validates array values.                         | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/is-array-rule?style=flat-square)](https://packagist.org/packages/aegisora/is-array-rule)                 |
| [`aegisora/boolean-rule`](https://github.com/Aegisora/boolean-rule)                   | Validates boolean values.                       | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/boolean-rule?style=flat-square)](https://packagist.org/packages/aegisora/boolean-rule)                   |
| [`aegisora/emptiness-rule`](https://github.com/Aegisora/emptiness-rule)               | Validates empty or non-empty values.            | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/emptiness-rule?style=flat-square)](https://packagist.org/packages/aegisora/emptiness-rule)               |
| [`aegisora/scalar-equality-rule`](https://github.com/Aegisora/scalar-equality-rule)   | Validates scalar value equality.                | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/scalar-equality-rule?style=flat-square)](https://packagist.org/packages/aegisora/scalar-equality-rule)   |
| [`aegisora/state-transition-rule`](https://github.com/Aegisora/state-transition-rule) | Validates allowed state transitions.            | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/state-transition-rule?style=flat-square)](https://packagist.org/packages/aegisora/state-transition-rule) |

### 🛡️ Rule Guardians

Rule Guardians are shortcut packages built on top of `aegisora/guardian` and specific validation rules.

They are useful when you want a direct, intention-revealing API without manually creating a rule pipeline every time.

| Package                                                                                     | Description                                                                      | Statistics                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`aegisora/instanceof-rule-guardian`](https://github.com/Aegisora/instanceof-rule-guardian) | Provides a shortcut for validating that a value is an instance of a given class. | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/instanceof-rule-guardian?style=flat-square)](https://packagist.org/packages/aegisora/instanceof-rule-guardian) |
| [`aegisora/email-rule-guardian`](https://github.com/Aegisora/email-rule-guardian)           | Provides a simple shortcut for email validation.                                 | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/email-rule-guardian?style=flat-square)](https://packagist.org/packages/aegisora/email-rule-guardian)           |
| [`aegisora/in-array-rule-guardian`](https://github.com/Aegisora/in-array-rule-guardian)     | Provides a simple shortcut for in-array value validation.                        | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/in-array-rule-guardian?style=flat-square)](https://packagist.org/packages/aegisora/in-array-rule-guardian)     |
| [`aegisora/boolean-rule-guardian`](https://github.com/Aegisora/boolean-rule-guardian)       | Provides a simple shortcut for boolean value validation .                        | [![Total Downloads](https://img.shields.io/packagist/dt/aegisora/boolean-rule-guardian?style=flat-square)](https://packagist.org/packages/aegisora/boolean-rule-guardian)       |

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

Install shortcut Rule Guardians when you want simplified application-level validation APIs:

```shell
composer require aegisora/instanceof-rule-guardian
```

You can combine only the packages your application actually needs.

---

## 🚀 Example Usage

Aegisora rules can be executed directly through `rule-contract`, composed into validation pipelines through `guardian`, or wrapped by Rule Guardians for shorter usage.

### Using Guardian Directly

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

### Using Rule Guardians

Rule Guardians provide shortcut classes for common validation checks.

```php
<?php

use Aegisora\Guardian\Guardian;
use Aegisora\RuleGuardians\InstanceofRule\InstanceofRuleGuardian;
use Aegisora\RuleGuardians\InstanceofRule\Exceptions\NotInstanceofException;

class User {}

$instanceofRuleGuardian = new InstanceofRuleGuardian(
    new Guardian()
);

try {
    $instanceofRuleGuardian->check(
        new User(),
        User::class
    );

    // value is instance of User
} catch (NotInstanceofException $exception) {
    // value is not instance of User
}
```

Rule Guardians are especially useful in application services, handlers, controllers, and domain workflows where validation should stay explicit but concise.

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

## 🧰 Rule Guardians

Rule Guardians are small shortcut packages that combine Guardian with a specific validation rule.

They are not replacements for rules or Guardian. Instead, they provide a simpler API for common checks.

For example, instead of writing:

```php
<?php

$guardian->check(
    $value,
    InstanceofRule::create(User::class),
    new InvalidUserException()
);
```

a Rule Guardian allows:

```php
<?php

$instanceofRuleGuardian->check(
    $value,
    User::class,
    new InvalidUserException()
);
```

This keeps application code shorter while preserving the same validation behavior underneath.

Rule Guardians may also provide package-specific exceptions, making validation failures easier to handle in application code.

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

### 🧩 Optional Shortcuts

Rule Guardians are optional shortcut packages.

They exist to make common validation checks more convenient without changing the underlying rule-based architecture.

Applications can use raw rules, Guardian pipelines, Rule Guardians, or any combination of them.

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
state-transition-rule
```

Rule Guardian packages follow this naming convention:

```text
*-rule-guardian
```

Examples:

```text
instanceof-rule-guardian
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
* wrapping common validations into convenient shortcut APIs

Use validation rules when you need reusable validation logic.

Use Guardian when you need fluent validation pipelines.

Use Rule Guardians when you want short, intention-revealing validation helpers for frequent checks.

---

## 🤝 Contributing

Contributions are welcome.

You can contribute by:

* reporting issues
* improving documentation
* adding tests
* suggesting new rule packages
* suggesting new Rule Guardian packages
* creating new reusable validation rules
* creating shortcut packages for common validation scenarios

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
