# Instructions

1. Open any file in Revit (a blank project is fine), then open Dynamo. Dynamo can only run inside Revit.
2. Open the graph and locate the newly added **④ Batch - RVT files** group:
   - Set the **Batch Mode** switch to `True`.
   - In the `files` list of the **RVT Files / Folders Code Block**, enter RVT file paths and/or folder paths. File and folder paths can be mixed. If you enter a folder, all `.rvt` files inside that folder will be checked.
   - Use forward slashes in paths, for example: `"D:/Project/Models"`.
3. Select a folder for **Output Folder**. All reports will be saved there. If no folder is selected, each report will be saved next to its corresponding RVT file.
4. Run the graph. The report name follows this format: `ModelName_ModelCheck_DateTime.xlsx`. When processing is complete, the output folder will open automatically.

When **Batch Mode** is set to `False`, the graph works as before and checks only the currently opened model.

## Run Results (Watch Node)

- **Item 1:** The XLSX path corresponding to each file.
- **Item 2:** A batch summary table listing the result for each file (`OK` / `ERROR`), number of passed checks, overall completion rate, report path, and processing time.
- **Item 3:** Informational messages, such as paths that could not be found.

If a file fails to open, it will only be recorded as `ERROR` in the summary table. The remaining files will continue to be processed normally.

## Batch Settings (Global Options)

| Option | Default | Purpose |
|---|---:|---|
| `DetachFromCentral` | `true` | Opens workshared files in detached mode, preventing the central model from being locked or modified. |
| `OpenAllWorksets` | `true` | Setting this to `false` can improve performance, but elements in closed worksets will not be checked. |
| `AuditOnOpen` | `false` | Determines whether Revit performs an Audit when opening a file. |
| `IncludeSubfolders` | `false` | When a folder is specified, determines whether subfolders are also searched. |
| `SkipBackupFiles` | `true` | Skips backup files such as `xxx.0001.rvt`. |

## Notes

- **Revit versions:** Files created in an older Revit version than the currently running version will be automatically upgraded in memory before checking. Because the files are not saved, the original files remain unchanged, although opening them may take longer.
- **Cloud models:** Currently, only local paths or network-drive paths are supported. Models hosted on BIM 360 / ACC must first be downloaded locally.
- **Largest Families:** This check exports families one by one to calculate their sizes. It can become very slow when processing many files. For batch runs, it is recommended to disable this check.
- **Not yet tested inside Revit:** File collection (including folders, subfolders, and skipping backup files), rule parsing, and report generation have been tested outside Revit and are working. However, opening RVT files in the background can only be verified inside Revit. It is recommended to test with two or three files first.
