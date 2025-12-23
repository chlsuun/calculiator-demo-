# Test-Driven Development (TDD) Rule

## Overview
This project follows Test-Driven Development (TDD) methodology for all core logic implementation (excluding UI components).

## Core Principles

### 1. Red-Green-Refactor Cycle
Always follow the TDD cycle:
1. **Red**: Write a failing test first
2. **Green**: Write minimal code to make the test pass
3. **Refactor**: Improve code while keeping tests green

### 2. Test-First Approach
- Write tests **before** implementing functionality
- Never write production code without a failing test
- Each test should test one specific behavior

### 3. Scope
**TDD applies to**:
- Calculator engine (calculator.js)
- Expression parser (parser.js)
- Math evaluator (evaluator.js)
- History manager (history.js)
- All utility functions and helpers

**TDD does NOT apply to**:
- UI components (HTML/CSS)
- Display manager (DOM manipulation)
- Theme manager (visual changes)
- Event handlers (user interaction)
- **No automated UI testing** - UI will be tested manually

> **IMPORTANT**: UI Testing Strategy
> UI components will be tested manually through browser testing, not with automated tests. 
> Focus TDD efforts on core calculation logic only.

## Test Coverage Requirements
- **Unit Tests**: 90%+ coverage for core logic only
- **Integration Tests**: Core logic integration (Calculator → Parser → Evaluator)
- **Edge Cases**: Must be tested
- **UI Testing**: Manual browser testing only (not automated)

## Workflow
1. Write a failing test (Red)
2. Write minimal code to pass (Green)
3. Refactor while keeping tests green
4. Commit code with tests

## Best Practices
- Use descriptive test names
- Follow AAA pattern (Arrange, Act, Assert)
- Test edge cases
- Keep tests independent
- One assertion per test when possible

## Enforcement
- All core logic tests must pass before merging
- Coverage must not decrease (90%+ for core logic)
- New core features must include tests
- Bug fixes must include regression tests
- UI changes tested manually, not automated

**Remember**: If you're writing core logic code without a failing test, you're doing it wrong!
