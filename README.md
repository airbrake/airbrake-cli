<p align="center">
  <img src="https://airbrake-github-assets.s3.amazonaws.com/brand/airbrake-full-logo.png" width="200">
</p>

# Airbrake CLI

The official command-line tool to interact with [Airbrake.io](https://airbrake.io/).

## Contents
- [Installation](#installation)
- [Authentication](#authentication)
  - [Username and password](#log-in-with-username-and-password)
  - [GitHub and SSO logins](#log-in-or-run-commands-without-a-username-and-password)
- [Command usage](#command-usage)
  - [Basic commands](#basic-commands)
  - [Going further](#going-further)

## Installation

### Homebrew

```
brew tap airbrake/airbrake-cli
brew install airbrake
```

## Authentication

### Log in with Username and Password

Log in to Airbrake by issuing the following command:

```
airbrake login
```

The `login` command will prompt you for your email, password, and an optional subdomain ([account subdomains](https://airbrake.io/docs/airbrake-faq/what-is-my-subdomain/) are used to differentiate if you have multiple Airbrake accounts using the same email address).

```
Enter your email: myemail@example.com
Enter your password:
Enter your subdomain (optional):
Done! The Airbrake CLI is configured for myemail@example.com
```

Completing the `login` command will generate a file in `$HOME/.airbrake.yaml` with contents like:

```
project-key: ""
user-key: ""
user-token: YOUR_USER_TOKEN
```
### Log in, or run commands, without a username and password

If your account requires GitHub logins, or an SSO login, you cannot use the `login` command. To authenticate in this situation, you must specify either the `--user-key` or `--project-key` flags to the Airbrake CLI, or configure your `$HOME/.airbrake.yaml` file.

The following are global flags for the `airbrake` command.

```
Flags:
      --config string        config file (default is $HOME/.airbrake.yaml)
      --project-key string   Project key used to access the API
      --user-key string      User key used to access the API
```

Instead of passing the flags to the command, you can set environment variables corresponding to the flags. The name of the environment variable must begin with `AB_` and be followed by the upper case version of the command flag with hyphens converted to underscores, e.g. `AB_USER_KEY` for the `user-key` flag.

```
export AB_USER_KEY=yourkey
airbrake projects list
```

Another alternative is to create a config file with your user key in it. Create a file in the default location, `$HOME/.airbrake.yaml`, with the following contents:

```
project-key: YOUR_PROJECT_KEY
user-key: YOUR_USER_KEY
```

## Command usage

### Basic commands

This short example will show you how to send a test error notice to a project with some basic commands.

#### List projects

Before we send the test error notice, we need to get the `id` of the project we want to send the notice to. To do this, invoke:

```
airbrake projects list
```

We'll be using the `id` field from the `project list` output in the next command.

#### Send error notice

Quickly create an error notice using the `notices create` command. Use the project ID you found when you listed your projects above.

```
airbrake notices create --project-id YOUR_PROJECT_ID \
    --type "Sample Error" \
    --message "My first error from the CLI"
```

This will send an error notice to the project you specified and provide you a direct link.

### Going further

For information on all the available commands like deploys and more, invoke:

```
airbrake --help
```
