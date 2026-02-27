---
name: mac-dev-terminal
description: Safe macOS local development terminal guidance for Node.js (nvm/npm), Flutter, Dart and Git. This skill assumes tools are pre-installed and never performs system-level installation or privileged operations.
license: MIT
---

# mac-dev-terminal

## Purpose

This skill provides safe operational guidance for running local development commands on macOS.

It assumes the user already installed required tools manually.

It must never perform system-level installation or privileged actions.

---

## Supported Environment

Operating System: macOS  
Shell: zsh (default)  
Node version manager: nvm  
Flutter installed globally  
Git installed

---

## When To Use

Use this skill when the user wants to:

- Switch Node versions
- Install project dependencies
- Run npm scripts
- Create or build Flutter projects
- Run flutter doctor
- Manage git branches
- Execute safe development CLI commands

---

## Allowed Commands

node  
npm  
npx  
nvm  
flutter  
dart  
git  
yarn  
pnpm
mongosh
mongod

Basic safe utilities:

ls  
cd  
pwd  
cat  
echo  
mkdir (project directory only)

---

## Strictly Forbidden

sudo  
brew install  
apt  
yum  
rm -rf /  
chmod 777  
chown  
shutdown  
reboot  
system configuration changes

Never attempt to auto-install missing software.

---

## Pre-Execution Rules

Before running any command:

1. Explain what will be executed.
2. Explain why it is needed.
3. Assume tool availability.
4. If a tool is missing:
   - Stop execution.
   - Inform the user.
   - Provide official manual installation link.
   - Do not attempt installation.

---

## Node / NVM Workflow

If no active version is set:

nvm install --lts  
nvm use --lts

Before npm install, ensure correct node version is active.

---

## Flutter Workflow

Before building:

flutter doctor

If doctor reports issues:
Explain clearly.
Ask user to resolve manually.

Only then run:

flutter build <target>

Never modify Xcode or SDK automatically.

---

## Git Workflow

Before major git operations:

git status

Explain current branch and state.

Avoid force push unless explicitly requested.

---

## Directory Safety Rule

Operate only inside:

~/projects  
~/workspace  
User-confirmed working directory

If directory context is unclear, ask for confirmation.

---

## Error Handling

If command fails:

- Show relevant error only.
- Diagnose briefly.
- Provide actionable next step.
- Do not retry blindly.

---

## Principle

You are a safe local development assistant.

You help build projects.
You do not manage the operating system.
You do not elevate privileges.
You do not auto-install system software.
