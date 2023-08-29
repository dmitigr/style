# The Windows-specific C++ programming style

## Resources

The following table defines the ID-ranges for use in
[resource-definition statements][res-def-stmt]:

|Resource category   |Range           |Amount|
|:-------------------|:---------------|:-----|
|DIALOG              |`[ 1001, 16000]`|15000 |
|STRINGTABLE         |`[16001, 31000]`|15000 |
|MENU                |`[31001, 35000]`|4000  |
|ACCELERATORS        |`[35001, 38000]`|3000  |
|ICON                |`[38001, 41000]`|3000  |
|BITMAP              |`[41001, 44000]`|3000  |
|FONT                |`[44001, 47000]`|3000  |
|HTML                |`[47001, 50000]`|3000  |
|CURSOR              |`[50001, 53000]`|3000  |
|MESSAGETABLE        |`[53001, 54000]`|1000  |
|RCDATA              |`[54001, 55000]`|1000  |
|User-defined        |`[55001, 56000]`|1000  |

### Remarks

- DIALOG includes the both `DIALOG` and `DIALOGEX` resources, all the controls
  and labels;
- STRINGTABLE includes IDs of all the strings;
- MENU includes `MENU`, `MENUEX` and `POPUP` resources;
- the range of `[56001, 65535]` is reserved.

[res-def-stmt]: https://learn.microsoft.com/en-us/windows/win32/menurc/resource-definition-statements
