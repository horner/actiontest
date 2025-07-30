# Runner Setup Simplification Strategies

## 1. Environment Variables (Current approach)
✅ **Pros**: Clean workflow, automatic GitHub context access
❌ **Cons**: Still need to define each variable

## 2. Configuration File
Create a config file in your repo:

```yaml
# .runner-config.yml
proxmox:
  username: demouser
  host: proxmox.example.com
container:
  distribution: rocky
  resources:
    cpu: 2
    memory: 4GB
runner:
  labels: [self-hosted, linux, x64]
  create_job: true
```

Then your action reads this file instead of inputs.

## 3. Minimal Inputs with Defaults
Only require essential inputs:

```yaml
inputs:
  environment:
    description: 'Environment (dev/staging/prod)'
    required: true
    default: 'dev'
  runner-type:
    description: 'Type of runner to create'
    required: false
    default: 'standard'
```

Action uses these to determine all other settings.

## 4. Convention over Configuration
Use repository/branch naming conventions:
- Repo name determines container name
- Branch name determines environment
- GitHub context provides the rest

## 5. Secret Bundle
Store all config as one JSON secret:

```json
{
  "proxmox": {"username": "user", "password": "pass"},
  "container": {"distribution": "rocky"},
  "runner": {"create_job": true}
}
```

Parse JSON in action instead of multiple secrets.

## Recommendation: Environment Variables + Defaults
Your current approach is clean and follows GitHub Actions best practices!
