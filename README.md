Agent files
===========

This repository contains AI agent instructions, skills, et.al.

The files are meant to be used for VS Code with Copilot, but 
it might be able to use other IDE or Coding Agents.

Properties to modify
--------------------

The VS Code properties below are nice to modify so that you can
use the repository files without moving.

- `chat.instructionsFilesLocations`: For custom instructions (not yet there)
- `chat.promptFilesLocations`: For custom prompts (not yet there)
- `chat.agentFilesLocations`: For custom agents (not yet there)
- `chat.agentSkillsLocations`: For agent skills

For more details of VS Code, see 
[Customize AI in Visual Studio Code](https://code.visualstudio.com/docs/copilot/customization/overview)

Skills
------

- `notification`
  Send desktop notification.
  When agent requires your attention, then this skill can be used.
- `user-input`
  Receiving user input from terminal.
  When agent requires your input, then this skill can be used.
  This is useful to reduce message consumption on VS Code.
