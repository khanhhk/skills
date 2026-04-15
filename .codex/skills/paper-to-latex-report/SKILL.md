---
name: paper-to-latex-report
description: Read a research paper and convert it into a professional Vietnamese multi-file LaTeX report with dynamic section and BibTeX generation.
---

# Purpose

This skill reads a research paper and converts it into a multi-file Vietnamese LaTeX report.

The initial template contains only:

templates/
└── main.tex

The agent must not assume that `templates/sections/` or `templates/refs.bib` already exist.
Both must be created dynamically during execution.

---

# Required Workflow

When given a paper, the agent must follow this workflow:

1. Read the full paper carefully to understand its logical structure and technical content.
2. Identify the major elements of the paper:
   - title
   - abstract
   - sections
   - subsections
   - subsubsections when present
   - mathematical formulas that should be preserved
   - references
3. Translate the scientific content into formal, neutral Vietnamese academic writing.
4. Ignore figures, illustrations, example code blocks, and algorithm demonstration code from the source paper.
5. Create `templates/sections/` if it does not exist.
6. Split the translated content into as many `.tex` files as needed inside `templates/sections/`.
7. Create `templates/refs.bib` and fill it with the required BibTeX entries.
8. Update `templates/main.tex` by appending `\input{sections/...}` lines in the correct reading order.
9. Append the bibliography block at the end of `main.tex` so the document loads references from `refs.bib`.

Standard bibliography block:

```latex
\bibliographystyle{plain}
\bibliography{refs}
```

---

# File Generation Policy

- Do not assume a fixed number of section files.
- The agent must determine the number of files from the structure of the paper.
- Filenames inside `templates/sections/` must be deterministic, easy to order, and easy to understand.
- Every generated content file inside `templates/sections/` must be referenced from `main.tex` using `\input{sections/...}`.
- If the paper has a reference list, the agent must create `templates/refs.bib`.

---

# Mandatory LaTeX Rules

## 1) Heading Order

The heading hierarchy must always follow this order:

- `\section{}`
- `\subsection{}`
- `\subsubsection{}`

Do not skip hierarchy levels when the source paper clearly uses them.

## 2) No Paragraph Indentation

Every normal paragraph must begin with:

```latex
\noindent
```

This rule exists to prevent default paragraph indentation throughout the translated report.

## 3) Line Breaks

When a line break is required in the content, use:

```latex
\\
```

Do not leave this behavior implicit and do not invent another line-break convention.

## 4) Ignore Images and Demonstration Code

Do not process:

- figures
- illustrations
- algorithm demonstration code
- example source code blocks

Only keep the academic content needed for the translated report.

## 5) Mathematical Equations

Mathematical equations that need to be preserved must use:

```latex
\begin{equation}
...
\end{equation}
```

Do not assign equation numbers manually.
Equation numbering must remain automatic.

If an equation needs to be referenced later, add labels in the form:

```latex
\label{eq:1}
\label{eq:2}
```

When referring to those equations, use:

```latex
\ref{eq:1}
\ref{eq:2}
```

Do not hardcode equation numbers directly in prose.

## 6) No Manual Bold or Italic Styling

Do not add manual emphasis commands such as:

- `\textbf{}`
- `\textit{}`
- `\emph{}`

Keep the text visually normal unless the source paper has a technical reason that cannot be omitted.

---

# Output Quality Requirements

- The translation must remain faithful to the original technical meaning.
- The writing style must be academic, concise, and neutral.
- Do not add claims, explanations, or interpretations that are not supported by the source paper.
- If a formula is important to the paper's reasoning, preserve it instead of paraphrasing it away.
- The final output structure must be consistent and ready for further LaTeX compilation work.
