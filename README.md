# everything is points

A node-based vector art tool. Wire shapes through transforms, scatters, masks, and modifiers.

Mac and Windows. Free. MIT licensed. Project files use the `.eip` extension.

[![watch this first — EIP The Basics](https://img.youtube.com/vi/y46z66O3Tf0/maxresdefault.jpg)](https://www.youtube.com/watch?v=y46z66O3Tf0&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)

> **Start here:** *EIP — The Basics* &nbsp;·&nbsp; click the image above

## Download

Grab the latest installer from the [Releases](https://github.com/alexanderbsolomon-alt/nodegarden/releases/latest) page:

- **Mac** (Apple Silicon + Intel) — `everything-is-points_*_universal.dmg`
- **Windows** — `everything-is-points_*_x64-setup.exe` (or the `.msi`)

The app is unsigned, so first launch needs a Gatekeeper / SmartScreen bypass:
- **Mac:** right-click the app → **Open** → **Open** in the dialog
- **Windows:** click **More info** → **Run anyway** on the SmartScreen popup

After that first bypass, it opens normally forever.

## Tutorials

Full playlist on YouTube: [EIP tutorials](https://www.youtube.com/playlist?list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)

| | |
|---|---|
| [![EIP — The Basics](https://img.youtube.com/vi/y46z66O3Tf0/0.jpg)](https://www.youtube.com/watch?v=y46z66O3Tf0&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**1. The Basics** | [![EIP 2 — combining shapes](https://img.youtube.com/vi/FhuP0iUKDkU/0.jpg)](https://www.youtube.com/watch?v=FhuP0iUKDkU&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**2. Combining shapes** |
| [![EIP 3 — let's make something](https://img.youtube.com/vi/mlcenlVMf2Q/0.jpg)](https://www.youtube.com/watch?v=mlcenlVMf2Q&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**3. Let's make something** | [![EIP 4 — Beyond the Basics](https://img.youtube.com/vi/yFs27gVHmgc/0.jpg)](https://www.youtube.com/watch?v=yFs27gVHmgc&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**4. Beyond the basics** |
| [![EIP 5 — repeat node and friends](https://img.youtube.com/vi/YabnnLgWrJo/0.jpg)](https://www.youtube.com/watch?v=YabnnLgWrJo&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**5. The repeat node and friends** | [![EIP 6 — the scatter node](https://img.youtube.com/vi/fxdaaXZImMI/0.jpg)](https://www.youtube.com/watch?v=fxdaaXZImMI&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**6. The scatter node** |
| [![EIP 7 — scatter grids](https://img.youtube.com/vi/YFlR-OchFI0/0.jpg)](https://www.youtube.com/watch?v=YFlR-OchFI0&list=PLrcll1JMwoxWxhkOGopgYmGt3np_hAydg)<br>**7. Scatter grids** | |

## Build from source

You'll need Rust (`rustup`), Node 20+, npm, and either Xcode Command Line Tools (Mac) or MSVC build tools (Windows).

```bash
git clone https://github.com/alexanderbsolomon-alt/nodegarden.git
cd nodegarden
npm install
npm run tauri dev          # hot-reload dev window
npm run tauri build        # produces .dmg / .msi / .exe in src-tauri/target/release/bundle/
```

For a Mac universal binary that runs on both Apple Silicon and Intel:

```bash
rustup target add x86_64-apple-darwin aarch64-apple-darwin
npm run tauri build -- --target universal-apple-darwin
```

## Architecture

A single-file `src/index.html` (~22k lines) with seven layers commented inline:

| Layer | What it does |
|---|---|
| L1 Geometry | point/primitive types, boolean ops, edge densification |
| L2 Engine | DAG graph, topological eval, attachments, history |
| L3 Node defs | every node type — shape, transform, scatter, recolor, etc. |
| L4 Renderer | geometry → SVG, bbox computation, swatch helpers |
| L5 Controls | schema-driven param UI |
| L6 Node View | node card rendering on the graph |
| L7 App | top-level state, event handlers, drag, selection |

The whole frontend is wrapped in [Tauri 2](https://tauri.app/) for native Mac and Windows installers. Project save/load goes through `tauri-plugin-dialog` and `tauri-plugin-fs`; the on-disk format is JSON with an `"eip"` header so older project files can be migrated forward in future versions.

## Contributing

Issues and pull requests welcome. The codebase is one big HTML file by design — pick the layer you want to touch using the table above as a guide.

## License

[MIT](LICENSE).
