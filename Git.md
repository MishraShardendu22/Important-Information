# Git and Basic Command Guide

This document provides a comprehensive overview of essential Git commands as well as a few basic shell commands that will help you navigate and manage your Git repositories.

## Table of Contents
1. [Setting Up](#setting-up)
2. [Creating and Managing Repositories](#creating-and-managing-repositories)
3. [Basic Workflow](#basic-workflow)
4. [Branching and Merging](#branching-and-merging)
5. [Stashing Changes](#stashing-changes)
6. [Remote Repositories](#remote-repositories)
7. [Miscellaneous Commands](#miscellaneous-commands)

---

## 1. Setting Up

### git config
- **Description**: Configures user information, such as name and email, for Git.
- **Usage**: 
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

### git --version
- **Description**: Displays the installed Git version.
- **Usage**: 
  ```bash
  git --version
  ```

---

## 2. Creating and Managing Repositories

### git init
- **Description**: Initializes a new Git repository.
- **Usage**: 
  ```bash
  git init
  ```

### mkdir
- **Description**: Creates a new directory.
- **Usage**:
  ```bash
  mkdir project-directory
  ```

### cd
- **Description**: Changes directory to the specified folder.
- **Usage**:
  ```bash
  cd project-directory
  ```

### touch
- **Description**: Creates a new, empty file.
- **Usage**:
  ```bash
  touch file.txt
  ```

---

## 3. Basic Workflow

### git add
- **Description**: Adds files to the staging area.
- **Usage**: 
  ```bash
  git add file.txt
  ```

### git status
- **Description**: Displays the status of the working directory and staging area.
- **Usage**: 
  ```bash
  git status
  ```

### git commit
- **Description**: Commits the staged changes.
- **Usage**: 
  ```bash
  git commit -m "Commit message"
  ```

### git diff
- **Description**: Shows the differences between files.
- **Usage**: 
  ```bash
  git diff
  ```

---

## 4. Branching and Merging

### git branch
- **Description**: Lists branches or creates a new branch.
- **Usage**:
  ```bash
  git branch new-branch
  ```

### git switch
- **Description**: Switches to a specified branch or commit.(Newer Alternative to git checkout)
- **Usage**:
  ```bash
  git switch new-branch
  ```

### git checkout
- **Description**: Switches to a specified branch or commit.
- **Usage**:
  ```bash
  git checkout new-branch
  ```

### git merge
- **Description**: Merges the specified branch into the current branch.
- **Usage**:
  ```bash
  git merge branch-name
  ```

### git rebase
- **Description**: Reapplies commits on top of another base tip.
- **Usage**:
  ```bash
  git rebase branch-name
  ```

---

## 5. Stashing Changes

### git stash
- **Description**: Temporarily saves changes in the working directory.
- **Usage**:
  ```bash
  git stash
  ```

---

## 6. Remote Repositories

### git remote
- **Description**: Manages remote connections to repositories.
- **Usage**:
  ```bash
  git remote add origin https://github.com/username/repo.git
  ```

### git push
- **Description**: Uploads changes to a remote repository.
- **Usage**:
  ```bash
  git push origin main
  ```

### git pull
- **Description**: Fetches and merges changes from a remote repository.
- **Usage**:
  ```bash
  git pull origin main
  ```

### git clone
- **Description**: Creates a copy of a repository.
- **Usage**:
  ```bash
  git clone https://github.com/username/repo.git
  ```

---

## 7. Miscellaneous Commands

### git rm --cached
- **Description**: Removes files from the staging area but keeps them in the working directory.
- **Usage**:
  ```bash
  git rm --cached file.txt
  ```

### ls and ls -la
- **Description**: Lists files and directories in the current folder; `-la` shows detailed information.
- **Usage**:
  ```bash
  ls
  ls -la
  ```

### pwd
- **Description**: Displays the current working directory.
- **Usage**:
  ```bash
  pwd
  ```
