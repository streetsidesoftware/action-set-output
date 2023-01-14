# streetsidesoftware/action-set-output

A GitHub Action to set the output value to any text value.

Writing script commands to set the output of a step can be painful.
This composite action makes that simple.

## Usage

```yaml
steps:
  - id: markdown
    uses: streetsidesoftware/action-set-output@v1
    with:
      value: |
        # Heading

        We want to use some markdown in our text.
  - name: Show Markdown
    env:
      MARKDOWN: ${{ steps.markdown.outputs.value }}
    run: |
      echo "$MARKDOWN" >> $GITHUB_STEP_SUMMARY
```

## Inputs

```yaml
inputs:
  value:
    description: The value to return.
    required: true
  debug:
    description: Show the value in the console.
    required: false
```

## The Action

The entire action is reproduced here to show how simple it is:

```yaml
name: set-output
description: |
  Set the output for this step to any text value.
author: "Street Side Software <info@streetsidesoftware.nl>"
inputs:
  value:
    description: The value to return.
    required: true
  debug:
    description: Show the value in the console.
    required: false
outputs:
  value:
    description: The value that was input.
    value: ${{ inputs.value }}
runs:
  using: "composite"
  steps:
    - name: Debug
      if: inputs.debug
      shell: bash
      env:
        VALUE: ${{ inputs.value }}
      run: |
        echo "$VALUE"
```
