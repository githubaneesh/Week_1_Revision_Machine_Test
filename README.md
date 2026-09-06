# Week 1 Linux Fundamentals Machine Test

This project is a practical revision of Week 1 DevOps and Linux fundamentals. The work is completed in an Ubuntu virtual machine and focuses on navigating the filesystem, creating a maintainable project layout, managing files, creating backups, protecting configuration files, and inspecting the current user.

## Project Overview

The machine test builds a small DevOps workspace named `DevOps-Lab`. It contains separate locations for projects, configuration, scripts, logs, temporary files, and backups. The `projects` directory contains a small demo application's files and supporting documentation.

The exercise demonstrates these core skills:

- Linux filesystem navigation and path awareness
- Creating directories and files from the terminal
- Listing files, including hidden files and detailed permissions
- Moving and renaming files
- Creating and storing backups
- Managing environment variables and project documentation
- Applying least-privilege file permissions
- Identifying the current user, UID, and groups

## Requirements

Complete the following tasks in an Ubuntu terminal.

### Task 1: Navigate the filesystem

Use `pwd`, `ls`, and `ls -la` to inspect the current directory. Practice moving to the home directory and filesystem root with `cd ~` and `cd /`.

```bash
pwd
ls
ls -la
cd ~
pwd
cd /
pwd
```

### Task 2: Confirm navigation paths

Return to the home directory and verify its contents. Use absolute and relative paths correctly while moving between directories.

```bash
cd ~
pwd
ls
cd /
pwd
```

### Task 3: Create the DevOps workspace

Create the main workspace and its supporting directories:

```text
DevOps-Lab/
├── backups/
├── configs/
├── logs/
├── projects/
├── scripts/
└── temp/
```

Commands:

```bash
mkdir -p ~/DevOps/Week1machineTest/DevOps-Lab/{backups,configs,logs,projects,scripts,temp}
cd ~/DevOps/Week1machineTest/DevOps-Lab
ls
ls -la
find .
```

Inside `projects`, create the initial application files:

```bash
cd projects
touch app.js index.html docker-compose.yml README.md
cd ../configs
touch app.env nginx.conf
cd ..
find .
```

### Task 4: Create and store backups

Create backups of `app.js` and `app.env`, then move the backup copies into the top-level `backups` directory.

```bash
cd ~/DevOps/Week1machineTest/DevOps-Lab/projects
cp app.js app.js.backup
cp app.env app.env.backup
mv app.js.backup ../backups/app.js.backup
mv app.env.backup ../backups/app.env.backup
ls
ls -la ../backups
```

Expected backup files:

```text
backups/
├── app.env.backup
└── app.js.backup
```

### Task 5: Organize and rename project files

Move the Docker Compose file into `scripts` and rename the project README to `project-info.md`.

```bash
cd ~/DevOps/Week1machineTest/DevOps-Lab/projects
mv docker-compose.yml ../scripts/docker-compose.yml
mv README.md project-info.md
ls
```

### Task 6: Add project information

Add environment values to `app.env`:

```bash
cd ~/DevOps/Week1machineTest/DevOps-Lab/projects
printf 'APP_NAME=devops-demo\nENV=production\n' > app.env
cat app.env
```

Add the project description to `project-info.md`:

```bash
printf '# Linux Fundamentals Machine Test\n' > project-info.md
cat project-info.md
```

### Task 7: Set file permissions

Protect the environment file so only the owner can read and write it. Allow the project information file to be read by everyone while only the owner can modify it.

```bash
chmod 600 app.env
chmod 644 project-info.md
ls -l app.env project-info.md
```

Expected permission modes:

```text
app.env         -rw-------  (600)
project-info.md -rw-r--r--  (644)
```

### Task 8: Inspect user identity

Display the current username, UID, and group membership:

```bash
whoami
id
groups
```

These commands confirm:

- `whoami`: the current username
- `id`: the user ID, primary group ID, and supplementary groups
- `groups`: the groups associated with the current user

## Final Project Structure

After completing the tasks, the workspace should look like this:

```text
DevOps-Lab/
├── backups/
│   ├── app.env.backup
│   └── app.js.backup
├── configs/
│   ├── app.env
│   └── nginx.conf
├── logs/
├── projects/
│   ├── app.env
│   ├── app.js
│   ├── index.html
│   └── project-info.md
├── scripts/
│   └── docker-compose.yml
└── temp/
```

> Note: The screenshots show `app.env` being created in `projects`. If the file is instead kept in `configs`, update the commands and final tree consistently.

## Verification Checklist

Run these commands from the `DevOps-Lab` directory before submitting:

```bash
pwd
find . -maxdepth 3 -print
ls -l projects/app.env projects/project-info.md
ls -la backups
cat projects/app.env
cat projects/project-info.md
whoami
id
groups
```

Confirm that:

- All six top-level directories exist.
- The backup files are inside `backups`.
- `docker-compose.yml` is inside `scripts`.
- The renamed documentation file is `projects/project-info.md`.
- `app.env` contains `APP_NAME=devops-demo` and `ENV=production`.
- `app.env` has mode `600` and `project-info.md` has mode `644`.
- User identity and group information can be displayed successfully.

## Evidence Screenshots

The original terminal work is recorded in these screenshots:

1. [Task 1](task_1.png)
2. [Task 2](task_2.png)
3. [Task 3 - workspace creation](task_3_1.png)
4. [Task 3 - structure verification](task_3_2.png)
5. [Task 4 and Task 5](task-4.png)
6. [Task 4 backup verification](task-5.png)
7. [Task 6 environment and project information](task-6.png)
8. [Task 7 permissions](task_7.png)
9. [Task 8 user identity](task-8.png)

## Learning Outcome

By completing this machine test, you practice the command-line operations needed to work safely with Linux-based DevOps environments and establish a clean foundation for later scripting, containerization, and deployment tasks.
