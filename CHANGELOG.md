# Changelog

All notable changes to this project will be documented in this file.

## [1.3.1] - 2025-09-26

### 🔄 Upstream Merge
- Merged latest changes from [attoae/quill-table-better](https://github.com/attoae/quill-table-better) upstream repository

### 🐛 Bug Fixes (from upstream)
- **Fixed error when deleting all rows via keyboard shortcut** (#134) - Resolved crashes when using Ctrl+X/Ctrl+Shift+X to delete entire rows
- **Fixed menu/property dialog positioning** - Table menus and property dialogs now position correctly in all screen configurations
- **Added null cell check to exitTableFocus** - Prevents errors when exiting table focus with invalid cell references
- **Fixed /src/config lose** - Resolved configuration loss issues

### ✨ Improvements (from upstream)
- **Refactored SVG icons to use currentColor** - Icons now properly inherit text color for better theming support
- **Removed unused save.svg icon** - Cleaned up unused assets to reduce package size
- **Enhanced dialog positioning logic** - Improved reliability of popup positioning calculations

### 🔧 Technical Details
- Updated cell selection logic with better null safety
- Improved table menu positioning algorithms
- Enhanced icon color inheritance for better theme compatibility
- Streamlined asset management

### 📈 Package Info
- **Size**: 144.2 kB (597.4 kB unpacked)
- **Files**: 96 files included
- **Compatibility**: Maintains full backward compatibility

## [1.3.0] - 2025-09-09 (Fork Release)

### 🚀 Fork Improvements
- **Instance-specific event management**: Implemented CellSelectionRegistry to only attach global event listeners when table-better instances exist
- **Automatic format registration**: Formats now register automatically when first table-better instance is created (lazy loading)
- **Toolbar compatibility fixes**: Fixed destructuring errors when using toolbar features in non-table Quill instances
- **Memory leak prevention**: Proper cleanup of global event listeners when instances are destroyed
- **Multiple instance support**: Applications can now safely mix Quill instances with and without table-better

### 🔧 Technical Changes
- Added `CellSelectionRegistry` class for managing global event listeners
- Updated `TableToolbar` to handle missing table-better module gracefully
- Implemented lazy format registration in `Table.ensureFormatsRegistered()`
- Added proper null checks in all toolbar event handlers
- Enhanced cleanup mechanisms in `Table.destroy()` and `CellSelection.cleanup()`

### 💔 Breaking Changes
None - This fork maintains full backward compatibility with the original package.

### 🙏 Credits
This is a fork of [attoae/quill-table-better](https://github.com/attoae/quill-table-better) v1.2.3.
Original work by [attoae](https://github.com/attoae).

---

## Original Package History
For the complete changelog of the original package (versions 1.0.0 - 1.2.3), please refer to:
https://github.com/attoae/quill-table-better/releases
