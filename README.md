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
  - [Install command](#install-command)
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

If your account requires GitHub or SSO login, or you have you two factor-authentication enabled, you cannot use the `login` command. To authenticate in this situation, you must specify either the `--user-key` flag to the Airbrake CLI, or configure the Airbrake CLI with your user key.

The following are global flags for the `airbrake` command.

```
Flags:
      --config string        config file (default is $HOME/.airbrake.yaml)
      --project-key string   Project key used to access the API
      --user-key string      User key used to access the API
```

Instead of passing the flags to individual commands, you can set credentials using the `airbrake config set` command. To set your user key (which can be retreived from [your profile settings page](https://airbrake.io/users/edit)) with the `config set` command, invoke:

```
airbrake config set user-key YOUR_USER_KEY_HERE
```

To check the values the Airbrake CLI is using, invoke:

```
airbrake config show
```

## Install command

The Airbrake CLI offers an installation command which supports Ruby, Rails, Go, C#, Java, JavaScript, PHP, Python, Swift, and TypeScript via the install command:

```
# Use the --project-id flag if you already have an Airbrake project in your account
airbrake install --project-id 12345

# Or have the install command create a new Airbrake project:
airbrake install --create-project=DESIRED_PROJECT_NAME
```

## Command usage

### Basic commands

This short example will show you how to send a test error notice to an Airbrake project with some basic commands.

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
