---
applyTo: "**"
---

General instructions
====================

Definition of done
------------------

- All tasks are completed.
- All tests have passed.
- The user is notified about the completion of the tasks.
- Request user approval for completion

Clarification
-------------

If you have any questions or need further clarification, send
notification to the user and ask user input for
clarification. Whenever an agent needs to ask a question to the user,
it **MUST USE** the `vscode_askQuestions` tool. This ensures that all
questions are presented in a structured and interactive manner,
allowing the user to provide clear and actionable responses.

Temporary files
---------------

In case you need to make a temporary file, you **MUST USE** the
project space.

After finishing all tasks
-------------------------

You **MUST** ask approval and/or feedback via the `vscode_askQuestions` tool.
I need to review your change and may provide extra feedback.
