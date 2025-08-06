# Chapter 2: Functions - Small, Focused, and Single-Purpose

## Description

Functions are the fundamental building blocks of clean code and serve as the primary means of organizing and expressing our programming logic. Robert C. Martin emphasizes that **functions should be small, do one thing well, and do it at a single level of abstraction**. This principle transforms complex, unwieldy code into readable, maintainable, and testable components.

![Single Responsibility](images/2_clean_code_functions.png)

### Core Principles of Clean Functions

**Size Matters - Keep Functions Small**
The first rule of functions is that they should be small. The second rule is that they should be smaller than that. Functions should rarely exceed 20 lines, and ideally should be much shorter. Small functions are easier to understand, test, and maintain. They also tend to have descriptive names that clearly communicate their purpose.

**Do One Thing**
Functions should do one thing, do it well, and do it only. If you can extract another function from a function with a name that is not merely a restatement of its implementation, then the function is doing more than one thing. This principle ensures that each function has a clear, focused responsibility.

**Single Level of Abstraction**
All statements within a function should be at the same level of abstraction. Don't mix high-level concepts with low-level details in the same function. This creates a clear hierarchy in your code and makes it easier to follow the flow of logic.

### Practical Examples

**Bad Function Example:**
```java
public List<User> processUserData(List<User> users) {
    List<User> validUsers = new ArrayList<>();
    for (User user : users) {
        if (user.getEmail() != null && user.getEmail().contains("@") && user.getName().length() > 0) {
            user.setName(user.getName().trim());
            user.setName(capitalize(user.getName()));
            user.setEmail(user.getEmail().toLowerCase());
            // Database connection logic
            try (Connection conn = getDbConnection()) {
                PreparedStatement stmt = conn.prepareStatement("INSERT INTO users (name, email) VALUES (?, ?)");
                stmt.setString(1, user.getName());
                stmt.setString(2, user.getEmail());
                stmt.executeUpdate();
            } catch (SQLException e) {
                e.printStackTrace();
            }
            validUsers.add(user);
        }
    }
    return validUsers;
}
```

**Clean Function Refactor:**
```java
public List<User> processUserData(List<User> users) {
    List<User> validUsers = validateUsers(users);
    List<User> formattedUsers = formatUserData(validUsers);
    saveUsers(formattedUsers);
    return formattedUsers;
}

private List<User> validateUsers(List<User> users) {
    return users.stream().filter(this::isValidUser).collect(Collectors.toList());
}

private boolean isValidUser(User user) {
    return user.getEmail() != null && user.getEmail().contains("@") && user.getName().length() > 0;
}

private List<User> formatUserData(List<User> users) {
    for (User user : users) {
        user.setName(capitalize(user.getName().trim()));
        user.setEmail(user.getEmail().toLowerCase());
    }
    return users;
}

private void saveUsers(List<User> users) {
    try (Connection conn = getDbConnection()) {
        for (User user : users) {
            PreparedStatement stmt = conn.prepareStatement("INSERT INTO users (name, email) VALUES (?, ?)");
            stmt.setString(1, user.getName());
            stmt.setString(2, user.getEmail());
            stmt.executeUpdate();
        }
    } catch (SQLException e) {
        e.printStackTrace();
    }
}

private String capitalize(String input) {
    if (input == null || input.isEmpty()) return input;
    return input.substring(0, 1).toUpperCase() + input.substring(1).toLowerCase();
}

```

### Function Arguments and Return Values

**Minimize Function Arguments**
The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible. More than three arguments requires very special justification and shouldn't be used anyway.

**Avoid Flag Arguments**
Flag arguments are ugly. Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, loudly proclaiming that this function does more than one thing.

### Why Functions Matter

Clean functions are crucial because they:
- **Enhance Readability**: Small, well-named functions read like well-written prose
- **Improve Testability**: Single-purpose functions are easier to test in isolation
- **Facilitate Debugging**: When bugs occur, small functions make it easier to pinpoint the issue
- **Enable Reusability**: Functions that do one thing well can be reused across different contexts
- **Support Maintainability**: Changes to functionality are localized to specific functions

## Key Points Summary

- Functions should be small (ideally under 20 lines) and do one thing well
- Maintain a single level of abstraction within each function
- Use descriptive names that clearly communicate the function's purpose
- Minimize the number of arguments (zero to two is ideal)
- Avoid flag arguments that indicate multiple responsibilities
- Extract functions when you can give the extracted code a meaningful name
- Functions should read like well-written prose when properly structured
