---
tags:
  - notes
---
[[Client.yml dependencies]]
[[server.yml dependencies]]

```
ARTCMDSYS-2721
```

```
ARTCMDSYS-2721.ConanTemplate/[^2.0.0]
```

```python
innerPath = name
    includeSubdirectory = name
```

```python
python_requires = "ConanTemplate/[^2.0.0]"
    python_requires_extend = "ConanTemplate.Library"
```

```cmake
set(LIBS_LIST ${CONAN_LIBS} ${CONAN_LIBS_RELEASE})
```

```cmake
set(CONAN_DISABLE_CHECK_COMPILER on)
```

```
ARTCMDSYS-2721.Up version for requirements rebuild
```

```
ARTCMDSYS-2721.Up version for requirements rebuild
```