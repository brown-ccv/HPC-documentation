# Python in batch jobs

By default, `print` in Python is buffered. When running Python in a batch job in SLURM you may see output less often than you would when running interactively. This is because the output is being buffered - the print statements are collected until there is a large amount to print, then the messages are all printed at once. For debugging or checking that a Python script is producing the correct output, you may want to switch off buffering.

## Switch off buffering

For a single python script you can use the `-u` option, e.g.

`python -u my_script.py`

The `-u` stands for "unbuffered". You can use the environment variable `PYTHONUNBUFFERED` to set unbuffered I/O for your whole batch script.

```text
#!/bin/bash
#SBATCH -n 1

export PYTHONUNBUFFERED=TRUE
python my_script.py
```

There is some performance penalty for having unbuffered print statements, so you may want to reduce the number of print statements, or run buffered for production runs.

