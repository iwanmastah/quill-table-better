# Changelog

All notable changes to this project will be documented in this file.

## [1.4.0] - 2025-09-26

### 🎨 New Features
- **Default inline table styling** - Tables now include default border, padding, and layout styles in Delta and HTML output
- **Visual consistency** - Tables appear identical in editor and when exported/rendered outside editor
- **Enhanced copy/paste fidelity** - Table styling is preserved during copy/paste operations

### 🔧 Technical Improvements
- **Inline style integration** - Default styles are embedded directly in Quill's Delta format
- **Dynamic styling** - New rows and columns automatically inherit proper styling
- **Style utility functions** - Added `formatStyleString`, `parseStyleString`, and `mergeStyles` utilities
- **Enhanced table creation** - `insertTable()` now applies comprehensive default styling

### 📋 Default Styles Applied
- **Tables**: `border-collapse: collapse`, `width: 100%`
- **Cells (TD)**: `border: 1px solid #000000`, `padding: 2px 5px`, `vertical-align: middle`
- **Headers (TH)**: Same as cells plus `background: #0000000d`, `font-weight: bold`

### 🛡️ Compatibility
- **Backward compatible** - Existing tables remain unchanged
- **Style override** - Manual styling still takes precedence
- **CSS fallback** - Editor CSS remains for unstyled tables

### 💎 Benefits
- Solves visual inconsistency between editor and exported content
- Tables render with borders when viewed outside the editor
- Improved developer experience with inline styles for debugging
- Better cross-platform consistency

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
