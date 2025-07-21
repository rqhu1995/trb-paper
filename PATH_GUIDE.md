# LaTeX Path Resolution Guide

## Understanding LaTeX Path Resolution

**Key Rule**: LaTeX resolves all paths **relative to the main document** (`trb_template.tex`), not relative to individual section files.

## Directory Structure
```
paper/                          # Root directory (where main document is)
├── trb_template.tex            # Main document (compilation starts here)
├── sections/
│   ├── introduction/
│   │   ├── introduction.tex    # Section file
│   │   └── figures/
│   │       ├── fig1.png        # Figure files
│   │       └── fig2.pdf
│   ├── abstract/
│   │   ├── abstract.tex
│   │   └── figures/
│   │       └── abstract-fig.png
│   └── conclusion/
│       ├── conclusion.tex
│       └── figures/
│           └── conclusion-fig.png
└── build/                      # Output directory (set in settings.json)
    └── trb_template.pdf        # Generated PDF
```

## Path Reference Examples

### ✅ CORRECT Paths (relative to main document)

#### From `sections/introduction/introduction.tex`:
```latex
% To reference figures in the same section:
\includegraphics{sections/introduction/figures/fig1}
\includegraphics{sections/introduction/figures/fig2}

% To reference figures from other sections:
\includegraphics{sections/abstract/figures/abstract-fig}
\includegraphics{sections/conclusion/figures/conclusion-fig}
```

#### From `sections/abstract/abstract.tex`:
```latex
% To reference figures in the same section:
\includegraphics{sections/abstract/figures/abstract-fig}

% To reference figures from other sections:
\includegraphics{sections/introduction/figures/fig1}
\includegraphics{sections/conclusion/figures/conclusion-fig}
```

### ❌ INCORRECT Paths (common mistakes)

```latex
% WRONG - relative to section file location:
\includegraphics{figures/fig1}           % ❌
\includegraphics{../figures/fig1}        % ❌
\includegraphics{./figures/fig1}         % ❌

% WRONG - absolute paths (not portable):
\includegraphics{/home/user/paper/sections/introduction/figures/fig1}  % ❌
```

## Why This Happens

1. **LaTeX Processing Order**: 
   - LaTeX starts with `trb_template.tex` (main document)
   - When it encounters `\input{sections/introduction/introduction.tex}`, it processes that file
   - But the **working directory** remains where `trb_template.tex` is located

2. **Build Directory**: 
   - Your `settings.json` sets `-output-directory=build`
   - This only affects where output files go, not how LaTeX resolves input paths
   - LaTeX still looks for input files relative to the main document

## Practical Examples

### Example 1: Figure in Introduction Section
**File**: `sections/introduction/introduction.tex`
**Figure**: `sections/introduction/figures/methodology.png`

```latex
\begin{figure}[!ht]
  \centering
  \includegraphics[width=0.8\textwidth]{sections/introduction/figures/methodology}
  \caption{Research methodology flowchart.}\label{fig:methodology}
\end{figure}
```

### Example 2: Cross-Reference Between Sections
**File**: `sections/conclusion/conclusion.tex`
**Figure**: `sections/introduction/figures/methodology.png`

```latex
As shown in Figure~\ref{fig:methodology}, our methodology follows a systematic approach.
```

### Example 3: Multiple Figures from Different Sections
**File**: `sections/abstract/abstract.tex`

```latex
\begin{figure}[!ht]
  \centering
  \includegraphics[width=0.6\textwidth]{sections/abstract/figures/overview}
  \caption{System overview.}\label{fig:overview}
\end{figure}

\begin{figure}[!ht]
  \centering
  \includegraphics[width=0.7\textwidth]{sections/introduction/figures/methodology}
  \caption{Detailed methodology.}\label{fig:methodology}
\end{figure}
```

## Tips and Best Practices

### 1. Use Consistent Naming
```latex
% Good - descriptive names
\includegraphics{sections/introduction/figures/methodology-flowchart}
\includegraphics{sections/results/figures/performance-comparison}

% Avoid - generic names
\includegraphics{sections/introduction/figures/fig1}
\includegraphics{sections/results/figures/image}
```

### 2. Use Relative Paths (Recommended)
```latex
% ✅ Good - portable and clear
\includegraphics{sections/introduction/figures/fig1}

% ❌ Avoid - not portable
\includegraphics{/absolute/path/to/fig1}
```

### 3. File Extensions
```latex
% ✅ Good - LaTeX will find the right format
\includegraphics{sections/introduction/figures/fig1}

% ✅ Also good - explicit extension
\includegraphics{sections/introduction/figures/fig1.png}
```

### 4. Organize by Section
Keep figures close to their related content:
- `sections/introduction/figures/` - for introduction figures
- `sections/methodology/figures/` - for methodology figures
- `sections/results/figures/` - for results figures

## Troubleshooting

### Common Error: "File not found"
If you get a "File not found" error:

1. **Check the path**: Make sure it's relative to `trb_template.tex`
2. **Check the file exists**: Verify the file is in the correct location
3. **Check file permissions**: Ensure LaTeX can read the file
4. **Check file format**: Ensure the image format is supported

### Debugging Paths
You can test if LaTeX can find your file by temporarily adding this to your main document:
```latex
\listfiles  % Add this to see what files LaTeX is looking for
```

## Summary

- **Always use paths relative to `trb_template.tex`**
- **Include the full path from the main document**: `sections/sectionname/figures/filename`
- **The build directory doesn't affect input path resolution**
- **Keep figures organized by section for better maintainability** 