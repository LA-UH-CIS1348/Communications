# Important: File Paths in Your investigate.py Script

## The Problem

Your script (`investigate.py`) is located in the `assignment/exam/` folder, and the data files you need to access are in that same folder (they're siblings to your script). However, when you open the project in VS Code, it opens the parent `assignment/` folder as the workspace root. 

When you click the "Run" button (▷) in VS Code, it executes your script with the working directory set to `assignment/`, not `assignment/exam/`. This means when your script tries to open `somefile.txt`, Python looks for it in the `assignment/` folder and can't find it.

## Directory Structure

Here's what your folder structure looks like:

```
assignment/
├── exam/
│   ├── investigate.py          ← Your script
│   ├── data.txt               ← Files you need to read
│   ├── output.txt             ← Files you need to write
│   └── members/               ← Subfolder with more files
│       ├── member1.txt
│       └── member2.txt
└── other_files...
```

## Wrong Solutions

Many of you have tried to "fix" this in ways that are **not acceptable**:

### ❌ Adding 'exam/' prefix:
```python
open('exam/somefile.txt', 'r')
```

### ❌ Using absolute paths:
```python
open('C:/Users/YourName/Documents/assignment/exam/somefile.txt', 'r')
# or
open('/home/yourname/assignment/exam/somefile.txt', 'r')
```

**Why these are wrong:** While they may work on your specific computer, they will **fail during grading**. The grading system runs your script from the `exam/` folder, and these paths won't exist on the grading server.

## The Right Solution: Use Relative Paths

Your script should **always use relative paths** as if it's running from inside the `exam/` folder (because it should be!).

### ✅ For files in the same folder as investigate.py:
```python
# To read data.txt (sibling file)
with open('data.txt', 'r') as f:
    content = f.read()

# To write output.txt (sibling file)
with open('output.txt', 'w') as f:
    f.write('results')
```

### ✅ For files in subfolders (like members/):
```python
# To read from the members/ subfolder
with open('members/member1.txt', 'r') as f:
    content = f.read()
```

**Key point:** Notice there's **no `exam/` prefix** and **no absolute paths**. The paths are relative to where `investigate.py` is located.

## How to Run Your Script from the Correct Folder in VS Code

To make this work in VS Code, you need to run your script from the correct directory. Here are your options:

### Option 1: Use the Terminal (Recommended)
1. Open a terminal in VS Code (Terminal → New Terminal, or `` Ctrl+` ``)
2. Navigate to the exam folder:
   ```bash
   cd exam
   ```
3. Run your script:
   ```bash
   python investigate.py
   ```

### Option 2: Change VS Code Settings
You can configure VS Code to always run Python files from their containing directory:

1. Open VS Code Settings (File → Preferences → Settings, or `Ctrl+,`)
2. Search for: `python.terminal.executeInFileDir`
3. Check the box to enable it

Now when you click the Run button (▷), it will automatically run from the `exam/` folder.

Your script should assume it's being run from the `exam/` folder where it lives.

## Summary

- ✅ **DO**: Use relative paths like `'data.txt'` or `'members/member1.txt'`
- ❌ **DON'T**: Use `'exam/data.txt'` or absolute paths like `'C:/Users/.../exam/data.txt'`
- 🎯 **Remember**: Your script will be graded by running it from inside the `exam/` folder

Please review your code and remove any `exam/` prefixes or absolute paths before final submission.
