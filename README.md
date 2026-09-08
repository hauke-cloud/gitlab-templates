<!-- llm-readme-management spec=1 commit=65ee1ebdd69ddbe1bcb9ba4630209aef4248b69b template=default model=qwen3.6-35b-a3b digest=598d66067ca0 generated=2026-09-08T19:40:40Z -->
<a href="https://hauke.cloud" target="_blank"><img src="https://img.shields.io/badge/home-hauke.cloud-brightgreen" alt="hauke.cloud" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud" target="_blank"><img src="https://img.shields.io/badge/github-hauke.cloud-blue" alt="hauke.cloud Github Organisation" style="display: block;" /></a>
<a href="https://github.com/hauke-cloud/llm-readme-management" target="_blank"><img src="https://img.shields.io/badge/template-default-orange" alt="Repository type - default" style="display: block;" /></a>


# Gitlab Templates


<img src="https://raw.githubusercontent.com/hauke-cloud/.github/main/resources/img/organisation-logo-small.png" alt="hauke.cloud logo" width="109" height="123" align="right">


<llm header>

This repository provides reusable YAML GitLab CI templates that reduce boilerplate in `.gitlab-ci.yml` files across hauke.cloud projects. You can include these definitions directly into your pipelines to standardise jobs like TFLint validation. It is designed for developers and operators managing CI/CD workflows within the organisation.

</llm>


## :book: Description

<llm description>

This repository provides reusable GitLab CI job templates that reduce boilerplate when writing `.gitlab-ci.yml` files across the hauke.cloud organisation. Instead of duplicating pipeline logic in every project, you include these templates directly via GitLab’s `include:` directive. The templates are designed for developers and operators managing Terraform or OpenTofu codebases, offering a consistent way to run linting checks without maintaining separate job definitions.

Within the hauke-cloud ecosystem, these templates serve as a shared foundation for CI configuration. You consume them by referencing their paths in your own pipeline files, and they support parameterisation through a custom `$[[ inputs.* ]]` interpolation syntax so you can adjust job names, stages, and failure policies without modifying the underlying logic.

- Defines a TFLint job that runs on merge request events and branch pipelines
- Uses the official `ghcr.io/terraform-linters/tflint` container image with configurable entrypoints
- Allows customisation of job names, CI stages, and `allow_failure` flags via template inputs

</llm>


## 🚀 Getting started

<llm getting_started hint="Assume nothing about the ecosystem beyond what the analysis names. If the repository has no build step, say what a reader does with it instead.">

1. Clone the repository and navigate into it.
```bash
git clone https://github.com/hauke-cloud/gitlab-templates.git
cd gitlab-templates
```

2. Reference the template in your project's `.gitlab-ci.yml` using GitLab's `include:` directive.
```yaml
include:
  - local: 'tofu/lint.yaml'
```

3. Pass parameters to customise the job name, stage, or failure behaviour.
```yaml
include:
  - local: 'tofu/lint.yaml'
    inputs:
      as: my-tflint-job
      stage: lint
      allow_failure: false
```

</llm>


## :airplane: Usage

<llm usage>

- **Include the template in your pipeline configuration.** You consume this repository by adding `include:` directives to your project's `.gitlab-ci.yml` file. The templates execute inside your existing GitLab CI/CD pipelines without requiring additional runner configuration or custom tooling on your side.

  ```yaml
  include:
    - project: 'hauke-cloud/gitlab-templates'
      ref: main
      file: 'tofu/lint.yaml'
      inputs:
        as: 'tofulint'
        stage: 'lint'
        allow_failure: false
  ```

- **Customise job behaviour.** The template accepts three input variables: `as`, `stage`, and `allow_failure`. You can override the defaults to match your pipeline structure or failure policies. The template resolves these values internally using its interpolation syntax, so you do not need to modify the underlying job definition or add extra scripts.

- **Run local pre-commit checks.** For validation before pushing, you can install the hooks defined in `.pre-commit-config.yaml`. The configuration uses `pre-commit-hooks` v4.4.0 and `gitleaks` v8.18.0 to enforce formatting, detect secrets, and check for large files or merge conflicts. Execute the pre-commit framework against your codebase to trigger these checks locally.

</llm>


## 📄 License

This Project is licensed under the GNU General Public License v3.0

- see the [LICENSE](LICENSE) file for details.


## :coffee: Contributing

To become a contributor, please check out the [CONTRIBUTING](CONTRIBUTING.md) file.


## :email: Contact

For any inquiries or support requests, please open an issue in this
repository or contact us at [contact@hauke.cloud](mailto:contact@hauke.cloud).
