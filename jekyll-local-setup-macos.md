# Jekyll Local Development Setup for macOS

This guide provides step-by-step instructions for setting up Jekyll locally on macOS for complete beginners developing sites with the Minimal Mistakes theme. Specifically tested on macOS 15 (Sequoia), this setup uses `chruby` and `ruby-install` as recommended by the official Jekyll documentation.

## Quick Reference (For Experienced Users)

If you've done this before, here's the command sequence:

```bash
# Install prerequisites
xcode-select --install
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install Ruby tools
brew install chruby ruby-install
ruby-install ruby 3.4.1

# Configure shell
cat >> ~/.zshrc << 'EOF'

# chruby configuration for Jekyll development
source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh
source $(brew --prefix)/opt/chruby/share/chruby/auto.sh
chruby ruby-3.4.1
EOF

source ~/.zshrc

# Set up Jekyll
cd your-project
gem install bundler
bundle install
bundle exec jekyll serve
```

Then visit http://127.0.0.1:4000/myreponame/ (or your configured baseurl)

**New to this?** Read the complete guide below with explanations for each step.

---

## Why This Setup?

- **Works on macOS 15+**: Homebrew's Ruby 4.0 and Ruby 3.3 have compatibility issues with native gem extensions on macOS 15
- **Recommended by Jekyll**: Official Jekyll docs recommend chruby + ruby-install
- **Version management**: Easily switch between Ruby versions for different projects
- **Matches production**: Using Ruby 3.4.1 compiles gems that work across environments
- **Minimal Mistakes compatible**: Works seamlessly with the Minimal Mistakes Jekyll theme
- **GitHub Pages compatible**: Uses the `github-pages` gem to match GitHub's Jekyll environment exactly

## Prerequisites

This guide assumes you're starting from a fresh macOS installation. We'll install everything you need:

- macOS (tested on macOS 15 Sequoia, but works on macOS 10.15 Catalina and later)
- Administrator access to your Mac
- Internet connection
- About 30-45 minutes for initial setup

## Complete Setup for Beginners

### Step 0: Open Terminal

Before we begin, you'll need to use the **Terminal** application:

1. Press `Command (⌘) + Space` to open Spotlight Search
2. Type "Terminal" and press Enter
3. Keep this Terminal window open - you'll use it throughout this guide

**Tip:** Pin Terminal to your Dock by right-clicking its icon and selecting "Options > Keep in Dock"

### Step 1: Install Xcode Command Line Tools

The Xcode Command Line Tools provide essential development tools like compilers that are needed to build Ruby and Jekyll.

**Install:**

```bash
xcode-select --install
```

A dialog box will pop up asking you to install the tools. Click "Install" and accept the license agreement. This download is about 500 MB and takes 5-15 minutes depending on your internet speed.

**Verify Installation:**

After installation completes, verify it worked:

```bash
xcode-select -p
```

You should see output like:
```
/Library/Developer/CommandLineTools
```

If you see an error, try running the install command again.

### Step 2: Install Homebrew

Homebrew is a package manager for macOS that makes it easy to install software from the command line.

**Install:**

Copy and paste this entire command into Terminal and press Enter:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

**What you'll see:**
- The script will explain what it will install
- You'll need to press Enter to continue
- You'll be asked for your Mac password (the same one you use to log in)
- Installation takes 5-10 minutes

**Important:** After installation completes, Homebrew may display a message in a highlighted box that says "Next steps:" Follow those instructions exactly - they typically involve running 2 commands to add Homebrew to your PATH. The commands will look like this (but use the exact commands shown in YOUR terminal):

```bash
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

**Verify Installation:**

```bash
brew --version
```

You should see something like `Homebrew 4.x.x`

**Troubleshooting:**
- If you see "command not found: brew", you need to run the "Next steps" commands shown after installation
- Close Terminal and open a new window, then try again

### Step 3: Install Ruby Version Manager (chruby and ruby-install)

Now that Homebrew is installed, we'll use it to install tools for managing Ruby versions.

**Install:**

```bash
brew install chruby ruby-install
```

This takes 1-2 minutes and installs two tools:
- **ruby-install**: Downloads and compiles Ruby from source
- **chruby**: Lets you switch between different Ruby versions

### Step 4: Install Ruby 3.4.1

This step compiles Ruby from source code, which takes 5-10 minutes:

```bash
ruby-install ruby 3.4.1
```

**What you'll see:**
- A lot of text scrolling by (this is normal)
- Progress messages about downloading and compiling
- Eventually a success message

**Why compile from source?** Homebrew's pre-built Ruby packages have compatibility issues with macOS 15's development tools. Compiling from source ensures everything works correctly.

**Troubleshooting:**
- If you see errors about missing tools, make sure Step 1 (Xcode Command Line Tools) completed successfully
- If compilation fails, try updating Homebrew first: `brew update`

### Step 5: Configure Your Shell to Use Ruby 3.4.1

Your Mac uses a shell program called **zsh** to interpret commands. We need to tell zsh to use the Ruby version we just installed.

**Configure:**

Copy and paste this entire command block into Terminal:

```bash
cat >> ~/.zshrc << 'EOF'

# chruby configuration for Jekyll development
source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh
source $(brew --prefix)/opt/chruby/share/chruby/auto.sh
chruby ruby-3.4.1
EOF
```

**What this does:** Adds a configuration to your `~/.zshrc` file that:
1. Loads chruby when you open a new terminal
2. Enables automatic Ruby version switching
3. Sets Ruby 3.4.1 as your default Ruby version

**For bash users:** If you know you're using bash instead of zsh (macOS uses zsh by default since macOS Catalina), replace `~/.zshrc` with `~/.bash_profile`.

### Step 6: Activate the Configuration

To apply the changes without closing Terminal, run:

```bash
source ~/.zshrc
```

**Tip:** Alternatively, you can close Terminal and open a new window - the configuration will load automatically.

### Step 7: Verify Ruby Installation

Check that everything is working correctly:

```bash
ruby -v
```

You should see something like:
```
ruby 3.4.1 (2024-12-25 revision 48d4efcb85) +PRISM [arm64-darwin24]
```

Now check that Ruby is installed in the right location:

```bash
which ruby
```

You should see:
```
/Users/YOUR_USERNAME/.rubies/ruby-3.4.1/bin/ruby
```

**Important:** If you see `/usr/bin/ruby`, the configuration didn't load. Go back to Step 6 and try again, or open a new Terminal window.

## Setting Up Your Jekyll Site with Minimal Mistakes

For this part, go to [install-theme-instructions](install-theme-instructions.md) to continue.



