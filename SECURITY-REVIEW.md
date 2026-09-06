# Security Review

## Scope

This review covers the complete tracked repository, including the Jupyter
notebook, generated PDF and PNG artifacts, `.gitignore`, repository
configuration, and reachable Git history. It focuses on credentials and
tokens, unsafe data handling, privacy exposure, notebook output leaks,
insecure downloads, dependency and configuration risks, and reproducibility
concerns.

## High-confidence finding

### Unpinned package installation in the public notebook

- **Severity:** High
- **Confidence:** 9/10
- **Location:** `stellar_classification.ipynb:525`
- **Finding:** The notebook executes `!pip install lightgbm -q` without an
  exact version, artifact hash, dependency lockfile, or explicitly trusted
  package source.
- **Impact:** Re-running the notebook may install a mutable or compromised
  package release and dependencies. Package code runs with the notebook
  kernel's access to local files, environment variables, and loaded data. The
  unpinned installation also prevents reliable reproduction.
- **Remediation:** Prefer a separately managed, pinned environment
  specification or lockfile covering every imported dependency. Pin exact
  versions and verify package hashes from a trusted HTTPS index. If the
  installation remains in the notebook, pin LightGBM and use hash-verified
  artifacts.

## Reviewed surfaces

- Notebook code, imports, shell commands, data-loading paths, model loading,
  and cell outputs.
- PDF text and metadata, PNG metadata, and exported artifacts.
- `.gitignore`, dependency declarations, installation commands, and download
  sources.
- Reachable Git history and prior tracked versions.

No high-confidence hardcoded API keys, passwords, authentication tokens,
private keys, or credential-like strings were found. Notebook outputs are
cleared, and no sensitive execution results, local paths, or secrets were
found in the notebook, PDF, or PNG metadata. No insecure HTTP downloads,
network fetches, unsafe deserialization, `eval`, `exec`, or model-loading
operations were identified. The dataset CSV is excluded by `.gitignore` and
is not tracked.

## Safe handling recommendations

1. Add a pinned dependency/environment file, including all notebook imports,
   and update it deliberately when dependencies change.
2. Keep datasets and derived artifacts containing personal or sensitive records
   outside version control; review notebook outputs before publishing.
3. Do not embed local filesystem paths, environment values, credentials, or
   raw records in notebooks or exported artifacts.
4. Re-run the notebook in a clean environment from the pinned specification
   and record the toolchain versions needed to reproduce the results.
