# Third-party notices

This file lists the third-party components used by **NO — NaanoOrder**,
their licences, sources, and distribution mode. It is factual information, not
legal advice.

## Definitions

- **Redistributed**: included in this repository or in an artifact you deliver
  (archive, image, binary).
- **Downloaded by the buyer**: fetched at runtime from the official source;
  absent from this repository and from delivered artifacts.
- **Not redistributed**: proprietary or service-bound; never delivered.

## Component notes

### `mt5server.exe`

- Verified provenance: the `server-1.1.1` release of the
  `lucas-campagna/mt5linux` repository does publish an `mt5server.exe` asset
  (built by GitHub Actions). Its SHA-256 is
  `eda5129716a28450e112856bac627d764198cadf5ca2243c108f6b5a4af60b19`, matching
  the value documented for `MT5SERVER_SHA256`.
- The binary is **not** shipped in this repository: the buyer downloads it via
  `MT5SERVER_URL` and verifies it with `MT5SERVER_SHA256`.
- If you redistribute it yourself (mirror, prebuilt image), you become a
  distributor of its contents. Audit the binary (`pyi-archive_viewer` if it is
  PyInstaller) and keep the notices for CPython, NumPy, OpenBLAS,
  `MetaTrader5`, `rpyc`, `plumbum`, and the MSVC runtime where applicable.
- The MIT licence of the `mt5linux` repository covers the project code; it does
  not replace the licences of the components bundled in the executable.

### Docker image

- The `gmag11/metatrader5_vnc:2.3` image is based on Debian and contains many
  packages, including GPL components. KasmVNC is GPL-2.0 and the LinuxServer
  base is GPL-3.0.
- If you publish a derived image, you must provide the sources for the exact
  versions of the GPL/LGPL components, or a written offer valid for three
  years.
- The recommended approach is not to distribute an image: ship the
  `Dockerfile`, the Compose file, and the code, and let the buyer build.

### MetaTrader 5 terminal and broker installer

- The terminal is proprietary (MetaQuotes EULA) and the installer belongs to
  the broker. They must never appear in an archive, an image, or a delivered
  volume.
- `start.sh` downloads them at runtime; keep that model.

### Wine Mono and Wine Gecko

- Wine Mono is not under a single licence: its `COPYING` file lists parts under
  LGPL, MIT, and zlib, with a few exceptions (SharpZipLib under GPL with an
  exception, the VB compiler under LGPL v2). See that file for the exact
  breakdown.
- Wine Gecko is distributed under MPL-2.0.
- Both are downloaded by Wine into the `/config` prefix on first start; they
  are not part of this repository.

### Python in the Wine prefix

If a Windows Python is installed in the prefix (some broker installers or
custom images do this), it is CPython under PSF-2.0. It is not provided by this
repository.

### Trademarks

"MetaTrader" and "MetaTrader 5" are trademarks of MetaQuotes Ltd. "FBS" is a
trademark of FBS Markets Inc. This project is not affiliated with either
company. Use descriptive wording such as "compatible with MetaTrader 5" and
avoid these marks in the name of a commercial product.

## Full texts of short licences

### MIT License

```text
MIT License

Copyright (c) <copyright holders>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

The copyright holders of each MIT component are listed in the corresponding
package's `LICENSE` file or metadata.

### BSD 2-Clause License

```text
Copyright (c) <copyright holders>
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

### BSD 3-Clause License

```text
Copyright (c) <copyright holders>
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this
   list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors
   may be used to endorse or promote products derived from this software
   without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

## Long licences: canonical texts

These texts are not duplicated here to avoid diverging from the official
versions. They are available at the canonical URLs below, and for Debian inside
the image at `/usr/share/common-licenses/`.

| Licence                                            | Official text                                           |
| -------------------------------------------------- | ------------------------------------------------------- |
| PSF-2.0 (Python)                                   | https://docs.python.org/3/license.html                  |
| MPL-2.0 (Wine Gecko)                               | https://www.mozilla.org/MPL/2.0/                        |
| LGPL-2.1-or-later (Wine)                           | https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html |
| GPL-2.0-or-later (KasmVNC, PyInstaller bootloader) | https://www.gnu.org/licenses/old-licenses/gpl-2.0.html  |
| GPL-3.0 (LinuxServer base)                         | https://www.gnu.org/licenses/gpl-3.0.html               |
| GCC Runtime Library Exception                      | https://www.gnu.org/licenses/gcc-exception-3.1.html     |
| Apache-2.0 (Playwright, archived code)             | https://www.apache.org/licenses/LICENSE-2.0             |
