# Hi there, I'm Preet 👋


<!-- AUTO_GENERATED_SECTION_END -->


---


## ⏱️ WakaTime Summary (optional)


![WakaTime](https://wakatime.com/share/@USERNAME/your-wakatime-embed.svg)


---


## 🧾 Visitor Count


[![Visitor Count](https://visitcount.itsvg.in/api?id=USERNAME&icon=0&color=0)](https://visitcount.itsvg.in)


---


## ✍️ Quote of the day


![Quote](https://quotes-github-readme.vercel.app/api?type=horizontal&theme=radical)


---


## ⚙️ How automation works (overview)


- Many of the *cards* are images served by external dynamic endpoints (e.g., `github-readme-stats` & `streak-stats`) — they update automatically. Some services cache; using the provided GitHub Action below helps force-refresh or regenerate a static README block.
- The included Node script shows how to fetch recent commit messages and pinned repos using GitHub API, then inject those entries between the `AUTO_GENERATED_SECTION_START` and `AUTO_GENERATED_SECTION_END` markers.


---


## 🔐 GitHub Action: auto-update README


Create `.github/workflows/update-readme.yml` in your profile repo with:


```yaml
name: Update README
on:
schedule:
- cron: '0 0 * * *' # daily
push:
branches: [ main, master ]
workflow_dispatch: {}


jobs:
update-readme:
runs-on: ubuntu-latest
permissions:
contents: write
steps:
- uses: actions/checkout@v4
- name: Set up Node
uses: actions/setup-node@v4
with:
node-version: 20
- name: Install dependencies
run: |
npm ci || true
- name: Run update script
env:
GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
WAKATIME_API_KEY: ${{ secrets.WAKATIME_API_KEY }}
run: |
# If using the provided Node script it will update README.md in place
node .github/scripts/update-readme.mjs || true
- name: Commit updated README
run: |
git config --local user.email "action@github.com"
git config --local user.name "GitHub Action"
git add README.md || true
git commit -m "chore: update README [skip ci]" || echo "no changes"
git push || true
