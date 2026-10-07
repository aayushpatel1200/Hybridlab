# Network Diagram: Open, Export, Commit

`diagram.drawio` is the editable source. `diagram.png` is the image that
GitHub shows. Edit the `.drawio`, then re-export the PNG so they stay in sync.

## Option A: Browser (nothing to install)

1. Go to <https://app.diagrams.net>.
2. If it asks where to save diagrams, pick **Device** (or **Decide later**).
3. Open the file: **File > Open from > Device...** and select `diagram.drawio`
   (or just drag the file onto the page).
4. Export: **File > Export as > PNG...**
5. In the export dialog set:
   - **Zoom:** `200%` (sharp on high-DPI screens; 100% also works)
   - **Border Width:** `10`
   - **Transparent Background:** unchecked (keeps the white background)
   - **Include a copy of my diagram:** unchecked (you commit the `.drawio` separately)
6. Click **Export**, name the file `diagram.png`, choose **Device / Download**.
7. Move `diagram.png` into the root of this repo, next to `diagram.drawio`.

## Option B: draw.io desktop app

1. Install from <https://www.drawio.com> (Windows, macOS, Linux).
2. **File > Open...** and select `diagram.drawio`.
3. **File > Export as > PNG...**, same settings as step 5 above.
4. Click **Export** and save as `diagram.png` in the repo root.

## Option C: Command line (desktop app installed)

Run from the repo root:

```bash
# Linux
drawio --export --format png --scale 2 --border 10 --output diagram.png diagram.drawio

# macOS
/Applications/draw.io.app/Contents/MacOS/draw.io --export --format png --scale 2 --border 10 --output diagram.png diagram.drawio
```

```powershell
# Windows (PowerShell)
& "C:\Program Files\draw.io\draw.io.exe" --export --format png --scale 2 --border 10 --output diagram.png diagram.drawio
```

Run `drawio --help` to confirm the flags on your installed version.

## Check before committing

- The PNG opens and every label is readable (FW01, 6 VLANs, BR-RTR01, AWS VPC).
- The background is white, not transparent or dark.
- Both files are in the repo root.

## Commit

```bash
git add diagram.drawio diagram.png diagram-export.md
git commit -m "Add hybrid-cloud network topology diagram"
git push
```

## Show it on the repo front page (optional)

Add this line to `README.md`:

```markdown
![Hybridlab network topology](diagram.png)
```

## What the diagram shows

| Element  | Details                                                        | Color  |
|----------|----------------------------------------------------------------|--------|
| FW01     | OPNsense; routes all VLANs; default-deny                       | Red    |
| Home LAN | 192.168.0.0/16 (Proxmox GUI, iDRAC); feeds FW01 WAN            | Blue   |
| BR-RTR01 | Branch 10.20.0.0/24; OSPF to FW01 over 10.255.0.0/30           | Blue   |
| AWS VPC  | 10.50.0.0/16 (CLOUD-RTR01, web tier); WireGuard + eBGP over 10.255.1.0/30, AS 65010 to 65050 | Yellow |
| MGMT, SERVERS, CLIENTS, DMZ | VLANs 10, 20, 30, 40                        | Green  |
| ATTACK, TARGETS | VLANs 99, 98; dashed line = only allowed path between them | Orange |

Host IPs, router IDs and ASNs come from `IP-Plan.md`. If that file
changes, update the diagram to match.
