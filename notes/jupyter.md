# Converting notebook into pdf, markdown, etc.

Simple nbconvert command lets you to convert jupyter notebooks into report-like readable formats, e.g., pdf. --no-input removes the codes, making the output file reader friendly.
```bash
jupyter nbconvert compare_bootstrap.ipynb --to pdf --no-input --no-prompt
```

# Install packages in jupyter

'''bash
!{sys.executable} -m pip install pandas
'''
