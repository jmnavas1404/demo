# JupyterLite site for Session 4

Static website that runs the Session 4 notebooks completely in the browser
(Python via Pyodide, no install, no login). Contents of `content/` are bundled:

- `S4_notebook.ipynb` – workshop notebook (5 cells)
- `session_4_advanced_v2.ipynb` – advanced notebook (student version, no solutions)
- `reference_data.csv` – reference recording (currently SYNTHETIC, see below)

## Publish on GitHub Pages (about 10 min, once)

1. Create a repository (e.g. `s4-notebook`). Move `github_workflow_deploy.yml` to
   `.github/workflows/deploy.yml` (a `.github` folder could not be written into the synced
   folder from here), then push everything to the `main` branch.
2. Repository → Settings → Pages → Source: **GitHub Actions**.
3. The workflow builds the site (`jupyter lite build --contents content --output-dir dist`)
   and deploys it. Takes 2–3 min; the URL is shown in the Actions run.

## Build locally / host on the institute web server

```bash
python -m pip install -r requirements.txt
jupyter lite build --contents content --output-dir dist
python -m http.server -d dist 8000        # test: http://localhost:8000/lab/index.html
```

Copy the `dist/` folder to any static web server (no server-side code needed).

## Direct link for the students

```
https://<host>/<path>/lab/index.html?path=S4_notebook.ipynb
```

`?path=` opens the notebook directly (tested on jupyterlite.github.io/demo, 23.11.2026).
Put this link into `LINK` in `make_pdfs.py` (or write it on the board) and rebuild the PDFs.

## Updating content

Replace a file in `content/` and push (or rebuild). Note: students who already opened the
site keep their own browser copy of a notebook they edited; new files appear automatically.

## Reference CSV

`reference_data.csv` is a synthetic placeholder in the exact Capture2Go export format
(`time_s, signal_1 … signal_6`, comma separator, dot decimal, 4 decimals, 200 Hz;
signal_1–3 = accelerometer m/s², signal_4–6 = gyroscope °/s), made with
`make_reference_csv.py`. Replace it with Timo's real recording under the same name.
