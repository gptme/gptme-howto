# How-To: Check an ibara MCP Connection

Connect gptme to ibara's local MCP server and verify tool discovery before asking an agent to use a computer.

ibara is computer use for agents on Omarchy computers you own. This recipe checks the connection only: it does not install ibara, pair computers, acquire a desktop or prove a GUI task succeeds.

## Before you start

- Install gptme. This recipe was checked with gptme **0.35.1**.
- Have the `ibara` command installed on the computer running gptme. The diagnostic used ibara **0.3.1-1**. Follow the [ibara installation guide](https://ibara.app/docs/install) for its Omarchy requirements.
- Run `command -v ibara` and keep its absolute path. This is a local stdio server; an ibara website URL is not its MCP endpoint.

## The prompt

```text
Help me connect gptme to the locally installed ibara MCP server.
Inspect my existing gptme MCP configuration first. Preserve other servers and settings;
show the proposed change before writing it. Use the absolute path returned by
command -v ibara, with the argument mcp. Run gptme-util mcp test ibara and
report whether the connection succeeded and which tools were discovered.
Stop after that diagnostic. Do not start a desktop task or change pairing,
network settings or tool approval settings.
```

## The configuration

In `~/.config/gptme/config.toml`, merge the following with your existing settings. Replace `/absolute/path/to/ibara` with the path you found:

```toml
[mcp]
enabled = true
auto_start = true

[[mcp.servers]]
name = "ibara"
enabled = true
command = "/absolute/path/to/ibara"
args = ["mcp"]
```

If `[mcp]` already exists, edit that table instead of adding it twice. Preserve its other servers; if one is already named `ibara`, update that entry. `auto_start` controls server startup in gptme sessions: retain your chosen policy if you already manage startup manually. The diagnostic below explicitly connects to the named server.

Run from your intended workspace:

```sh
gptme-util mcp test ibara
```

Project and conversation settings can override global settings. For a project-defined server, current gptme asks for confirmation and shows the command it will execute; inspect it before approving. See [gptme's MCP configuration documentation](https://gptme.org/docs/mcp.html).

## What to verify

The witnessed diagnostic printed:

```text
Testing ibara (stdio)...
Connected successfully!
Available tools (11):
```

The discovered tools included `computer_status`, `computer_begin`, `computer_observe`, `computer_act` and `computer_finish`. Check the actual output for your installed release rather than treating eleven as a permanent contract.

A successful connection means gptme initialized the server and discovered tools. It does not establish that a computer is paired, awake, unlocked, available or permitted for a task. Use ibara's [agent setup](https://ibara.app/docs/agents) and [first-task guide](https://ibara.app/docs/first-task) for those next steps.

## Verification scope

The connection command was run with gptme 0.35.1 and ibara 0.3.1-1 on a build host, using a separate home/config/data/cache directory and no model credentials. It exited successfully, discovered eleven tools and left no task processes running. No model request or desktop tool was called. The prompt above is a suggested way to request setup; it was not exercised as a model-driven conversation. This is not gptme desktop-task certification or independent adoption evidence.

## Tips

- If the executable cannot be found, check the absolute path and the environment from which gptme starts its server.
- If a workspace supplies another `ibara` entry, inspect its command and configuration precedence before retrying.
- Model usage in a later agent session has its own provider costs. The connection diagnostic itself needs no model request.

Disclosure: I build [ibara](https://github.com/MayberryDT/ibara).
