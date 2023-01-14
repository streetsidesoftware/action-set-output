# streetsidesoftware/action-set-output

A GitHub Action to set the output value to any text value.

Writing script command to set the output of a step can be painful.
This action makes that simple.

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
          echo "$MARKDOWN"
```
