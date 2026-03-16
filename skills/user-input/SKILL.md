---
name: user-input
description: Guide for requesting user input and receiving it. Use this when you need to ask user for information or decision.
argument-hint: Question to ask user
user-invocable: true
---

Requesting user input
=====================

This skill must be used when an agent needs to ask user for information or decision.

**IMPORTANT for agents:** When using `run_in_terminal` tool to execute user input commands, set `timeout` parameter to `0` (no timeout) or a very long value (e.g., `300000` for 5 minutes) to give users sufficient time to respond.

When to use single-line vs multi-line input
============================================

**Use single-line input for:**
- Yes/no questions
- Short answers (names, numbers, single words)
- Selecting from options
- File paths or URLs
- Any input expected to be less than one sentence

**Use multi-line input for:**
- Detailed explanations or feedback
- Code snippets or configuration content
- Multiple items or lists
- Any input expected to be more than one sentence
- When user might want to compose thoughtful responses

How to receive user input
==========================

The user input is shell dependent. Follow the instructions below to receive appropriately.

**Platform defaults:**
- macOS: Zsh (since macOS 10.15 Catalina)
- Linux: Usually Bash
- Windows: PowerShell or cmd

Zsh (macOS default)
-------
Use `read` with prompt syntax. The command waits indefinitely by default. 

**Recommended (with colored prompt for clarity):**

```zsh
echo -n "\033[1;33m{question} \033[0m" && read user_input
echo "User input: $user_input"
```

Alternative (simple):

```zsh
read "user_input?{question} "
echo "User input: $user_input"
```

Note: The colored version uses yellow (1;33m) to distinguish the prompt from user input. Avoid using `-t` flag for timeout as it will terminate if user doesn't respond quickly.

Bash and other POSIX-compliant shells
-------
Use `read -p` command. The command waits indefinitely by default. 

**Recommended (with colored prompt for clarity):**

```bash
echo -n -e "\033[1;33m{question} \033[0m" && read user_input
echo "User input: $user_input"
```

Alternative (simple):

```bash
read -p "{question} " user_input
echo "User input: $user_input"
```

Note: The colored version uses yellow (1;33m) to distinguish the prompt from user input. Avoid using `-t` flag for timeout as it will terminate if user doesn't respond quickly.

PowerShell
-------
Use `Read-Host` cmdlet.

**Recommended (with colored prompt for clarity):**

```powershell
Write-Host "{question} " -ForegroundColor Yellow -NoNewline
$user_input = Read-Host
Write-Host "User input: $user_input"
```

Alternative (simple):

```powershell
$user_input = Read-Host -Prompt "{question} "
Write-Host "User input: $user_input"
```

Note: The colored version uses yellow to distinguish the prompt from user input.

Windows cmd
-----------
Use `set /p` command. Example:

```cmd
set /p user_input="{question} "
echo User input: %user_input%
```

Note: cmd does not support colored prompts natively. Consider using PowerShell for better user experience.

Multi-line input
================

For longer responses, use these methods to accept multi-line input.

**IMPORTANT:** Always include termination instructions in your prompt (e.g., "Press Ctrl+D when done") so users know how to finish their input.

Zsh / Bash
----------
Use heredoc or `cat`. User presses Ctrl+D to finish.

```zsh
echo -e "\033[1;33m{question} (Press Ctrl+D when done)\033[0m"
user_input=$(cat)
echo "User input: $user_input"
```

PowerShell
----------
Read multiple lines until empty line:

```powershell
Write-Host "{question} (Press Enter twice when done)" -ForegroundColor Yellow
$lines = @()
while ($true) {
    $line = Read-Host
    if ([string]::IsNullOrEmpty($line)) { break }
    $lines += $line
}
$user_input = $lines -join "`n"
Write-Host "User input: $user_input"
```
```
