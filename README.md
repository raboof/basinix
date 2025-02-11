## WARNING: This is very much in alpha, do not expect this to be working or polished

# Basinix

This is meant to be a pull request reviewing tool for nixpkgs.

This is intended to be an intersection of [nixpkgs-review](https://github.com/Mic92/nixpkgs-review), [ofborg](https://github.com/NixOS/ofborg) and [hydra](https://github.com/NixOS/hydra). In which each PR will be a jobset, all changed packages will be built and cached. Then when failures or regressions occur, there's enough data to pinpoint when the failures occured and with what commit. Also, failures will only be attempted to be built once.

This is also meant to be exposed as a website similar to Hydra. However, there will be more emphasis as on this being used as a tool, and will allow for users to view information. Users will also be able to login with thier github credentials, and perform PR actions.

# Roadmap (Initial NixOS/nixpkgs support)

- [ ] Server
  - [x] Ability to pull Github events
    - [x] Initial polling of api events
    - [x] Filter events relevant to needing a rebuild
    - [x] Deconflict with previous events
  - [ ] Building derivations
    - [ ] Initial Evaluation support
      - [ ] Verify PR didn't break nixpkgs evaluation
        - [ ] support `allowAliases = false;` scenario
      - [ ] Determine new or changed attrs
    - [ ] Deconflict with previous builds (successful or unsuccessful)
    - [ ] Create priority queue of nix builds needed to be complete
      - Probably optimize for lowest rebuild number (increase # of PRs able to be reviewed)
    - [ ] Accurately adjust (remove no-longer relevant, add new builds) to PRs getting push events
    - [ ] Detect "tests", and build those as well
    - [ ] Nix garbage collection policies
      - [ ] Retain "fixed-output-derivations" on a branch
      - [ ] Retain all derivations on a branch
      - [ ] "Archive", or keep everything
- [ ] Web UI
  - [ ] Initial layout
  - [ ] Be able to view PR status
    - [ ] New / changed / removed packages
    - [ ] Build status of affected packages
    - [ ] (Optional) Linting gates?
  - [ ] Github Integration
    - [ ] Oauth support
    - [ ] PR actions
      - [ ] View PR diff (for easy checking)
      - [ ] Merge
        - [ ] without comment
        - [ ] with comment
          - [ ] Enumerate newly failing, newly succeeding, still failing, still suceeding, removed packages
          - [ ] Addtional checks (tests, etc)
      - [ ] Review Comment (see above)
- [ ] Packaging
  - [ ] Expose nix modules

