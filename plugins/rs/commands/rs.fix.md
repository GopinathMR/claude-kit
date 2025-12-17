---
description: Build the Rust project and get expert guidance on fixing compilation errors
---

# Fix Rust Compilation Issues

You are helping the user fix Rust compilation errors with expert guidance.

## Step 1: Run the build

First, run `cargo build` to identify compilation issues.

## Step 2: Analyze errors with Rust expert

If there are compilation errors:

1. Use the Task tool with `subagent_type: "systems-programming:rust-pro"` to analyze the errors
2. In your prompt to the rust-pro agent, include:
   - The full compilation error output
   - Ask the agent to:
     - Explain WHY the error occurs (what Rust principle/concept is being violated)
     - Provide multiple fix options if applicable (e.g., different approaches)
     - For each option, explain the trade-offs and when to use it
     - Include references to official Rust documentation, The Rust Book, or tutorials
     - Provide the actual code changes needed

## Step 3: Present options to user

Use the AskUserQuestion tool to present the fix options to the user with:
- Clear descriptions of each approach
- Explanation of the principle behind each fix
- Links to learning resources

## Step 4: Apply the fix

Once the user selects an option:
1. Apply the chosen fix using the Edit tool
2. Run `cargo build` again to verify the fix works
3. If there are still errors, repeat the process
4. If successful, confirm the fix is complete

## Important guidelines

- Always explain the underlying Rust concept (ownership, borrowing, lifetimes, trait bounds, etc.)
- Provide educational value - help the user learn, not just fix
- Include links to:
  - The Rust Book (https://doc.rust-lang.org/book/)
  - Rust by Example (https://doc.rust-lang.org/rust-by-example/)
  - Rust Reference (https://doc.rust-lang.org/reference/)
  - Specific std documentation when relevant
- If multiple errors exist, tackle them one at a time
- Always verify the fix with a rebuild
