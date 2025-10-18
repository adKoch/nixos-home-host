# Claude AI Project Guidelines

## Core Principles

- Be brief in all documentation
- Follow hexagonal architecture with clean, understandable solutions
- No explanation comments - code should be self-explanatory
- Minimal documentation

## Development Environment

- Use Taskfile as main interaction method - no random script running
- All packages and dependencies via Nix
- Only Taskfile and Nix should be installed on computer

### Nix Best Practices

- Use `nix develop` instead of `nix-shell` with flakes
- Define project environments in `flake.nix` with `devShells`
- Use `direnv` with `.envrc` containing `use flake` for automatic environment loading
- Lock dependencies with `flake.lock` for reproducibility
- Keep same nixpkgs revision across projects to avoid multiple downloads

Example `flake.nix`:

```nix
{
  description = "Development environment";
  inputs.nixpkgs.url = "github:nixos/nixpkgs/nixos-unstable";
  outputs = { self, nixpkgs }: let
    system = "x86_64-linux";
    pkgs = nixpkgs.legacyPackages.${system};
  in {
    devShells.${system}.default = pkgs.mkShell {
      buildInputs = with pkgs; [ nodejs_20 python3 postgresql ];
      shellHook = ''echo "🚀 Dev environment loaded"'';
    };
  };
}
```

Example `.envrc`:

```bash
use flake
```

## Clean Code Principles

- **Intention-revealing names**: Names should explain why, what, and how
- **Single Responsibility**: Functions do one thing only
- **Small functions**: Ideally <20 lines, single level of abstraction
- **Command-Query Separation**: Functions either do something or return something
- **Boy Scout Rule**: Leave code cleaner than you found it
- **Self-explanatory code**: Minimize comments, code should speak for itself

## Clean Architecture Principles

- **Dependency Rule**: Dependencies point inward only (outer → inner layers)
- **Layers**: Frameworks → Adapters → Use Cases → Entities
- **Dependency Inversion**: Depend on abstractions, not concretions
- **Independence**: Business logic isolated from frameworks, databases, UI
- **Testability**: Inner layers testable without external dependencies
- **Hexagonal Architecture**: Same isolation via ports & adapters pattern
