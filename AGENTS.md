<coding_guidelines>
The user uses fish shell with Starship prompt.
</coding_guidelines>

<factory_configuration>
## Personal Configuration Management

My Factory AI configuration files are managed in `~/.agents/` and symlinked to `~/.factory/`:

| Component | Location | Description |
|-----------|----------|-------------|
| **Commands** | `~/.agents/commands/` | Custom slash commands (e.g., `/commit`, `/cp`) |
| **Skills** | `~/.agents/skills/` | Reusable skill definitions |
| **Hooks** | `~/.agents/hooks/` | Lifecycle hooks for agent execution |
| **Rules** | `~/.agents/rules/` | Custom rules and constraints |
| **Droids** | `~/.agents/droids/` | Custom subagent configurations |

All configuration is version-controlled in the `~/.agents/` directory and symlinked to Factory's expected locations under `~/.factory/`.
</factory_configuration>
