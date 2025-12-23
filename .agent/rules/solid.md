# SOLID Principles Rule

## Overview
All code implementation in this project must follow SOLID principles to ensure maintainability, scalability, and testability.

## The Five Principles

### 1. Single Responsibility Principle (SRP)
**Definition**: A class should have only one reason to change.

**Rules**:
- Each class/module should have one and only one responsibility
- If a class does multiple things, split it into separate classes
- Functions should do one thing and do it well

**Example**:
`javascript
// ❌ Bad - Multiple responsibilities
class Calculator {
  calculate(expression) { /* ... */ }
  saveToHistory(expression, result) { /* ... */ }
  displayResult(result) { /* ... */ }
}

// ✅ Good - Single responsibility
class Calculator {
  calculate(expression) { /* ... */ }
}

class HistoryManager {
  save(expression, result) { /* ... */ }
}

class DisplayManager {
  show(result) { /* ... */ }
}
`

### 2. Open/Closed Principle (OCP)
**Definition**: Software entities should be open for extension but closed for modification.

**Rules**:
- Use abstraction and polymorphism
- Extend behavior without modifying existing code
- Use interfaces or abstract classes

**Example**:
`javascript
// ✅ Good - Open for extension
class Operation {
  execute(a, b) {
    throw new Error('Must implement execute');
  }
}

class Addition extends Operation {
  execute(a, b) {
    return a + b;
  }
}

class Multiplication extends Operation {
  execute(a, b) {
    return a * b;
  }
}

// Add new operations without modifying existing code
class Power extends Operation {
  execute(a, b) {
    return Math.pow(a, b);
  }
}
`

### 3. Liskov Substitution Principle (LSP)
**Definition**: Objects of a superclass should be replaceable with objects of a subclass without breaking the application.

**Rules**:
- Subclasses must be substitutable for their base classes
- Don't strengthen preconditions
- Don't weaken postconditions
- Maintain behavioral compatibility

**Example**:
`javascript
// ✅ Good - Substitutable
class MathFunction {
  calculate(value) {
    return value;
  }
}

class SineFunction extends MathFunction {
  calculate(value) {
    return Math.sin(value);
  }
}

class CosineFunction extends MathFunction {
  calculate(value) {
    return Math.cos(value);
  }
}

// Can use any MathFunction interchangeably
function applyFunction(func, value) {
  return func.calculate(value);
}
`

### 4. Interface Segregation Principle (ISP)
**Definition**: Clients should not be forced to depend on interfaces they don't use.

**Rules**:
- Create specific interfaces rather than general-purpose ones
- Split large interfaces into smaller, focused ones
- Classes should only implement methods they need

**Example**:
`javascript
// ❌ Bad - Fat interface
class Calculator {
  add() {}
  subtract() {}
  multiply() {}
  divide() {}
  sin() {}
  cos() {}
  tan() {}
  log() {}
}

// ✅ Good - Segregated interfaces
class BasicCalculator {
  add() {}
  subtract() {}
  multiply() {}
  divide() {}
}

class ScientificCalculator extends BasicCalculator {
  sin() {}
  cos() {}
  tan() {}
}

class LogarithmicCalculator extends BasicCalculator {
  log() {}
  ln() {}
}
`

### 5. Dependency Inversion Principle (DIP)
**Definition**: High-level modules should not depend on low-level modules. Both should depend on abstractions.

**Rules**:
- Depend on abstractions, not concretions
- Use dependency injection
- Invert the dependency direction

**Example**:
`javascript
// ❌ Bad - Direct dependency
class Calculator {
  constructor() {
    this.history = new LocalStorageHistory(); // Tight coupling
  }
}

// ✅ Good - Dependency injection
class Calculator {
  constructor(historyManager) {
    this.history = historyManager; // Depends on abstraction
  }
}

// Can inject any history implementation
const calculator1 = new Calculator(new LocalStorageHistory());
const calculator2 = new Calculator(new InMemoryHistory());
const calculator3 = new Calculator(new CloudHistory());
`

## Application in This Project

### Calculator Module
- **SRP**: Calculator only handles calculation logic
- **OCP**: Extend with new operations without modifying core
- **DIP**: Inject dependencies (parser, evaluator, history)

### Parser Module
- **SRP**: Only responsible for parsing expressions
- **OCP**: Support new syntax without changing existing parser
- **LSP**: Different parsers can be substituted

### Evaluator Module
- **SRP**: Only evaluates parsed expressions
- **ISP**: Separate basic and scientific evaluation
- **DIP**: Depends on operation abstractions

## Code Review Checklist

- [ ] Each class has a single, well-defined responsibility
- [ ] New functionality added through extension, not modification
- [ ] Subclasses can replace base classes without issues
- [ ] No class is forced to implement unused methods
- [ ] Dependencies are injected, not hard-coded

## Benefits

1. **Maintainability**: Easy to understand and modify
2. **Testability**: Easy to mock and test in isolation
3. **Flexibility**: Easy to extend and adapt
4. **Reusability**: Components can be reused in different contexts
5. **Scalability**: Easy to add new features

---

**Remember**: SOLID principles lead to clean, maintainable, and testable code!
