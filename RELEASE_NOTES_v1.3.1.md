# Release v1.3.1 - Upstream Merge & Bug Fixes

## 🔄 What's New

This patch release merges the latest improvements from the upstream [attoae/quill-table-better](https://github.com/attoae/quill-table-better) repository, bringing important bug fixes and enhancements while maintaining all the instance management improvements from our fork.

## 🐛 Bug Fixes

- **Fixed error when deleting all rows via keyboard shortcut** (#134)
  - Resolved crashes when using `Ctrl+X` or `Ctrl+Shift+X` to delete entire table rows
  - Improved keyboard interaction stability

- **Fixed menu/property dialog positioning**
  - Table context menus and property dialogs now position correctly in all screen configurations
  - Enhanced positioning logic for better reliability across different viewport sizes

- **Added null cell check to exitTableFocus**
  - Prevents runtime errors when exiting table focus with invalid cell references
  - Improved robustness of table navigation

- **Fixed configuration loss issues**
  - Resolved problems with `/src/config` lose scenarios
  - Better configuration persistence and reliability

## ✨ Improvements

- **Enhanced SVG icons with currentColor support**
  - Icons now properly inherit text color for better theme compatibility
  - Improved visual consistency across different UI themes

- **Optimized package assets**
  - Removed unused `save.svg` icon to reduce package size
  - Streamlined asset management for better performance

- **Enhanced dialog positioning algorithms**
  - Improved popup positioning calculations
  - Better handling of edge cases in menu placement

## 🔧 Technical Details

- Updated cell selection logic with enhanced null safety
- Improved table menu positioning algorithms  
- Enhanced icon color inheritance system
- Streamlined asset management and optimization

## 📦 Package Information

- **Package Size**: 144.2 kB (597.4 kB unpacked)
- **Total Files**: 96 files included
- **NPM Package**: `@iwanmastah/quill-table-better@1.3.1`

## 🔗 Installation

```bash
npm install @iwanmastah/quill-table-better@latest
```

Or update existing installation:

```bash
npm update @iwanmastah/quill-table-better
```

## 🔄 Backward Compatibility

✅ **Fully backward compatible** - No breaking changes  
✅ **Existing API unchanged** - All current integrations continue to work  
✅ **Instance management improvements preserved** - All fork-specific enhancements maintained

## 🙏 Credits

- Upstream fixes by [attoae](https://github.com/attoae), [MrGong](https://github.com/MrGong), [mudoo](https://github.com/mudoo), and other contributors
- Fork maintenance and instance management improvements by [iwanmastah](https://github.com/iwanmastah)
- Original package by [attoae](https://github.com/attoae/quill-table-better)

---

**Full Changelog**: https://github.com/iwanmastah/quill-table-better/compare/v1.3.0...v1.3.1