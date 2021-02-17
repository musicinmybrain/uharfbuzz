[![Githun CI Status](https://github.com/harfbuzz/uharfbuzz/workflows/Build%20+%20Deploy/badge.svg)](https://github.com/harfbuzz/uharfbuzz/actions?query=workflow%3A%22Build+%2B+Deploy%22)
[![Appveyor Build status](https://ci.appveyor.com/api/projects/status/k52t0vwqb9rhcl9v/branch/master?svg=true)](https://ci.appveyor.com/project/fonttools/uharfbuzz/branch/master)
[![PyPI](https://img.shields.io/pypi/v/uharfbuzz.svg)](https://pypi.org/project/uharfbuzz)

## uharfbuzz

Streamlined Cython bindings for the [HarfBuzz][hb] shaping engine.


### Example

```python
import sys

import uharfbuzz as hb


with open(sys.argv[1], 'rb') as fontfile:
    fontdata = fontfile.read()

text = sys.argv[2]

face = hb.Face(fontdata)
font = hb.Font(face)

buf = hb.Buffer()
buf.add_str(text)
buf.guess_segment_properties()

features = {"kern": True, "liga": True}
hb.shape(font, buf, features)

infos = buf.glyph_infos
positions = buf.glyph_positions

for info, pos in zip(infos, positions):
    gid = info.codepoint
    cluster = info.cluster
    x_advance = pos.x_advance
    x_offset = pos.x_offset
    y_offset = pos.y_offset
    print(f"gid{gid}={cluster}@{x_advance},{x_offset}+{y_offset}")
```


[hb]: https://github.com/harfbuzz/harfbuzz
