## Watch and preview Markdown with PlantUML

This repository provides some scripts to run an inotify-based script to watch a directory containing markdown `.md` files and convert the saved (`WRITE_CLOSE` event) ones into the /tmp/out.html file.
Then, `watch-markdown` reload the current tab in [qutebrowser](https://qutebrowser.org).
With this script you can continue using your favourite text-editor (e.g., vim) having a nice live-preview of your markdown files with support for PlantUML (within the markdown), syntax highlighting for code blocks and others of the most used features of (Github/Gitlab) Markdown.

## Usage

```bash
cd /into/your/markdown/repository
watch-markdown
```

Then, use vim or another editor to modify your markdown files. Whenever you save one of them, it will be rendered in the `qutebrowser` window

## Installation

**Depencencies**:

- plantuml.jar (only for the non-dockerized configuration)
- Docker (only for  the dockerized configuration)
- qutebrowser (you can change to another browser editing he watch-markdown script)
- Python3

**Python modules dependencies**:

- Python-Markdown (markdown2html converter)
- pygments (syntax highlighting)
- markdown-checklist (allows conversion of checklists into html checkboxes)

No script is still available for installation. However the script(s) are really simple to install in your PATH and you can adjust them for your needs.

These are simple "bash" steps for an installation, assuming `/opt/bin` is in your PATH.

```bash
sudo apt install qutebrowser
pip3 install git+https://github.com/Python-Markdown/markdown.git
pip3 install plantuml-markdown pygments markdown-checklist
mkdir -p ~/.watch-markdown
cd /into/this/repository
cp plantuml /opt/bin/
cp watch-markdown /opt/bin
cp config.yml ~/.watch-markdown/config.yml
cp md.css ~/.watch-markdown/
```

**Adjust the variable `$CONF_DIR` into the script `watch-markdown` if needed.**

### Local plantuml.jar instance

Adjust the path to your plantuml.jar in the `plantuml` script.

**Adjust config.yml to not use a remote instance of plantuml (you can just delete -c "path/to/config.yml" from `watch-markdown`**

### Dockerized plantuml server

You can also use a dockerized plantuml server to avoid time wasting due to the plantuml.jar startup time.

Let's only execute on the directory of this repository:

```bash
docker-compose up
# OR
docker-compose start plantuml
# OR
docker run -p 4444:8080 plantuml/plantuml-server:jetty
```

It will expose on http://localhost:4444 a local plantuml server

The `config.yml` file and `watch-markdown` itself are configured to work in this scenario.

If you want, you can put the `docker run` command above into the watch-markdown script.

## Acknowledgements

- [Python-Markdown](https://github.com/Python-Markdown/markdown.git)
- [PlantUML Markdown](https://github.com/mikitex70/plantuml-markdown)
- [Markdown Checklist](https://github.com/FND/markdown-checklist)
- [qutebrowser](https://qutebrowser.org)
- [markdown-css-themes](https://github.com/ryusas/markdown-css-themes.git)

