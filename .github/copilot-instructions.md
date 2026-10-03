# Copilot instructions

Apply these writing rules to all content in this repository:

- Use Markdown only. Represent diagrams with fenced Mermaid code blocks. Store image files in `assets/images/` and reference them with relative paths.
- Tag every code fence with its language. Ensure code is correct and idiomatic for that language.
- Every algorithm and data structure note must state both time and space complexity. Include best, average, and worst cases when they differ.
- Keep notes short and scannable; prefer bullets, tables, and examples over long paragraphs.
- Use relative links between related notes.
- Use lowercase kebab-case for filenames, such as `binary-search.md`.
- Never invent facts. If something is uncertain, add `> TODO: verify` rather than guessing.
- Start every note with YAML front matter containing `title`, `tags`, `difficulty`, `status`, and `last_reviewed`.
- Each note: definition, how it works, working code example, complexity/trade-offs, common mistakes, and at least 5 interview questions with model answers.
- Code must be correct and runnable: TypeScript for frontend/DSA, Java for backend/DSA, Python only where the topic is Python-specific.
- Use current versions and patterns (React 19, Next.js App Router, Java 17+, Spring Boot 3); flag anything version-sensitive.
- File names lowercase-kebab-case; relative links between related notes; short, scannable notes.
- Resume notes: use ONLY facts from my resume. Where a metric's measurement method is unknown, leave "How I measured this: (fill in)" instead of making one up. Do not fill these in yourself.
