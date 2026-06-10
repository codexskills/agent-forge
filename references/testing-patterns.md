# Testing Patterns Reference

## Test Structure

### The Prove-It Pattern
Every test follows three phases:

```
GIVEN  →  Set up preconditions and input data
WHEN   →  Execute the behavior under test
THEN   →  Assert the expected outcome
```

```typescript
it('should return user profile when given valid userId', () => {
  // GIVEN
  const userId = 'user-123';
  const mockRepo = { findById: vi.fn().mockResolvedValue({ id: userId, name: 'Alice' }) };
  const service = new UserService(mockRepo);

  // WHEN
  const result = await service.getProfile(userId);

  // THEN
  expect(result.name).toBe('Alice');
  expect(mockRepo.findById).toHaveBeenCalledWith(userId);
});
```

## Test Naming

### Files
- `*.test.ts` or `*.spec.ts` for unit tests
- `*.integration.test.ts` for integration tests
- `*.e2e.test.ts` or `*.cy.ts` for end-to-end tests
- Co-located with source files: `Button.tsx` → `Button.test.tsx`

### Descriptions
```
describe('[Component/Module/Function]', () => {
  it('should [expected behavior] when [condition]', () => { ... });
});
```

**Good**:
- `should return 0 when cart is empty`
- `should throw error when email is invalid`
- `should not apply discount when coupon is expired`

**Bad**:
- `works correctly`
- `test1`
- `handles edge cases` (too vague)

## Assertion Patterns

### Basic Assertions
```typescript
expect(value).toBe(42);                    // Primitive equality
expect(value).toEqual({ a: 1 });           // Deep equality
expect(value).toStrictEqual({ a: 1 });     // Deep equality + type check
expect(value).toBeNull();                  // Null check
expect(value).toBeUndefined();             // Undefined check
expect(value).toBeDefined();               // Not undefined
expect(value).toBeTruthy();                // Truthy check
expect(value).toBeFalsy();                 // Falsy check
```

### String Assertions
```typescript
expect(str).toContain('partial');          // Contains substring
expect(str).toMatch(/regex/);              // Regex match
expect(str).toHaveLength(10);              // String length
expect(str).not.toBeEmpty();               // Not empty
```

### Array Assertions
```typescript
expect(arr).toHaveLength(3);               // Array length
expect(arr).toContain('item');             // Contains item
expect(arr).toContainEqual({ id: 1 });     // Contains object
expect(arr).toEqual(expect.arrayContaining(['a', 'b']));  // Subset match
```

### Object Assertions
```typescript
expect(obj).toHaveProperty('name');        // Property exists
expect(obj).toHaveProperty('age', 30);     // Property exists with value
expect(obj).toMatchObject({ name: 'Alice' });  // Partial match
expect(obj).toMatchSnapshot();             // Snapshot match
```

### Function Assertions
```typescript
expect(fn).toHaveBeenCalled();             // Was called
expect(fn).toHaveBeenCalledTimes(1);       // Called exactly once
expect(fn).toHaveBeenCalledWith('arg');    // Called with specific args
expect(fn).toHaveBeenLastCalledWith('x');  // Last call args
expect(fn).toHaveBeenNthCalledWith(2, 'y'); // Nth call args
```

### Async Assertions
```typescript
await expect(promise).resolves.toEqual(value);    // Resolve check
await expect(promise).rejects.toThrow('error');   // Reject check
```

## Mocking Patterns

### Creating Mocks
```typescript
// Function mock
const mockFn = vi.fn();
const mockFn = vi.fn().mockReturnValue('default');
const mockFn = vi.fn().mockResolvedValue({ data: 'async' });
const mockFn = vi.fn().mockRejectedValue(new Error('fail'));
const mockFn = vi.fn().mockImplementation((x) => x * 2);

// Module mock
vi.mock('../services/database', () => ({
  query: vi.fn().mockResolvedValue([{ id: 1 }]),
  connect: vi.fn().mockResolvedValue(true),
}));
```

### Spy Patterns
```typescript
const spy = vi.spyOn(console, 'log');
spy.mockImplementation(() => {});          // Suppress log
expect(spy).toHaveBeenCalledWith('hello');
spy.mockRestore();                         // Clean up
```

### Mock Reset Rules
```typescript
beforeEach(() => {
  vi.clearAllMocks();    // Clear call history
  vi.resetAllMocks();    // Clear + reset implementations
  vi.restoreAllMocks();  // Restore originals (spies)
});
```

## React Testing Patterns

### Render Patterns
```typescript
import { render, screen, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';

it('should handle user interaction', async () => {
  const user = userEvent.setup();
  render(<MyComponent />);

  // Find elements
  expect(screen.getByText('Title')).toBeInTheDocument();
  expect(screen.getByRole('button', { name: /submit/i })).toBeEnabled();
  expect(screen.getByLabelText('Email')).toHaveValue('');
  expect(screen.getByPlaceholderText('Enter name')).toBeInTheDocument();
  expect(screen.getByTestId('custom-element')).toBeInTheDocument();

  // Async find
  expect(await screen.findByText('Loaded')).toBeInTheDocument();
  await waitFor(() => expect(screen.getByText('Done')).toBeInTheDocument());
});
```

### User Interaction Patterns
```typescript
// Click
await user.click(screen.getByRole('button'));

// Type
await user.type(screen.getByLabelText('Name'), 'Alice');

// Select
await user.selectOptions(screen.getByRole('combobox'), 'option-value');

// Keyboard
await user.keyboard('{Enter}');
await user.tab();

// Hover
await user.hover(screen.getByText('Tooltip target'));
```

### Testing Component States
```typescript
it('should show loading state', () => {
  render(<DataList />);
  expect(screen.getByRole('status')).toHaveTextContent('Loading...');
});

it('should show error state', async () => {
  render(<DataList />);
  expect(await screen.findByRole('alert')).toHaveTextContent('Failed to load');
});

it('should show empty state', async () => {
  render(<DataList />);
  expect(await screen.findByText('No items found')).toBeInTheDocument();
});

it('should show data', async () => {
  render(<DataList />);
  expect(await screen.findByRole('list')).toHaveLength(3);
});
```

## API Testing Patterns

### Integration Tests (Supertest)
```typescript
import request from 'supertest';
import app from '../app';

describe('GET /api/users/:id', () => {
  it('should return user when found', async () => {
    const res = await request(app)
      .get('/api/users/123')
      .expect(200);

    expect(res.body).toMatchObject({ id: '123', name: expect.any(String) });
  });

  it('should return 404 when user not found', async () => {
    await request(app)
      .get('/api/users/nonexistent')
      .expect(404);
  });

  it('should return 401 without auth token', async () => {
    await request(app)
      .get('/api/users/123')
      .expect(401);
  });
});
```

### Testing Error Responses
```typescript
it('should return validation errors', async () => {
  const res = await request(app)
    .post('/api/users')
    .send({})  // Missing required fields
    .expect(400);

  expect(res.body.errors).toEqual(
    expect.arrayContaining([
      expect.objectContaining({ field: 'name', message: 'Name is required' }),
    ])
  );
});
```

## E2E Testing Patterns

### Cypress
```typescript
describe('Authentication Flow', () => {
  beforeEach(() => {
    cy.visit('/login');
  });

  it('should log in with valid credentials', () => {
    cy.get('[data-testid="email"]').type('user@example.com');
    cy.get('[data-testid="password"]').type('valid-password');
    cy.get('[data-testid="submit"]').click();
    cy.url().should('include', '/dashboard');
    cy.get('[data-testid="welcome"]').should('contain', 'Welcome back');
  });

  it('should show error with invalid credentials', () => {
    cy.get('[data-testid="email"]').type('user@example.com');
    cy.get('[data-testid="password"]').type('wrong-password');
    cy.get('[data-testid="submit"]').click();
    cy.get('[data-testid="error"]').should('be.visible');
    cy.url().should('include', '/login');
  });
});
```

### Playwright
```typescript
test('should complete checkout', async ({ page }) => {
  await page.goto('/products');
  await page.click('text=Add to Cart');
  await page.click('text=Checkout');
  await page.fill('[name="email"]', 'user@example.com');
  await page.fill('[name="card"]', '4242424242424242');
  await page.click('text=Pay Now');
  await expect(page.locator('text=Order confirmed')).toBeVisible();
});
```

## Anti-Patterns

| Anti-Pattern | Problem | Solution |
|-------------|---------|----------|
| Testing internals | Fragile, breaks on refactor | Test public API only |
| Multiple behaviors per test | Unclear failures | One assertion per it() |
| Flaky assertions | Intermittent failures | Use `findBy` (async) instead of `getBy` (sync) |
| Snapshot-first | Blind acceptance | Write explicit assertions first, snapshot for structure |
| Mocking everything | False confidence | Mock at boundaries only |
| Testing the framework | Wasted maintenance | Trust React, Express, etc. |
| Testing types only | No runtime verification | Add value-based assertions |
| Skipping error tests | Happy-path only | Always test error states |

## Testing Utilities Reference

### Vitest
```typescript
import { describe, it, expect, vi, beforeEach, afterEach } from 'vitest';
```

### Jest
```typescript
import { describe, it, expect, jest, beforeEach, afterEach } from '@jest/globals';
```

### Testing Library Queries
```
getByText        → Find by text content
getByRole        → Find by ARIA role (preferred)
getByLabelText   → Find by associated label
getByPlaceholder → Find by placeholder
getByTestId      → Find by data-testid (last resort)
queryByText      → Returns null if not found
findByText       → Async, waits for element
```

## Usage
Reference this document when writing tests. Use the Prove-It pattern for all tests, follow naming conventions, and avoid the anti-patterns listed above.
