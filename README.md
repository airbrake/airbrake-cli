<p align="center">
  <img src="https://airbrake-github-assets.s3.amazonaws.com/brand/airbrake-full-logo.png" width="200">
</p>

# Airbrake CLI

The official command-line tool to interact with [Airbrake.io](https://airbrake.io/).

## Contents
- [Installation](#installation)
- [Authentication](#authentication)
  - [Login command](#login-command)
  - [Config command](#config-command)
  - [Global flags](#global-flags)
- [Commands](#commands)
  - [Install command](#install-command)
  - [Projects list command](#projects-list-command)
  - [Notices create command](#notices-create-command)
  - [Going further](#going-further)

## Installation

### Homebrew

```
brew tap airbrake/airbrake-cli
brew install airbrake
```

## Authentication

### Login command

_**Note:** the `login` command requires username and password and does not support two-factor authentication. For alternative authentication methods (eg: in cases where GitHub logins, SSO, or two-factor authentication are used), please use the [`config` command](#config-command) or [global flags](#global-flags)._

Log in with the Airbrake CLI by issuing the following command:

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

### Config command

If your account requires GitHub or SSO logins, or you have you two-factor authentication enabled, you cannot authenticate with the `login` command. To authenticate in this situation, you can set credentials using the `airbrake config set` command. To set your user key (which can be retreived from [your profile settings page](https://airbrake.io/users/edit)) with the `config set` command, invoke:

```
airbrake config set user-key YOUR_USER_KEY_HERE
```

To check the values the Airbrake CLI is using, invoke:

```
airbrake config show
```

### Global flags

Alternative to the `login` and `config` commands, you may specify the `--user-key` flag to the Airbrake CLI. The following are global flags for the `airbrake` command:

```
Flags:
      --config string        config file (default is $HOME/.airbrake.yaml)
      --project-key string   Project key used to access the API
      --user-key string      User key used to access the API
```

## Commands

### Install command

The Airbrake CLI offers an installation command which supports Ruby, Rails, Go, C#, Java, JavaScript, PHP, Python, Swift, and TypeScript via the `install` command:

```
# Use the --project-id flag if you already have an Airbrake project in
# your account you want to use
airbrake install --project-id 12345

# Or have the install command create a new Airbrake project:
airbrake install --create-project=DESIRED_PROJECT_NAME
```

### Projects list command

This short example will show you how to send a test error notice to an Airbrake project with some basic commands.

Before we send the test error notice, we need to get the `id` of the project we want to send the notice to. To do this, invoke:

```
airbrake projects list
```

We'll be using the `id` field from the `project list` output in the next command.

### Notices create command

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
