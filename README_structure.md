# TRB Paper Structure

This document is organized into separate folders for better management and collaboration.

## Folder Structure

```
paper/
├── trb_template.tex          # Main document file
├── trb_template.bib          # Bibliography file
├── trbunofficial.cls         # TRB document class
├── trb.bst                   # TRB bibliography style
├── build/                    # Build output directory
├── sections/                 # All section folders
│   ├── abstract/
│   │   ├── abstract.tex     # Abstract section
│   │   └── figures/         # Figures for abstract
│   ├── introduction/
│   │   ├── introduction.tex # Introduction section
│   │   └── figures/         # Figures for introduction
│   ├── features/
│   │   ├── features.tex     # Features section
│   │   └── figures/         # Figures for features
│   ├── captions/
│   │   ├── captions.tex     # Captions section
│   │   └── figures/         # Figures for captions
│   ├── bibliography/
│   │   ├── bibliography.tex # Bibliography section
│   │   └── figures/         # Figures for bibliography
│   ├── equations/
│   │   ├── equations.tex    # Equations section
│   │   └── figures/         # Figures for equations
│   ├── conclusion/
│   │   ├── conclusion.tex   # Conclusion section
│   │   └── figures/         # Figures for conclusion
│   └── acknowledgements/
│       ├── acknowledgements.tex # Acknowledgements section
│       └── figures/         # Figures for acknowledgements
└── README_structure.md       # This documentation file
```

## How to Use

### Adding Content
1. Edit the appropriate `.tex` file in each section folder under `sections/`
2. Add figures to the `figures/` subfolder in each section
3. Reference figures using relative paths: `\includegraphics{figures/filename}`

### Adding New Sections
1. Create a new folder with the section name under `sections/`
2. Create a `figures/` subfolder
3. Create a `.tex` file with the section content
4. Add `\input{sections/sectionname/sectionname}` to the main document

### Compilation
The main document `trb_template.tex` automatically includes all sections using `\input` commands. Compile the main document as usual.

### Benefits
- **Better organization**: Each section is in its own folder under a central `sections/` directory
- **Easier collaboration**: Multiple authors can work on different sections
- **Figure management**: Figures are organized with their related content
- **Maintainability**: Easier to find and edit specific sections
- **Version control**: Better git history for individual sections
- **Clean root directory**: Main document and configuration files are separate from content

## Notes
- All sections are included in the main document using `\input{sections/section/file}`
- The bibliography and document class remain in the root directory
- Build output goes to the `build/` directory
- Each section can have its own figures in the `figures/` subfolder
- The `sections/` folder keeps all content organized and separate from configuration files 