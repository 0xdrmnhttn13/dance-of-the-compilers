# Dance of the Compilers

> From algebra to silicon.

A public learning notebook about compilers, AI systems, quantum computing, mathematics, and low-level systems.

## Run locally

Install Hugo, then:

```bash
hugo server -D
```

Open `http://localhost:1313`.

## Publish with GitHub Pages

1. Create a GitHub repository named `dance-of-the-compilers`.
2. Replace `USERNAME` in `hugo.toml` with your GitHub username.
3. Push this repository to the `main` branch.
4. In GitHub: **Settings → Pages → Build and deployment → Source → GitHub Actions**.
5. The included workflow will build and deploy the site on every push to `main`.

If the repository itself is named `USERNAME.github.io`, change `baseURL` to `https://USERNAME.github.io/`.

## Write a post

Copy `content/posts/_template.md`, rename it, set `draft: false`, then write.

```bash
cp content/posts/_template.md content/posts/001-my-post.md
```

The point is to document understanding, including mistakes and unresolved questions, rather than pretending every note is a textbook chapter.
