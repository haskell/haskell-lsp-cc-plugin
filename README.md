# haskell-language-server-lsp

Haskell language server ([HLS](https://haskell-language-server.readthedocs.io/)) for Claude Code, providing code intelligence, diagnostics and navigation for Haskell projects.

## Supported Extensions
`.hs`, `.lhs`, `.cabal`

## Installation

The plugin only registers the server with Claude Code; `haskell-language-server-wrapper` must be on your `PATH`. The wrapper picks the HLS build matching the GHC version your project uses.

### Via GHCup (recommended)
```bash
ghcup install hls
```

### Via Homebrew (macOS)
```bash
brew install haskell-language-server
```

### Via package manager (Linux)
```bash
# Arch Linux
sudo pacman -S haskell-language-server

# Nix
nix profile install nixpkgs#haskell-language-server
```

Verify the install with `haskell-language-server-wrapper --version`.

## Project setup

HLS discovers how to build your project through a [cradle](https://haskell-language-server.readthedocs.io/en/latest/configuration.html#configuring-your-project-build): `cabal.project`, `stack.yaml` or an `hie.yaml` are detected automatically. The first request in a project can be slow while HLS builds the cradle and loads dependencies, which is why this plugin sets a 120s startup timeout. The project should build with `cabal build` or `stack build` before you rely on HLS.

## Known limitations
- **Slow first request.** HLS loads your project and its dependencies on startup. The first one or two LSP calls in a session can fail with `server is starting`; retrying a moment later succeeds.
- **The project must build.** HLS needs a working cradle (`cabal build` / `stack build` succeeding at least once), otherwise it reports cradle errors instead of code intelligence.

## Install the plugin
```
/plugin install haskell-language-server-lsp --marketplace LaurentRDC/haskell-lsp
```

## More Information
- [HLS documentation](https://haskell-language-server.readthedocs.io/)
- [GitHub Repository](https://github.com/haskell/haskell-language-server)
