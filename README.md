# Helm Commands Quick Reference Guide

## Repository Management

```bash
# Add a repository
helm repo add [name] [url]
# Example: helm repo add stable https://charts.helm.sh/stable

# Update repositories
helm repo update

# List repositories
helm repo list

# Remove a repository
helm repo remove [name]

# Search for charts
helm search repo [keyword]
# Example: helm search repo nginx
```

## Chart Management

```bash
# Create a new chart
helm create [chart-name]
# Creates basic chart structure with default templates

# Package a chart
helm package [chart-directory]
# Creates a versioned archive file

# Validate a chart
helm lint [chart-directory]
# Examines chart for possible issues

# Show chart details
helm show chart [chart-name]
# Displays chart information

# Show chart values
helm show values [chart-name]
# Displays configurable values
```

## Release Management

```bash
# Install a release
helm install [release-name] [chart-name]
# Example: helm install my-nginx nginx

# Install with custom values
helm install -f values.yaml [release-name] [chart-name]
# Uses custom values from file

# Install with values set directly
helm install --set key1=value1,key2=value2 [release-name] [chart-name]

# Upgrade a release
helm upgrade [release-name] [chart-name]
# Example: helm upgrade my-nginx nginx

# Rollback a release
helm rollback [release-name] [revision]
# Example: helm rollback my-nginx 1

# Uninstall a release
helm uninstall [release-name]
# Removes all resources
```

## Status & Information

```bash
# List releases
helm list
# Shows all releases in current namespace

# List all releases in all namespaces
helm list --all-namespaces

# Get release status
helm status [release-name]
# Shows current state of release

# Get release history
helm history [release-name]
# Shows revision history

# Get release values
helm get values [release-name]
# Shows current configuration
```

## Testing & Debugging

```bash
# Test a release
helm test [release-name]
# Runs tests defined in chart

# Debug template rendering
helm template [chart-directory]
# Shows rendered templates

# Dry run installation
helm install --dry-run --debug [release-name] [chart-name]
# Shows what would be installed
```

## Environment & Configuration

```bash
# Switch namespace
helm -n [namespace] [command]
# Example: helm -n production list

# Use specific kubeconfig
helm --kubeconfig [path] [command]

# Set output format
helm list --output json
# Supports json, yaml, table formats
```

## Helpful Tips

1. Version Control
```bash
# Check helm version
helm version

# See chart versions
helm search repo [chart-name] --versions
```

2. Common Flags
```bash
--namespace, -n: Specify namespace
--create-namespace: Create namespace if not exists
--wait: Wait for resources to be ready
--timeout: Set timeout for operations
--debug: Enable verbose output
```

3. Values Management
```bash
# Generate values file
helm show values [chart-name] > values.yaml

# Compare values
helm get values [release-name] --revision 1 > old_values.yaml
helm get values [release-name] > new_values.yaml
diff old_values.yaml new_values.yaml
```

4. Plugin Management
```bash
# List plugins
helm plugin list

# Install plugin
helm plugin install [url]

# Update plugin
helm plugin update [plugin-name]
```

## Best Practices

1. Always use version control for your chart files

2. Document your values.yaml thoroughly

3. Use --dry-run before actual installations

4. Keep release names consistent across environments

5. Regularly update repositories and dependencies

6. Use namespaces to organize releases

7. Implement proper RBAC for Helm usage

## Common Scenarios

1. Installing with Custom Values
```bash
helm install -f custom-values.yaml my-release stable/nginx
```

2. Upgrading with Multiple Value Files
```bash
helm upgrade -f common.yaml -f prod.yaml my-release ./my-chart
```

3. Rolling Back Failed Upgrade
```bash
helm history my-release    # Find last working revision
helm rollback my-release 2 # Rollback to revision 2
```

4. Debugging Failed Installation
```bash
helm install --debug --dry-run my-release ./my-chart
