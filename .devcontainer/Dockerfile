FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:24-trixie

USER node

ENV PATH="/home/node/.elan/bin:/home/node/.local/bin:$PATH"

# Install Lean 4
RUN curl https://elan.lean-lang.org/elan-init.sh | sh -s -- -y --default-toolchain none
RUN elan default leanprover/lean4:v4.31.0
RUN lake --version
RUN lean --version
