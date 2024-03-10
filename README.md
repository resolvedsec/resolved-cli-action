<img src='resolved.jpg' width='500'>

# Resolved Security GitHub Action

Resolved Security GitHub action scans your project for vulnerable open source libraries and suggest fixes using Resolved Security hardened open source libraries, helping you improve your code's security posture.

If you want to learn more, contact us at <info@resolvedsecurity.com>.

###### Features

* Identifies vulnerabilities in your project's open-source dependencies.
* Suggests hardened versions of vulnerable libraries (when available).
* Integrates seamlessly into your CI/CD workflow.

###### Benefits

* Rapidly minimize exposure window for open source vulnerabilities.
* Reduce R&D interrupts and save development time with automated vulnerability remediation.
* Proactive security by addressing open-source vulnerabilities early.

#### Getting Started

1. Create a Resolved Security account
  If you do not already have an account, please contact us at <sales@resolvedsecurity.com>
2. Obtain user credentials
3. Configure required [secrets and variables](#inputs)
4. Add the action to your [project's workflow](#using-the-resolved-security-github-action-in-your-workflow)

#### Using the Resolved Security GitHub Action In Your Workflow

Here is a sample workflow using the Resolved Security GitHub action:

```yaml
name: NPM Demo CI
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]
jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [ 18 ]
    steps:
    - uses: actions/checkout@v4
    - name: Use Node.js ${{ matrix.node-version }}
      uses: actions/setup-node@v4
      with:
        node-version: ${{ matrix.node-version }}
    - name: Run Resolved Security Action
      uses: resolvedsec/resolved-cli-action@v0.1
      with:
        ecosystem: ${{ vars.ECOSYSTEM }}
        resolved_user: ${{ secrets.RESOLVED_USER }}
        resolved_token: ${{ secrets.RESOLVED_TOKEN }}
        resolved_token_base64: ${{ secrets.RESOLVED_TOKEN_BASE64 }}
    - name: Run NPM Install
      run: npm install
```

### Inputs

It is recommended to use repository level [secrets and variables](https://docs.github.com/en/actions/learn-github-actions/variables) to manage action configuration.

#### `ecosystem`

Description: Configures the ecosystem of your project. For example: 'npm', 'pypi', 'maven'.
Default: None
Required: Yes

```yaml
with:
ecosystem: npm
```

or, if you are using a repository variable:

```yaml
with:
ecosystem: ${{ vars.ECOSYSTEM }}
```

#### `resolved_user`

Description: Credentials for running the GitHub action.
Default: None
Required: Yes

```yaml
with:
resolved_user: my_user
```

or, if you are using a repository variable:

```yaml
with:
resolved_user: ${{ vars.RESOLVED_USER }}
```

#### `resolved_token`

Description: Credentials for running the GitHub action.
Default: None
Required: Yes

```yaml
with:
resolved_token: my_token
```

or, if you are using a repository variable:

```yaml
with:
resolved_token: ${{ vars.RESOLVED_TOKEN }}
```

#### `resolved_token_base64`

Description: Credentials for running the GitHub action. This value can be obtained by running `echo <resolved_token> | base64`
Default: None
Required: Yes

```yaml
with:
resolved_token_base64: my_token_in_base64
```

or, if you are using a repository variable:

```yaml
with:
resolved_token_base64: ${{ vars.RESOLVED_TOKEN_BASE64 }}
```

### License

Please refer to [LICENSE](LICENSE) file.
