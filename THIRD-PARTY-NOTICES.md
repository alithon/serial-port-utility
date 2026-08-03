# Third-party notices

Serial Port Utility is built on open-source components. Their copyright holders and license
terms are listed below; these terms apply to those components, not to Serial Port Utility
itself (see [LICENSE.md](LICENSE.md)).

## Qt 6

Copyright © The Qt Company Ltd. and other contributors.

Serial Port Utility uses the Qt 6 framework — Qt Core, Qt GUI, Qt Widgets, Qt Network,
Qt Serial Port and Qt 5 Compatibility Module — under the **GNU Lesser General Public License
version 3 (LGPLv3)**.

- Qt homepage: <https://www.qt.io/>
- Qt source code: <https://download.qt.io/archive/qt/>
- LGPLv3: <https://www.gnu.org/licenses/lgpl-3.0.html>
- GPLv3 (which LGPLv3 incorporates by reference): <https://www.gnu.org/licenses/gpl-3.0.html>

The Qt libraries are shipped as separate dynamic libraries (`.dll` on Windows, `.framework`
inside the application bundle on macOS) and are loaded at run time, so they can be replaced
with a compatible build of the same Qt version. Users exercising that right can rebuild or
substitute the Qt libraries in the installation directory. On Linux the published archive
links against the Qt packages installed on your own system.

If you need the exact Qt version and configuration used for a given release, or a copy of the
corresponding Qt sources, write to <bill@alithon.com> and name the release.

## Icons and fonts

Application and toolbar artwork is © 2026 Alithon Studio. Where third-party icon sets are
used, their licenses permit redistribution within an application.

---

Corrections and omissions: <bill@alithon.com>.
