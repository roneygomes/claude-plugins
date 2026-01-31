# Claude Plugins

Custom plugins for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## Installation

Add this marketplace to Claude Code:

```bash
/plugin marketplace add roneygomes/claude-plugins
```

Browse available plugins:

```bash
/plugin browse
```

Install a specific plugin:

```bash
/plugin install <plugin-name>@roneygomes-plugins
```

## Available Plugins

| Plugin | Description |
|--------|-------------|
| [ralphy-planning](./plugins/ralphy-planning) | Design planning workflow for [ralphy](https://github.com/michaelshimeles/ralphy) task orchestration |

## Plugin Details

### ralphy-planning

Creates PRDs (Product Requirements Documents) optimized for ralphy's agent-based task execution.

**Skills:**
- `ralphy-planning:start-ralphy-plan` - Full design workflow to ralphy-ready PRD
- `ralphy-planning:flesh-it-out-for-ralphy` - Quick idea refinement before planning

**Install:**
```bash
/plugin install ralphy-planning@roneygomes-plugins
```

**Dependencies:** Requires `ed3d-plan-and-execute` from [ed3d-plugins](https://github.com/ed3dai/ed3d-plugins).

## Contributing

1. Fork this repository
2. Create your plugin in `plugins/your-plugin-name/`
3. Add entry to `.claude-plugin/marketplace.json`
4. Submit a pull request

## License

MIT
