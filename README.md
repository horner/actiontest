# Local GitHub Action Testing

This repository contains a local GitHub Action that echoes environment variables and demonstrates how to test it using ACT.

## Structure

```
actiontest/
├── .github/
│   └── workflows/
│       └── test.yml          # Workflow to test the action
├── myaction/                 # Your custom action
│   └── action.yml           # Action definition
└── README.md               # This file
```

## Action Description

The `myaction` action:
- Displays a custom message
- Lists all environment variables (sorted)
- Shows the count of environment variables
- Highlights GitHub-specific environment variables

## Testing with ACT

### Install ACT

```bash
# On macOS with Homebrew
brew install act

# Or download from GitHub releases
# https://github.com/nektos/act/releases
```

### Run Tests Locally

1. **Test the default workflow:**
   ```bash
   act
   ```

2. **Test specific job:**
   ```bash
   act -j test-action
   ```

3. **Test with specific event:**
   ```bash
   act push
   ```

4. **Test with verbose output:**
   ```bash
   act -v
   ```

5. **Test with specific runner:**
   ```bash
   act -P ubuntu-latest=catthehacker/ubuntu:act-latest
   ```

### Common ACT Commands

```bash
# List available workflows and jobs
act -l

# Dry run (don't actually run, just show what would run)
act -n

# Run with secrets file
act --secret-file .secrets

# Run specific workflow file
act -W .github/workflows/test.yml
```

### Example .secrets file (optional)

Create a `.secrets` file in the root directory:

```
GITHUB_TOKEN=your_token_here
CUSTOM_SECRET=secret_value
```

## Action Inputs

- `custom-message`: Custom message to display before environment variables (optional)

## Action Outputs

- `env-count`: Number of environment variables found

## Testing the Action

The workflow tests the action on multiple operating systems:
- Ubuntu (Linux)
- Windows
- macOS

Each job sets up custom environment variables and then runs the action to display all environment variables.

## Expected Output

When you run the action, you should see:
1. Your custom message
2. A sorted list of all environment variables
3. The total count of environment variables
4. GitHub-specific environment variables (if any)

## Troubleshooting

If ACT fails to run:
1. Make sure Docker is running
2. Check that you have the correct permissions
3. Try running with `act -v` for verbose output
4. Ensure your workflow YAML is valid
