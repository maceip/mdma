# Installation & Setup

## 1. Build from Source
Ensure you have the Rust toolchain installed.

```bash
git clone https://github.com/maceip/merge-engine.git
cd merge-engine
cargo build --release
```

The binary will be available at `target/release/merge-engine`.

## 2. Global Installation
```bash
cargo install --path .
```

## 3. Configure as Git Merge Driver

### Step A: Update `.gitconfig`
Add the following to your global or project-specific `.gitconfig`:

```gitconfig
[merge "merge-engine"]
    name = merge-engine structured merge driver
    driver = merge-engine %O %A %B %P
```

### Step B: Update `.gitattributes`
Tell Git which files should use the engine. Create or update `.gitattributes` in your repository:

```gitattributes
*.rs merge=merge-engine
*.ts merge=merge-engine
*.js merge=merge-engine
*.py merge=merge-engine
*.go merge=merge-engine
*.java merge=merge-engine
*.kt merge=merge-engine
*.c merge=merge-engine
*.cpp merge=merge-engine
*.toml merge=merge-engine
*.yaml merge=merge-engine
```

## 4. Verification
To verify the installation, you can run a dry-run on a known conflict scenario:

```bash
merge-engine base.rs left.rs right.rs path.rs
```

If it prints the merged content or conflict markers without crashing, the installation is successful.
