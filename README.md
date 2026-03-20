# 🖋️ WP-Template

There were quite a few times this past month where I really wished I was better at this whole "organisation" thing. When I started this writing journey, I thought it would be simple—just sit down and let the world fall out onto the page. But man, in the stories I read, it all seemed so easy. The reality? It’s a bit more like trying to plumb a house while the water’s already running.

I’ve reached the point where the "bare bones" aren't enough anymore. I needed a way to restructure my existing projects and build a solid foundation for every new world to come. This template is my "wastewater engineering certificate" for fiction. It’s designed to keep my author-facing "sludge" separate from the pure, public-facing wiki and stories that end up on my website.

## 🏗️ The Pipeline (How it Works)

I’ve designed this to work with a custom "source-to-sink" pipeline that feeds my personal website’s headless CMS. 

### The Siphon (GitHub Actions)
Whenever I push an update via Obsidian or VS Code, a GitHub Action kicks in to scrub the files:
* **The Underscore Filter:** Any frontmatter field starting with an underscore (e.g., `_status`, `_todo`, `_priority`) is considered author-facing and is stripped before the file moves.
* **Private Files:** Any file with `_author_only: true` in its frontmatter is blocked from the push entirely.
* **The S-Bend (Author Notes):** The Action acts like a perfect siphon for prose; it cuts every markdown file at the `## Author Notes` heading, keeping my messy drafting notes far away from the public eye.

## 📂 Project Structure

The folder layout follows a strict "Wiki Structure Spec" to ensure the website knows exactly where to put everything:

* **`world-building/wiki/`**: The public-facing heart of the project. Categories like `characters/`, `magic/`, and `lore/` each have their own `_overview.md` and `_template.md`.
* **`stories/`**: Structured for story planning, chapter planning, and the final chapters.
* **`_dashboard.md`**: My author-facing command centre—using Dataview to track what’s a draft and what’s ready for the world to see.

## ⚙️ Setup & Secrets

To get the pipeline moving, you’ll need to set up a few bits in **GitHub Secrets**:
* `CMS_REPO_TOKEN`: A Personal Access Token with write access to your website's CMS repo.
* `CMS_REPO_URL`: The path to the repository where the public content is "sunk."

## 📜 The Golden Rules

1.  **Child → Parent (Mostly):** Generally, links flow "upwards"—a character points to their group, but the group doesn't list every member. It’s not an unbreakable law (sometimes the inverse is just more practical), but nine times out of ten, it keeps the metadata a hell of a lot cleaner.
2.  **File Naming:** All filenames must be lowercase and hyphenated (e.g., `kael-vashen.md`). No underscores, no spaces, no clutter.
3.  **Spoilers:** Every entry uses `first_revealed` to ensure a reader doesn't accidentally learn about a character's death before they've even met them.

It isn’t much, but it’s honest work. It’s the home my stories deserve.
