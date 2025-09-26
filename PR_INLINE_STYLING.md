# Add Default Inline Styles to Tables and Cells

**Fixes #46 - Default Borders**

## 🔍 Problem Statement

Currently, tables in quill-table-better appear with 1px black borders in the editor due to CSS styling (`.ql-editor td`), but when content is exported via `getContents()` or `getSemanticHTML()`, there are no actual border styles in the Delta format or HTML output. This creates inconsistency:

- **In Editor**: Tables display with borders due to CSS
- **Exported Content**: Tables have no borders when viewed outside the editor
- **User Confusion**: Border styles only appear after manually setting them via cell properties

### Example of Current Issue:

**Creating a 1x1 table returns:**

```json
{"ops":[{"attributes":{"table-temporary":{"data-class":"ql-table-better"}},"insert":"\n"},{"attributes":{"table-cell-block":"cell-opf2","table-cell":{"data-row":"row-fep7","width":"72"}},"insert":"\n"},{"insert":"\n"}]}
```

```html
<table class="ql-table-better">
  <tbody>
    <tr>
      <td data-row="row-fep7" width="72">
        <p class="ql-table-block" data-cell="cell-opf2"><br></p>
      </td>
    </tr>
  </tbody>
</table>
```

**No border styles in the output** → Tables appear unstyled when rendered outside the editor.

## 💡 Solution

This PR automatically applies default inline styles to newly created tables and cells, ensuring consistent appearance both in the editor and in exported content.

### Default Styles Applied:

**Tables:**
- `border-collapse: collapse`
- `width: 100%`

**Table Cells (TD):**
- `border: 1px solid #000000`
- `padding: 2px 5px`
- `vertical-align: middle`

**Header Cells (TH):**
- `border: 1px solid #000000`
- `padding: 2px 5px`
- `vertical-align: middle`
- `background: #0000000d`
- `font-weight: bold`

## 🚀 Implementation Details

### 1. **Configuration Constants** (`src/config/index.ts`)
```typescript
const TABLE_DEFAULT_INLINE_STYLES: Props = {
  'border-collapse': 'collapse',
  'width': '100%'
};

const CELL_DEFAULT_INLINE_STYLES: Props = {
  'border': '1px solid #000000',
  'padding': '2px 5px',
  'vertical-align': 'middle'
};

const TH_DEFAULT_INLINE_STYLES: Props = {
  'border': '1px solid #000000',
  'padding': '2px 5px', 
  'vertical-align': 'middle',
  'background': '#0000000d',
  'font-weight': 'bold'
};
```

### 2. **Style Utility Functions** (`src/utils/index.ts`)
```typescript
// Convert style object to CSS string
function formatStyleString(styles: Props): string

// Parse CSS string to style object  
function parseStyleString(styleString: string): Props

// Merge default and existing styles
function mergeStyles(defaultStyles: Props, existingStyle?: string): string
```

### 3. **Enhanced Table Creation** (`src/quill-table-better.ts`)
- Modified `insertTable()` to apply default styles to table and cells
- Styles are embedded directly in Delta operations

### 4. **Enhanced Format Handling** (`src/formats/table.ts`)
- Updated `TableCell.create()` to properly handle inline styles
- Enhanced `insertTableCell()` and `insertColumnCell()` for dynamic operations
- Maintained existing attribute handling while adding style support

## 🧪 Testing

### Expected Behavior After Fix:

**Creating a 1x1 table now returns:**

```json
{"ops":[{"attributes":{"table-temporary":{"style":"border-collapse: collapse; width: 100%"}},"insert":"\n"},{"attributes":{"table-cell-block":"cell-abc","table-cell":{"data-row":"row-xyz","style":"border: 1px solid #000000; padding: 2px 5px; vertical-align: middle"}},"insert":"\n"},{"insert":"\n"}]}
```

```html
<table style="border-collapse: collapse; width: 100%">
  <tbody>
    <tr>
      <td data-row="row-xyz" style="border: 1px solid #000000; padding: 2px 5px; vertical-align: middle">
        <p class="ql-table-block" data-cell="cell-abc"><br></p>
      </td>
    </tr>
  </tbody>
</table>
```

**✅ Border styles are now preserved in both Delta and HTML output!**

### Test Cases:
1. ✅ New table creation includes inline styles
2. ✅ Dynamic row insertion applies default styles
3. ✅ Dynamic column insertion applies default styles  
4. ✅ Existing tables remain unaffected (backward compatibility)
5. ✅ Copy/paste operations preserve styling
6. ✅ HTML export shows borders when rendered

## 📊 Impact

### Addresses Issue #46 Requirements:
- ✅ **Visual Consistency**: Tables look the same in editor and exported content
- ✅ **Border Preservation**: Default borders are included in Delta/HTML output
- ✅ **Property Alignment**: Cell properties UI now matches actual content attributes
- ✅ **Export Compatibility**: HTML renders correctly outside the editor

### Backward Compatibility:
- ✅ **Existing Content**: No changes to previously created tables
- ✅ **API Compatibility**: All existing methods work unchanged
- ✅ **Style Override**: Manual style changes still take precedence
- ✅ **CSS Fallback**: Editor CSS remains as fallback for unstyled tables

## 🔧 Technical Notes

### Style Priority Order:
1. **Manual Styles**: User-set styles via cell properties (highest priority)
2. **Default Styles**: Applied automatically to new elements
3. **CSS Fallback**: Editor CSS for backward compatibility (lowest priority)

### Performance Considerations:
- Minimal overhead: Styles applied only during creation, not on every render
- No impact on existing tables or editor performance
- Efficient string formatting utilities

### Memory Impact:
- Slightly larger Delta size due to inline styles (~50-100 bytes per table)
- More accurate representation of actual table appearance
- Better compression potential for repeated style patterns

## 🎯 Benefits

1. **🎨 Visual Consistency**: Tables appear identical in editor and exported content
2. **📤 Export Reliability**: HTML exports include proper table styling
3. **🔄 Copy/Paste Fidelity**: Table styling preserved across operations
4. **🛠️ Developer Experience**: Inline styles make debugging and customization easier
5. **📱 Cross-Platform**: Consistent appearance across different rendering environments
6. **🔒 Backward Compatible**: Existing functionality unchanged

---

## 📝 Related Issues
- Fixes #46 - Default Borders
- Addresses visual consistency reported by @winterlimelight  
- Implements solution suggested by @Stegosauro76

This change ensures that quill-table-better provides a seamless experience where the table appearance in the editor matches exactly what users get when they export or view the content elsewhere.