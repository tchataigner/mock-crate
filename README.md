<h1 align="center">Welcome to mock crate</h1>

> This repository is meant to test out some Github actions flows that would be useful when developing a crate project.

### 🏠 [Homepage](https://holium.org/)

## Preparation work

_crates.io account_

In order to publish on [crates.io](https://crates.io/) we will need to create an account. The account is linked to a 
Github account. Also, an **email address needs to be verified**.

_Cargo metadata_

To be able to publish a crate with cargo we will need to have manifest metadata specified. Metadata list can be found 
[here](https://doc.rust-lang.org/cargo/reference/manifest.html). 

Required metadata are `name`, `description`, `version` & `license`.

Some important metadata are `readme`, `homepage` & `repository`. 

## Content

### Github actions

The project proposes 3 different flows. On commands that require to be ran in each individual crates (`cargo publish`...)
we install the cargo plugin [`cargo workspaces`](https://github.com/pksunkara/cargo-workspaces).

### Check, lint, unused deps & tests

Basic flow for generic checks.

_Events_

On Pull Request for the `develop` & `main` branches.

_Jobs_

- `cargo check`: Check that our crate compiles.
- `cargo fmt --all -- --check`: Checks that our crate follows basic Rust formatting.
- `cargo workspaces exec cargo +nightly udeps`: Makes sure that the branch does not have any unused dependencies.
- `cargo test`: Makes sure tests are passing.

### Publish, dry run

Flow that will do a dry run on every internal crates before publication, making sure the action will be possible.

_Events_

On Pull Request for the `main` branch.

_Job_

- `cargo workspaces exec cargo publish --dry-run`: Execute a dry run for publication on each crate in the repo, making sure 
that publication will be possible on merge.


### Publish

Flow that will publish all internal crates to [crates.io](https://crates.io/).

_Events_

On commit on the `main` branch.

_Job_

- `cargo workspaces exec cargo publish --token ***`: For every crate in our workspace, publish it on crates.io.


***
_This README was generated with ❤️ by [readme-md-generator](https://github.com/kefranabg/readme-md-generator)_